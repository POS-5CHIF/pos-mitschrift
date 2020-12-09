# Spring Security

spring liefert standard-logindialog
default user `user` und password beim starten generiert und geloggt
default user auch über application.propierts konfigurierbar
rechte rollenbasiert

`spring.security.user.{name,password,roles} = ...`
`HTTPSession` bei Funktion mit `RequestMapping` in `@RestController`

Frontend speichert Session Key

Auth.Konfig.:
`@Configuration` und `extends WebSecurityConfigurerAdapter`
