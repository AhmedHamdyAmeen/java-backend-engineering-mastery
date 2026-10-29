# JNR-023 · File operations — Exercises and lab

## Lab
### JNR-023-LAB1 · Product images
**Outcomes:** 1–4 · **Time:** ~2 h
Upload, list, and download product images in Shop API. Enforce a size limit and a content-type allow-list; store files in a configured directory outside the application using generated names; stream downloads. Complete the security checklist below.

Security checklist: filename never used in a path; size limit enforced; content type allow-listed; files outside the JAR; `nosniff` header set; downloads only through the controller.

**Acceptance:** path traversal attempt rejected; 20 MB file rejected.

## Exercises (assessment: lab plus security checklist)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-023-EX01 | 1 | Implement a multipart endpoint and upload a file with `curl -F`. |
| JNR-023-EX02 | 1 | Configure a 2 MB limit and show the response for a 3 MB file. |
| JNR-023-EX03 | 1 | Reject files whose content type is not `image/png` or `image/jpeg`, and empty files. |
| JNR-023-EX04 | 2 | Return a stored file as a `Resource` with the right `Content-Type`, and `404` when missing. |
| JNR-023-EX05 | 3 | Store uploads in a configured external directory using UUID names, with the original name kept as metadata. |
| JNR-023-EX06 | 4 | Explain path traversal, oversized files, and content sniffing, each with one prevention. |

## Solutions
- **EX01** `curl -i -F "file=@pen.png" localhost:8080/products/1/images`.
- **EX02** `spring.servlet.multipart.max-file-size=2MB`; the response is an error status (413 or a mapped one) with a clear body.
- **EX03** `Set.of("image/png","image/jpeg").contains(file.getContentType())`; `file.isEmpty()` gives `400`.
- **EX04** `new FileSystemResource(path)` in `ResponseEntity.ok().contentType(...).body(resource)`; missing record gives `404`.
- **EX05** `String stored = UUID.randomUUID().toString(); Files.copy(file.getInputStream(), base.resolve(stored));`
- **EX06** Path traversal: never use the client name, normalize and check `startsWith(base)`. Oversized files: size limits. Sniffing: correct `Content-Type` plus `X-Content-Type-Options: nosniff`.

**Outcome 4** is also covered by the security checklist and quiz Q08 to Q10.
