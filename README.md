# 🚀 MottuTrackAPI1 — Integração com Azure DevOps (CI/CD)

## 📘 Descrição do Projeto
O **MottuTrackAPI1** é uma API REST desenvolvida em **Spring Boot** que realiza o gerenciamento de **filiais e motos** da empresa Mottu.  
O objetivo é permitir o controle centralizado das operações de frota, garantindo integração com o **Azure DevOps** para automação completa do ciclo de vida de deploy.

Este projeto faz parte da **Sprint 4 – Azure DevOps**, cujo foco é configurar e validar todo o processo de **integração contínua (CI)** e **entrega contínua (CD)** de uma aplicação Java hospedada no **Azure App Service**.

---

## ⚙️ Stack de Tecnologias
| Camada | Tecnologias Utilizadas |
|:-------:|-------------------------|
| Backend | Java 17 • Spring Boot 3 • Maven |
| Cloud | Azure App Service • Azure SQL Database |
| CI/CD | Azure DevOps Pipelines (Build + Release) |
| Versionamento | GitHub + Repos do Azure DevOps |
| Outros | Visual Paradigm (diagramas), Postman (testes), Git |

---

## 🧱 Detalhamento dos Componentes

| 🧩 **Nome do Componente** | ⚙️ **Tipo** | 🧠 **Descrição Funcional** | 🧰 **Tecnologia / Ferramenta** |
|----------------------------|-------------|------------------------------|--------------------------------|
| 💾 **Repositório de Código** | SCM | Onde o código-fonte está versionado e armazenado. | 🧠 GitHub |
| 🧪 **Pipeline de Build (CI)** | Orquestrador CI | Compila o projeto, executa testes unitários e gera o artefato (.jar). | ⚙️ Azure DevOps Pipelines |
| 📦 **Artefato (drop)** | Gerenciador de Artefatos | Armazena o artefato gerado pela pipeline para posterior deploy. | 📁 Azure DevOps Artifacts |
| 🚀 **Pipeline de Release (CD)** | Orquestrador CD | Realiza o deploy automatizado do artefato para o ambiente de desenvolvimento. | ⚙️ Azure DevOps Releases |
| 🔐 **Variáveis de Ambiente** | Configuração | Define credenciais e parâmetros necessários para conexão com o banco de dados. | ⚙️ Azure DevOps Variables / ☁️ Azure App Service |
| ☁️ **Aplicação Hospedada** | Infraestrutura Cloud | Serviço em nuvem que executa a aplicação Java Spring Boot. | ☁️ Azure App Service |
| 🗄️ **Banco de Dados** | Persistência | Armazena as informações das entidades **Filial** e **Moto**. | 🐘 Azure Database for PostgreSQL |
| 👨‍💻 **Desenvolvedor** | Persona | Responsável por versionar o código e disparar o pipeline (commit/push). | 🧠 Git / Azure DevOps |
| 👤 **Usuário Final** | Persona | Consome os endpoints da API após o deploy no App Service. | 🌐 Postman / Browser |

---

## 🧩 Arquitetura do Sistema

O sistema é composto por duas entidades principais:

- **Filial:** Representa uma unidade operacional da Mottu.  
  Contém atributos como nome, endereço e capacidade de operação.  
- **Moto:** Representa uma motocicleta registrada em uma filial.  
  Contém informações de placa, modelo, ano e disponibilidade.  

A API segue o padrão **RESTful**, permitindo as operações CRUD completas para ambas as entidades.

---

## 🧠 Estrutura da Aplicação
src/
├── main/
│ ├── java/com/mottutrack/api/
│ │ ├── controller/ → Endpoints REST
│ │ ├── model/ → Entidades (Filial, Moto)
│ │ ├── repository/ → Interfaces JPA
│ │ ├── service/ → Regras de negócio (BO)
│ │ ├── dto/ → Transferência de dados
│ │ └── exceptions/ → Tratamento de erros
│ └── resources/
│ └── application.properties
└── test/
└── java/ → Testes unitários e de integração

yaml
Copiar código

---

## 🔁 Fluxo de Integração CI/CD

O processo completo de integração contínua e entrega contínua foi configurado no **Azure DevOps**, conforme o diagrama abaixo:

### 🔹 **Etapas do Pipeline**

1. **Commit no Repositório GitHub**  
   O desenvolvedor realiza o push do código para a branch principal (`main`).

2. **Pipeline de Build (CI)**  
   - A pipeline é disparada automaticamente após o commit.  
   - As tasks executam:  
     - Build do projeto com Maven  
     - Execução de testes unitários  
     - Publicação do artefato `.jar` no diretório `drop`

3. **Publicação do Artefato**  
   O artefato é armazenado e versionado dentro do **Azure DevOps Artifacts**.

4. **Pipeline de Release (CD)**  
   - O artefato é implantado no **Azure App Service**.  
   - As variáveis de ambiente são configuradas automaticamente no serviço.

5. **Deploy Automático no App Service**  
   A aplicação é atualizada e publicada automaticamente no ambiente cloud.

---

## 🧩 Diagrama de Arquitetura CI/CD

*(Insira aqui a imagem exportada do Visual Paradigm — ex: “diagram-ci-cd.png”)*  
**Exemplo:**
![Diagrama CI/CD](./assets/diagram-ci-cd.png)

Legenda:
1️⃣ Commit no GitHub  
2️⃣ Build Pipeline  
3️⃣ Publicação do Artefato  
4️⃣ Release e Deploy no App Service  

---

## 🔐 Configurações de Variáveis de Ambiente

As variáveis de ambiente foram configuradas diretamente no **Azure DevOps** dentro da task de deploy, utilizando o formato correto para o App Service:

-SPRING_DATASOURCE_URL "$(SPRING_DATASOURCE_URL)"
-SPRING_DATASOURCE_USERNAME "$(SPRING_DATASOURCE_USERNAME)"
-SPRING_DATASOURCE_PASSWORD "$(SPRING_DATASOURCE_PASSWORD)"

perl
Copiar código

Essas variáveis são consumidas no `application.properties` via:
spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}

yaml
Copiar código

---

## ✅ Casos de Teste (Work Items)

| ID | Título | Status | Resultado Esperado |
|----|---------|--------|--------------------|
| 01 | Executar pipeline de build manualmente | ✅ Concluído | Build bem-sucedido |
| 02 | Validar publicação do artefato | ✅ Concluído | Artefato gerado e disponível |
| 03 | Executar release e fazer deploy | ✅ Concluído | Aplicação publicada no App Service |
| 04 | Validar aplicação rodando após deploy | ✅ Concluído | API acessível via browser |
| 05 | Validar variáveis de ambiente do App Service | ✅ Corrigido | Configurações válidas e aplicadas |
| 06 | Disparar pipeline ao fazer commit no repositório | ✅ Concluído | Pipeline acionado automaticamente |
| 07 | Ajustar variáveis de ambiente no DevOps | ✅ Corrigido | Deploy final sem erros (Release-6) |

---

## 🌐 URLs e Recursos

| Recurso | Link |
|----------|------|
| **Azure DevOps Project** | [https://dev.azure.com/RM558438/Sprint%204%20%E2%80%93%20Azure%20DevOps](https://dev.azure.com/RM558438/Sprint%204%20%E2%80%93%20Azure%20DevOps)|


| **Azure App Service (API Online)** | [https://mottutrack-api-558438.azurewebsites.net/login](https://mottutrack-api-558438.azurewebsites.net/login) |


| **Vídeo de Demonstração (YouTube)** | [https://youtu.be/<link-video>](https://youtu.be/<link-video>) |



---

## 🧠 Conclusão

O projeto **MottuTrackAPI1** conclui com sucesso o ciclo de automação CI/CD, integrando o Azure DevOps com o Azure App Service.  
O processo garante **entregas automatizadas**, **versionamento contínuo** e **deploy seguro** da aplicação Java em nuvem.

Além disso, o troubleshooting realizado no caso das **variáveis de ambiente** reforçou o domínio prático de DevOps e a compreensão sobre o fluxo completo de deploy corporativo.

---

## 👨‍💻 Desenvolvedores

| Nome                          | RM      | GitHub |
|-------------------------------|---------|--------|
| Enzo Dias Alfaia Mendes       | 558438  | [@enzodam](https://github.com/enzodam) |
| Matheus Henrique Germano Reis | 555861  | [@MatheusReis48](https://github.com/MatheusReis48) |
| Luan Dantas dos Santos        | 559004  | [@lds2125](https://github.com/lds2125) |
