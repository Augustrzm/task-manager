# ✅ Task Manager

API de gerenciamento de tarefas construída com **Spring Boot**, em evolução.
Projeto de estudo de back-end Java.

## Tecnologias

- Java 17
- Spring Boot 4.1 (Web MVC, Data JPA, Validation, Security)
- PostgreSQL
- Lombok
- Maven (wrapper incluso, não precisa instalar o Maven)

## Pré-requisitos

- JDK 17+
- PostgreSQL rodando (ou Docker)

## Configuração (segredos fora do código)

A aplicação **não guarda senha no repositório**. Os dados do banco vêm de variáveis de ambiente:

| Variável | Descrição | Padrão |
|---|---|---|
| `DB_URL` | URL JDBC | `jdbc:postgresql://localhost:5432/taskmanager` |
| `DB_USER` | usuário | `taskmanager` |
| `DB_PASSWORD` | senha | *(obrigatória)* |

Um modelo está em [`.env.example`](.env.example).

Subindo um PostgreSQL local com Docker (troque a senha):

```bash
docker run --name taskmanager-db -e POSTGRES_DB=taskmanager \
  -e POSTGRES_USER=taskmanager -e POSTGRES_PASSWORD=troque_esta_senha \
  -p 5432:5432 -d postgres:16
```

## Executando

**Linux / macOS**
```bash
export DB_PASSWORD=troque_esta_senha
./mvnw spring-boot:run
```

**Windows (PowerShell)**
```powershell
$env:DB_PASSWORD = "troque_esta_senha"
.\mvnw.cmd spring-boot:run
```

## Testes

```bash
./mvnw test
```

Os testes usam banco **H2 em memória**, então não precisam de PostgreSQL.

## Segurança

- Credenciais via variáveis de ambiente; `.env` está no `.gitignore`
- `open-in-view` desativado e detalhes de erro (stack trace/mensagens) ocultos nas respostas
- Spring Security está no projeto: **configure as regras de acesso antes de expor endpoints**
  (por padrão, o Spring protege tudo com um usuário gerado automaticamente)
