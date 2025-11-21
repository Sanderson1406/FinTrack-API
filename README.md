# FinTrack API | Sistema de Acompanhamento Financeiro Pessoal

Um robusto sistema de backend desenvolvido com **ASP.NET Core** que permite aos usuários gerenciar suas finanças pessoais, registrando transações, categorizando gastos e monitorando orçamentos. Este projeto visa demonstrar o domínio da stack .NET, implementação de APIs resilientes e a utilização de múltiplas tecnologias de persistência de dados, conforme as melhores práticas de desenvolvimento.

## Destaques Técnicos e Pilares da Formação

Este projeto é uma prova da proficiência nos seguintes pilares cruciais da formação .NET Developer:

| Recurso | Tecnologia | Objetivo no Projeto |
| :--- | :--- | :--- |
| **Backend Core** | ASP.NET Core 8.0, C\# | Criação de uma API RESTful de alta performance, seguindo o padrão REST. |
| **POO & Arquitetura**| Padrão Repository, DTOs, Injeção de Dependência | Garantir um código modular, escalável e de fácil manutenção, aplicando conceitos sólidos de Orientação a Objetos. |
| **Dados Relacionais**| SQL Server + Entity Framework Core | Usado para dados críticos (Transações, Orçamentos) que exigem **integridade transacional** e relacionamentos fortes. |
| **Dados Não-Relacionais**| **Azure Table Storage** | Utilizado para **logs de eventos** (chave-valor), demonstrando o uso de serviços nativos do Azure para persistência NoSQL. |
| **Resiliência** | XUnit, Testes Unitários | Cobertura de testes nas regras de negócio (e.g., cálculo de saldo, validações) para garantir a confiabilidade. |
| **Cloud (Opcional)**| Microsoft Azure App Services | Demonstração de habilidades em **Deploy, Hospedagem e Otimização** na nuvem. |

## Endpoints Principais

A documentação da API está disponível via **Swagger UI** após a inicialização do projeto, facilitando a exploração dos endpoints.

| Rota | Método | Descrição |
| :--- | :--- | :--- |
| `/api/transactions` | `POST` | Cria uma nova transação (entrada ou saída). |
| `/api/transactions` | `GET` | Lista todas as transações, com suporte a filtros por data e categoria. |
| `/api/transactions/{id}` | `PUT`/`DELETE` | Atualiza ou remove uma transação específica. |
| `/api/categories` | `POST`/`GET` | Gerencia as categorias financeiras e seus limites de orçamento. |
| `/api/reports/balance` | `GET` | Retorna o saldo total atual e o saldo por categoria, demonstrando consultas avançadas com EF Core. |

## Modelo de Dados (Entidades Chave)

O projeto utiliza um design de dados híbrido para otimizar o desempenho e a integridade.

| Entidade | Banco de Dados | Propriedades Chave (Exemplos) |
| :--- | :--- | :--- |
| **Transaction** | SQL Server (EF Core) | Id, Description, Amount, Type (Income/Expense), Date, CategoryId |
| **Category** | SQL Server (EF Core) | Id, Name, BudgetLimit |
| **LogEntry** | **Azure Table Storage** | PartitionKey (e.g., UserId), RowKey (e.g., Timestamp), Action, Payload |

## Estrutura do Projeto

A API é organizada usando uma arquitetura limpa, separando as responsabilidades em camadas para melhor manutenibilidade e testabilidade:

* `\src\FinTrack.API`: A camada de apresentação (Controllers, Middlewares).
* `\src\FinTrack.Core`: A camada de domínio (Entidades, Interfaces, Regras de Negócio).
* `\src\FinTrack.Infrastructure`: A camada de persistência de dados (Contextos do EF Core, Repositórios SQL e MongoDB).
* `\tests\FinTrack.UnitTests`: Projetos de testes unitários e de integração usando **XUnit**.

## Como Executar o Projeto Localmente

Para rodar a aplicação em sua máquina e replicar o ambiente, siga os passos abaixo:

### Pré-requisitos
* [.NET 8 SDK](https://dotnet.microsoft.com/download)
* SQL Server (Recomendado LocalDB ou Docker)
* Azure Storage Emulator (Azutite) ou acesso a uma conta de Azure Storage.

### 1. Clonagem e Configuração
```bash
git clone [https://github.com/SeuUsuario/FinTrack-API.git](https://github.com/SeuUsuario/FinTrack-API.git)
cd FinTrack-API
```

### 2. Configuração do Banco de Dados
Abra o arquivo appsettings.Development.json e configure as connection strings para o SQL Server (DefaultConnection) e para o MongoDB (MongoDbSettings).

### 3. Migrações do Entity Framework
Execute as migrações para criar o esquema do banco de dados SQL e garantir que o Entity Framework está configurado corretamente:
```bash
dotnet ef database update --project FinTrack.Infrastructure
```

### 4. Execução da API
Execute o projeto principal na raiz do seu terminal:
```bash
dotnet run --project FinTrack.API
```

A API estará acessível em https://localhost:5001 (ou na porta definida na sua configuração).

## ✅ Validação e Resiliência (Testes Unitários)

A camada de testes unitários é o que garante a resiliência deste sistema financeiro. O foco é testar as regras de negócio críticas, validando o pilar de **Resiliência** da sua formação.

* **Tecnologia:** XUnit e Moq.
* **Foco:**
    * **Teste de Lógica Financeira:** Garantir que o cálculo de saldo (`/api/reports/balance`) seja preciso, considerando entradas e saídas.
    * **Validação de Negócio:** Assegurar que transações inválidas (ex: valor negativo, data futura) sejam rejeitadas antes de tocar o banco de dados.
    * **Testes de Integração:** Verificar a comunicação correta entre os Repositórios (SQL/MongoDB) e os Serviços.

Para executar todos os testes, use o comando:

```bash
dotnet test --project FinTrack.UnitTests
```

## Link para o Deploy no Azure (Cloud Computing)

Esta seção demonstra o domínio do pilar Cloud Computing (Azure). O ambiente de produção da API e, opcionalmente, o banco de dados estão hospedados na nuvem.

* **Serviços Azure Utilizados:** App Service (para hospedagem da API) e, idealmente, Azure SQL Database

### Desenvolvido por: 
Sanderson de Oliveira Machado
[LinkedIn](www.linkedin.com/in/sandersonomachado) 