# Configuration des vues

* Les classes d'implémentation de l'interface `ViewResolver` fournissent le mécanisme de sélection des vues selon un identifiant logique retourné par la méthode gestionnaire du controller.

* La plus courante d'utilisation avec les JSPs est InternalResourceViewResolver qui extrait la ressource depuis un chemin fabriqué avec le nom logique.

* Le nom logique est préfixé et suffixé pour fournir le chemin de la vue.

Exemple :

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/" />
    <property name="suffix" value=".jsp" />
</bean>
```