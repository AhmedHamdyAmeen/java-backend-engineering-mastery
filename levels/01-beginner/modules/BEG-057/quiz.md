# BEG-057 · Verifying AI-generated code — Quiz

Outcomes: O1 read and trace · O2 test against the requirement · O3 spot plausible-but-wrong code · O4 licensing, integrity, disclosure.

**Q01 (O1)** Before using generated code you should: A. Paste it and move on B. Explain what each part does C. Trust it because it compiles D. Only read the first line
**Q02 (O1)** A trace table records: A. Variable values after each step B. Test names C. Library versions D. Licenses
**Q03 (O1)** Who is responsible for AI-generated code you submit? A. The assistant B. The tool vendor C. You D. Nobody
**Q04 (O2)** Tests for generated code should be written from the: A. Generated code B. Requirement C. Output it printed D. Comments in the code
**Q05 (O2)** Writing the tests before pasting the code helps because: A. It is faster to type B. It is required by Java C. Tests then reflect the requirement, not the code's mistakes D. The code runs twice
**Q06 (O2)** Which input set is best for a search method? A. One typical value B. Empty, one item, first, last, missing C. Only large arrays D. Only `null`
**Q07 (O3)** `for (int i = 1; i < a.length; i++)` used to visit every item is an example of a(n): A. Invented method B. Complexity issue C. Licensing issue D. Off-by-one error
**Q08 (O3)** A call to a method that does not exist in the library is called: A. An invented library call B. An overload C. A regression D. A boundary
**Q09 (O3)** A generated loop calls `list.contains` on every item. The risk is: A. Wrong type B. Quadratic time C. Unchecked exception D. Memory leak
**Q10 (O4)** Honest disclosure of AI use includes: A. Nothing, if the code works B. Only the tool's name C. What you used it for and what you checked or changed D. A copy of the chat only

## Answers
Q01 B · Q02 A · Q03 C · Q04 B · Q05 C · Q06 B · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Assessment: given generated code with hidden defects, find them with tests and explain each (score = defects caught and explained), plus lab `BEG-057-LAB1` and exercises `BEG-057-EX01` to `EX06`. Pass: at least half of the hidden defects caught and explained, tests written before the code, and at least 8 of 10 quiz answers correct.
