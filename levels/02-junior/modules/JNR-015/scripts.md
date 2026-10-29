# JNR-015 · Error handling — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a hospital reception: every problem goes to one desk that gives the patient a clear form, while the doctors' private notes stay in the back office.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-015-L01 · Errors are part of the API (7 min)
**Goal:** treat error responses as a designed contract.

**Key points**
- Clients depend on error responses as much as on success ones.
- Use the right status: 400 bad input, 404 not found, 409 conflict, 422 or 400 for a broken business rule, 500 for our bug.
- Never return 200 with `"error": true`: tools and clients read the status first.
- One error shape for the whole API.

**Show:** a table: situation / status / meaning.

**Check:** A product id does not exist. Which status? *(404.)*

---

## JNR-015-L02 · Application exception hierarchy (8 min)
**Goal:** design a small set of exceptions.

**Key points**
- Define a base `ShopException` (unchecked) and a few subclasses: `NotFoundException`, `ConflictException`, `BusinessRuleException`.
- Services throw them; they say what happened, not which HTTP status.
- Carry useful data: the entity name and id.
- Keep the tree small; do not create one class per message.

**Show**
```java
public class NotFoundException extends ShopException {
    public NotFoundException(String entity, Object id) { super(entity + " " + id + " not found"); }
}
```

**Check:** Does the service choose the HTTP status? *(No; the advice maps the exception to a status.)*

---

## JNR-015-L03 · `@RestControllerAdvice` (10 min)
**Goal:** handle exceptions in one place.

**Key points**
- `@RestControllerAdvice` is a class whose `@ExceptionHandler` methods apply to all controllers.
- Each handler maps an exception type to a response.
- Remove `try/catch` from controllers; let exceptions travel up.
- Order: specific handlers first; add a catch-all for `Exception`.
- Validation failures arrive as `MethodArgumentNotValidException`.

**Show**
```java
@RestControllerAdvice
class ApiExceptionHandler {
    @ExceptionHandler(NotFoundException.class)
    ProblemDetail notFound(NotFoundException ex) {
        return ProblemDetail.forStatusAndDetail(HttpStatus.NOT_FOUND, ex.getMessage());
    }
}
```

**Check:** Where should the `try/catch` for not-found live? *(Nowhere in controllers; the advice handles it.)*

---

## JNR-015-L04 · Problem Details (8 min)
**Goal:** return the standard error body.

**Key points**
- RFC 9457 (which replaces RFC 7807) defines a JSON error format: `type`, `title`, `status`, `detail`, `instance`.
- Content type: `application/problem+json`.
- Spring has `ProblemDetail`; you can add extra fields with `setProperty`, for example field errors.
- Spring can also produce Problem Details for its own errors when enabled; verify the property for your version before recording.

**Show**
```json
{ "type": "about:blank", "title": "Not Found", "status": 404,
  "detail": "Product 42 not found", "instance": "/products/42" }
```

**Check:** What content type does Problem Details use? *(`application/problem+json`.)*

---

## JNR-015-L05 · What not to tell the client (7 min)
**Goal:** avoid leaking internals.

**Key points**
- Never return stack traces, SQL, class names, or file paths.
- Database messages can reveal table names and values; map them to a safe message.
- Log the full exception server-side with a correlation id; give the client the id to quote.
- For unexpected errors return a generic 500 body.

**Show**
```java
@ExceptionHandler(Exception.class)
ProblemDetail unexpected(Exception ex) {
    log.error("Unhandled error", ex);
    return ProblemDetail.forStatusAndDetail(HttpStatus.INTERNAL_SERVER_ERROR, "Unexpected error");
}
```

**Check:** Where does the stack trace go? *(Into the server log, not the response.)*

---

## JNR-015-L06 · Demo: centralized Problem Details error handling (10 min)
**Goal:** one advice class returns 400, 404, 409, 500; prepares JNR-015-LAB1.

**Steps**
1. Add the exception hierarchy and make `ProductService` throw `NotFoundException`.
2. Create `ApiExceptionHandler` with handlers for not found and conflict.
3. Add a handler for `MethodArgumentNotValidException` that returns field errors in a property.
4. **Planned mistake:** a catch-all that returns `ex.getMessage()` leaks a database message. Fix: log it, return a generic detail.
5. Call each case with `curl` and compare the bodies.
