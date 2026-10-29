# JNR-011 · Spring Boot — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a meal kit: the box arrives with sensible ingredients already chosen, and you swap any you dislike.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-011-L01 · What Boot adds to Spring (8 min)
**Goal:** state what Boot does on top of the Framework.

**Key points**
- Boot adds starters (dependency bundles), auto-configuration, an embedded server, and production features (Actuator).
- It sets defaults but never blocks you from changing them.
- Boot does not replace Spring; it configures it for you.
- The goal: `main` and a few properties give a running service.

**Show**
```java
@SpringBootApplication
public class ShopApiApplication {
    public static void main(String[] args) { SpringApplication.run(ShopApiApplication.class, args); }
}
```

**Check:** Does Boot replace the Spring Framework? *(No; it configures it.)*

---

## JNR-011-L02 · Starters (7 min)
**Goal:** explain what a starter is.

**Key points**
- A starter is one dependency that pulls in a tested set of libraries for a job.
- `spring-boot-starter-web` brings Spring MVC, Jackson, and an embedded server.
- Versions are managed by Boot's parent, so you rarely write library versions.
- Add only what the app needs.

**Show:** the `pom.xml` dependencies of the Shop API; then `./mvnw dependency:tree` for the web starter.

**Check:** Why do starters usually have no version? *(The Boot parent manages versions.)*

---

## JNR-011-L03 · Auto-configuration and conditions (12 min)
**Goal:** explain how Boot decides what to create.

**Key points**
- Auto-configuration classes are bundled with starters and run at startup.
- Each is guarded by conditions: `@ConditionalOnClass` (a library is present), `@ConditionalOnMissingBean` (you have not defined your own), `@ConditionalOnProperty`.
- Result: add a library and a bean appears; define your own bean and Boot backs off.
- Nothing magic: it is ordinary `@Configuration` with conditions.

**Show**
```java
@Bean
@ConditionalOnMissingBean
ObjectMapper objectMapper() { ... }   // simplified shape
```

**Check:** What does `@ConditionalOnMissingBean` mean for your own bean? *(Boot's default is skipped.)*

---

## JNR-011-L04 · Overriding defaults (8 min)
**Goal:** change Boot's behavior in the right order of preference.

**Key points**
- First choice: a property in `application.yml`.
- Second: a customizer bean for the component.
- Third: define your own bean of that type; Boot backs off.
- Excluding an auto-configuration is a last resort and needs a reason.

**Show**
```yaml
server:
  port: 8081
spring:
  jackson:
    default-property-inclusion: non_null
```

**Check:** Which is safer, property or exclusion? *(A property; exclusion removes everything that configuration provides.)*

---

## JNR-011-L05 · Embedded servers and executable JARs (8 min)
**Goal:** describe how the app runs as one file.

**Key points**
- The server (Tomcat by default) runs inside your app; you do not install one.
- `./mvnw package` produces an executable "fat" JAR containing your code and libraries.
- Run it with `java -jar target/shop-api-0.0.1-SNAPSHOT.jar`.
- Port and context path are settings, not install steps.

**Show:** `./mvnw package`, list `target/`, then `java -jar ...` and call `/actuator/health`.

**Check:** What do you need on the server to run the JAR? *(Only a Java runtime.)*

---

## JNR-011-L06 · Project structure conventions (7 min)
**Goal:** follow the standard layout.

**Key points**
- Main class in the top package; everything else below it.
- `src/main/resources`: `application.yml`, templates, static files.
- `src/test/java` mirrors the main packages.
- Keep config classes in a `config` package.

**Show:** tree: `com.shop.api` with `ShopApiApplication`, `products`, `config`.

**Check:** Why must the main class be in the top package? *(So scanning covers all sub-packages.)*

---

## JNR-011-L07 · Demo: reading the conditions evaluation report (12 min)
**Goal:** see why something was or was not configured; prepares JNR-011-LAB1.

**Steps**
1. Start the Shop API with `--debug` (or `debug=true`).
2. Find the "CONDITIONS EVALUATION REPORT" in the log.
3. Read "Positive matches": pick `DispatcherServletAutoConfiguration` and the condition that matched.
4. Read "Negative matches": pick `DataSourceAutoConfiguration` and note the missing class or bean.
5. **Planned mistake:** assume it is missing because of a bug; the report shows it is correctly skipped (no database starter present). Fix: confirm by adding the starter in a scratch branch and rerunning.

---

## JNR-011-L08 · Demo: overriding Jackson's auto-configuration (12 min)
**Goal:** change JSON date output in two ways.

**Steps**
1. Call an endpoint returning a date and observe the format (the default depends on version; verify version before recording).
2. Set a property such as `spring.jackson.serialization.write-dates-as-timestamps=false`; observe.
3. Define a `Jackson2ObjectMapperBuilderCustomizer` bean (or the customizer for the current Jackson line) to set a format.
4. **Planned mistake:** define a whole new `ObjectMapper` bean and lose Boot's module registration and settings. Fix: prefer the property or customizer; define your own mapper only when you need full control.
5. Check the conditions report: the default mapper bean is skipped when you define your own.
