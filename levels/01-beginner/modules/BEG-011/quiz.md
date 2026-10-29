# BEG-011 · Input and output — Quiz

Outcomes: O1 Scanner · O2 parse and validate · O3 formatting · O4 never trust input.

**Q01 (O1)** Which reads a whole line? A. `nextInt()` B. `nextLine()` C. `print()` D. `parseInt()`
**Q02 (O1)** To use `Scanner` you must: A. Import `java.util.Scanner` B. Install a library C. Use `var` D. Nothing
**Q03 (O1)** `nextLine()` returns empty right after `nextInt()` because: A. A bug in Java B. The leftover Enter is still in the input C. The scanner is closed D. The number was negative
**Q04 (O2)** `Integer.parseInt("12") + 1` is: A. `121` B. `13` C. `12` D. An error
**Q05 (O2)** `in.hasNextInt()` tells you: A. Whether an int is waiting to be read B. The max int C. The line count D. Nothing
**Q06 (O3)** `%.2f` prints: A. A decimal with 2 digits after the point B. 2 numbers C. A 2-character string D. An int
**Q07 (O3)** `%-10s` does what? A. Left-aligns text in 10 characters B. Right-aligns C. Prints 10 times D. Prints a minus sign
**Q08 (O3)** `%n` in `printf` is: A. A number B. A new line C. A name D. An error
**Q09 (O4)** Why validate input? A. Users can type wrong values B. It is slower C. It is optional always D. It deletes data
**Q10 (O4)** Best response to the quantity `abc`: A. Crash B. Ask again with a clear message C. Use 0 silently D. Ignore the program

## Answers
Q01 B · Q02 A · Q03 B · Q04 B · Q05 A · Q06 A · Q07 A · Q08 B · Q09 A · Q10 B

## Practical part
Five exercises `BEG-011-EX01` to `EX05` plus the receipt printer. Pass: at least four exercises and a lab that re-prompts on invalid input.
