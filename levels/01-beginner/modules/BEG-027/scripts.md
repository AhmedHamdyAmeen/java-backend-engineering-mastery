# BEG-027 · Packages and organization — Lecture scripts

**Video:** 38 min · **Analogy used throughout:** a filing cabinet with labeled drawers.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-027-L01 · Packages and folders (8 min)
**Goal:** put classes into packages that match folders.

**Key points**
- A package groups related classes and gives them a full name: `com.example.bank.Account`.
- The first line of the file declares it: `package com.example.bank;`.
- The folder path must match: `com/example/bank/Account.java`.
- Names are lowercase; companies use a reversed domain (`com.example`) to avoid clashes.
- Never leave everything in the default (unnamed) package.

**Show**
```java
package com.example.bank;

public class Account { }
```
Folder tree: `src/com/example/bank/Account.java`.

**Check:** What must match the `package` line? *(The folder structure.)*

---

## BEG-027-L02 · Imports and name clashes (7 min)
**Goal:** use classes from other packages.

**Key points**
- `import com.example.bank.Account;` lets you write `Account` instead of the full name.
- `java.lang` (such as `String`) is imported automatically.
- Avoid `import something.*;` in real code; explicit imports are clearer.
- If two classes share a name (`java.util.Date` and `java.sql.Date`), import one and write the other's full name.
- Packages in the same package need no import.

**Show**
```java
import java.util.List;
java.sql.Date d = new java.sql.Date(0);  // full name to avoid the clash
```

**Check:** Which package is imported automatically? *(`java.lang`.)*

---

## BEG-027-L03 · Package-private: the forgotten modifier (7 min)
**Goal:** hide implementation classes.

**Key points**
- A class with no modifier is visible only inside its own package.
- Use it for helpers that outsiders should not touch.
- Make public only what other packages truly need: the "public surface".
- A small public surface is easier to maintain and change.
- The same rule applies to methods and constructors.

**Show**
```java
class InterestCalculator { }          // package-private helper
public class Account { }               // the public class
```

**Check:** Who can use a package-private class? *(Only classes in the same package.)*

---

## BEG-027-L04 · Package by feature vs by layer (8 min)
**Goal:** choose a grouping and justify it.

**Key points**
- By layer: `controller/`, `service/`, `repository/`. Related code is spread across folders.
- By feature: `account/`, `customer/`, `notification/`. Everything for one feature is together.
- Feature packages allow package-private hiding and make features easy to find and remove.
- Layer packages force many classes to be `public` so layers can reach each other.
- Both are used in industry; for small and medium apps, feature packages are a strong default.

**Show:** two trees side by side: layer (`service/AccountService`, `repository/AccountRepository`) and feature (`account/AccountService`, `account/AccountRepository`).

**Check:** Which grouping keeps a feature's classes together? *(By feature.)*

---

## BEG-027-L05 · Demo: reorganizing Bank Accounts into feature packages (8 min)
**Goal:** split the project into packages with a minimal public surface. Prepares `BEG-027-LAB1`.

**Steps**
1. Start with all classes in the default package.
2. Create `bank.account`, `bank.customer`, and `bank.notification`; move the classes and fix the `package` lines.
3. Add imports where one package uses another.
4. Make helper classes package-private; keep only intended classes `public`.
5. **Planned mistake:** try to use a package-private class from `Main` in another package and read the compile error. Fix by using the public class instead of exposing the helper.
6. Run the program to confirm it still works.
