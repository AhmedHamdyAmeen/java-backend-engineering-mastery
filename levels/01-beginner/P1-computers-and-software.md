# BEG-P1 — Introduction to Computers and Software Engineering

**Phase goal:** a learner who has never programmed can explain what a computer and the internet do, describe the jobs in a software team, and run a Java program from both the terminal and an IDE.

**Phase practice:** set up a complete Java development environment, compile and run a program from the terminal, then run it in IntelliJ IDEA.

**Phase total:** ~6.5 h video · ~12 h practice

---

### BEG-001 · Understanding computers
`n: 1` · **Video:** 58 min · **Practice:** 2 h

**Prerequisites:** none

**Learning outcomes** — the learner can:
1. Name the main hardware components (CPU, RAM, storage, I/O devices) and state each one's job.
2. Explain why data in RAM is lost on power-off and data on an SSD is not.
3. Convert small numbers between decimal and binary, and explain bits and bytes.
4. Distinguish an operating system, an application, and a process, and list running processes on their own machine.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-001-L01 | What a computer actually does: input, processing, storage, output | 10 |
| BEG-001-L02 | CPU, RAM, and storage: the kitchen analogy | 10 |
| BEG-001-L03 | Bits, bytes, and binary numbers | 12 |
| BEG-001-L04 | The operating system's job | 8 |
| BEG-001-L05 | Applications and processes: Task Manager / Activity Monitor tour | 10 |
| BEG-001-L06 | Demo: watching RAM and CPU while opening apps | 8 |

**Lab** — `BEG-001-LAB1` *Know your machine:* record your CPU, RAM, and disk capacity; find the five processes using the most memory; open a large app and observe how RAM use changes. Acceptance: a short table with values and one sentence explaining each observation.

**Common mistakes:** confusing storage capacity with memory; thinking "the computer" means the monitor or case; treating a process and a program as the same thing.

**Assessment:** quiz (10 questions) plus converting five numbers to and from binary.

**Career relevance:** vocabulary for every later topic: memory (BEG-038, MID-002), processes (JNR-048), performance (MID-008).

---

### BEG-002 · Understanding software
`n: 2` · **Video:** 48 min · **Practice:** 1 h

**Prerequisites:** BEG-001

**Learning outcomes** — the learner can:
1. Classify a given piece of software as desktop, mobile, web frontend, backend, or embedded.
2. Explain the difference between a program that runs and exits and a service that runs continuously.
3. Describe the stages of the software lifecycle (requirements, design, build, test, release, operate, retire).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-002-L01 | What software is: instructions, data, and behavior | 8 |
| BEG-002-L02 | Kinds of software, with everyday examples | 10 |
| BEG-002-L03 | Programs vs services: why a backend never "finishes" | 10 |
| BEG-002-L04 | The software lifecycle | 12 |
| BEG-002-L05 | Demo: one app, many pieces: mobile app, website, and backend | 8 |

**Lab** — `BEG-002-LAB1` *Software around you:* list ten pieces of software you used today, classify each, and mark which ones depend on a backend service. Acceptance: correct classification of at least eight.

**Common mistakes:** believing a website and its backend are the same thing; thinking software is "done" once released.

**Assessment:** classification exercise and a one-paragraph description of what happens behind one app you use.

**Career relevance:** frames why backend engineering exists; the lifecycle returns in JNR-053 and SRC-011.

---

### BEG-003 · The internet
`n: 3` · **Video:** 63 min · **Practice:** 1.5 h

**Prerequisites:** BEG-001

**Learning outcomes** — the learner can:
1. Distinguish the internet (the network) from the web (one service that runs on it).
2. Trace what happens from typing a URL to seeing a page: DNS lookup, connection, request, response, rendering.
3. Look up a domain's IP address with `nslookup` and explain the result.
4. Explain what HTTPS adds over HTTP and why it matters.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-003-L01 | Internet vs web | 8 |
| BEG-003-L02 | IP addresses and ports | 10 |
| BEG-003-L03 | Domains and DNS | 10 |
| BEG-003-L04 | Clients, servers, requests, and responses | 12 |
| BEG-003-L05 | HTTP vs HTTPS: what encryption protects | 8 |
| BEG-003-L06 | Watching a request in the browser's developer tools | 7 |
| BEG-003-L07 | Demo: following a URL with `nslookup` and the Network tab | 8 |

**Lab** — `BEG-003-LAB1` *Follow a request:* use `nslookup` on three domains, then open the browser's Network tab, load a site, and identify the request method, status code, and response type of the main document. Acceptance: screenshots plus labeled answers.

**Common mistakes:** thinking a domain *is* a server; believing HTTPS hides which site you visit; confusing IP address and port.

**Assessment:** draw and narrate the URL-to-page sequence diagram.

**Career relevance:** foundation for BEG-052, JNR-017, and every networking topic through ARC-013.

---

### BEG-004 · Introduction to engineering
`n: 4` · **Video:** 48 min · **Practice:** 1 h

**Prerequisites:** BEG-002

**Learning outcomes** — the learner can:
1. Explain how a software engineer's responsibilities extend beyond writing code (design, testing, operation, collaboration).
2. Describe the roles of frontend, backend, full-stack, QA, DevOps, SRE, and architect, and how they hand off work.
3. Describe the path this curriculum follows from Beginner to Solution Architect and what each level adds.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-004-L01 | Developer vs software engineer | 8 |
| BEG-004-L02 | Roles in an engineering team | 12 |
| BEG-004-L03 | How a feature travels from idea to production | 10 |
| BEG-004-L04 | Your career map: the eight levels of this course | 10 |
| BEG-004-L05 | Demo: a day in a backend engineer's workflow, walked through | 8 |

**Lab** — `BEG-004-LAB1` *Read job posts:* collect three real junior backend job posts, list required skills, and map each to a module in this curriculum. Acceptance: mapping table with at least 15 skills.

**Common mistakes:** assuming seniority means only deeper technical knowledge; ignoring operation and collaboration.

**Assessment:** short written reflection: which role interests you and what it requires.

**Career relevance:** sets expectations; revisited in MID-065 and STF-001.

---

### BEG-005 · Development environment
`n: 5` · **Video:** 58 min · **Practice:** 2 h

**Prerequisites:** BEG-001

**Learning outcomes** — the learner can:
1. Install the baseline JDK and confirm the installation with `java -version` and `javac -version`.
2. Install IntelliJ IDEA and create, run, and close a project.
3. Explain environment variables and `PATH`, and fix a "command not found" error caused by a missing `PATH` entry.
4. Show hidden file extensions and explain why `.java` vs `.java.txt` matters.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-005-L01 | Files, folders, and extensions on Windows, macOS, and Linux | 8 |
| BEG-005-L02 | Installing the JDK (all three operating systems) | 12 |
| BEG-005-L03 | Environment variables and PATH | 10 |
| BEG-005-L04 | Installing and tour of IntelliJ IDEA | 12 |
| BEG-005-L05 | VS Code as an alternative | 8 |
| BEG-005-L06 | Demo: installing the JDK and fixing a broken PATH | 8 |

**Lab** — `BEG-005-LAB1` *Working toolbox:* install JDK and IDE, print the versions in a terminal, deliberately break `PATH` in a new terminal session, observe the error, and restore it. Acceptance: screenshots of both states and the fix.

**Common mistakes:** installing a JRE instead of a JDK; multiple JDKs with the wrong one first on `PATH`; editing `PATH` and not opening a new terminal.

**Assessment:** practical check: versions printed and a new project runs in the IDE.

**Career relevance:** every lab depends on it; environment differences return in JNR-054.

---

### BEG-006 · Command line
`n: 6` · **Video:** 68 min · **Practice:** 3 h

**Prerequisites:** BEG-005

**Learning outcomes** — the learner can:
1. Navigate directories with absolute and relative paths (`pwd`, `cd`, `ls`/`dir`).
2. Create, copy, move, and delete files and folders from the terminal.
3. Use pipes and redirection to filter output and save it to a file.
4. Read and set an environment variable for the current session in Bash and PowerShell.
5. Explain file permissions at a basic level and why a script may fail to execute.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-006-L01 | Terminal, shell, and prompt | 8 |
| BEG-006-L02 | Paths: absolute, relative, home, `.` and `..` | 10 |
| BEG-006-L03 | Working with files and folders | 12 |
| BEG-006-L04 | Pipes and redirection | 10 |
| BEG-006-L05 | Environment variables in the shell | 8 |
| BEG-006-L06 | Permissions basics | 7 |
| BEG-006-L07 | Bash vs PowerShell cheat sheet | 5 |
| BEG-006-L08 | Demo: setting up a project folder using only the terminal | 8 |

**Lab** — `BEG-006-LAB1` *Terminal-only project setup:* using only the terminal, create a folder structure for a project, create files, list them sorted by size, save the listing to a file, and search it for a word. Acceptance: command history file plus final folder tree.

**Common mistakes:** spaces in paths without quotes; running `rm`/`del` without checking the current directory; mixing Bash and PowerShell syntax.

**Assessment:** timed terminal task (10 commands) with no GUI use.

**Career relevance:** daily tool from here on; deepened in JNR-048.

---

### BEG-007 · How code runs
`n: 7` · **Video:** 48 min · **Practice:** 1.5 h

**Prerequisites:** BEG-002, BEG-006

**Learning outcomes** — the learner can:
1. Explain the difference between source code, bytecode, and machine code.
2. Distinguish JDK, JRE, and JVM and say which one a developer needs.
3. Compile a `.java` file with `javac` and run the resulting class with `java` from the terminal.
4. Distinguish a compile-time error from a runtime error, given an example of each.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-007-L01 | From text to execution: compilers and interpreters | 10 |
| BEG-007-L02 | Java's approach: bytecode and the JVM | 10 |
| BEG-007-L03 | JDK vs JRE vs JVM | 8 |
| BEG-007-L04 | Compile and run from the terminal | 12 |
| BEG-007-L05 | Demo: compile, run, break, and fix Hello World in the terminal | 8 |

**Lab** — `BEG-007-LAB1` *Hello from the terminal:* type a provided program, compile and run it from the terminal, inspect the generated `.class` file, introduce a syntax error and a division-by-zero error, and record each message. Then run the same program in IntelliJ. Acceptance: both error messages captured and classified correctly.

**Common mistakes:** class name not matching file name; running `java Hello.class`; confusing "it compiled" with "it works".

**Assessment:** explain the compile/run pipeline aloud while demonstrating it.

**Career relevance:** basis for build tools (BEG-054) and JVM internals (MID-001).
