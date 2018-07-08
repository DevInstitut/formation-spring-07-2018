# TP #1 - Configuration XML

Objectif :
* Comprendre la création du contexte Spring.
* Comprendre le mécanisme d'injection de dépendance.

## Modèle métier

![](images/entites.png)

> Répartissons les sujets.

## Github

* Créer un fork du projet `evalme-back`.
* Importer le projet sur votre poste.
* Ouvrir STS (Spring Tools Suite).
* Importer le projet Maven.


## Fichier XML de jeu de données

* Créer un fichier de jeu de données : `src/main/resources/jdd/jdd-ENTITE.xml` (remplacer `ENTITE` par le nom de votre entité). 

```xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	
    <!-- TODO -->

</beans>
```

* Y ajouter 3 objets complets.

## Test Unitaire du jeu de données

*  Créer un test unitaire `dev.entites.JddENTITETest_ de la forme suivante :
  
  ```java
  public class JddENTITETest {
  
  	private ClassPathXmlApplicationContext context;
  
  	@Before
  	public void onSetup() {
  		context = new ClassPathXmlApplicationContext("jdd/jdd-ENTITE.xml");
  		
  	}
  
      @Test
  	public void test_ENTITE_1() {
  		Entite entite1 = context.getBean("bulletin1", Entite.class);
  		
  		// TODO Ajouter des assertions
  	}
  
  	@Test
  	public void test_ENTITE_2() {
  		// TODO
  	}
  
  	@Test
  	public void test_ENTITE_3() { 
  	    // TODO
  	}
  	
  	@After
  	public void onExit() {
  		context.close();
  	}
  
  }
```