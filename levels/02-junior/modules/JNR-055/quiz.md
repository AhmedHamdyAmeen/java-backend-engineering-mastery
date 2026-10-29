# JNR-055 · AI-assisted development workflow — Quiz

Outcomes: O1 using assistants · O2 prompts · O3 generated tests · O4 reviewing AI-assisted PRs · O5 team policy.

**Q01 (O1)** A good use of an assistant is: A. Skipping all review B. Pasting secrets C. Drafting boilerplate D. Hiding code
**Q02 (O1)** Who is responsible for AI-written code you commit? A. The tool B. You C. The vendor D. Nobody
**Q03 (O2)** A good prompt includes: A. Only "fix it" B. Only the error C. Nothing else D. Code, constraints, and expected result
**Q04 (O2)** Why state conventions in a prompt? A. So output matches team style B. To make it faster C. To hide code D. To use more tokens
**Q05 (O3)** `assertNotNull(result)` alone is: A. A strong test B. A weak assertion C. A compile error D. A security fix
**Q06 (O3)** How can you check that a generated test is useful? A. Count lines B. Run it once C. Break the code and see it fail D. Ask the assistant
**Q07 (O4)** AI-assisted pull requests get: A. A lighter review B. No review C. A review only by the tool D. The same review standard
**Q08 (O4)** A very large generated diff should: A. Be accepted B. Be split into smaller changes C. Be merged quickly D. Be hidden
**Q09 (O5)** May you paste a production password into a prompt? A. No B. Yes if short C. Yes at night D. Only in chat
**Q10 (O5)** Which tools may you use? A. Any tool you like B. Only tools the employer approved C. Only free tools D. Only unknown tools

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 B · Q06 C · Q07 D · Q08 B · Q09 A · Q10 B

## Practical part
Seven exercises `JNR-055-EX01` to `EX07` plus the lab; the assessment is reviewing a provided AI-assisted pull request for defects and policy issues. Pass: at least 8 of 10 quiz answers, six exercises correct, and a lab log with at least two reasoned rejections and tests that stay green.
