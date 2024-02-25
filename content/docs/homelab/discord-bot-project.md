---
title: "Discord Bot Project"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
## Discord Bot Project with WebUI

**Backend (Discord Bot)**

* **Language:** Java 17
* **Libraries:**
    * [Javacord: Discord bot library](https://javacord.org/)
    * [Jackson: JSON serialization/deserialization](https://github.com/FasterXML/jackson)
    * [Lombok: simplifies boilerplate code](https://projectlombok.org/)

**API Server**
* **Framework:** [Spring Boot](https://spring.io/quickstart) (Java)
    * **Reasoning:** Mature and well-established framework for building REST APIs in Java. Offers features like dependency injection, auto-configuration, and built-in web server.

**Frontend (WebUI):**

* **Framework:** Svelte
    * **Reasoning:** Highly dynamic and performant framework with built-in animation capabilities. Supports Material Design icons and theming out of the box. Relatively easy to learn compared to other complex frameworks.

**Communication:**

* RESTful API using Spring Boot for defined endpoints.
* Utilize Jackson for data serialization/deserialization between modules.

**Additional Considerations:**

* **Database:** Consider using a database like PostgreSQL or MySQL to store persistent data (e.g., bot statistics, user preferences).
* **Deployment:** Leverage Kubernetes for containerized deployment and management of all modules.
* **Security:** Implement authentication and authorization mechanisms for both API server and WebUI access.

**Learning Resources:**

* Spring Boot: [https://start.spring.io/](https://start.spring.io/)
* Svelte: [https://svelte.dev/docs](https://svelte.dev/docs)
* Javacord: [https://github.com/Discord4J/Discord4J](https://github.com/Discord4J/Discord4J)
* Jackson: [https://github.com/FasterXML/jackson](https://github.com/FasterXML/jackson)
* Lombok: [https://mvnrepository.com/artifact/org.projectlombok/lombok](https://mvnrepository.com/artifact/org.projectlombok/lombok)

**Getting Started:**

1. **Backend (Discord Bot):**
    * Familiarize yourself with Javacord library for interacting with the Discord API.
    * Define bot functionalities and implement communication with the API server using REST calls.

```java
import me.koply.kcommando.KCommando;
import me.koply.kcommando.integration.impl.javacord.JavacordIntegration;
import org.javacord.api.DiscordApi;
import org.javacord.api.DiscordApiBuilder;
import org.javacord.api.entity.intent.Intent;
try {
            DiscordApi api = new DiscordApiBuilder()
                    .setToken(token)
                    .addIntents(Intent.MESSAGE_CONTENT)
                    .addIntents(Intent.GUILDS)
                    .login().join();

            if (args.length == 1) {
                logger.info("Setting bot status to match Git Commit of " + args[0]);
                api.updateActivity("v." + args[0]);
            } else {
                logger.info("Setting bot status to match internal version of " + Constants.VERSION);
                api.updateActivity("v." + Constants.VERSION);
            }

            JavacordIntegration jci = new JavacordIntegration(api);
            KCommando kc = new KCommando(jci)
                    .addPackage(Command.class.getPackageName())
                    .setReadBotMessages(false)
                    .setPrefix("/")
                    .setOwners(Constants.OWNER_ID)
                    .setVerbose(false);
        catch (Exception e) {
            logger.error(e.getMessage());
        }                    
```                    

2. **API Server (Spring Boot):**
    * Set up a Spring Boot project and define REST API endpoints for the WebUI to interact with.
    * Implement logic to handle requests, interact with the bot backend, and potentially store data in a database.

```java
@RestController
@RequestMapping("/api/v1/bot")
public class BotController {

    @Autowired
    private BotService botService;

    @GetMapping("/statistics")
    public ResponseEntity<Map<String, Object>> getStatistics() {
        Map<String, Object> statistics = botService.getStatistics();
        return ResponseEntity.ok(statistics);
    }
}
```
```java
public interface BotService {

    Map<String, Object> getStatistics();
}
```
3. **Frontend (WebUI):**
    * Learn the basics of Svelte for building web applications.
    * Utilize Svelte's features for dynamic UI updates and animations.
    * Integrate Material Design icons and explore theming options.

4. **Deployment:**
    * Containerize each module using Docker.
    * Deploy them to a Kubernetes cluster for managing deployments and scaling.

