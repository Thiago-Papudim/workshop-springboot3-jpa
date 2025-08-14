## &#x20;Workshop Spring Boot 3 + JPA

Uma API RESTful em Java com Spring Boot 3, Spring Data JPA e Hibernate, projetada para permitir operações de CRUD sobre várias entidades relacionadas. Ideal como base para estudo ou extensão com PostgreSQL, autenticação, testes, etc.

---

### &#x20;Objetivos

* Criar um projeto com Spring Boot 3 e Maven
* Modelar domínio com relacionamentos (1\:N, N:1, N\:N)
* Organizar camadas: *Resource*, *Service*, *Repository*
* Usar banco em memória H2 para testes
* Popular dados iniciais programaticamente
* Suportar operações CRUD completas
* Tratar exceções com respostas HTTP apropriadas
* Facilitar migração para PostgreSQL no ambiente de produção

---

### &#x20;Tecnologias

* **Java 17+** (requisito do Spring Boot 3)
* **Spring Boot 3**
* **Spring Data JPA + Hibernate**
* **H2 Database** (in-memory, para ambiente de dev/test)
* **Maven** (build & gerenciamento dependências)
* **Apache Tomcat** (servidor embarcado)
* **Postman** (ferramenta de testes)
* (Produção) **PostgreSQL** via `application-prod.properties`

---

### &#x20;Pré-requisitos

* Java 17 ou superior
* Maven
* Git

---

### &#x20;Como rodar

1. Clone o repositório:

   ```bash
   git clone https://github.com/Thiago-Papudim/workshop-springboot3-jpa.git
   cd workshop-springboot3-jpa
   ```
2. Execute a aplicação:

   ```bash
   ./mvnw spring-boot:run
   ```
3. Acesse o console H2 (em ambiente dev/test):
   `http://localhost:8080/h2-console`

   * **JDBC URL**: `jdbc:h2:mem:testdb`
   * **User**: `sa`
   * **Pass**: (vazio)

---

### &#x20;Endpoints REST

|                     Método                     | Endpoint       | Descrição                     |
| :--------------------------------------------: | :------------- | :---------------------------- |
|                       GET                      | `/users`       | Lista todos os usuários       |
|                       GET                      | `/users/{id}`  | Busca usuário por id          |
|                      POST                      | `/users`       | Cria novo usuário             |
|                       PUT                      | `/users/{id}`  | Atualiza usuário existente    |
|                     DELETE                     | `/users/{id}`  | Remove usuário (se permitido) |
|                       GET                      | `/orders`      | Lista todos os pedidos        |
|                       GET                      | `/orders/{id}` | Busca pedido por id           |
|                       GET                      | `/products`    | Lista todos os produtos       |
|                       GET                      | `/categories`  | Lista todas as categorias     |

---

### &#x20;Camadas do Projeto

1. **Controller (Resource)**: expõe endpoints REST, recebe e envia JSON.
2. **Service**: lógica de negócio, orquestra operações e lança exceções.
3. **Repository**: interfaces JpaRepository para persistência automática.
4. **Entities**: classes anotadas com `@Entity`, modelando o banco.
5. **DTOs**: evitam vazamento de modelo interno nas APIs.

---

### &#x20;Inicialização e População

Ao iniciar, a aplicação carrega dados de teste (`CommandLineRunner` típicos), facilitando execuções rápidas e testes via Postman ou Swagger.

---

### &#x20;Tratamento de Erros

Erros são interceptados e convertidos em respostas HTTP com status apropriado (ex.: `404 Not Found`, `400 Bad Request`), usando `@ControllerAdvice`.

---

### &#x20;Migração para PostgreSQL

Apenas crie um perfil `prod` com `application-prod.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/seubanco
spring.datasource.username=usuario
spring.datasource.password=senha
spring.jpa.hibernate.ddl-auto=update
```

E execute com:

```bash
./mvnw spring-boot:run -Dspring.profiles.active=prod
```

---

### &#x20;Referências & Boas Práticas

* **Spring Data JPA** elimina necessidade de repositórios manuais ([Home][1])
* Repositórios de CRUD já incluem métodos como `save()`, `findAll()`, `deleteById()` ([Home][1])
* Projeto segue estrutura recomendada de camadas, facilitando manutenção e testes

---

### &#x20;Como contribuir

1. Clone e crie uma branch: `git checkout -b feature/novo-recurso`
2. Faça suas alterações com padrão atual de código
3. Teste local com H2 e endpoints via Postman
4. Envie Pull Request para revisão

---

### &#x20;Autor

Thiago Papudim
🔗 \[[Site pessoal](https://thiago-papudim.github.io/imersaocss/)]

---
