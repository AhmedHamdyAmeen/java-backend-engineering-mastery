# MID-072 · AI-assisted engineering at codebase scale — Quiz

Outcomes: O1 context for assistants · O2 debugging with evidence · O3 refactoring under tests · O4 useful generated tests · O5 measuring effect.

**Q01 (O1)** Best context for an assistant: A. The whole repository B. Only the error message C. Relevant files, tests, conventions, and failing output D. Nothing
**Q02 (O1)** Which must never be put in a prompt? A. Secrets and customer data B. Class names C. Test names D. Public docs
**Q03 (O2)** An AI-suggested cause of a bug should be: A. Applied immediately B. Confirmed with evidence before changing code C. Ignored D. Merged with tests removed
**Q04 (O2)** The best first request when debugging: A. "Fix it" B. "Rewrite the module" C. Ranked hypotheses and how to test each D. "Delete the test"
**Q05 (O3)** Safe refactoring with AI means: A. One large change B. Small steps with tests run after each C. No tests D. Changing contracts freely
**Q06 (O3)** An AI step turns tests red. You: A. Continue on red B. Disable the test C. Merge anyway D. Revert or fix that step before continuing
**Q07 (O4)** A generated test that mirrors the implementation: A. Is the best kind B. Adds little protection and may be discarded C. Proves correctness D. Replaces review
**Q08 (O4)** A surviving mutant means: A. The code is perfect B. The mutation tool failed C. No test detected the behavior change D. Tests are too slow
**Q09 (O5)** A good measure of AI assistance: A. Lines generated B. Prompts per day C. Review time, defect rate, and test quality D. Tool cost only
**Q10 (O5)** Who is responsible for AI-written code in a PR? A. The tool B. The author who submits it C. The reviewer only D. Nobody

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 D · Q07 B · Q08 C · Q09 C · Q10 B

## Practical part
Five exercises `MID-072-EX01` to `EX05` plus the lab. Pass: at least four exercises correct, and a review of an AI-generated pull request that decides what to accept, change, or reject with reasons.
