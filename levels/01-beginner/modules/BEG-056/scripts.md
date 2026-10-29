# BEG-056 · AI coding assistants for learners — Lecture scripts

**Video:** 42 min · **Analogy used throughout:** a very well-read autocomplete friend who answers fast and sounds sure, but never checks the facts.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-056-L01 · What an AI coding assistant actually is (8 min)
**Goal:** explain in simple terms how an assistant produces text.

**Key points**
- An assistant is built on a large language model (LLM), trained on huge amounts of text and code.
- Text is cut into tokens: small pieces of words or code.
- The model predicts the next token, again and again, to build an answer.
- It learns patterns from training data; it does not run your code or look things up unless a tool is attached.
- So it is fluent, but fluent is not the same as correct.

**Show:** a diagram: your question, split into tokens, the model picking one likely next token at a time, the answer growing left to right.

**Check:** What does the model do at each step? *(Predicts the next token.)*

---

## BEG-056-L02 · Why assistants sound right and are sometimes wrong (10 min)
**Goal:** recognize hallucinations and other typical failures.

**Key points**
- A hallucination is a confident answer that is invented or false.
- Examples: a method that does not exist, a wrong library call, an outdated API, a wrong explanation.
- The tone is the same whether the answer is right or wrong.
- Training data has a cutoff date, so very new versions may be missing.
- Always verify: compile it, run it, check the official documentation.

**Show:** an assistant suggests `list.addAll(5)` for a `List<Integer>`; the compiler rejects it. Show how the compiler message and the docs settle it.

**Check:** Does a confident tone mean a correct answer? *(No. Verify every answer.)*

---

## BEG-056-L03 · Asking good questions: goal, code, error, attempts (8 min)
**Goal:** write a question that gets a useful answer.

**Key points**
- State the goal: what you want the code to do.
- Give the smallest code that shows the problem, not the whole project.
- Paste the exact error message or stack trace.
- Say what you already tried and what happened.
- Mention the Java version and anything relevant.

**Show**
```text
Goal: count words longer than 4 letters.
Code: (10-line method)
Error: ArrayIndexOutOfBoundsException at Words.java:7
Tried: printed the array length; it was 0 for empty input.
Question: why does it fail on empty input?
```

**Check:** Name the four parts of a good question. *(Goal, code, exact error, what you tried.)*

---

## BEG-056-L04 · Learning with AI without skipping the learning (8 min)
**Goal:** use an assistant to learn, not to avoid thinking.

**Key points**
- Try first: write your own hypothesis before you ask.
- Ask for an explanation of the error or concept, not a finished answer to copy.
- Explain the answer back in your own words; if you cannot, ask again.
- Check it with the debugger or a small test.
- Follow safe-use rules: never paste passwords, keys, tokens, or personal data; follow course and employer policies.

**Show:** a three-step routine: 1 my hypothesis, 2 ask, 3 confirm or reject with evidence.

**Check:** Name two things you must never paste into a chat. *(Passwords or keys, and personal data.)*

---

## BEG-056-L05 · Demo: using an assistant to understand a stack trace, then checking it (8 min)
**Goal:** apply the routine to a real trace. Prepares `BEG-056-LAB1`.

**Steps**
1. Run a program from the bug hunt and copy the stack trace.
2. Write your own hypothesis first.
3. Ask with goal, code, exact error, and what you tried.
4. Read the answer and restate it in your own words.
5. **Planned mistake:** the assistant names a method that does not exist. The compiler and the documentation show it is a hallucination; ask again with that evidence.
6. Confirm the real cause with the debugger and log the result.

**Check:** What settled the disagreement? *(The compiler, the documentation, and the debugger, not the assistant's confidence.)*
