# JNR-023 · File operations — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a post office counter for parcels: weigh every parcel, check what is inside, put it in your own labeled box (never the sender's label), and store it in the warehouse, not behind the counter.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-023-L01 · Multipart uploads (10 min)
**Goal:** accept a file in a request.

**Key points**
- Browsers and clients upload files with `multipart/form-data`: the body has several named parts, each with its own headers.
- In Spring, bind a file part with `@RequestPart` or `@RequestParam` of type `MultipartFile`.
- `MultipartFile` gives the original name, content type, size, and a stream of bytes.
- Other form fields can arrive in the same request.
- Test with `curl -F "file=@pen.png"`.

**Show**
```java
@PostMapping(value = "/products/{id}/images", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
ResponseEntity<ImageResponse> upload(@PathVariable long id, @RequestParam("file") MultipartFile file) { ... }
```

**Check:** Which content type carries file uploads? *(`multipart/form-data`.)*

---

## JNR-023-L02 · Limits and validation (8 min)
**Goal:** reject files that are too big or the wrong kind.

**Key points**
- Set size limits in configuration (`spring.servlet.multipart.max-file-size` and `max-request-size`); verify property names for your version.
- An oversized upload gives `413 Content Too Large` (verify wording) or a mapped error; handle it with a clear message.
- Check the declared content type against an allow-list (`image/png`, `image/jpeg`), and reject empty files.
- The declared type can lie; for stronger checks, inspect the first bytes (file signature) before accepting.
- Return `400` or `415` for wrong type, with a Problem Details body.

**Show**
```yaml
spring.servlet.multipart.max-file-size: 5MB
spring.servlet.multipart.max-request-size: 6MB
```

**Check:** Why check size in configuration? *(So huge uploads are stopped early.)*

---

## JNR-023-L03 · Streaming downloads (10 min)
**Goal:** send big files without loading them into memory.

**Key points**
- Reading a whole file into a `byte[]` uses memory per request; ten parallel downloads can crash the server.
- Return a `Resource` (for example `FileSystemResource`) or a `StreamingResponseBody`; Spring copies it in chunks.
- Set `Content-Type` from your stored record, and `Content-Length` when known.
- `Content-Disposition: attachment; filename="..."` makes browsers download; `inline` displays.
- Return `404` if the file record or file is missing.

**Show**
```java
@GetMapping("/images/{id}")
ResponseEntity<Resource> download(@PathVariable String id) {
    Resource r = storage.load(id);
    return ResponseEntity.ok().contentType(MediaType.IMAGE_PNG).body(r);
}
```

**Check:** Why not return a `byte[]`? *(The whole file sits in memory for each request.)*

---

## JNR-023-L04 · Where to store files (7 min)
**Goal:** pick a safe storage location and naming.

**Key points**
- Never store uploads inside the JAR or the project folder; they vanish on redeploy and the folder may be public.
- Use a configured directory outside the application (`app.storage.dir`), a mounted volume, or object storage such as S3 later (MID-056).
- Generate the stored name yourself, for example a UUID, and keep the original name only as metadata.
- Keep a record (ID, original name, content type, size, stored name) in your data model.
- Do not rely on the local disk if you run several instances.

**Show:** record `ImageRecord(id, productId, originalName, contentType, size, storedName)`; the file is stored as `<dir>/<uuid>`.

**Check:** Who chooses the stored file name? *(The server, never the client.)*

---

## JNR-023-L05 · Upload security (5 min)
**Goal:** name the main upload risks.

**Key points**
- **Path traversal:** a name like `../../etc/passwd` escapes the folder. Prevent it by never using the client name in a path; if you must resolve a path, `normalize()` it and check it stays inside the base directory.
- **Oversized files:** exhaust disk or memory. Enforce limits.
- **Content sniffing:** a browser may guess a type and run a file as script. Send the right `Content-Type`, and `X-Content-Type-Options: nosniff`.
- **Trusting the declared type:** verify signatures for important types.
- Serve uploads only through your controller, with access checks.

**Show**
```java
Path target = base.resolve(storedName).normalize();
if (!target.startsWith(base)) throw new IllegalArgumentException("Bad path");
```

**Check:** Which input should never be part of a path? *(The client's filename.)*

---

## JNR-023-L06 · Demo: product image upload and streaming download (10 min)
**Goal:** build upload, list, and download for product images. Prepares JNR-023-LAB1.

**Steps**
1. Add configuration for the storage directory and size limits.
2. Implement `POST /products/{id}/images`: check type and size, generate a UUID name, save to the storage directory, and return `201` with `Location`.
3. Implement `GET /products/{id}/images` (list) and `GET /images/{imageId}` (stream with the right `Content-Type`).
4. **Planned mistake:** the first version saves the file using `file.getOriginalFilename()`; a name with `../` writes outside the folder. Fix: generate the name and keep the original only as metadata.
5. Upload a 20 MB file and a fake `.png` and show both rejected.
