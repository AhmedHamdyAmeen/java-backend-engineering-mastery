# BEG-001 · Understanding computers — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a restaurant kitchen.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-001-L01 · What a computer actually does: input, processing, storage, output (10 min)
**Goal:** see every computer as four steps: input, processing, storage, output.

**Key points**
- Input is anything that goes in: keyboard, touch, microphone, a message from the network.
- Processing is the computer working on that input.
- Storage is where it keeps data for later.
- Output is anything that comes out: screen, sound, a file, a message sent away.
- A computer follows instructions exactly. It does what you said, not what you meant.

**Show:** a calculator app: tap `2 + 3` (input), it computes (processing), shows `5` (output), remembers the last result (storage).

**Check:** Name one input and one output of an ATM. *(Card or keypad in; cash or screen out.)*

---

## BEG-001-L02 · CPU, RAM, and storage: the kitchen analogy (10 min)
**Goal:** tell CPU, RAM, and storage apart by their jobs.

**Key points**
- CPU = the chef. It does the work.
- RAM = the countertop. Small and fast; holds what you are working on now.
- Storage (SSD) = the pantry. Big and slower; keeps things for a long time.
- Opening an app copies it from the pantry to the countertop.
- Power off: the countertop is wiped (RAM forgets), the pantry stays full (SSD remembers).
- "Save" means copy from RAM to storage.

**Show:** the kitchen picture, then a table: part / job / speed / size / survives power-off.

**Check:** Power fails before you save an essay. Where was it, and why is it gone? *(In RAM; RAM forgets without power.)*

---

## BEG-001-L03 · Bits, bytes, and binary numbers (12 min)
**Goal:** read and write small binary numbers.

**Key points**
- A bit is one switch: 0 or 1.
- 8 bits make 1 byte, which can hold 256 different values.
- Decimal positions are worth 1, 10, 100. Binary positions are worth 1, 2, 4, 8, 16.
- `1011` = 8 + 0 + 2 + 1 = 11.
- To go the other way, take the biggest power of two that fits and repeat. 13 = 8 + 4 + 1 = `1101`.
- Text, colours, and photos are all stored as numbers.

**Show:** eight on/off switches with the decimal value updating as you click them.

**Check:** `110` in decimal? *(6)* 9 in binary? *(`1001`)*

---

## BEG-001-L04 · The operating system's job (8 min)
**Goal:** say what the OS does and why programs need it.

**Key points**
- The OS (Windows, macOS, Linux, Android) is the restaurant manager.
- It talks to the hardware so programs do not have to.
- It shares CPU and RAM between everything running.
- It offers services: open a file, draw a window, use the network.
- Your Java programs will run on an OS, usually Linux on servers.

**Show:** layers: hardware, operating system, applications.

**Check:** Name two things the OS shares between programs. *(CPU time, RAM.)*

---

## BEG-001-L05 · Applications and processes: Task Manager / Activity Monitor tour (10 min)
**Goal:** tell an application from a process and find processes on your machine.

**Key points**
- An application is a file on storage: a recipe in the cookbook.
- A process is that application running: the dish being cooked now.
- One application can have several processes. Each has an ID (PID), CPU use, and RAM use.
- Windows: Task Manager (`Ctrl+Shift+Esc`). macOS: Activity Monitor. Linux: `top`.
- A service is a process that runs all the time, waiting for work. A backend server is one.

**Show:** Task Manager sorted by memory; point at one PID.

**Check:** Chrome the application vs. a Chrome process? *(File on disk vs. running copy with a PID.)*

---

## BEG-001-L06 · Demo: watching RAM and CPU while opening apps (8 min)
**Goal:** see the kitchen analogy happen on a real machine. Prepares `BEG-001-LAB1`.

**Steps**
1. Open Task Manager / Activity Monitor. Read out CPU model, RAM size, disk size.
2. Note RAM in use with nothing open.
3. Open a heavy app. Watch RAM rise and CPU spike, then settle.
4. Sort by memory and name the top five processes.
5. **Planned mistake:** about to end the wrong process; stop and check name and PID first.
6. Close the app and watch RAM drop.

**Then:** the learner pauses and does the lab.
