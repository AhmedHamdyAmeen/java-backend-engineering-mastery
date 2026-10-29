# JNR-003 · Code quality — Quiz

Outcomes: O1 naming · O2 cohesion and coupling · O3 DRY, KISS, YAGNI · O4 smells and refactoring.

**Q01 (O1)** Which name shows intent best? A. `x` B. `calc2` C. `data` D. `totalWithTax`
**Q02 (O1)** A boolean method should read like: A. A question, such as `isEmpty` B. A noun C. A number D. A class name
**Q03 (O2)** High cohesion means: A. Parts of a class belong together B. Many dependencies C. Many methods D. Many comments
**Q04 (O2)** Low coupling means a class: A. Has no methods B. Depends on few other things C. Is very short D. Has no tests
**Q05 (O2)** A good way to reduce coupling is to: A. Use `new` everywhere B. Make fields public C. Depend on an interface D. Copy code
**Q06 (O3)** YAGNI means: A. Yet another good name idea B. Always use interfaces C. Never write tests D. Do not build what you do not need yet
**Q07 (O3)** DRY can conflict with: A. KISS B. Compilation C. Maven D. Git
**Q08 (O4)** Using `double` for money is: A. Feature envy B. Primitive obsession C. A long method D. Good practice
**Q09 (O4)** The fix for a long method is: A. Add comments B. Add more lines C. Extract Method D. Delete tests
**Q10 (O4)** Before refactoring you should: A. Have passing tests B. Change behavior C. Skip commits D. Turn off the IDE

## Answers
Q01 D · Q02 A · Q03 A · Q04 B · Q05 C · Q06 D · Q07 A · Q08 B · Q09 C · Q10 A

## Practical part
Seven exercises `JNR-003-EX01` to `EX07`, the smell-spotting review of an unseen class, and the lab. Pass: at least 8 of 10 quiz answers, six exercises correct, and a lab history where every commit is one named refactoring with tests green.
