# BEG-054 · Build tools — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a recipe card plus a kitchen assistant who fetches ingredients and follows the steps in order.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-054-L01 · Why build tools (7 min)
**Goal:** see why `javac` by hand does not scale.

**Key points**
- Real projects have many files, libraries, and steps: compile, test, package.
- Typing `javac` with long class paths is slow and easy to get wrong.
- A build tool does it the same way for everyone, on every machine.
- It also downloads libraries (dependencies) for you.
- Maven is the build tool we use; Gradle is another.

**Show:** a long manual `javac -cp ...` command next to `mvn package`.

**Check:** Name two jobs of a build tool. *(Compile/test/package and fetch dependencies.)*

---

## BEG-054-L02 · Project structure and `pom.xml` (12 min)
**Goal:** read a Maven project.

**Key points**
- Standard layout: `src/main/java` for code, `src/test/java` for tests, `pom.xml` at the root.
- Wrong folder layout is the most common beginner error.
- Coordinates identify the project: `groupId`, `artifactId`, `version`.
- Properties set the Java version; plugins add build steps.
- Build output goes to `target/`.

**Show**
```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>library</artifactId>
  <version>1.0-SNAPSHOT</version>
  <properties>
    <maven.compiler.release>21</maven.compiler.release>
  </properties>
</project>
```

**Check:** Where does test code live? *(`src/test/java`.)*

---

## BEG-054-L03 · Dependencies and Maven Central (10 min)
**Goal:** add a library.

**Key points**
- A dependency is a library your code uses.
- You declare its coordinates; Maven downloads it from Maven Central and caches it locally.
- Scope `test` means it is used only for tests, such as JUnit.
- Find coordinates on the library's page at Maven Central; verify the current version before recording.
- Transitive dependencies come along automatically.

**Show**
```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>VERIFY-VERSION</version>
  <scope>test</scope>
</dependency>
```

**Check:** What does `<scope>test</scope>` mean? *(Used only when running tests.)*

---

## BEG-054-L04 · The build lifecycle (10 min)
**Goal:** know what each phase does.

**Key points**
- Phases run in order: `validate`, `compile`, `test`, `package`, `verify`, `install`, `deploy`.
- Running a phase runs all earlier ones too.
- `mvn compile` builds classes; `mvn test` also runs tests; `mvn package` also builds the JAR.
- `mvn clean` deletes `target/` for a fresh start.

**Show**
```bash
mvn clean package
```

**Check:** Does `mvn package` run tests? *(Yes, `test` comes before `package`.)*

---

## BEG-054-L05 · Running tests with Maven (6 min)
**Goal:** run tests from the terminal.

**Key points**
- Tests are in `src/test/java` and usually end in `Test`.
- `mvn test` runs them and prints a summary.
- A failing test fails the build.
- Same command works for everyone, so teammates and servers agree.

**Show**
```bash
mvn test
```
Expected tail: `Tests run: 5, Failures: 0` and `BUILD SUCCESS`.

**Check:** What does a failing test do to the build? *(It fails the build.)*

---

## BEG-054-L06 · Demo: converting a project to Maven (8 min)
**Goal:** convert the data-structures project. Prepares BEG-054-LAB1.

**Steps**
1. Create `pom.xml` with coordinates and the Java version.
2. Move sources to `src/main/java` and tests to `src/test/java`.
3. **Planned mistake:** leave test classes in `src/main/java`; the JUnit import fails. Fix: move them to `src/test/java`.
4. Add JUnit as a `test` dependency.
5. Run `mvn test`, add `target/` to `.gitignore`, and commit.
