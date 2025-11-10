# 🚀 MottuTrack — Azure DevOps (CI/CD)

## 📘 Descrição do Projeto
O MottuTrack é uma aplicação desenvolvida em Java Spring Boot com o objetivo de gerenciar e monitorar motocicletas de forma eficiente, integrando funcionalidades de cadastro, atualização e controle de disponibilidade.
O projeto utiliza integração contínua (CI) e entrega contínua (CD) por meio do Azure DevOps, garantindo que cada alteração no código seja automaticamente compilada, testada e implantada em produção.

A automação elimina processos manuais, aumenta a confiabilidade do deploy e reduz o tempo entre o desenvolvimento e a disponibilização de novas versões da API.
A aplicação é hospedada no Azure Web App, com um banco de dados PostgreSQL em nuvem configurado via variáveis de ambiente para segurança e escalabilidade.

---

## ⚙️ Stack de Tecnologias
| Camada | Tecnologias Utilizadas |
|:-------:|-------------------------|
| Backend | Java 17 • Spring Boot 3 • Maven |
| Cloud | Azure App Service • Banco PostGreSQL |
| CI/CD | Azure DevOps Pipelines (Build + Release) |
| Versionamento | GitHub + Repos do Azure DevOps |
| Outros | Visual Paradigm (diagramas), Banco PostGreSQL (testes), Git |

---


## 🧩 Arquitetura CI/CD

![Arquitetura CI/CD - MottuTrack](./docs/arquitetura-cicd.png)

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


## 🧠 Estrutura da Aplicação

```text
src/
├── main/
│   ├── java/com/mottutrack/api/
│   │   ├── controller/        # Endpoints REST
│   │   ├── model/             # Entidades (Filial, Moto, etc.)
│   │   ├── repository/        # Interfaces JPA
│   │   ├── service/           # Regras de negócio
│   │   ├── dto/               # Objetos de transferência de dados
│   │   └── exceptions/        # Tratamento de erros
│   └── resources/
│       └── application.properties  # Configurações (DB, porta, etc.)
└── test/
    └── java/                  # Testes unitários e de integração
````

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

| 💾 Recurso | 🔗 Link |
|-------------|---------|
| 🧩 **Azure DevOps Project** | [Acessar Pipeline no Azure DevOps](https://dev.azure.com/RM558438/Sprint%204%20%E2%80%93%20Azure%20DevOps) |
| ☁️ **Azure App Service (API Online)** | [Acessar API hospedada](https://mottutrack-api-558438.azurewebsites.net/login) |
| 🎥 **Vídeo de Demonstração (YouTube)** | [Assistir vídeo da entrega](https://youtu.be/tPo-aedx2Dg) |


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
