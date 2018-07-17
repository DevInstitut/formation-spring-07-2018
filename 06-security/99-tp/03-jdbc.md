# Authentification via JDBC

## Hashage du mot de passe

* Compléter la classe _dev.config.WebSecurityConfig_ :

```java
...
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
...
public class WebSecurityConfig {
	
    // le bean `passwordEncoder` contient l'algorithme de hashage des mots de passe de l'application.
	@Bean
	public PasswordEncoder passwordEncoder() {
	    return new BCryptPasswordEncoder();
	}
	...

}
```

Voici un exemple d'utilisation de ce bean :

```java
@Service
public class SuperService {

	private PasswordEncoder passwordEncoder;
	
	public SuperService(PasswordEncoder passwordEncoder) {
	    this.passwordEncoder = passwordEncoder;
	}

	@Override
	public void utiliserAlgoEncodage() {
	    
		String iciUnMotDePasse = "topSecret";
		
		String iciMotDePasseHashe = this.passwordEncoder.encode(iciUnMotDePasse);
	}

}
```

## Configuration JDBC

L'authentification va être désormais pilotée par une table `utilisateur`.


* Compléter la configuration `dev.config.WebSecurityConfig` comme suit :

```java
...
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
 
    
    @Bean
    public UserDetailsService userDetailsService(DataSource ds) {
        // changement de stratégie Mémoire => JDBC
        JdbcUserDetailsManager manager = new JdbcUserDetailsManager();
        
        // configuration de la source de données
        manager.setDataSource(ds);
        
        // requête pour obtenir les informations d'un utilisateur en fonction du nom d'utilisateur
        manager.setUsersByUsernameQuery("select identifiant, mot_de_passe, 'true' from utilisateur where identifiant=?");
        
        // requête pour obtenir les rôles d'un utilisateur
        manager.setAuthoritiesByUsernameQuery("select identifiant, profil from profil_utilisateur where identifiant=?");

        return manager;
    }

}

```


* Compléter les scripts pour ajouter la table utilisateur.

* Compléter les scripts pour ajouter quelques données.

* Vérifier que l'authentification fonctionne.
