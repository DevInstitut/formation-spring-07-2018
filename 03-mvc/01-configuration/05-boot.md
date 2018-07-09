# Dans Spring Boot

## Starter Web


```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## Support de JSP (comme moteur de templating)

```xml
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
    <scope>provided</scope>
</dependency>
```

## JSTL

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
</dependency>
```

## Configuration des vues (ViewResolver)

Dans le fichier `application.properties`.

```properties
# mvc
spring.mvc.view.prefix = /pages/
spring.mvc.view.suffix = .jsp
```