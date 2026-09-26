
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

### Criptografia Assimetrica

Tambem chamada de criptografia de chave publica, utiliza uma dinamica onde o que uma chave cifra, apenas a outra do mesmo par pode decifrar. Geralmente, a chave publica cifra a mensagem, e a chave privada do receptor a decifra.

**Principais Plgoritmos e Protocolos**

- **RSA ( Riverst-Shamir-Adleman )**: Baseado na dificuldade de fatoracao de numeros primos grandes. Eh o mais utilizado no mundo, operando com chaves de 2048 bits ou mais. Eh extremamente seguro, porem lento devido a complexidade matematica
- **E**
****




---

[[TLS e SSL]]