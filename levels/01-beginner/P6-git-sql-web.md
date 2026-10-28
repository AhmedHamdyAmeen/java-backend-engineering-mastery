# BEG-P6 — Git, SQL, and Web Foundations

**Phase goal:** the learner versions their work with Git and GitHub, models and queries a relational database, connects Java to PostgreSQL, understands HTTP and APIs from the outside, and builds with Maven — everything needed for the Beginner capstone.

**Phase practice:** move every previous project into Git; design the Library database; call public APIs with Postman.

**Phase total:** ~9.7 h video · ~27.5 h practice

---

### BEG-046 · Version control
`n: 46` · **Video:** 71 min · **Practice:** 3 h

**Prerequisites:** BEG-006

**Learning outcomes** — the learner can:
1. Initialize a repository, stage changes, and write clear commit messages.
2. Inspect history and differences with `log`, `status`, and `diff`.
3. Create, switch, and merge branches, and resolve a merge conflict by hand.
4. Write a `.gitignore` that excludes build output and secrets.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-046-L01 | Why version control | 7 |
| BEG-046-L02 | Repositories, staging, and commits | 12 |
| BEG-046-L03 | History and diffs | 8 |
| BEG-046-L04 | Branches | 10 |
| BEG-046-L05 | Merging and conflicts | 12 |
| BEG-046-L06 | `.gitignore` | 6 |
| BEG-046-L07 | Demo: putting Bank Accounts under Git | 8 |
| BEG-046-L08 | Demo: creating and resolving a merge conflict | 8 |

**Lab** — `BEG-046-LAB1` *Version your work:* put the Bank Accounts project under Git with meaningful commits; create a feature branch, make conflicting changes on both branches, merge, and resolve. Acceptance: clean history; conflict resolved correctly.

**Common mistakes:** "fix" commit messages; committing `target/` or `.idea/`; committing passwords.

**Assessment:** terminal-only Git task.

**Career relevance:** daily tool; team workflows in JNR-053.

---

### BEG-047 · GitHub
`n: 47` · **Video:** 48 min · **Practice:** 2 h

**Prerequisites:** BEG-046

**Learning outcomes** — the learner can:
1. Connect a local repository to a GitHub remote and push and pull.
2. Open a pull request, respond to review comments, and merge.
3. Write a README in Markdown with description, setup, and usage.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-047-L01 | Remotes, push, and pull | 10 |
| BEG-047-L02 | Authentication with GitHub (SSH keys or tokens) | 8 |
| BEG-047-L03 | Pull requests and reviews | 12 |
| BEG-047-L04 | Markdown and a good README | 10 |
| BEG-047-L05 | Demo: publishing a project and reviewing a pull request | 8 |

**Lab** — `BEG-047-LAB1` *Public portfolio start:* publish two projects with READMEs; open a PR for a small change and have a peer review it. Acceptance: repos public; PR has at least one review round.

**Common mistakes:** pushing directly to `main`; READMEs without setup steps.

**Assessment:** portfolio check.

**Career relevance:** portfolio and every team workflow afterward.

---

### BEG-048 · Data fundamentals
`n: 48` · **Video:** 38 min · **Practice:** 1 h

**Prerequisites:** BEG-002

**Learning outcomes** — the learner can:
1. Explain why applications store data in a database rather than in files.
2. Distinguish relational and nonrelational databases at a high level.
3. Explain what a DBMS and a schema are.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-048-L01 | Why databases | 8 |
| BEG-048-L02 | Structured vs unstructured data | 7 |
| BEG-048-L03 | Relational vs nonrelational | 8 |
| BEG-048-L04 | DBMS and schemas | 7 |
| BEG-048-L05 | Demo: why the contacts CSV breaks at scale | 8 |

**Lab** — `BEG-048-LAB1` *Files vs database:* list the problems the Contacts CSV file would have with 1 million contacts and 100 simultaneous users. Acceptance: at least five distinct problems.

**Common mistakes:** "NoSQL is faster" as a blanket belief.

**Assessment:** quiz.

**Career relevance:** data selection (MID-044) revisits this with depth.

---

### BEG-049 · Relational modeling
`n: 49` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** BEG-048

**Learning outcomes** — the learner can:
1. Model entities as tables with appropriate columns and types.
2. Choose primary keys and define foreign keys.
3. Model one-to-many and many-to-many relationships (junction tables).
4. Normalize a flat table to third normal form and explain the anomalies removed.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-049-L01 | Tables, rows, and columns | 8 |
| BEG-049-L02 | Primary keys | 8 |
| BEG-049-L03 | Foreign keys and relationships | 12 |
| BEG-049-L04 | Many-to-many | 8 |
| BEG-049-L05 | Normalization in practice | 14 |
| BEG-049-L06 | Demo: normalizing a library spreadsheet into tables | 8 |

**Lab** — `BEG-049-LAB1` *Library schema:* design the ER diagram for books, authors, members, and loans. Acceptance: 3NF; relationships correct; peer-reviewed.

**Common mistakes:** comma-separated values in a column; duplicated data across tables.

**Assessment:** normalize a provided spreadsheet.

**Career relevance:** the Library capstone; data modeling at scale (MID-019).

---

### BEG-050 · SQL foundations
`n: 50` · **Video:** 91 min · **Practice:** 6 h

**Prerequisites:** BEG-049

**Learning outcomes** — the learner can:
1. Create and alter tables with DDL.
2. Insert, update, and delete rows with DML, always with a correct `WHERE`.
3. Query with `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, and aggregates.
4. Combine tables with inner and left joins and explain the difference.
5. Use a subquery where it is clearer than a join.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-050-L01 | SQL overview: DDL vs DML | 7 |
| BEG-050-L02 | `CREATE` and `ALTER` | 10 |
| BEG-050-L03 | `INSERT`, `UPDATE`, `DELETE` | 10 |
| BEG-050-L04 | `SELECT`, `WHERE`, `ORDER BY` | 10 |
| BEG-050-L05 | Aggregates, `GROUP BY`, `HAVING` | 12 |
| BEG-050-L06 | Joins | 15 |
| BEG-050-L07 | Subqueries | 11 |
| BEG-050-L08 | Demo: answering library questions with SQL | 8 |
| BEG-050-L09 | Demo: joins that silently drop rows | 8 |

**Lab** — `BEG-050-LAB1` *Library queries:* 25 graded queries against a seeded library database (overdue loans, most-borrowed authors, members with no loans…). Acceptance: 20 of 25 correct.

**Common mistakes:** `UPDATE` without `WHERE`; `WHERE` on aggregates instead of `HAVING`; inner join silently dropping rows.

**Assessment:** timed SQL test (also part of the BEG graduation gate).

**Career relevance:** SQL mastery (MID-011) and every data-access module.

---

### BEG-051 · PostgreSQL basics
`n: 51` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-005, BEG-050

**Learning outcomes** — the learner can:
1. Install PostgreSQL and connect with `psql` and a GUI client (pgAdmin or DBeaver).
2. Create a database, schema, and user.
3. Apply `NOT NULL`, `UNIQUE`, `CHECK`, and foreign-key constraints and observe rejected data.
4. Wrap several statements in a transaction and roll it back.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-051-L01 | Installing PostgreSQL | 10 |
| BEG-051-L02 | `psql` and a GUI client | 10 |
| BEG-051-L03 | Databases, schemas, and users | 8 |
| BEG-051-L04 | Constraints that protect data | 10 |
| BEG-051-L05 | First look at transactions | 7 |
| BEG-051-L06 | Demo: creating the Library database with constraints | 8 |

**Lab** — `BEG-051-LAB1` *Library database live:* create the Library schema from BEG-049 as a SQL script with constraints and seed data; try to insert invalid rows and record the errors; demonstrate a rollback. Acceptance: script re-runnable from scratch.

**Common mistakes:** working as the `postgres` superuser; constraints only in application code.

**Assessment:** practical check of the script.

**Career relevance:** primary database for the whole curriculum.

---

### BEG-052 · Web fundamentals
`n: 52` · **Video:** 58 min · **Practice:** 2 h

**Prerequisites:** BEG-003

**Learning outcomes** — the learner can:
1. Describe the structure of an HTTP request and response (method, URL, headers, body, status).
2. Choose the right HTTP method and interpret status code classes (2xx, 3xx, 4xx, 5xx).
3. Read and write JSON, and map it mentally to Java objects.
4. Identify path, query parameters, and fragments in a URL.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-052-L01 | Anatomy of an HTTP request | 10 |
| BEG-052-L02 | Methods: GET, POST, PUT, PATCH, DELETE | 10 |
| BEG-052-L03 | Status codes | 8 |
| BEG-052-L04 | Headers | 7 |
| BEG-052-L05 | JSON | 8 |
| BEG-052-L06 | URLs and query parameters | 7 |
| BEG-052-L07 | Demo: reading real HTTP traffic in the browser | 8 |

**Lab** — `BEG-052-LAB1` *Read real traffic:* capture five requests from a real site in the browser's Network tab and annotate method, URL parts, key headers, status, and body type. Acceptance: all parts correctly labeled.

**Common mistakes:** GET with side effects; treating every error as 500.

**Assessment:** quiz.

**Career relevance:** HTTP in depth (JNR-017).

---

### BEG-053 · API fundamentals
`n: 53` · **Video:** 48 min · **Practice:** 2 h

**Prerequisites:** BEG-052

**Learning outcomes** — the learner can:
1. Explain what an API is and the REST idea of resources.
2. Read API documentation and make requests to a public API with Postman and `curl`.
3. Sketch endpoint designs (URL + method + status) for a simple resource.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-053-L01 | What an API is | 8 |
| BEG-053-L02 | REST in plain language | 10 |
| BEG-053-L03 | Postman tour | 10 |
| BEG-053-L04 | `curl` from the terminal | 6 |
| BEG-053-L05 | Sketching endpoints for a resource | 6 |
| BEG-053-L06 | Demo: exploring a public API with Postman and curl | 8 |

**Lab** — `BEG-053-LAB1` *API explorer:* call a public API for list, single item, and filtered queries; save a Postman collection; then sketch the endpoints a Library API would need. Acceptance: collection exported; endpoint sketch reviewed.

**Common mistakes:** verbs in URLs (`/getBooks`).

**Assessment:** endpoint design exercise.

**Career relevance:** the Junior capstone builds exactly such an API (JNR-018).

---

### BEG-054 · Build tools
`n: 54` · **Video:** 53 min · **Practice:** 2.5 h

**Prerequisites:** BEG-006, BEG-045

**Learning outcomes** — the learner can:
1. Explain what a build tool does and why manual `javac` does not scale.
2. Read a `pom.xml`: coordinates, dependencies, and plugins.
3. Run `mvn compile`, `test`, and `package` and explain the lifecycle phases.
4. Add a dependency from Maven Central and convert an existing project to Maven.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-054-L01 | Why build tools | 7 |
| BEG-054-L02 | Project structure and `pom.xml` | 12 |
| BEG-054-L03 | Dependencies and Maven Central | 10 |
| BEG-054-L04 | The build lifecycle | 10 |
| BEG-054-L05 | Running tests with Maven | 6 |
| BEG-054-L06 | Demo: converting a project to Maven | 8 |

**Lab** — `BEG-054-LAB1` *Mavenize:* convert the data-structures project to Maven with JUnit as a test dependency; `mvn test` passes from the terminal. Acceptance: builds on a clean machine.

**Common mistakes:** wrong folder layout; committing `target/`.

**Assessment:** practical check.

**Career relevance:** Maven in depth (JNR-002).

---

### BEG-055 · JDBC essentials
`n: new (added in v1.0)` · **Video:** 66 min · **Practice:** 3 h

**Prerequisites:** BEG-029, BEG-051, BEG-054

> **Why this module exists:** the Beginner capstone requires PostgreSQL via JDBC, but the roadmap first taught JDBC in JNR-025 (Junior). This module teaches the minimum needed for the capstone; JNR-025 builds on it with connection management, batching, and the move to Spring.

**Learning outcomes** — the learner can:
1. Add the PostgreSQL JDBC driver with Maven and open a connection from configuration (not hard-coded credentials).
2. Execute queries and updates with `PreparedStatement` and map `ResultSet` rows to objects.
3. Close connections, statements, and result sets with try-with-resources.
4. Demonstrate a SQL injection with string concatenation and prevent it with parameters.
5. Group related statements in a transaction with `setAutoCommit(false)`, `commit`, and `rollback`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-055-L01 | How Java talks to a database | 8 |
| BEG-055-L02 | Connecting: driver, URL, credentials from environment variables | 10 |
| BEG-055-L03 | Querying and mapping rows to objects | 12 |
| BEG-055-L04 | SQL injection, live | 10 |
| BEG-055-L05 | Transactions from Java | 10 |
| BEG-055-L06 | Demo: building the BookRepository with JDBC | 8 |
| BEG-055-L07 | Demo: SQL injection, then the PreparedStatement fix | 8 |

**Lab** — `BEG-055-LAB1` *Library DAO:* a `BookRepository` interface with a JDBC implementation (save, findById returning `Optional`, findByTitle, delete) and integration tests against a local test database. Acceptance: no string-concatenated SQL; resources closed; tests pass.

**Common mistakes:** concatenating user input into SQL; leaking connections; credentials committed to Git.

**Assessment:** implement a new repository method with a test; explain why parameters prevent injection.

**Career relevance:** JNR-025 to JNR-029 build on this toward Spring Data JPA.

---

## Beginner capstone — Library Management System (`BEG-CAP`)

Full brief, acceptance criteria, and rubric: [`projects/ladder.md`](../../projects/ladder.md#01--library-management-system-beg-cap).
