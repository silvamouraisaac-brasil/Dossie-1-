# 🛡️ Core Security Ecosystem: ShieldVault & Vigilant

Este repositório centraliza o desenvolvimento de duas soluções móveis nativas de alta performance focadas em segurança da informação, criptografia aplicada e inteligência de dados de última geração para o ecossistema corporativo. Ambos os sistemas utilizam **Kotlin** e **Jetpack Compose** no ambiente Android Studio, operando sob arquitetura modular e blindada.

---

## 📱 1. SHIELDVAULT: Air-Gapped Cryptographic Authenticator

O **ShieldVault** é um ecossistema de autenticação e assinatura digital offline projetado para proteger operações críticas de alto escalão (como movimentações financeiras institucionais e deploys de infraestrutura). O sistema transforma o dispositivo móvel em um token de hardware inviolável sem depender de conexão com a internet.

### ⚙️ Engenharia Criptográfica e Fluxo de Dados
1. **Isolamento de Hardware:** O aplicativo utiliza o **Android Keystore System** para gerar pares de chaves assimétricas (Pública/Privada) protegidas diretamente no chip de segurança física do aparelho (TEE/StrongBox). A chave privada permanece inacessível e nunca deixa o hardware.
2. **Protocolo Air-Gapped via QR Code:** O canal de comunicação entre o terminal do usuário e o dispositivo móvel ocorre de forma estritamente visual para mitigar ataques de rede (*Man-in-the-Middle* ou malwares locais):
   * O backend gera um payload dinâmico com os dados da transação somados a um *nonce* de uso único.
   * Esse payload é exibido na tela do terminal como um código QR.
   * O aplicativo mobile escaneia o código, calcula o hash do payload e solicita a autenticação biométrica do usuário.
3. **Assinatura Baseada em Hashing:** Após a validação biométrica nativa, a chave privada assina o hash gerado. O aplicativo exibe um novo código QR contendo apenas a assinatura criptográfica, que é lido pelo terminal para validação final no backend usando a chave pública correspondente.

---

## 👁️ 2. VIGILANT: Supply Chain Cyber Intelligence & Data Harvesting

O **Vigilant** é uma plataforma distribuída de inteligência cibernética focada na antecipação e monitoramento de riscos em cadeias de suprimentos corporativas. O sistema opera como um motor contínuo e assíncrono de coleta e análise de dados externos.

### ⚙️ Arquitetura de Coleta e Anonimização
1. **Data Harvesting Assíncrono:** O backend emite rotinas automatizadas que varrem bases de dados globais de vulnerabilidades, repositórios públicos de código e registros de vazamentos na internet em busca de dados expostos de empresas cadastradas.
2. **Ingestão Blindada com Hashing:** Alinhado aos princípios de *Privacy by Design*, os dados capturados pelo pescador de dados são processados imediatamente por funções de hash unidirecionais (**SHA-256**). O sistema armazena apenas as assinaturas matemáticas resultantes, tornando o banco de dados imune a vazamentos de texto claro.
3. **Protocolo K-Anonymity (Zero-Knowledge):** Para garantir privacidade total nas buscas feitas pelo aplicativo móvel:
   * O usuário insere o termo ou domínio a ser monitorado.
   * O aplicativo calcula o hash SHA-256 localmente, trunca o resultado e envia apenas os **5 primeiros caracteres (prefixo do hash)** para a API.
   * O backend retorna todos os hashes correspondentes àquele prefixo.
   * A filtragem e a correspondência exata (*match*) ocorrem estritamente dentro do dispositivo do usuário, garantindo que o servidor jamais saiba qual empresa específica está sendo auditada.

---

## 📐 Arquitetura de Software Unificada

Ambos os projetos são estruturados sob os princípios de **Clean Architecture** e padrão **MVVM (Model-View-ViewModel)**, garantindo desacoplamento total entre a lógica de persistência, as regras de negócio e a interface declarativa do usuário.


* **Linguagem:** Kotlin 2.x
* **Ambiente de Desenvolvimento:** Android Studio / IntelliJ IDEA
* **Interface Móvel:** Jetpack Compose (Arquitetura Declarativa)
* **Gerenciador de Dependências:** Gradle (Kotlin DSL)
* **Comunicação de Rede:** Ktor Client / Retrofit com serialização nativa
* **Módulos Críticos:** Android Keystore System, Biometric Prompt API, SHA-256 / S
