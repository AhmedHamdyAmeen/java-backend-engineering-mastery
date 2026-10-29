# JNR-022 · API clients — Exercises and lab

## Lab
### JNR-022-LAB1 · Shop collection
**Outcomes:** 1–4 · **Time:** ~1.5 h
Create a shared Postman collection for Shop API with `local` and `deployed` environments and chained requests (create, read, update, delete). In the application, fetch exchange rates from an external API through `RestClient`, with connect and read timeouts configured.

**Acceptance:** the collection runs end-to-end; timeout configured.

## Exercises (assessment: lab check)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-022-EX01 | 1 | Create `local` and `deployed` environments with `baseUrl` and use `{{baseUrl}}` in every request. |
| JNR-022-EX02 | 2 | Chain: create a product, store its ID, then fetch it with the stored ID. |
| JNR-022-EX03 | 2 | Add tests to the chain that check status codes and that the returned `id` is present. |
| JNR-022-EX04 | 3 | Write `curl` commands for list, create (JSON body), update, and delete on products. |
| JNR-022-EX05 | 4 | Call a public JSON API with `RestClient` and map the response to a record. |
| JNR-022-EX06 | 4 | Configure timeouts and show what happens when the remote is slow or unreachable. |

## Solutions
- **EX01** Environment variables `baseUrl`; requests use `{{baseUrl}}/products`; no host strings remain.
- **EX02** `pm.environment.set("productId", pm.response.json().id)`, then `GET {{baseUrl}}/products/{{productId}}`.
- **EX03** `pm.test("201", () => pm.response.to.have.status(201));` and check `json.id`.
- **EX04** e.g. `curl -i -X PUT localhost:8080/products/1 -H 'Content-Type: application/json' -d '{...}'`; `curl -i -X DELETE localhost:8080/products/1`.
- **EX05** `client.get().uri(...).retrieve().body(MyRecord.class)`.
- **EX06** Build the client with request factory settings for connect and read timeouts (verify the exact API for your Spring version); catch the exception and return a clear error or fallback.

**Outcome 1** is also checked by quiz Q01 and the lab's two environments.
