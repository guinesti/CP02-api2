# CP02 - API REST com Spring Boot - API 2

API REST desenvolvida com Spring Boot para o Checkpoint 02 da FIAP.  
O projeto contém dois domínios: **Brasileirão** (campeonato brasileiro) e **Olimpíadas** (edições dos jogos olímpicos).

---

## Tecnologias utilizadas

- Java 17
- Spring Boot 4.0.3
- Spring Data JPA
- MySQL 8
- Lombok
- SpringDoc OpenAPI (Swagger UI)
- Docker
---

## Pré-requisitos

- [Java 17+](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- [Maven](https://maven.apache.org/)
- [Docker](https://www.docker.com/)
---

## 1. Subindo o banco de dados com Docker

Antes de rodar a aplicação, suba o MySQL via Docker com o comando abaixo no terminal (Git Bash ou PowerShell):

```bash
docker run -d \
  --name mysql-api \
  -e MYSQL_ROOT_PASSWORD=root_pwd \
  -e MYSQL_DATABASE=api \
  -p 3306:3306 \
  mysql:8
```

Verifique se o container está rodando:

```bash
docker ps
```

Você deve ver o container `mysql-api` listado com a porta `3306` mapeada.

> **Atenção:** toda vez que reiniciar o computador ou o Docker, rode o comando acima novamente antes de iniciar a aplicação.

---

## 2. Configuração do banco

O arquivo `src/main/resources/application.properties` já está configurado para conectar ao MySQL local:

```properties
server.port=8080

springdoc.swagger-ui.path=/

spring.datasource.url=jdbc:mysql://localhost:3306/api?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=root_pwd

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```

O banco `api` é criado automaticamente na primeira execução.

---

## 3. Rodando a aplicação

Com o Docker rodando, execute na raiz do projeto:

```bash
mvn spring-boot:run
```

A aplicação estará disponível em: **http://localhost:8080**

---

## 4. Documentação interativa (Swagger UI)

Acesse a documentação e teste os endpoints diretamente pelo navegador:

```
http://localhost:8080
```

---

## 5. Endpoints disponíveis

### Brasileirão — `/campeonatobrasileiro`

| Método | Rota                         | Descrição                  |
|--------|------------------------------|----------------------------|
| GET    | `/campeonatobrasileiro`      | Lista todos os campeonatos |
| GET    | `/campeonatobrasileiro/{id}` | Busca campeonato por ID    |
| POST   | `/campeonatobrasileiro`      | Cria um novo campeonato    |
| PUT    | `/campeonatobrasileiro/{id}` | Atualiza um campeonato     |
| DELETE | `/campeonatobrasileiro/{id}` | Remove um campeonato       |

#### Exemplo de body (POST/PUT):
```json
{
  "id": 1,
  "campeao": "Flamengo",
  "artilheiro": "Pedro",
  "revelacao": "Endrick",
  "goleada": "Flamengo 6x0 Vasco"
}
```

---

### Olimpíadas — `/olimpiadas`

| Método | Rota               | Descrição              |
|--------|--------------------|------------------------|
| GET    | `/olimpiadas`      | Lista todas as edições |
| GET    | `/olimpiadas/{id}` | Busca edição por ID    |
| POST   | `/olimpiadas`      | Cria uma nova edição   |
| PUT    | `/olimpiadas/{id}` | Atualiza uma edição    |
| DELETE | `/olimpiadas/{id}` | Remove uma edição      |

#### Exemplo de body (POST/PUT):
```json
{
  "id": 1,
  "ano": "2024",
  "sede": "Paris",
  "maiorMedalhista": "Estados Unidos",
  "maiorVencedor": "Léon Marchand"
}
```

> **Atenção:** o campo `id` deve ser enviado manualmente no body, pois não é gerado automaticamente.

---

## 6. Estrutura do projeto

```
src/main/java/br/com/fiap/cp01_api02/
├── Application.java
├── controller/
│   ├── BrasileiraoController.java
│   └── OlimpiadasController.java
├── model/
│   ├── Brasileirao.java
│   └── Olimpiadas.java
└── repository/
    ├── BrasileiraoRepository.java
    └── OlimpiadasRepository.java
```
 
