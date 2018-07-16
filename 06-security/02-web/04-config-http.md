# Configuration de base

* `@EnableWebSecurity` : pour activer la gestion de la sécurité (inutile pour Spring Boot).

* Créer une classe qui étend `WebSecurityConfigurerAdapter`.

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
    // Configuration de la partie HTTP
    // Les règles de sécurisation y sont définies
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        
        // toutes les requêtes doivent être authentifiées
    	http.authorizeRequests().anyRequest().authenticated()
    	
    	        // Permettre  aux utilisateurs de s'authentifier via une page d'authentification
    			.and().formLogin()
    			
    			// Permettre aux utilisateurs de s'authentifier via HTTP Basic Authentification
    			.and().httpBasic();
    }
    
    // Configuration de la source d'identité
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