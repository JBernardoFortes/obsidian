# Compartilhamento de Arquivos em Rede


> **Protocolo usado: SMB (não NFS).** O Windows só tem cliente NFS nas edições Pro/Enterprise e a conversão de permissões UID/GID gera muito problema. O SMB é nativo no Windows e o Linux fala o mesmo protocolo via Samba — os dois mundos conversam sem adaptação.

---

## Parte 1 — Entre PCs Windows

Passos **1 e 2** em todos os PCs. Passos **3 a 6** apenas no PC que vai guardar os arquivos (o "servidor"). Passos **7 e 8** nos demais PCs.

### 1. Definir a rede como Particular

Configurações → Rede e Internet → clique na conexão ativa (Wi-Fi ou Ethernet) → marque **Rede particular**.

Se ficar como "Pública", o Windows bloqueia a descoberta e os PCs não se enxergam. É o motivo nº 1 de compartilhamento que "não funciona".

### 2. Ativar descoberta e compartilhamento

Painel de Controle → Central de Rede e Compartilhamento → **Alterar configurações de compartilhamento avançadas**.

No perfil **Particular**, ative:

- Ativar a descoberta de rede
- Ativar o compartilhamento de arquivos e impressoras

Mantenha o **compartilhamento protegido por senha LIGADO**. Salve as alterações.

### 3. Criar as contas de acesso no servidor

Configurações → Contas → Outros usuários → Adicionar outra pessoa → "Não tenho as informações de login" → **Adicionar usuário sem conta da Microsoft**.

Crie um usuário e senha para cada pessoa da equipe. Anote — essas credenciais serão pedidas nos outros PCs.

### 4. Compartilhar a pasta

Botão direito na pasta → Propriedades → aba **Compartilhamento** → **Compartilhamento Avançado** → marque "Compartilhar esta pasta".

- Dê um nome simples e **sem acento** (ex.: `Arquivos`)
- Clique em **Permissões**, remova o grupo "Todos"
- Adicione os usuários criados no passo 3
- Marque **Alterar** (permite gravar) ou **Controle total** (permite também apagar)

### 5. Conferir a aba Segurança

Ainda nas Propriedades da pasta → aba **Segurança** → Editar → Adicionar → digite o nome dos mesmos usuários → Verificar nomes → OK → conceda **Modificar**.

> Esse passo é o que mais gera "acesso negado". O Windows exige a permissão nas **duas** abas: Compartilhamento e Segurança.

### 6. Descobrir o nome ou IP do servidor

No Prompt de Comando:

```
ipconfig
```

Anote o **Endereço IPv4** (ex.: `192.168.0.15`). O nome da máquina está em Configurações → Sistema → Sobre.

Reserve esse IP fixo no roteador (reserva de DHCP), senão ele muda e os atalhos quebram.

### 7. Acessar dos outros PCs

Abra o Explorador de Arquivos e digite na barra de endereço:

```
\\192.168.0.15\Arquivos
```

ou

```
\\NOME-DO-PC\Arquivos
```

Informe uma das contas criadas no passo 3 e marque **Lembrar minhas credenciais**.

### 8. Mapear como unidade de rede

Com a pasta aberta → botão direito → **Mapear unidade de rede** → escolha uma letra (Z:) → marque **Reconectar na entrada** → Concluir.

A pasta passa a aparecer em "Este Computador" toda vez que o PC liga, como se fosse um HD local.

---

## Parte 2 — Linux servindo os arquivos (Samba)

### Instalação

```bash
sudo apt update && sudo apt install samba
sudo mkdir -p /srv/arquivos
sudo chown -R $USER:$USER /srv/arquivos
```

### Configuração

Edite `/etc/samba/smb.conf` e adicione ao final:

```ini
[arquivos]
   path = /srv/arquivos
   browseable = yes
   read only = no
   valid users = @equipe
   create mask = 0664
   directory mask = 0775
```

### Usuários

Cada pessoa precisa de um usuário Samba:

```bash
sudo groupadd equipe
sudo useradd -M -G equipe paula
sudo smbpasswd -a paula
sudo smbpasswd -e paula
sudo systemctl restart smbd
```

### Firewall e IP

```bash
sudo ufw allow samba
ip a | grep inet
```

### Acesso pelos Windows

Explorador de Arquivos → `\\192.168.x.x\arquivos` → mapear como unidade de rede.

---

## Parte 3 — Linux acessando um compartilhamento Windows

```bash
sudo apt install cifs-utils
sudo mkdir /mnt/compartilhado
sudo mount -t cifs //192.168.0.15/Arquivos /mnt/compartilhado \
  -o username=seuusuario,uid=1000,gid=1000
```

### Montagem automática no boot

Crie `/etc/samba/credenciais`:

```
username=seuusuario
password=suasenha
```

```bash
sudo chmod 600 /etc/samba/credenciais
```

Adicione ao `/etc/fstab`:

```
//192.168.0.15/Arquivos /mnt/compartilhado cifs credentials=/etc/samba/credenciais,uid=1000,gid=1000,_netdev 0 0
```

---

## Problemas comuns

| Sintoma                              | Causa provável                 | Solução                                                                                            |
| ------------------------------------ | ------------------------------ | -------------------------------------------------------------------------------------------------- |
| "Acesso negado" com tudo configurado | Aba Segurança esquecida        | Refazer o passo 5                                                                                  |
| Pede senha e recusa a correta        | Credencial errada em cache     | Painel de Controle → Gerenciador de Credenciais → Credenciais do Windows → remover a entrada do PC |
| PC não aparece em "Rede"             | Descoberta automática instável | Acessar direto por `\\IP\pasta`                                                                    |
| Unidade Z: com X vermelho            | Servidor desligado ou suspenso | Religar; desativar suspensão no servidor                                                           |
| Funciona e depois para do nada       | IP do servidor mudou           | Reserva de DHCP no roteador                                                                        |

---

## Operação e riscos

**O servidor precisa ficar ligado.** Suspensão também derruba o acesso — a placa de rede cai junto. No Linux, para desativar:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

No Windows: Configurações → Sistema → Energia → suspensão "Nunca". Deixar só o monitor desligar não atrapalha.

**Nobreak.** Desligamento abrupto durante gravação corrompe arquivo. Um nobreak simples para o servidor e o roteador resolve.

**Compartilhamento não é backup.** Se o disco do servidor falhar, todos perdem junto. Mantenha uma cópia em disco externo ou nuvem.

**Para volume alto de vídeo bruto**, avalie um NAS dedicado: consome 15–30 W (contra 60–150 W de um desktop), é feito para operar continuamente e já traz RAID e rotina de backup.