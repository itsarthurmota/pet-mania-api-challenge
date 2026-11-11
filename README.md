# Pet Mania API - Desafio Back-end Spring Boot

Projeto desenvolvido como parte da atividade prática de análise, diagnóstico, correção e teste de uma API RESTful utilizando **Java com Spring Boot** e **Spring Data JPA**.

A aplicação tem como objetivo realizar o gerenciamento (CRUD) de animais de estimação para a plataforma **Pet Mania**, servindo como back-end para integração com uma aplicação front-end.

---
##  Como Executar o Projeto

1. **Clonar o repositório:**
   ```bash
   git clone https://github.com/itsarthurmota/pet-mania-api-challenge

2. Configurar o banco de dados (application.properties):
 Garantir que as configurações no arquivo src/main/resources/application.properties estejam apontando corretamente para o banco (H2 em memória ou MySQL).

3. Executar a aplicação:

 Pela sua IDE (IntelliJ IDEA, Eclipse, VS Code), execute a classe principal PetManiaApplication.java.

 Ou via terminal na raiz do projeto:
 
 **mvn spring-boot:run**
 
4. Acessar a API:
A aplicação estará rodando no endereço: http://localhost:8080/api/pets

##  Tecnologias Utilizadas

* **Java 17+** (ou superior)
* **Spring Boot 3. / 4.**
* **Spring Data JPA**
* **MySQL**
* **Maven**
* **Postman** (Testes de integração REST)

---

##  Diagnóstico e Correções Realizadas (Passo 2)

Durante a análise inicial do projeto, foram identificados diversos problemas de sintaxe, estrutura e regras de negócio no ecossistema Spring Boot/JPA. Abaixo estão as principais correções efetuadas:

### 1. Entidade (`Pet.java`)
* **Ajuste de Pacote:** Correção na sintaxe do `package`.
* **Mapeamento de Chave Primária:** O atributo `nome` estava incorretamente anotado com `@Id` e `@GeneratedValue`. Foi criado o campo `Long id` para atuar como chave primária autoincrementada.
* **Mapeamento JPA:** Adicionada a anotação `@Entity` e corrigida a sintaxe da anotação `@Table(name = "tb_pet")`.
* **Construtor Padrão:** Inclusão do construtor sem argumentos (`public Pet() {}`), requisito obrigatório do JPA.
* **Tipagem de Atributos e Encapsulamento:** Correção de incompatividades nos métodos *Getters* e *Setters* (ex: idade declarada como `int` com getter retornando `String`).

### 2. Repositório (`PetRepository.java`)
* **Generics e Tipos Wrapper:** Substituição da herança `CrudRepository<Pet, int>` por `JpaRepository<Pet, Long>`, corrigindo a utilização de tipo primitivo no ID.

### 3. Controller (`PetController.java`)
* **Anotações de Mapeamento:** Correção de erros ortográficos (`@RequestMapping`) e remoção da rota de dentro do `@RestController`.
* **Readequação de Verbos HTTP:**
  * Reorganização dos métodos HTTP (`@GetMapping` para listagem e `@PostMapping` para criação).
  * Adição da anotação `@RequestBody` no método de criação de pets.
* **Implementação de Endpoints Faltantes:**
  * Implementado o endpoint de busca por ID (`GET /api/pets/{id}`).
  * Implementado o endpoint de remoção (`DELETE /api/pets/{id}`).
* **Configuração de CORS:** Adicionada a anotação `@CrossOrigin("*")` para permitir a comunicação com o front-end web.

---

##  Endpoints da API REST

A API disponibiliza as seguintes rotas na rota base `/api/pets`:

| Método | Endpoint | Descrição | Corpo da Requisição (JSON) | Status Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | `/api/pets` | Listar todos os pets cadastrados | *Nenhum* | `200 OK` |
| **GET** | `/api/pets/{id}` | Buscar pet específico por ID | *Nenhum* | `200 OK` |
| **POST** | `/api/pets` | Cadastrar um novo pet | Exemplo abaixo | `200 OK` / `201 Created` |
| **DELETE** | `/api/pets/{id}` | Excluir um pet por ID | *Nenhum* | `200 OK` / `204 No Content` |

### Exemplo de JSON para Cadastro (`POST`):

```json
{
  "nome": "Rex",
  "especie": "Cachorro",
  "raca": "Labrador",
  "idade": 3,
  "sexo": "Macho",
  "porte": "Grande",
  "personalidade": "Dócil e brincalhão",
  "foto": "[https://images.unsplash.com/photo-1552053831-71594a27632d](https://images.unsplash.com/photo-1552053831-71594a27632d)",
  "disponivel": true
}
```




## Anexos





