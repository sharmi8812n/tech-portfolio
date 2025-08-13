# 🌐 Spring Boot GraphQL CRUD Example

A sample **Spring Boot** application demonstrating a full **GraphQL API** with CRUD operations using **Spring for GraphQL**, **Spring Data JPA**, and an **H2 in-memory database**. This project includes queries, mutations, and an interactive **GraphiQL interface**.

---

## 📌 Features

- **CRUD Operations**: Create, Read, Update, Delete entities
- **GraphQL Queries & Mutations**: Define and resolve API operations
- **Spring Data JPA**: Database interaction with JPA repositories
- **H2 Database**: In-memory database for quick testing
- **GraphiQL Interface**: Interactive query editor
- **Spring Boot 3.x**: Quick setup with embedded Tomcat

---

## 🛠 Tech Stack

- **Java 17+**
- **Spring Boot 3.x**
- **Spring for GraphQL**
- **Spring Data JPA**
- **H2 Database**
- **GraphiQL**
- **Maven**

---

## Run the Application: mvn spring-boot:run
## Access GraphiQL Interface: http://localhost:8080/graphiql

type Author {
  id: ID!
  firstName: String!
  lastName: String!
}

type Book {
  id: ID!
  title: String!
  isbn: String!
  pageCount: Int!
  author: Author!
}

type Query {
  findAllBooks: [Book]
  findBookById(id: ID!): Book
}

type Mutation {
  newBook(title: String!, isbn: String!, pageCount: Int!, authorId: ID!): Book
  updateBook(id: ID!, title: String, isbn: String, pageCount: Int): Book
  deleteBook(id: ID!): Boolean
}


Fetch All Books:
query {
  findAllBooks {
    id
    title
    isbn
    pageCount
    author {
      firstName
      lastName
    }
  }
}

Create a New Book:
mutation {
  newBook(
    title: "Spring Boot in Action"
    isbn: "9781617292545"
    pageCount: 300
    authorId: 1
  ) {
    id
    title
  }
}

Update a Book:
mutation {
  updateBook(id: 1, title: "Updated Book Title") {
    id
    title
  }
}

Delete a Book:
mutation {
  deleteBook(id: 1)
}

