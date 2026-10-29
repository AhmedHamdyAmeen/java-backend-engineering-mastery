# BEG-002 · Understanding software — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a restaurant, with the dining room (what you see) and the kitchen (what does the work).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-002-L01 · What software is: instructions, data, and behavior (8 min)
**Goal:** say what software is in one sentence.

**Key points**
- Software is a set of instructions plus the data those instructions use.
- Hardware is what you can touch; software is what tells it what to do.
- The same phone can become a map, a camera, or a game by changing the software.
- People write software in a programming language; the computer runs it.

**Show:** one phone, three apps, same hardware.

**Check:** Is a photo on your phone software? *(It is data. Software is the instructions that open and edit it.)*

---

## BEG-002-L02 · Kinds of software, with everyday examples (10 min)
**Goal:** classify any app as desktop, mobile, web frontend, backend, or embedded.

**Key points**
- Desktop: installed on a PC (a text editor).
- Mobile: installed on a phone (a ride app).
- Web frontend: runs in your browser (the page you see).
- Backend: runs on a server you never see; stores data and applies the rules.
- Embedded: lives inside a device (a washing machine, a car).

**Show:** a table with one everyday example per kind.

**Check:** Where does the app on a smart TV that plays its own menu run? *(Embedded, on the TV itself.)*

---

## BEG-002-L03 · Programs vs services: why a backend never "finishes" (10 min)
**Goal:** explain the difference between a program that exits and a service that keeps running.

**Key points**
- A program runs, does its job, and exits, like a calculator closing.
- A service starts and keeps running, waiting for requests, like a restaurant that stays open.
- A backend is a service. It answers many users, all day.
- If it stops, everyone who depends on it is affected.

**Show:** a program timeline ending, and a service timeline that never ends.

**Check:** Which one is a banking server: a program or a service? *(A service.)*

---

## BEG-002-L04 · The software lifecycle (12 min)
**Goal:** name the seven stages of a piece of software's life.

**Key points**
- Requirements: what is needed.
- Design: how it will work.
- Build: write the code.
- Test: check it works.
- Release: give it to users.
- Operate: keep it running.
- Retire: shut it down when it is no longer needed.
- It is a loop: after release, users ask for changes and the cycle starts again.

**Show:** the stages in a circle, with a feedback arrow from Operate back to Requirements.

**Check:** At which stage do bugs found by real users usually appear? *(Operate.)*

---

## BEG-002-L05 · Demo: one app, many pieces: mobile app, website, and backend (8 min)
**Goal:** see that one product is several pieces working together.

**Steps**
1. Open a food-ordering app (or a prepared demo) and place an order.
2. Open the same account on the website. Same data appears.
3. Say what each piece is: phone app, web frontend, backend that stores the order.
4. Switch off the network on the phone and show what still works and what does not.
5. **Planned mistake:** call the website "the backend"; correct it: the website is a frontend; the backend is the hidden service.
