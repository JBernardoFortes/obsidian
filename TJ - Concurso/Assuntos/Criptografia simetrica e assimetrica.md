
---


### 1. Conceitos Fundamentais e a Logica das Chaves

A criptografia eh o conjunto de tecnicas destinadas a ocultar dados por meio de cifras (codigicacao), transformando informacoes legiveis em codigos indecifraveis para quem nao possui autorizacao. O elemento central desse processo eh a chave que funciona logicamente como uma senha: o segredo necessario para cifrar ou decifrar o dado.

DIferenciados os dois modelos principais pela organizacao dessas chaves:

- **Criptografia Simetria**: Utiliza uma chave unica, secreta e compartilhada entre emissor e receptor, para ambos os sentidos ( crifracao e decifracao )
- **Criptografia Assimetrica**: Utiliza um par de chaves matematicamente relacionadas - uma publica e uma privada

---

### 2. Criptgrafia Simetrica

Neste metodo, a mesma chave privada eh compartilhada entre os pontos. A seguranca reside inteiramente na manutencao do segredo dessa chave unica. Eh o metodo focado primariamente no pilar da Confidencialdade

#### Classificacao dos Algoritmos

Os algoritmos simetricos dividem-se em dois subgrupos principais:

##### A. Cifras de Block ( Block Ciphers )

Processam a mensagem em blocos de tamanho fixo

- **DES ( Date Encryption Standard  )**: Opera com blocos de 64 bits. Atualmente eh considerado vulneravel a ataques de forca bruta

- **3DES ( Tripe DES )**: Executa o processo de "codificar-decodificar-codificar" usando tres chaves de 64 bits. Esse processamento triplo eh o motivo de ser considerado um algoritmo lento comparado aos modernos

- **AES ( Advanced Encrypton Standard )**: O padrao atual do mercado. Trabalha com blocos de 128 bits e chaves de 128, 192 ou 256 bits. Eh altamente eficiente por processar os dados em varias rodadas ( iteracoes ), garantindo seguranca e rapidez

- **Blowfish**: Utiliza blocos de 8 bytes ( 64 bits ) e chaves variaveis de 32 e 448 bits

- **IDEA ( International Data Encryption Algorithm )**: Opera em blocos de 64 bits com chaves de 128 bits; baseia-se em operacoes matematicas complexas para evitar criptoanalise

##### B. Cifras de Fluxo ( Stream Ciphers ):

Processam os dados bit a bit ou byte a byte:

- **RC4**: Opera 1 byte por vez. Foi a base do antigo protocolo SSL, mas hoje eh considerado defasado e inseguro
	**Vantagens**: Alta velocidade de processamento e baixo custo computacional
	**Desvantagens**: Complexidade na gestao e troca segura de chaves ( problema de distribuicao ); baixa escalabilidade e nao oferece irretratabilidade ( nao prova a autoria )

---

### 3. Criptografia Assimetrica

Tambem chamada de criptografia de chave publica, utiliza uma dinamica onde o que uma chave cifra, apenas a outra do mesmo par pode decifrar. Geralmente, a chave publica cifra a mensagem, e a chave privada do receptor a decifra.

**Principais Plgoritmos e Protocolos**

- **RSA ( Riverst-Shamir-Adleman )**: Baseado na dificuldade de fatoracao de numeros primos grandes. Eh o mais utilizado no mundo, operando com chaves de 2048 bits ou mais. Eh extremamente seguro, porem lento devido a complexidade matematica
- **ECC ( Curva Eliptica )**: Oferece alto nivel de seguranca com chaves menores, sendo eficiente para dispositivos com pouco recursos.
- **DSA ( Digital Signature Algorithm )**: Algoritmo focado especificamente em garantir a autenticidade atraves de assinaturas digitais.
- **Diffie-Hellman**: Protocolo focado na troca segura de chaves simetricas sobre canais inseguros, utilizando logaritmos discretos
- **ElGamal**: Baseado na dificuldade de resolver logaritmos discretos, similar ao Diffie-Hellman

**Pilares e certificacao**

A criptografia assimetrica eh a base para garantir: **Autenticidade**, **Integridade** e **Nao-repudio ( Irretratabilidade )**. O **Certificado Digital** eh o documento eletronico, emitido por uma Autoridade Certificadora (AC ), que valida a identidade de um titular. Para o funcionamento de criptografia, o ponto crucial eh que o **Certificado Digital contem a Chave Publica** do seu proprietario, permitindo que terceiros iniciem comunicacoes seguras com ele.

---

### 4. Criptografia Hibrida: O Equilibrio no TLS/HTTPS

A criptografia hibrida combina a seguranca da assimetrica com a velocidade da simetrica, sendo a base do protocolo **HttPS** ( Via camada TLS, sucessora do SSL )

O processo ocorre em duas etapas logicas:

- **Handshake**: Utiliza-se a **criptografia assimetrica**. O navegador utiliza a Chave Publica do servidor ( Obtida no Certificado Digital ) para cifrar uma chave de sessao ( que eh simetrica ). Dessa forma, apenas a Chave Privada do servidor pode revelar essa chave de sessao, garantindo que o segredo nao seja interceptado.
- **Trafego de Dados**: Uma vez que ambos possuem a mesma chave de sessao, passa-se a utilizar a **criptografia simetrica** para o fluxo continuo de dados, garantindo a performance necesaria para a navegacao web.

---

### 5. Tabela comparativa e Guia 


| Criterio                 | Criptografia Simetrica                       | Criptografia Assimetrica                    |
| ------------------------ | -------------------------------------------- | ------------------------------------------- |
| Quantidade de <br>Chaves | 1 ( Secreta/Compartilhada)                   | 2 (Par: Publica e Privada)                  |
| Velocidade               | Alta                                         | Baixa                                       |
| Recursos                 | Baixo Consumo                                | Alto Consumo                                |
| Escalabilidade           | Baixa ( Dificil gerenciar <br>muitas chaves) | Alta ( Cada usuario tem<br>apenas um par)   |
| Pilares principais       | Confidencialidade                            | Autenticidade, integridade<br>e Nao repudio |


---

[[TLS e SSL]]