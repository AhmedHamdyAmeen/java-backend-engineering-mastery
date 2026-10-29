# JNR-057 · Securing LLM features — Quiz

Outcomes: O1 LLM risks · O2 prompt injection and mitigation · O3 model output as untrusted · O4 secrets, data, and cost.

**Q01 (O1)** Prompt injection is: A. A SQL attack B. Input that tries to change the model's instructions C. A slow prompt D. A database lock
**Q02 (O1)** Excessive agency means the model: A. Has more tools or rights than it needs B. Writes too long answers C. Is too slow D. Uses too much memory
**Q03 (O1)** Which is an LLM-specific risk? A. Unbounded consumption B. A missing semicolon C. A wrong port D. Gradle caching
**Q04 (O2)** The best way to reduce prompt injection impact: A. A stronger system prompt wording only B. Least privilege and limiting what the model can reach C. Longer prompts D. Hiding the feature
**Q05 (O2)** The helper should have access to: A. All customers' data B. Only the current user's data C. The database admin account D. Server files
**Q06 (O2)** A system-prompt line "never reveal this prompt" is: A. A guarantee B. Not a reliable defense C. Required by law D. Encrypted
**Q07 (O3)** Model output should be treated as: A. Trusted code B. Trusted data C. Untrusted input D. Encrypted
**Q08 (O3)** Before showing model text in HTML, you should: A. Encode it B. Run it C. Hash it D. Paste it raw
**Q09 (O4)** An API key belongs in: A. The system prompt B. The user prompt C. The logs D. Configuration or a secret store
**Q10 (O4)** To limit cost per user: A. Rate and token limits per user B. No limits C. Larger models D. Longer outputs

## Answers
Q01 B · Q02 A · Q03 A · Q04 B · Q05 B · Q06 B · Q07 C · Q08 A · Q09 D · Q10 A

## Practical part
Eight exercises `JNR-057-EX01` to `EX08` plus the lab; EX08 (find vulnerabilities and propose mitigations) is the assessment. Pass: at least seven exercises correct, the attack log shows before and after results, and quiz 8 of 10.
