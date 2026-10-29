# JNR-007 · Configuration — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a radio with dials: the same radio plays different stations because the settings are outside the machine.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-007-L01 · Why externalize configuration (7 min)
**Goal:** keep settings out of the code.

**Key points**
- Configuration is anything that changes between places: database address, tax rate, API key.
- If it is in the code, you must rebuild to change it.
- The twelve-factor rule: separate config from code.
- Build the JAR once, run it anywhere with different settings.
- Do not write `if (env.equals("prod"))` in code.

**Show:** a hard-coded `String url = "jdbc:...prod..."` replaced by `config.get("db.url")`.

**Check:** What does twelve-factor say about config? *(Keep it separate from code.)*

---

## JNR-007-L02 · Properties and YAML (10 min)
**Goal:** read settings from a file.

**Key points**
- A `.properties` file has `key=value` lines.
- YAML uses indentation for nesting and is easy to read; spaces matter, tabs are not allowed.
- Put the default file on the classpath (`src/main/resources`).
- Read values with `Properties.load` (plain Java) or a framework later.
- Give a clear error if a required value is missing.

**Show**
```properties
shop.currency=EUR
shop.tax-rate=0.19
```
```yaml
shop:
  currency: EUR
  tax-rate: 0.19
```

**Check:** What must you avoid in YAML indentation? *(Tabs; use spaces.)*

---

## JNR-007-L03 · Environment variables and system properties (8 min)
**Goal:** override settings from outside.

**Key points**
- Environment variables are set by the operating system or container: `System.getenv("SHOP_TAX_RATE")`.
- System properties are set when starting Java: `-Dshop.tax-rate=0.07`; read with `System.getProperty`.
- Names are usually UPPER_SNAKE_CASE for environment variables.
- Common pattern: file gives defaults, environment overrides.
- Convert types yourself and fail clearly on bad values.

**Show**
```java
String rate = System.getenv().getOrDefault("SHOP_TAX_RATE", props.getProperty("shop.tax-rate"));
```

**Check:** How do you pass a system property? *(With `-Dname=value` on the `java` command.)*

---

## JNR-007-L04 · Profiles and precedence (8 min)
**Goal:** explain which value wins and how environments differ.

**Key points**
- A profile is a named set of settings, such as `dev`, `test`, `prod`.
- Precedence: the more specific or later source wins.
- Typical order, weakest to strongest: defaults in the file, profile file, environment variable, command-line option.
- Frameworks (like Spring Boot, later) define this order; read their documentation (verify before recording).
- Document the order in the README.

**Show:** a table: source / strength. For example `application.yml` < `application-prod.yml` < env var < command line.

**Check:** If the file says 0.19 and the env var says 0.07, which wins? *(The environment variable.)*

---

## JNR-007-L05 · Secrets do not belong in Git (7 min)
**Goal:** keep secrets out of the repository.

**Key points**
- Secrets: passwords, API keys, tokens.
- Git remembers everything; deleting a file later does not remove it from history.
- Put secrets in environment variables or a secrets manager.
- Commit `.env.example` with fake values; put `.env` in `.gitignore`.
- If a secret leaks, rotate it (replace it) at once.

**Show**
```
# .env.example (committed)
SHOP_API_KEY=changeme
# .gitignore
.env
```

**Check:** You committed a key by mistake. First step? *(Revoke and replace the key; then clean up history.)*

---

## JNR-007-L06 · Demo: one JAR, three environments (10 min)
**Goal:** run the same JAR with dev, test, and prod settings. Prepares JNR-007-LAB1.

**Steps**
1. Build `shop-cli.jar` once.
2. Run with the default file: currency `EUR`, tax 19%.
3. Run with `SHOP_TAX_RATE=0.07`; the output changes.
4. **Planned mistake:** commit a `.env` with a real key; spot it in `git status`. Fix: remove it from the index, add it to `.gitignore`, rotate the key, and commit `.env.example`.
5. Run a third time with `-Dshop.currency=USD`.
6. Show the precedence order in the README.

**Check:** Did we rebuild between runs? *(No; same JAR, different configuration.)*
