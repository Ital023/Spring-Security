# Spring Security Estudos Italo
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)

# Sobre o projeto
Este repositório é destinado aos meus estudos sobre Spring Security com OAuth2. O projeto implementa um Authorization Server e Resource Server, utilizando as interfaces do Spring Security para gerenciar autenticação e autorização, focando em práticas seguras e modernas para proteger APIs RESTful.

### Tecnologias Utilizadas

- *Back end*: Spring Boot, com foco em segurança, utilizando Spring Security e OAuth2. Aprofundei meus conhecimentos em criptografia de senhas com Bcrypt, gerenciamento de autenticação e autorização de login via tokens JWT, além de integração com Authorization e Resource Servers.

Esse projeto permitiu a implementação de práticas avançadas de segurança, criando uma aplicação robusta, segura e escalável.


## Modelo conceitual
![Modelo Conceitual](/assetsReadme/DER.png)

# Tecnologias utilizadas
## Back end
- Java
- Spring Boot
- JPA / Hibernate
- Maven
## Front end
- HTML / CSS / JS / TypeScript
- ReactJS
## Implantação em produção
- Back end: Heroku
- Front end web: Netlify
- Banco de dados: Postgresql

# Rotas
&#9679;	Produtos

| Método | Caminho                      | Descrição                                           | Role Necessária                  |
| ------ | ---------------------------- | -------------------------------------------------- | -------------------------------- |
| GET    | /products/{id}             | Retorna um produto específico pelo ID.              | Nenhuma                          |
| GET    | /products                  | Retorna uma lista paginada de produtos, podendo filtrar pelo nome. | Nenhuma            |
| POST   | /products                  | Adiciona um novo produto.                           | ROLE_ADMIN                     |
| PUT    | /products/{id}             | Atualiza os dados de um produto específico pelo ID. | ROLE_ADMIN                     |
| DELETE | /products/{id}             | Remove um produto específico pelo ID.               | ROLE_ADMIN                     |

&#9679;	Pedidos
| Método | Caminho                      | Descrição                                           | Role Necessária                      |
| ------ | ---------------------------- | -------------------------------------------------- | ------------------------------------ |
| GET    | /orders/{id}               | Retorna uma ordem específica pelo ID.              | ROLE_ADMIN ou ROLE_CLIENT        |
| POST   | /orders                    | Cria uma nova ordem.                               | ROLE_CLIENT                        |

&#9679;	Categorias
| Método | Caminho          | Descrição                                      | Role Necessária |
| ------ | ---------------- | --------------------------------------------- | --------------- |
| GET    | /categories    | Retorna a lista de todas as categorias.       | Nenhuma         |

&#9679;	Usuario
| Método | Caminho        | Descrição                                        | Role Necessária                      |
| ------ | -------------- | ----------------------------------------------- | ------------------------------------ |
| GET    | /users/me    | Retorna as informações do usuário autenticado.  | ROLE_ADMIN ou ROLE_CLIENT        |


# Como executar o projeto

## Back end
Pré-requisitos: Java 21

```bash
# clonar repositório
git clone https://github.com/Ital023/DSCommerce.git

# executar o projeto
./mvnw spring-boot:run
```

## Front end web
Pré-requisitos: npm / yarn

```bash
# clonar repositório
git clone https://github.com/Ital023/DSCommerce-FrontEnd.git

# instalar dependências
yarn install

# executar o projeto
yarn start
```
## 🤝 Colaboradores

Agradecemos às seguintes pessoas que contribuíram para este projeto:

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/Ital023" title="Github do Ítalo Miranda">
        <img src="https://avatars.githubusercontent.com/u/113559117?v=4" width="100px;" alt="Foto do Ítalo Miranda no GitHub"/><br>
        <sub>
          <b>Ítalo Miranda</b>
        </sub>
      </a>
    </td>
  </tr>
</table>
