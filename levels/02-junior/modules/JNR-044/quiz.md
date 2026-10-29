# JNR-044 · Mocking — Quiz

Outcomes: O1 test doubles · O2 stubbing and verifying · O3 captors · O4 over-mocking.

**Q01 (O1)** A working in-memory implementation of a repository is a: A. Stub B. Mock C. Spy D. Fake
**Q02 (O1)** A stub mainly: A. Returns canned answers B. Records every call only C. Wraps a real object D. Deletes data
**Q03 (O2)** Which stubs a return value? A. `verify(m).x()` B. `when(m.x()).thenReturn(v)` C. `captor.capture()` D. `never()`
**Q04 (O2)** To simulate a timeout you use: A. `thenReturn` B. `times(0)` C. `thenThrow` D. `@Spy`
**Q05 (O2)** `verify(mock, never()).refund(any())` checks that: A. refund returned null B. refund was called twice C. refund is private D. refund was not called
**Q06 (O3)** `ArgumentCaptor` is used to: A. Create mocks B. Inspect an argument passed to a collaborator C. Delete data D. Start a container
**Q07 (O3)** After `verify(repo).save(captor.capture())` you read it with: A. `captor.getValue()` B. `captor.reset()` C. `repo.get()` D. `captor.next()`
**Q08 (O4)** Which type should you NOT mock directly? A. Your own interface B. A type you do not own, like `HttpClient` C. A fake D. A service interface
**Q09 (O4)** Verifying every internal call makes tests: A. Faster B. More readable C. Tied to implementation D. Immune to refactoring
**Q10 (O4)** A mock returning another mock usually signals: A. Great design B. Needed Mockito feature C. Faster tests D. Over-coupling or a leaky test

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 D · Q06 B · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Seven exercises `JNR-044-EX01` to `EX07` plus the lab; for the assessment, refactor a provided over-mocked suite so it still passes after an internal refactor. Pass: quiz 8/10, at least five exercises correct, and the refactor accepted.
