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

## Implentação Oauth2 (Passo a Passo)

### Passo 1 (Persistencia das entidades) : 
- Criar as entidades referentes ao diagrama.
- User deve ter um relacionamento muitos pra muitos com roles.
- Utilização de Set<> para não haver objetos repetidos na estrutura de dados
- Métodos addRole ``` public void addRole(Role role) {
        roles.add(role);
    } ```
- Métodos hasRole
  ```
  public boolean hasRole(String roleName) {
        for(Role role : roles) {
            if(role.getAuthority().equals(roleName)) return true;
        }
        return false;
    }
  ```
### Passo 2 (Adicionar Spring Security) : 
  ```
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
  </dependency>
  
  <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-test</artifactId>
      <scope>test</scope>
  </dependency>
  ```
 - Desativar as restrições default do Spring Security
    
    ```
    @Configuration
    public class SecurityConfig {
    
    	@Bean
    	public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    		http.csrf(csrf -> csrf.disable());
    		http.authorizeHttpRequests(auth -> auth.anyRequest().permitAll());
    		return http.build();
    	}
    
    }
    ```
- Adicionar o componente de encode de caracteres no SecurityConfig
    ```
    @Bean
    public PasswordEncoder getPasswordEncoder() {
        return new BCryptPasswordEncoder();
    }
    ```






# Tecnologias utilizadas
## Back end
- Java
- Spring Boot
- JPA / Hibernate
- Maven
- Oauth2
- Resource Server
- Authorization Server
  

# Rotas
&#9679;	Produtos

| Método | Caminho                      | Descrição                                           | Role Necessária                  |
| ------ | ---------------------------- | -------------------------------------------------- | -------------------------------- |
| GET    | /products                  | Retorna uma lista de produtos                        | Nenhuma            |
| GET    | /products/{id}             | Retorna um produto específico pelo ID.              | Nenhuma                          |
| POST   | /products                  | Adiciona um novo produto.                           | Nenhuma                     |

# Como executar o projeto

## Back end
Pré-requisitos: Java 17

```bash
# clonar repositório
git clone https://github.com/Ital023/Spring-Security.git

# executar o projeto
./mvnw spring-boot:run
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
