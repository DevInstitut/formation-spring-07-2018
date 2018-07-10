# Support de Bean Validation

Spring Web MVC offre un support de Bean Validation (Spécification Java EE de validation d'objet Java).


Dépendances Maven :

```xml
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
    <version>${validation-api.version}</version>
</dependency>

<!-- Implémentation la plus utilisée de Bean Validation -->
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>${hibernate-validator.version}</version>
</dependency>
```


## Validation d'un Bean

Les contraintes peuvent être posées directement sur les champs de l'entité à valider.

Exemple :


```java

import javax.validation.constraints.Email;
import javax.validation.constraints.NotEmpty;
import javax.validation.constraints.Size;

public class Personne {

	@NotEmpty
	private String prenom;
	
	@NotEmpty
	@Size(min = 3)
	private String nom;
	
	@Email
	private String email;
    
	// ...
		
}
```

## Activation de la validation avec Spring MVC

L'annotation `@Valid` positionnné sur un objet active sa validation.

Le paramètre `BindingResult` donne accès au résultat de la validation.

```java

    @RequestMapping(method = RequestMethod.POST)
    public ModelAndView post(@ModelAttribute("personne") @Valid Personne st, BindingResult bindingResult) {
        
        if(bindingResult.hasErrors()) {
            
            // en cas d'erreur
            
        } else {
            
            // en cas de succès
        }
        
        // Il est possible de créer ses propres erreurs de validation
        
        bindingResult.reject("errors.obj", "L'objet personne n'est pas comme je veux");
        
        bindingResult.rejectValue("prenom", "errors.prenom", "Le champ prénom n'est pas comme je veux");
        
        // ...
        ModelAndView mv = new ModelAndView();
        
        // ...
        return mv;
    }

```

## Prise en compte de la validation dans la vue

Le tag `<form:errors path="">` permet d'afficher un message d'erreur issu de la validation.

* Exemple d'affichage d'erreurs par champ :

```html
<form:form modelAttribute="personne">

    <form:input path="nom"></form:input>
    <form:errors path="nom"></form:errors>
    
    <form:input path="prenom"></form:input>
    <form:errors path="prenom"></form:error>

    <input type="submit" value="Valider">
</form:form>

```

* Exemple d'affichage d'erreurs en global


```html
<form:form modelAttribute="personne">

    <form:input path="nom"></form:input>
    <form:input path="prenom"></form:input>

    <!-- affiche de toutes les erreurs -->
    <form:errors path="*"></form:errors>

    <input type="submit" value="Valider">
</form:form>

```

* Personnalisation du message dans la page HTML.


```html
<form:form modelAttribute="personne">

    <form:input path="nom"></form:input>
    
    <form:errors path="nom">
        <p>Message personnalisé</p>
    </form:errors>
    
    <form:input path="prenom"></form:input>
    <form:errors path="prenom"></form:error>

    <input type="submit" value="Valider">
</form:form>

```

