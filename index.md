# [Kitty](https://github.com/kitty-project/kitty), a very lightweight Java microframework
### Sample
```java
import kitty.HttpMethod;
import kitty.HttpStatus;
import kitty.Kitty;

public class App {
    public static void main(String[] args) {
        final UserService userService = new UserService();
        Kitty.create(router -> router
            .get("/users", (request, response) -> response.status(HttpStatus.OK).body(userService.findAll()))
            .get("/users/{id}", (request, response) -> {
                final Integer id = request.pathParam("id").asInt();
                return userService.findById(id)
                    .map(user -> response.status(200).body(user))
                    .orElse(response.status(404).body("User with " + id + " was not found."));
            })
            .anyOf(Set.of(HttpMethod.GET, HttpMethod.POST), "/kumusta", (request, response) -> response.body("Kumusta?"))
            .any("/how-are-you", (request, response) -> response.body("How are you?"))
        ).run(7000, () -> System.out.println("App is listening on port " + 7000 + "..."));
    }
}

```