# [Kitty](https://github.com/kitty-project/kitty), a very lightweight Java microframework
### Sample
```java
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
        ).run(7000, () -> System.out.println("App is running on port " + 7000 + "..."));
    }
}

```
