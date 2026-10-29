# JNR-023 · File operations — Quiz

Outcomes: O1 uploads and limits · O2 streaming downloads · O3 storage · O4 upload risks.

**Q01 (O1)** File uploads use which content type? A. `application/json` B. `text/plain` C. `multipart/form-data` D. `image/png` only
**Q02 (O1)** A Spring type for an uploaded file is: A. `MultipartFile` B. `UploadBean` C. `FileJson` D. `Part32`
**Q03 (O1)** Why check content type and size? A. To speed up JSON B. To reject unwanted or huge files early C. To rename files D. To enable caching
**Q04 (O2)** Streaming a download avoids: A. Using HTTP B. Setting headers C. Loading the whole file into memory D. Status codes
**Q05 (O2)** Which return type suits a file download? A. `Resource` B. `int` C. `byte[]` for every file D. `Void` only
**Q06 (O3)** Where should uploads be stored? A. Inside the JAR B. In a configured directory outside the application C. In the source folder D. In the URL
**Q07 (O3)** Who chooses the stored filename? A. The client B. The browser C. The server, for example a UUID D. The OS user
**Q08 (O4)** A filename `../../secret.txt` is an example of: A. Content sniffing B. Path traversal C. Streaming D. Pagination
**Q09 (O4)** Best defense against that attack: A. Use the client name carefully lowercased B. Trust the content type C. Increase the size limit D. Never use the client name in the path
**Q10 (O4)** `X-Content-Type-Options: nosniff` helps against: A. Slow uploads B. Large files C. Browsers guessing and running a wrong type D. Missing files

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 A · Q06 B · Q07 C · Q08 B · Q09 D · Q10 C

## Practical part
Six exercises `JNR-023-EX01` to `EX06`, the product-images lab, and the security checklist. Pass: at least five exercises and a lab that rejects the traversal attempt and the 20 MB file.
