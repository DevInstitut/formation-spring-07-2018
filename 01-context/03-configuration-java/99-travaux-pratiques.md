# TP #2 - Configuration Java

## Partie 1 - Repository

* Créer une interface `dev.paie.services.ENTITERepository` :

```java
public interface ENTITERepository extends CrudRepository<ENTITE> {
	
}
```

* Créer une implementation `dev.repositories.ENTITERepositoryMemoire` :

```java
@Service
public class ENTITERepositoryMemoire implements ENTITERepository {

    private List<ENTITE> entites = new ArrayList<>();
    
    /**
    * Initialiser la liste des entites
    */
    @PostConstruct
    public void initialiser() {
        // TODO créer un contexte avec la classe ClassPathXmlApplicationContext
        // TODO Récupérer les données via la méthode context.getBeansOfType(...)
        // TODO fermer le contexte
    }
    
    // TODO implémenter les méthodes
}
```

* Créer une classe de test `dev.repositories.ENTITERepositoryMemoireTest` :

```java
// Sélection des classes de configuration Spring à utiliser lors du test
@ContextConfiguration(classes = { ENTITERepositoryMemoire.class })
// Configuration JUnit pour que Spring prenne la main sur le cycle de vie du test
@RunWith(SpringRunner.class)
public class ENTITERepositoryMemoireTest {

	@Autowired private ENTITERepositoryMemoire repository;

	// TODO tester toutes les méthodes du repository
}
```

## Partie 2 - Mini application console avec Spring

* Créer (dans la partie test du projet), une application console qui permet de créer une instance d'ENTITE et de lister toutes les ENTITES.

```
*** ENTITE App ***
1. Créer
2. Lister
```