# MCABank

O **MCABank** é um sistema bancário digital construído sobre arquitetura de microserviços, com foco em segurança, escalabilidade e modularidade.  

Este repositório serve como ponto central de documentação e orquestração de todos os serviços que compõem o ecossistema MCABank.  
Ele não contém código-fonte de serviços específicos, mas agrupa informações, links e guias para facilitar o desenvolvimento e a operação.

---

## Índice

1. [Arquitetura](#arquitetura)  
2. [Serviços Principais](#serviços-principais)  
3. [Tecnologias](#tecnologias)  
4. [Como Rodar Localmente](#como-rodar-localmente)  


---

## Arquitetura

O MCABank é dividido em múltiplos serviços independentes que se comunicam entre si via APIs REST/gRPC e eventos assíncronos.  

### Principais características:
- Autenticação e autorização centralizadas  
- Gerenciamento de clientes  
- Processamento de pagamentos  
- API Gateway para unificação do acesso  
- Definições de contratos em Protobuff para comunicação eficiente  
- Frontend web integrado aos serviços  

> Um diagrama da arquitetura pode ser adicionado em [`docs/architecture.png`](docs/architecture.png).  

---

## Serviços Principais

- **[MCABankAuth](https://github.com/rasteiro11/MCABankAuth)** → Gerenciamento de usuários, autenticação e autorização.  
- **[MCABankCustomer](https://github.com/rasteiro11/MCABankCustomer)** → Cadastro e gerenciamento de clientes.  
- **[MCABankPayment](https://github.com/rasteiro11/MCABankPayment)** → Processamento de pagamentos.  
- **[MCABankGateway](https://github.com/rasteiro11/MCABankGateway)** → API Gateway para roteamento, autenticação e entrada unificada.  
- **[MCABankProtobuff](https://github.com/rasteiro11/MCABankProtobuff)** → Definições de contratos gRPC para padronização de comunicação entre serviços.  
- **[MCABankFrontEnd](https://github.com/rasteiro11/MCABankFrontEnd)** → Interface web para interação com os serviços do sistema.  
- **[PogCore](https://github.com/rasteiro11/PogCore)** → Core de desenvolvimento de microsserviços em Go.


---

## Tecnologias

### Linguagens e Frameworks
- **Go** – Backend, microsserviços.
- **TypeScript / Angular** – Frontend web.
- **gRPC / Protobuf** – Comunicação padronizada entre microsserviços.
- **PogCore** – Core para desenvolvimento de microsserviços em Go com padrões e utils.

### Banco de Dados
- **MySQL** – Persistência.

### Mensageria e Filas
- **Amazon SQS (LocalStack)** – Filas assíncronas para eventos.

### Infraestrutura
- **Docker** – Containerização de serviços.
- **Kubernetes (MicroK8s)** – Orquestração de containers.
- **ArgoCD** – GitOps para deploy contínuo.
- **ConfigMaps / Secrets** – Gestão de configuração e credenciais por serviço.
- **DockerHub** – Registry das imagens Docker geradas.

### Autenticação e Segurança
- **JWT** – Tokens de autenticação.

### CI/CD e DevOps
- **GitHub Actions** – Build, testes e publicação de imagens.
- **GitOps** – Deploy e sincronização do estado do cluster via ArgoCD.

### Observabilidade (planejado / opcional)
- **Jaeger** – Planejado para tracing distribuído entre microsserviços.  
- **Grafana** – Planejado para visualização de métricas e dashboards.  
- **OpenTelemetry** – Planejado para coleta unificada de métricas, traces e logs distribuídos.

---

### Boas práticas e padrões

- **Microsserviços isolados por responsabilidade** – cada serviço é independente e encapsula sua lógica e dados.  
- **Isolamento dos serviços no cluster** – cada microsserviço roda em seu próprio namespace/deployment, evitando interferência e facilitando escalabilidade.  
- **Versionamento de contratos (Protobuf) e imagens Docker** – garante rastreabilidade e compatibilidade entre serviços.  
- **Estrutura de repositórios modular** – cada serviço mantém sua própria configuração de infraestrutura (manifests, ConfigMaps, Secrets).  
- **CI/CD automatizado e GitOps** – pipelines para build, testes e deploy via ArgoCD.  
- **Mensageria assíncrona** – uso de filas (SQS) para eventos desacoplados entre serviços.  
- **Rastreabilidade e observabilidade planejadas** – integração futura com OpenTelemetry, Jaeger e Grafana.  
- **Testes automatizados** – unitários.  
- **Documentação de APIs com Swagger** – padronização e fácil integração entre serviços e com clientes.  
- **Utilização de um core para desenvolvimento de microsserviços** – todos os serviços Go utilizam o **PogCore** para padronização de middlewares, logging, tracing, validação e integração com filas/DB, garantindo consistência entre microsserviços.  
- **Boas práticas de segurança** – autenticação via JWT, segredos gerenciados via Kubernetes Secrets.  
- **Documentação centralizada** – README e diagramas de arquitetura atualizados, facilitando onboarding e manutenção.

---

### Benefícios das boas práticas

- **Escalabilidade** – microsserviços isolados e deploys independentes permitem escalar apenas o que é necessário.  
- **Manutenção simplificada** – repositórios modulares e PogCore padronizam desenvolvimento e reduzem duplicação de código.  
- **Segurança aprimorada** – autenticação via JWT e gerenciamento de segredos via Kubernetes Secrets garantem proteção de dados sensíveis.  
- **Rastreabilidade e monitoramento** – integração futura com OpenTelemetry, Jaeger e Grafana permitirá identificar problemas rapidamente.  
- **Padronização de APIs** – contratos Protobuf e documentação Swagger facilitam integração entre serviços e com clientes.  
- **Confiabilidade** – pipelines CI/CD, testes unitários e GitOps reduzem risco de falhas em produção e possibilitam rollbacks rápidos.  
- **Desacoplamento e resiliência** – mensageria assíncrona (SQS) desacopla serviços, tornando o sistema mais robusto frente a indisponibilidades momentâneas.


---

