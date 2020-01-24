# Kitty, a very lightweight Java microframework
### Sample
```java
import app.UserService;
import kitty.Kitty;

public class App {
  public static void main(String[] args) {
    final UserService userService = new UserService();    
    Kitty
      .create(router -> router
        .get("/users", (request, response) -> response.status(200).body(userService.findAll()))
        .get("/users/{id}", (request, response) -> {
          final Integer id = request.param("id").asInt();
          return userService.findById(id)
            .map(user -> response.status(200).body(user))
            .orElse(response.status(404).body("User with " + id " was not found."));
        })
      )
      .run(8080);
  }
}
```
