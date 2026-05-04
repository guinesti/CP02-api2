# CP02-api2

# 📌 API REST - Esportes (Brasileirão e Olimpíadas)

Projeto desenvolvido para o **Checkpoint 2** da disciplina  
**Microservices and Web Engineering**

## 🚀 Tecnologias utilizadas

- Java 17+
- Spring Boot
- Spring Data JPA
- MySQL
- Swagger (Springdoc OpenAPI)
- Docker

---

## 📂 Estrutura do Projeto

- `model` → Entidades (Brasileirao, Olimpiadas)
- `repository` → Interfaces JPA
- `controller` → Endpoints REST (CRUD)

---

## 📊 Funcionalidades

A API permite:

### 📌 Brasileirão
- Criar campeonato
- Listar todos
- Buscar por ID
- Atualizar
- Deletar

### 📌 Olimpíadas
- Criar edição
- Listar todas
- Buscar por ID
- Atualizar
- Deletar

---

## 🔌 Configuração do Banco de Dados (Docker)

### 📦 Subindo MySQL com Docker

Execute o comando:

```bash
docker run -d \
  --name mysql-api \
  -e MYSQL_ROOT_PASSWORD=root_pwd \
  -e MYSQL_DATABASE=api \
  -p 3306:3306 \
  mysql:8
