# JNR-052 · Deployment basics — Quiz

Outcomes: O1 deploying the app and database · O2 environment configuration · O3 liveness and readiness · O4 graceful shutdown and rollback.

**Q01 (O1)** The easiest first deployment target is usually a: A. Kubernetes cluster B. Data center C. PaaS D. Mainframe
**Q02 (O1)** Between environments you should keep the same: A. Image B. Password C. Database D. URL
**Q03 (O2)** Where should database credentials live? A. In the image B. In Git C. In the Dockerfile D. In the platform's secret store
**Q04 (O2)** `SPRING_DATASOURCE_URL` maps to: A. `server.port` B. `spring.datasource.url` C. `logging.level` D. `app.name`
**Q05 (O3)** Readiness answers: A. Can the app take traffic now? B. Is the JVM installed? C. Is the disk big? D. Is the code compiled?
**Q06 (O3)** Liveness answers: A. Is the database full? B. Is the cache warm? C. Is the process stuck and in need of restart? D. Are tests green?
**Q07 (O3)** A liveness probe that calls the database can cause: A. Faster startups B. Restart loops during a database outage C. Better logs D. Smaller images
**Q08 (O4)** Graceful shutdown means the app: A. Kills requests immediately B. Ignores SIGTERM C. Deletes data D. Finishes in-flight requests before exiting
**Q09 (O4)** The quickest rollback is: A. Redeploying the previous image tag B. Rebuilding from scratch C. Editing the live server D. Deleting the database
**Q10 (O4)** Why keep old image tags? A. To enable rollback B. To confuse the team C. To slow the registry D. No reason

## Answers
Q01 C · Q02 A · Q03 D · Q04 B · Q05 A · Q06 C · Q07 B · Q08 D · Q09 A · Q10 A

## Practical part
Seven exercises `JNR-052-EX01` to `EX07` plus the lab; the assessment is a deployment walkthrough. Pass: quiz 8/10, at least five exercises correct, deployed instance reachable, and a documented rollback under 5 minutes.
