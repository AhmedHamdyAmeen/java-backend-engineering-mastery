# JNR-008 · Spring ecosystem — Lecture scripts

**Video:** 40 min · **Analogy used throughout:** a well-equipped workshop: tools, power, and a starter kit so you do not build the workbench first.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-008-L01 · Why frameworks exist (7 min)
**Goal:** explain what problem a framework solves for the Shop API.

**Key points**
- Every web service needs the same plumbing: receive HTTP, create objects, connect them, read settings, handle errors.
- A library is code you call. A framework is code that calls yours.
- Without a framework you wire every object by hand with `new`, and you rewrite the plumbing in each project.
- Spring takes over creating and connecting objects so you write business code.

**Show**
```java
// by hand: you build the whole chain
var repo = new InMemoryProductRepository();
var service = new ProductService(repo);
var controller = new ProductController(service);
```
Then say: "Now imagine 60 classes."

**Check:** Library or framework: who calls whom? *(A framework calls your code; you call a library.)*

---

## JNR-008-L02 · The Spring family (10 min)
**Goal:** tell the main Spring projects apart.

**Key points**
- **Spring Framework:** the core: the container, dependency injection, web MVC, testing support.
- **Spring Boot:** starters and auto-configuration so an app runs with almost no setup.
- **Spring Data:** repositories over databases with little code (used from JNR-P4).
- **Spring Security:** login, permissions, and protection against common attacks (JNR-P5).
- They are layered: Boot sits on top of the Framework; Data and Security plug in.

**Show:** a stack diagram: Spring Framework at the bottom, Boot on it, Data and Security as side blocks, the Shop API on top.

**Check:** Which project decides what to configure automatically? *(Spring Boot.)*

---

## JNR-008-L03 · Spring Initializr walkthrough (8 min)
**Goal:** generate a project and name its parts.

**Key points**
- Initializr is the project generator at start.spring.io (also built into IDEs).
- Choose: build tool (Maven), language (Java), Boot version, group, artifact, Java version.
- Add dependencies (starters): Spring Web, Validation, Actuator for the Shop API.
- The result: `pom.xml`, `mvnw`, `src/main/java` with an `@SpringBootApplication` class, `src/main/resources/application.properties`, `src/test`.

**Show:** the generated tree and the `pom.xml` parent `spring-boot-starter-parent`. Use the current stable Boot version (verify version before recording).

**Check:** Which file lets you build without installing Maven? *(`mvnw`, the Maven wrapper.)*

---

## JNR-008-L04 · Reading Spring's documentation (5 min)
**Goal:** find answers in the official docs.

**Key points**
- Docs live at docs.spring.io; each project has a reference guide and API docs.
- Pick the page that matches your version.
- Search the reference for the concept, then the API docs for exact names.
- The Boot "Application Properties" appendix lists every setting.

**Show:** open the Boot reference, find "Actuator endpoints", and locate `management.endpoints.web.exposure.include`.

**Check:** Why check the docs version? *(Features and names change between versions.)*

---

## JNR-008-L05 · Demo: first Spring Boot app from Initializr to running endpoint (10 min)
**Goal:** go from nothing to a running app answering `/actuator/health`; prepares JNR-008-LAB1.

**Steps**
1. Open Initializr; pick Maven, Java, current Boot; name it `shop-api`.
2. Add Spring Web, Validation, Actuator. Download and unzip; open in the IDE.
3. **Planned mistake:** add five extra starters "just in case" and watch startup grow and fail on a missing database setting. Fix: remove everything you do not need.
4. Run `./mvnw spring-boot:run` and read the startup log (port, "Started ShopApiApplication").
5. Open `http://localhost:8080/actuator/health` and see `{"status":"UP"}`.
6. Stop the app with Ctrl+C.
