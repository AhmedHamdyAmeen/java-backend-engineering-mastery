# JNR-002 · Maven in depth — Lecture scripts

**Video:** 70 min · **Analogy used throughout:** a shopping list for a kitchen: you list the ingredients you need, and the supplier also brings the ingredients those ingredients need.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-002-L01 · Dependency scopes (8 min)
**Goal:** choose the right scope for each dependency.

**Key points**
- A scope says when a dependency is needed: compile, test, or run.
- `compile` (default): needed to build and run. Example: a library you call in your code.
- `provided`: needed to build, but the server supplies it at run time.
- `runtime`: not needed to compile, only to run. Example: a database driver.
- `test`: only for tests. Example: JUnit. Never use `compile` for test libraries.

**Show**
```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>${junit.version}</version>
  <scope>test</scope>
</dependency>
```

**Check:** Which scope for a JDBC driver you never call directly? *(`runtime`.)*

---

## JNR-002-L02 · Transitive dependencies and `dependency:tree` (10 min)
**Goal:** see everything your project really pulls in.

**Key points**
- Your dependency has its own dependencies. These are transitive.
- Like the supplier who brings the ingredients' ingredients.
- `mvn dependency:tree` prints the whole tree.
- Use it to find where a library comes from and why it is there.
- More transitive jars means more risk: size, conflicts, security.

**Show**
```
[INFO] com.shop:shop-core:jar:1.0
[INFO] +- com.google.guava:guava:jar:33.0.0:compile
[INFO] |  \- com.google.guava:failureaccess:jar:1.0.2:compile
```
(Versions are examples; verify before recording.)

**Check:** Which command shows transitive dependencies? *(`mvn dependency:tree`.)*

---

## JNR-002-L03 · Version conflicts and dependency management (10 min)
**Goal:** resolve two versions of the same library.

**Key points**
- Two dependencies may need different versions of one library. Maven picks one jar.
- Default rule: the nearest definition in the tree wins, not the newest.
- That may pick a version that breaks the other library.
- Fix it with `<dependencyManagement>`: you state the version once, for everyone.
- `<exclusions>` remove a dependency you do not want.

**Show**
```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>${jackson.version}</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```

**Check:** Which version does Maven pick in a conflict by default? *(The nearest one in the tree.)*

---

## JNR-002-L04 · BOMs (7 min)
**Goal:** align many versions with one import.

**Key points**
- A BOM (bill of materials) is a POM that lists tested, matching versions.
- You import it in `dependencyManagement` with scope `import` and type `pom`.
- Then you add dependencies without versions.
- Spring Boot uses a BOM so hundreds of libraries match each other.
- Update one version number, and the whole set moves together.

**Show**
```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>${boot.version}</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

**Check:** Why does Spring Boot use a BOM? *(So all its libraries use versions tested together.)*

---

## JNR-002-L05 · Plugins and the build lifecycle revisited (10 min)
**Goal:** configure the common plugins.

**Key points**
- Lifecycle phases: `validate`, `compile`, `test`, `package`, `verify`, `install`, `deploy`.
- Plugins do the work in each phase.
- Compiler plugin: sets the Java release, for example `<release>`.
- Surefire runs unit tests (`*Test`) in the `test` phase.
- Failsafe runs integration tests (`*IT`) in `integration-test` and checks them in `verify`.

**Show**
```xml
<plugin>
  <artifactId>maven-compiler-plugin</artifactId>
  <configuration><release>${java.version}</release></configuration>
</plugin>
```

**Check:** Which plugin runs integration tests? *(Failsafe.)*

---

## JNR-002-L06 · Multi-module projects (10 min)
**Goal:** split one project into modules with a parent POM.

**Key points**
- A parent POM has `<packaging>pom</packaging>` and lists `<modules>`.
- Each module has its own POM and points to the parent.
- Shared versions and plugin settings live in the parent.
- One command builds all modules in the right order.
- Example: `shop-core` (domain) and `shop-cli` (depends on core).

**Show**
```
shop/
  pom.xml          (parent: modules shop-core, shop-cli)
  shop-core/pom.xml
  shop-cli/pom.xml (depends on shop-core)
```

**Check:** What packaging does a parent POM use? *(`pom`.)*

---

## JNR-002-L07 · Reproducible builds and the Maven Wrapper (5 min)
**Goal:** make the build give the same result on every machine.

**Key points**
- A reproducible build: the same source gives the same output anywhere.
- Fix every version; avoid ranges and `LATEST`.
- The Maven Wrapper (`mvnw`) downloads the exact Maven version the project needs.
- Commit the wrapper files to Git.
- New teammates run `./mvnw verify` without installing Maven.

**Show**
```
./mvnw verify          (Linux/macOS)
mvnw.cmd verify        (Windows)
```

**Check:** Why use `mvnw` instead of `mvn`? *(Everyone uses the same Maven version.)*

---

## JNR-002-L08 · Demo: untangling a dependency conflict with `dependency:tree` (10 min)
**Goal:** find and fix a version conflict. Prepares JNR-002-LAB1.

**Steps**
1. Show an app that fails at run time with `NoSuchMethodError`.
2. Run `./mvnw dependency:tree -Dverbose` and search for the library name.
3. Find that two dependencies request different versions.
4. **Planned mistake:** add an exclusion on the wrong dependency, and the error remains. Fix: read the tree again and exclude from the right one, or better, pin the version in `dependencyManagement`.
5. Run `./mvnw verify` and confirm green.
6. Write one sentence in the README on the cause.

**Check:** Better than an exclusion for a shared library? *(Pin the version once in `dependencyManagement`.)*
