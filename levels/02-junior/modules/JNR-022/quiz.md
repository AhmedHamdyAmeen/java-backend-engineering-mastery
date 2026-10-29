# JNR-022 · API clients — Quiz

Outcomes: O1 collections and environments · O2 chaining · O3 curl · O4 RestClient.

**Q01 (O1)** A Postman environment holds: A. Source code B. Variables such as `baseUrl` and `token` C. Database tables D. Servers
**Q02 (O1)** Why not hard-code hosts and tokens in a shared collection? A. It is slower B. Postman forbids it C. They differ per environment and secrets leak D. JSON cannot hold them
**Q03 (O2)** How does request 2 use an ID from request 1? A. Retyping it B. A post-response script stores it in a variable C. It is automatic D. Via the URL bar history
**Q04 (O2)** What do Postman tests add? A. Pass or fail checks on responses B. Faster servers C. Encryption D. Code generation
**Q05 (O3)** `curl -i` does what? A. Installs curl B. Sends invalid data C. Shows response status and headers D. Ignores errors
**Q06 (O3)** To send JSON with curl you set: A. `-i` only B. `Content-Type: application/json` and `-d` C. `-o` D. Nothing
**Q07 (O3)** Which sets the method? A. `-X` B. `-s` C. `-o` D. `-L`
**Q08 (O4)** `RestClient` is used to: A. Define controllers B. Create database tables C. Call an external HTTP API from Spring D. Render HTML
**Q09 (O4)** A client without timeouts risks: A. Faster responses B. A slow remote blocking your threads C. Smaller JSON D. Cached data
**Q10 (O4)** After `.retrieve()`, `.body(Rates.class)` does: A. Deletes the response B. Sends the request twice C. Closes the app D. Converts the JSON body into a `Rates` object

## Answers
Q01 B · Q02 C · Q03 B · Q04 A · Q05 C · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Six exercises `JNR-022-EX01` to `EX06` plus the collection lab. Pass: at least five exercises and a lab where the collection runs end to end and the `RestClient` has timeouts.
