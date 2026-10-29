# BEG-001 · Understanding computers — Exercises and lab

Each exercise lists the outcome it checks (see `BEG-001` in `levels/01-beginner/P1-computers-and-software.md`). Solutions are in the instructor section at the end.

## Lab

### BEG-001-LAB1 · Know your machine
**Outcomes:** 1, 2, 4 · **Time:** ~1 h

1. Record your CPU model, total RAM, and storage type (SSD/HDD) and capacity.
2. Note the current RAM in use and CPU % with only the system idle.
3. Find the five processes using the most memory. Write name, PID, and memory for each.
4. Open one large application. Record RAM in use again.
5. Close it and record RAM once more.

**Acceptance criteria**
- A table with the values from steps 1–5.
- One sentence per observation explaining it with the terms CPU, RAM, storage, or process (for example, why RAM rose when the app opened and fell when it closed).

## Exercises

| ID | Outcome | Task |
| --- | --- | --- |
| BEG-001-EX01 | 1 | For a smartphone, list two input devices, two output devices, and where its storage is. |
| BEG-001-EX02 | 1 | Match each to CPU, RAM, or storage: "holds your photos for years", "runs the instructions", "holds the app you are using right now". |
| BEG-001-EX03 | 2 | Explain in two sentences why an unsaved document is lost in a power cut but a saved one is not. |
| BEG-001-EX04 | 3 | Convert to decimal: `101`, `1111`, `10010`. |
| BEG-001-EX05 | 3 | Convert to binary: 5, 12, 20, 37. |
| BEG-001-EX06 | 3 | How many different values can 3 bits hold? 8 bits? 10 bits? Write the pattern you used. |
| BEG-001-EX07 | 3 | A photo file is 3 MB. Roughly how many bytes is that? |
| BEG-001-EX08 | 4 | Give one example of each: an operating system, an application, a process. |
| BEG-001-EX09 | 4 | Open two windows of the same app. How many processes do you see, and how can you tell? |
| BEG-001-EX10 | 4 | Start a process that uses CPU (for example, a video in the browser). Find it in Task Manager / Activity Monitor and record its PID and CPU %. |

## Instructor section (solutions)

- **EX01** Input: touch screen, microphone, camera. Output: screen, speaker. Storage: internal flash memory.
- **EX02** Storage; CPU; RAM.
- **EX03** An unsaved document exists only in RAM, which needs power to keep data. Saving copies it to storage (SSD), which keeps data without power.
- **EX04** 5, 15, 18.
- **EX05** `101`, `1100`, `10100`, `100101`.
- **EX06** 8, 256, 1024. Pattern: 2ⁿ for n bits.
- **EX07** About 3,000,000 bytes (3,145,728 if using 1024-based units; either accepted).
- **EX08** Any valid triple, for example Windows / Chrome / the Chrome process with PID 4312.
- **EX09** Depends on app; many apps show several processes. Evidence: separate rows with different PIDs.
- **EX10** Any running process with its PID and CPU % recorded.
