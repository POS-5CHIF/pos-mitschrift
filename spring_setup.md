# Spring

[Initializr](https://start.spring.io/)

Dependencies:

- Dev Tools
- Web
- Data JPA
- H2 / Postgres
- Validation

`/h2-console` -> H2-Web-Oberfläche

application.properties:

```
server.port=8080
spring.datasource.url=jdbc:h2:mem:lab01
```

SQL files in resources-ordner
wenn `data.sql` genannt -> automatisch geladen

## Data Source festlegen

Connection type auf in-memory stellen
H2 auswählen
![Data Sources](res/data_sources.png)

## Entity

```java
@Entity
@Table(name="...")
```

Jedes Entity braucht einen parameterlosen Kunstruktor

Als GenerationType GenerationType.IDENTITY wählen

## Many-To-One

Many-Seite:

```java
@ManyToOne
@JoinColumn(name = "taet_mit_id")
private Mitarbeiter employee;
```

One-Seite:

```java
@OneToMany(mappedBy = "employee") // employee ist Bezeichner aus Taetigkeit-Klasse
List<Taetigkeit> taetigkeiten = new ArrayList<>();
```

# Repository

```java
@Repository
public interface MitarbeiterRepository extends JpaRepository<Mitarbeiter, String> {
    Mitarbeiter findAllByZuname(String zuname);
}

```

Oder mit `@Query` eigene Query

## Rest-Controller

```java
@RestController
public class AppController {
    // final
    private final MitarbeiterRepository mitarbeiterRepository;

    // Constructor-Injection
    public AppController(MitarbeiterRepository mitarbeiterRepository) {
        this.mitarbeiterRepository = mitarbeiterRepository
    }

}
```

### GET

```java
@GetMapping(path = "/employees")
public List<Mitarbeiter> getAllEmployees() {
    return mitarbeiterRepository.findAll();
}
```

### POST

ReponseEntity erstellen die 201 CREATED returned

```java
@PostMapping("/employees")
public ResponseEntity<Mitarbeiter> addMitarbeiter(@Valid @RequestBody Mitarbeiter mitarbeiter) {
    mitarbeiter = mitarbeiterRepository.save(mitarbeiter);

    URI uri = ServletUriComponentsBuilder.fromCurrentRequest().replacePath("/employee/{id}").
            build(mitarbeiter.getId());
    return ResponseEntity.created(uri).body(mitarbeiter);
}
```

## ExceptionHandler
