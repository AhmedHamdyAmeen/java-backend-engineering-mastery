# MID-071 · AI application threats — Quiz

Outcomes: O1 OWASP LLM categories · O2 indirect injection · O3 exfiltration · O4 cost abuse · O5 threat model and tests.

**Q01 (O1)** Why are LLM apps prone to injection? A. The model cannot reliably separate instructions from data B. Java is unsafe C. Prompts are too long D. HTTP is insecure
**Q02 (O1)** "Excessive agency" means: A. A very fast model B. The model has too many tools or too much permission C. Too many users D. Large context windows
**Q03 (O1)** Treating model output as raw HTML is: A. Improper output handling B. A cost control C. Prompt caching D. A good practice
**Q04 (O2)** Indirect prompt injection arrives through: A. Only the chat box B. The model weights C. Retrieved content such as a help article D. The network cable
**Q05 (O2)** Which defense is enforced outside the model? A. Restricting tools while untrusted content is in context B. Asking nicely in the prompt C. A longer system prompt D. Lower temperature
**Q06 (O2)** Content from your own index should be: A. Always trusted B. Never used C. Encrypted only D. Treated as untrusted data when put in the prompt
**Q07 (O3)** To stop exfiltration via links in output: A. Allow any domain B. Allowlist domains and strip other URLs C. Use shorter links D. Hide the answer
**Q08 (O3)** Secrets in the system prompt should be: A. Allowed if short B. Avoided; assume the prompt can leak C. Base64 encoded D. Stored in the vector index
**Q09 (O4)** A control against cost abuse is: A. Unlimited retries B. A bigger model C. Per-user token quotas and loop limits D. Longer prompts
**Q10 (O5)** Attack tests for the assistant should: A. Run once manually B. Be deleted after fixing C. Be written by the attacker D. Run in CI so regressions are caught

## Answers
Q01 A · Q02 B · Q03 A · Q04 C · Q05 A · Q06 D · Q07 B · Q08 B · Q09 C · Q10 D

## Practical part
Threat-model the assistant (rank the top five risks with mitigations) plus lab `MID-071-LAB1`. Pass: quiz at least 8/10, all attack tests in CI and passing after fixes, and an updated threat model.
