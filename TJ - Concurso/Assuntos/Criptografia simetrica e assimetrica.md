
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

- **AES ( **




---

[[TLS e SSL]]