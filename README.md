
Tópico: Criptografia RSA: Princípios, Funcionamento e Aplicações em Segurança da Informação
Introdução ao RSA
O RSA (Rivest-Shamir-Adleman) é um dos primeiros e mais amplamente utilizados algoritmos de criptografia assimétrica, desenvolvido em 1977. O RSA é considerado assimétrico porque utiliza duas chaves distintas—uma chave pública e uma chave privada.
O Princípio Básico do RSA é que, se Bob usa a chave pública de Alice para criptografar uma mensagem, apenas Alice pode descriptografar essa mensagem utilizando sua chave privada correspondente.

--------------------------------------------------------------------------------
I. 🧮 Princípios Matemáticos do RSA
A segurança e a funcionalidade do RSA dependem de conceitos robustos da teoria dos números:
1. Aritmética Modular
A aritmética modular é o pilar do RSA. Ela lida com restos de divisões e permite a realização de cálculos eficientes de exponenciação, como o cálculo de (a 
k
 )modn.
2. Números Primos e o Problema da Fatoração
O RSA exige a escolha de dois números primos grandes, p e q.
• O módulo n é o produto desses primos: n=p×q.
• A segurança do RSA está fundamentada na dificuldade computacional do Problema da Fatoração: dado n, é extremamente difícil encontrar p e q se n for um número grande.
3. Função Totiente de Euler (ϕ(n))
Esta função é crucial para a geração da chave privada e deve ser mantida em segredo.
• ϕ(n) conta quantos números menores que n são coprimos com n.
• Para o RSA, se n=p×q, a função totiente é calculada como: ϕ(n)=(p−1)×(q−1).
4. Teorema de Euler e Inverso Modular
O Teorema de Euler é o que prova que a descriptografia funciona corretamente. Um corolário desse teorema garante que a mensagem original será recuperada.
O inverso modular é usado para calcular a chave privada (d) a partir da chave pública (e) e de ϕ(n). d é o inverso modular de e se:
• e×d≡1(modϕ(n)).
• Este cálculo é realizado usando o Algoritmo Euclidiano Estendido.

--------------------------------------------------------------------------------
II. ⚙ Funcionamento do Algoritmo RSA
O algoritmo RSA é dividido em três fases principais:
Fase 1: Geração de Chaves
Esta fase gera o par de chaves (pública e privada).
1. Geração dos Primos (p,q): Gere dois números primos distintos e grandes (p e q) de tamanhos similares (cerca de n/2 bits cada).
2. Cálculo do Módulo (n): Calcule n=p×q. n define o tamanho da chave e será público.
3. Cálculo de ϕ(n): Calcule ϕ(n)=(p−1)×(q−1). (Este valor deve ser secreto).
4. Escolha do Expoente Público (e): Escolha e (geralmente e=65537) tal que 1<e<ϕ(n). O valor 65537 é popular porque é primo e torna a exponenciação eficiente.
5. Cálculo do Expoente Privado (d): Calcule d, o inverso modular de e módulo ϕ(n).
Resultado Final:
• Chave Pública: (n,e) (compartilhada).
• Chave Privada: (n,d) (secreta).
Fase 2: Criptografia
Para criptografar a mensagem m (que deve ser convertida em um número tal que m<n), utiliza-se a chave pública (n,e):  c = m^e \bmod n  Onde c é o texto criptografado.
Fase 3: Descriptografia
Para descriptografar o texto cifrado c e recuperar a mensagem original m, utiliza-se a chave privada (n,d):  m = c^d \bmod n  Isto funciona matematicamente porque m 
ed
 ≡m(modn), uma consequência direta do Teorema de Euler e da relação entre e e d.

--------------------------------------------------------------------------------
III. Aplicações Práticas e Considerações de Segurança
1. Aplicações em Segurança da Informação
O RSA é amplamente adotado e é a base de muitos protocolos de segurança:
• Protocolos Seguros: É utilizado em protocolos como HTTPS, SSH e VPNs.
• Troca de Chaves Simétricas: Devido à sua baixa performance (cerca de 1000x mais lento que AES), o RSA é tipicamente usado para criptografar chaves simétricas menores, em vez de criptografar grandes volumes de dados.
• Assinatura Digital: O RSA pode ser usado para assinatura digital, garantindo a autenticidade e a não-repúdio da mensagem (usando PSS em produção).
2. Recomendações de Chave e Segurança
A robustez da segurança do RSA depende diretamente do tamanho do módulo n.
• O tamanho de 1024 bits é considerado quebrado (❌).
• O tamanho de 2048 bits é o mínimo atualmente seguro (✅).
• O tamanho de 3072 bits é o recomendado para 2025 (✅).
Para garantir a segurança em implementações profissionais, é crucial:
• Usar chaves ≥2048 bits.
• Usar padding seguro, como OAEP, para criptografia.
• Utilizar bibliotecas criptográficas testadas (como OpenSSL).
3. Limitações Críticas
O RSA tem limitações importantes:
1. Performance: É lento para criptografar dados grandes, sendo superado por algoritmos simétricos e pela Criptografia de Curva Elíptica (ECC).
2. Vulnerabilidade Quântica: O algoritmo de Shor, se implementado em um computador quântico funcional, pode quebrar o RSA em tempo polinomial ao fatorar n. A migração para criptografia pós-quântica (como Kyber ou Dilithium) será necessária no futuro.
