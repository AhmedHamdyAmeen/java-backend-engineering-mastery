# BEG-003 · The internet — Exercises and lab

## Lab
### BEG-003-LAB1 · Follow a request
**Outcomes:** 2, 3 · **Time:** ~1 h
1. Run `nslookup` on three domains and record the IP addresses.
2. Open a site with the browser's Network tab open and reload.
3. Find the main document request; record its method, status code, and type.

**Acceptance:** screenshots plus labeled answers.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-003-EX01 | 1 | List two internet services that are not the web. |
| BEG-003-EX02 | 2 | Write, in order, the steps from typing a URL to seeing the page. |
| BEG-003-EX03 | 2 | Explain the difference between an IP address and a port. |
| BEG-003-EX04 | 3 | Run `nslookup` on a domain of your choice. Which line holds the IP address? |
| BEG-003-EX05 | 3 | Why can one domain return several IP addresses? |
| BEG-003-EX06 | 4 | State two things HTTPS adds over HTTP. |
| BEG-003-EX07 | 4 | True or false, with a reason: HTTPS hides which site you visit. |

## Solutions
- **EX01** Email, video calls, online games, file transfer.
- **EX02** URL typed → DNS lookup → connect to the server → send request → server sends response → browser renders the page.
- **EX03** IP identifies the computer; the port identifies the service on it.
- **EX04** The "Address" line(s) after the name in the answer section.
- **EX05** The site may run on several servers for capacity and reliability.
- **EX06** Encryption in transit, and proof that you reached the real site.
- **EX07** False. The domain can still be seen; only the content is encrypted.
