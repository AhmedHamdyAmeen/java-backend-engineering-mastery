# JNR-016 · Spring testing basics — Exercises and lab

## Lab
### JNR-016-LAB1 · Test the products feature
**Outcomes:** 1–4 · **Time:** ~3 h
1. Write unit tests for `ProductService` using a fake or in-memory repository (found, not found, rule violation).
2. Write `@WebMvcTest` tests for `ProductController`: `GET /products/{id}` success, `POST /products` validation failure, and not found.
3. Mock the service with Mockito inside the slice tests.
4. Assert the JSON body and the Problem Details shape, not only the status.
5. Add one `@SpringBootTest` smoke test and record the run times of both kinds.
**Acceptance:** tests run in seconds; no full context in controller tests; every test asserts the body or behavior.

## Exercises (assessment: write the missing tests for a provided controller)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-016-EX01 | 1 | Unit-test `PricingService` with constructor-passed fakes (no annotations). |
| JNR-016-EX02 | 2 | Write a MockMvc test for `GET /products` returning two items; assert the array length and a field. |
| JNR-016-EX03 | 2 | Write a MockMvc test where a blank `name` returns 400; assert the field error. |
| JNR-016-EX04 | 3 | Stub `service.get(5)` to throw `NotFoundException` and verify the 404 body; also `verify` the service call. |
| JNR-016-EX05 | 4 | Time a slice test versus a `@SpringBootTest` for the same endpoint; write two sentences on when each is right. |
| JNR-016-EX06 | 4 | Given a suite with eight `@SpringBootTest` classes, each with a different `@MockitoBean`, explain the slowness and propose a fix. |

## Solutions
- **EX01** `var service = new PricingService(fakeRates); assertThat(service.total(...)).isEqualByComparingTo("12.00");`
- **EX02** `mvc.perform(get("/products")).andExpect(status().isOk()).andExpect(jsonPath("$.length()").value(2)).andExpect(jsonPath("$[0].name").value("Pen"));`
- **EX03** `mvc.perform(post("/products").contentType(APPLICATION_JSON).content("{\"name\":\"\"}")).andExpect(status().isBadRequest())` plus a `jsonPath` check on the errors.
- **EX04** `when(service.get(5)).thenThrow(new NotFoundException("Product",5));` then check the 404 and `verify(service).get(5)`.
- **EX05** Slice: faster, tests the web layer only. Full context: slower, tests the wiring and everything together.
- **EX06** Each different mock creates a new cached context; reduce them by using slices, or share one configuration or base class.
