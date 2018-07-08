# TP #2 - Configuration Java

## Partie 1 - Service

* Créer une interface `dev.paie.services.ENTITEService` :

```java
public interface ENTITEService extends CrudService<ENTITE> {
	
}
```

* Créer une implementation `dev.paie.services.ENTITEServiceMemoire` :

```java
@Service
public class ENTITEServiceMemoire implements ENTITEService {

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

* Créer une classe de test `dev.paie.services.ENTITEServiceMemoireTest` :

```java
// Sélection des classes de configuration Spring à utiliser lors du test
@ContextConfiguration(classes = { ENTITEServiceMemoire.class })
// Configuration JUnit pour que Spring prenne la main sur le cycle de vie du test
@RunWith(SpringRunner.class)
public class ENTITEServiceMemoireTest {

	@Autowired private ENTITEServiceMemoire service;

	// TODO tester toutes les méthodes du service
}
```

## Partie 2 - Mini application console avec Spring

* Créer (dans la partie test du projet), une application console qui permet de créer une instance d'ENTITE et de lister toutes les ENTITES.

```
*** ENTITE App ***
1. Créer
2. Lister
```