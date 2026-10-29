# JNR-012 · Configuration management — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** the settings panel of a car: one set of controls, different presets for city, highway, and winter.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-012-L01 · `application.yml` and profiles (10 min)
**Goal:** configure the app with YAML and switch profiles.

**Key points**
- `application.yml` holds settings in a readable tree; `.properties` says the same in flat form.
- A profile is a named set of settings, such as `dev` or `prod`.
- Profile files: `application-dev.yml`, `application-prod.yml`; they add to or override the base file.
- Activate with `spring.profiles.active=dev` or the environment variable `SPRING_PROFILES_ACTIVE`.

**Show**
```yaml
# application.yml
shop:
  currency: EUR
---
# application-dev.yml
shop:
  currency: USD
```

**Check:** How do you choose the `prod` profile without editing files? *(Set `SPRING_PROFILES_ACTIVE=prod`.)*

---

## JNR-012-L02 · Typed configuration with `@ConfigurationProperties` (12 min)
**Goal:** bind settings to a record.

**Key points**
- Group related settings under a prefix and bind them to one class.
- A record gives an immutable, constructor-bound holder.
- Register with `@ConfigurationPropertiesScan` or `@EnableConfigurationProperties`.
- Kebab-case in YAML (`page-size-max`) maps to camelCase in Java.
- Prefer this over `@Value` scattered around the code.

**Show**
```java
@ConfigurationProperties(prefix = "shop")
public record ShopProperties(String currency, BigDecimal taxRate, int pageSizeMax) {}
```

**Check:** Why a record rather than a class with setters? *(Immutable: values cannot change after startup.)*

---

## JNR-012-L03 · Validating configuration (8 min)
**Goal:** fail fast on bad settings.

**Key points**
- Add `@Validated` to the properties type and bean validation constraints to its components.
- If a value is missing or invalid, startup fails with a message naming the property.
- Failing at startup beats a failure at 3 a.m. on the first request.
- Use sensible constraints: `@NotBlank`, `@Min`, `@DecimalMin`.

**Show**
```java
@Validated @ConfigurationProperties("shop")
public record ShopProperties(
    @NotBlank String currency,
    @DecimalMin("0.00") @DecimalMax("1.00") BigDecimal taxRate,
    @Min(1) @Max(100) int pageSizeMax) {}
```

**Check:** When is a bad value detected? *(At startup, before the app serves traffic.)*

---

## JNR-012-L04 · Property-source precedence (10 min)
**Goal:** know which value wins.

**Key points**
- Many sources can set one property; Boot defines an order, highest priority first (summary).
- Command-line arguments beat environment variables, which beat profile files, which beat the base `application.yml`.
- Defaults in code are lowest.
- Environment variable `SHOP_TAXRATE` or `SHOP_TAX_RATE` maps to `shop.tax-rate` by relaxed binding.
- Secrets belong in the environment or a secret store, never in committed YAML. Verify the full order in the docs for your version.

**Show:** a ladder: command line → env vars → `application-{profile}.yml` → `application.yml` → defaults.

**Check:** Which wins: env var or `application.yml`? *(The environment variable.)*

---

## JNR-012-L05 · Demo: typed, validated `ShopProperties` that fail fast (10 min)
**Goal:** build `ShopProperties`, see it fail on bad input; prepares JNR-012-LAB1.

**Steps**
1. Create the `ShopProperties` record and enable scanning.
2. Add `shop.currency`, `shop.tax-rate`, `shop.page-size-max` to `application.yml`; inject the record into a service.
3. Add `dev` and `prod` profile files with different values.
4. **Planned mistake:** set `tax-rate: 1.5`; the app refuses to start. Read the message ("Binding to target ... failed") and the property name; fix the value.
5. Override the value with an environment variable and show it winning.
