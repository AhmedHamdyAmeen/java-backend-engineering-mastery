# JNR-007 · Configuration — Quiz

Outcomes: O1 externalize config · O2 twelve-factor · O3 precedence and profiles · O4 secrets.

**Q01 (O1)** Configuration is best kept: A. In code B. In comments C. Outside the code D. In tests only
**Q02 (O2)** The twelve-factor rule for config says: A. Hard-code it B. Separate it from code C. Use only YAML D. Never change it
**Q03 (O1)** Which reads an environment variable? A. `System.getenv("NAME")` B. `System.getProperty("NAME")` C. `Files.readAll` D. `Config.load`
**Q04 (O1)** How do you set a system property? A. `--env=x` B. `export x` C. `-Dname=value` D. `@name`
**Q05 (O1)** In YAML, nesting is shown by: A. Braces B. Indentation with spaces C. Tabs D. Semicolons
**Q06 (O3)** File says 0.19, environment variable says 0.07. The usual winner is: A. The file B. The first alphabetically C. Neither D. The environment variable
**Q07 (O3)** A profile is: A. A user account B. A Java class C. A named set of settings D. A test report
**Q08 (O4)** Where should a real API key live? A. In Git B. In an environment variable or secrets manager C. In the README D. In a comment
**Q09 (O4)** What do you commit for local setup? A. `.env.example` with fake values B. `.env` with real values C. Nothing D. A screenshot
**Q10 (O4)** A key was committed by mistake. First, you: A. Delete the file only B. Ignore it C. Revoke and replace the key D. Rename the branch

## Answers
Q01 C · Q02 B · Q03 A · Q04 C · Q05 B · Q06 D · Q07 C · Q08 B · Q09 A · Q10 C

## Practical part
Six exercises `JNR-007-EX01` to `EX06` plus the lab check (same JAR, different behavior). Pass: at least 8 of 10 quiz answers including the precedence question, five exercises correct, and no secrets in the repository.
