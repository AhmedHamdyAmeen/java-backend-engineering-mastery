# BEG-020 · Classes and objects — Quiz

Outcomes: O1 write a class · O2 create objects · O3 `this` · O4 static vs instance.

**Q01 (O1)** A constructor: A. Has a return type `void` B. Has the class name and no return type C. Must be static D. Is called with `.`
**Q02 (O1)** If you write any constructor yourself, the free no-argument one: A. Stays B. Becomes static C. Becomes private D. Disappears
**Q03 (O1)** Several constructors with different parameters is called: A. Overloading B. Overriding C. Shadowing D. Casting
**Q04 (O1)** The default value of an `int` field is: A. null B. 1 C. 0 D. undefined
**Q05 (O2)** To create an object: A. `Account a = Account();` B. `Account.new()` C. `new a = Account;` D. `Account a = new Account();`
**Q06 (O2)** After `Account b = a;` there are: A. One object, two references B. Two objects C. Zero objects D. An error
**Q07 (O2)** Calling a method on a `null` reference throws: A. `ArithmeticException` B. `NullPointerException` C. `IOException` D. Nothing
**Q08 (O3)** In `Account(String owner) { owner = owner; }` the field: A. Is set B. Is deleted C. Stays unset D. Causes a compile error
**Q09 (O3)** `this(...)` inside a constructor: A. Ends the program B. Calls another constructor of the same class C. Calls the superclass D. Creates a thread
**Q10 (O4)** Which should be `static`? A. A constant shared by all accounts B. An owner name C. A balance D. A deposit amount

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 A

## Practical part
Five exercises `BEG-020-EX01` to `EX05` plus Bank Accounts v1. Pass: at least four exercises correct and the lab meeting its acceptance.
