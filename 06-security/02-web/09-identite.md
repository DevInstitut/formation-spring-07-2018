# Configurer le gestionnaire d'identité

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Bean
    @Override
    public UserDetailsService userDetailsService() {
        // Ici une gestion en "mémoire" des utisateurs
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        
        // Création d'un utilisateur en "dur"
        manager.createUser(
                User.withDefaultPasswordEncoder().username("user").password("password").roles("USER").build());
        return manager;
    }
}
```

## Identité stockée en base de données

Schéma base de données par défaut : voir https://docs.spring.io/spring-security/site/docs/current/reference/html/appendix-schema.html.

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
    // Choix de l'algorithme d'encodage du mot de passe
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    // Définition d'une stratégie de gestion d'identité stockée en base de données.
    @Bean
    public UserDetailsService userDetailsService(DataSource ds) {
        JdbcUserDetailsManager manager = new JdbcUserDetailsManager();
        manager.setDataSource(ds);
        manager.setUsersByUsernameQuery("select identifiant, mot_de_passe, 'true' from utilisateur where identifiant=?");
        manager.setAuthoritiesByUsernameQuery("select identifiant, profil from utilisateur where identifiant=?");
        return manager;
    }
}
```