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

# Comunicação Resource Server e Authorization Server
<img src="/assetsReadme/OAuth2.png" alt="ResourceAuthorizationServer" width="500">


## Implentação Oauth2 (Passo a Passo)

### Passo 1 (Persistencia das entidades) : 
- Criar as entidades referentes ao diagrama.
- User deve ter um relacionamento muitos pra muitos com roles.
  ```
  @ManyToMany
  @JoinTable(name = "tb_user_role",
          joinColumns = @JoinColumn(name = "user_id"),
        inverseJoinColumns = @JoinColumn(name = "role_id")
    )
    private Set<Role> roles = new HashSet<>();

  ```
  
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
- Criação da entidade Role (ID, Authority) as (1, ROLE_ADMIN)
```
@Entity
@Table(name = "tb_role")
public class Role {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String authority;

   constructor() ...

   get & setters () ...

}

```

### Passo 2 (Adicionar Spring Security) : 
- Adicionando as dependências no pom.xml
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
### Passo 3 (Implementar as interfaces Spring Security) : 
  Entidade User: 
  ```
public class User implements UserDetails {

  // É necessário Role implementar de GrantedAuthority 
  @Override // Aqui ficara a collection de roles do usuário, como definimos o atributo roles como isso retornamos roles
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return roles;
    }

    @Override // Retornar o atributo que representa o username do usuario, ou seja, o atributo unico que diferencia dos demais
    public String getUsername() {
        return email;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }

}
  ```

Entidade Role: 
  ```
public class Role implements GrantedAuthority {
  @Override //Retorna qual é o valor representado pela authority like (ROLE_ADMIN)
      public String getAuthority() {
          return authority;
      }
}
  ```

Camada Service: 
  ```
@Service
public class UserService implements UserDetailsService {

  @Autowired
    private UserRepository repository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

        List<UserDetailsProjection> result = repository.searchUserAndRolesByEmail(username);

        if(result.size() == 0) {
            throw new UsernameNotFoundException("User Not Found");
        }

        User user = new User();
        user.setEmail(username);
        user.setPassword(result.get(0).getPassword());
        for(UserDetailsProjection projection : result) {
            user.addRole(new Role(projection.getRoleId(), projection.getAuthority()));
        }


        return user;

}
  ```
### Passo 4 (Configuração do OAuth2) :
- Configurar o application.properties
  
  ```
  security.client-id=${CLIENT_ID:myclientid}
  security.client-secret=${CLIENT_SECRET:myclientsecret}
  
  security.jwt.duration=${JWT_DURATION:86400}
  
  cors.origins=${CORS_ORIGINS:http://localhost:3000,http://localhost:5173}
  ```
- Adicionando as dependências no pom.xml
  ```
  <dependency>
  	<groupId>org.springframework.security</groupId>
  	<artifactId>spring-security-oauth2-authorization-server</artifactId>
  </dependency>
  
  <dependency>
  	<groupId>org.springframework.boot</groupId>
  	<artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
  </dependency>
  
  ```
- Adicionar os arquivos AuthorizationServerConfig, ResourceServerConfig e o pacote customgrant as a library





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
