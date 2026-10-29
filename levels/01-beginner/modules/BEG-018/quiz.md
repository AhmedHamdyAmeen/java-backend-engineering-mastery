# BEG-018 · Debugging — Quiz

Outcomes: O1 breakpoints and stepping · O2 inspecting variables · O3 stack traces · O4 debugging process.

**Q01 (O1)** A breakpoint: A. Deletes a line B. Pauses the program before that line C. Stops compilation D. Prints a value
**Q02 (O1)** "Step into" does what? A. Runs the line and skips the method B. Enters the called method C. Exits the method D. Restarts the program
**Q03 (O1)** A conditional breakpoint pauses: A. Always B. Only when its condition is true C. Never D. After the program ends
**Q04 (O2)** A watch is used to: A. Keep an expression's value in view B. Change the program C. Save the file D. Format code
**Q05 (O2)** When a variable's value surprises you, you should: A. Ignore it B. Treat it as a clue and form a hypothesis C. Change code at random D. Restart the IDE
**Q06 (O3)** In a stack trace, which line do you open first? A. The last line B. The first line that points to your own code C. The middle line D. None
**Q07 (O3)** `Index 5 out of bounds for length 5` means: A. The array has 6 items B. Index 5 is one past the last valid index 4 C. The array is null D. It is a syntax error
**Q08 (O3)** `Integer.parseInt("abc")` throws: A. `NumberFormatException` B. `ArithmeticException` C. `StackOverflowError` D. `NullPointerException`
**Q09 (O4)** The correct order is: A. Fix, reproduce, test B. Reproduce, isolate, hypothesize, test, fix, verify C. Verify, fix, reproduce D. Guess, fix, ship
**Q10 (O4)** Fixing the symptom rather than the cause means: A. The bug may return in another form B. The bug is gone forever C. Tests are not needed D. The code is faster

## Answers
Q01 B · Q02 B · Q03 B · Q04 A · Q05 B · Q06 B · Q07 B · Q08 A · Q09 B · Q10 A

## Practical part
Five exercises `BEG-018-EX01` to `EX05` plus the five-bug hunt with written trails; the live debugging demonstration (also part of the BEG graduation gate) is assessed by the instructor. Pass: all five bugs fixed with trails and a successful live demonstration.
