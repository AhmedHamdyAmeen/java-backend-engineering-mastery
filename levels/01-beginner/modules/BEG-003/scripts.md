# BEG-003 · The internet — Lecture scripts

**Video:** 63 min · **Analogy used throughout:** the postal system (addresses, a phone book, letters, replies).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-003-L01 · Internet vs web (8 min)
**Goal:** know that the web is one thing that runs on the internet.

**Key points**
- The internet is the global network of connected computers: the roads.
- The web is websites you open in a browser: one kind of traffic on those roads.
- Email, video calls, and games also use the internet but are not the web.
- A mobile app talking to a server uses the internet, often without a browser.

**Show:** a big circle (internet) with smaller circles inside: web, email, video calls.

**Check:** Is email part of the web? *(No. It uses the internet but is not the web.)*

---

## BEG-003-L02 · IP addresses and ports (10 min)
**Goal:** explain what an IP address and a port are.

**Key points**
- Every device on a network has an IP address, like a building's street address.
- Example: `93.184.216.34`.
- A port is a door number on that building. One computer runs many services, each on its own port.
- Web traffic uses port 80 (HTTP) or 443 (HTTPS).
- Address + port finds one specific service on one specific computer.

**Show:** a building with numbered doors.

**Check:** What does the port add to the IP address? *(It picks which service on that computer.)*

---

## BEG-003-L03 · Domains and DNS (10 min)
**Goal:** explain why we type names and how they become addresses.

**Key points**
- Humans remember names (`example.com`); computers use numbers (IP addresses).
- DNS is the internet's phone book: it turns a name into an IP address.
- Your computer asks a DNS server, gets the IP, then connects to it.
- A domain is a name, not a server. One domain can point to many servers.

**Show:** a lookup: name → DNS → IP.

**Check:** Is a domain the same as a server? *(No. It is a name that points to one or more.)*

---

## BEG-003-L04 · Clients, servers, requests, and responses (12 min)
**Goal:** trace what happens from typing a URL to seeing a page.

**Key points**
- The client (your browser) asks. The server answers.
- Steps: type URL → DNS lookup → connect → send request → server sends response → browser draws the page.
- A request has a method (like GET), an address, and optional data.
- A response has a status code (200 OK, 404 not found) and content.
- One page load is usually many requests: HTML, images, scripts.

**Show:** a sequence diagram with the browser on the left, the server on the right, and arrows for each step.

**Check:** What does status 404 mean? *(The server could not find what was asked for.)*

---

## BEG-003-L05 · HTTP vs HTTPS: what encryption protects (8 min)
**Goal:** say what HTTPS adds.

**Key points**
- HTTP sends data as readable text; anyone on the path could read it.
- HTTPS encrypts it: scrambled in transit, readable only by you and the server.
- It also proves you reached the real site, not a fake.
- It does not hide which site you visit, and it does not make the site itself trustworthy.

**Show:** a letter in a postcard (HTTP) vs. a sealed envelope (HTTPS).

**Check:** Does HTTPS hide which website you visit? *(No.)*

---

## BEG-003-L06 · Watching a request in the browser's developer tools (7 min)
**Goal:** find the requests a browser makes.

**Key points**
- Press `F12` and open the Network tab.
- Reload the page; each row is one request.
- Click a row: method, status code, and type are listed.
- The first row is usually the main document.

**Show:** the Network tab on a simple site, with the main request highlighted.

**Check:** Where do you see the status code of a request? *(In the Network tab, on that request's row.)*

---

## BEG-003-L07 · Demo: following a URL with `nslookup` and the Network tab (8 min)
**Goal:** trace one real URL end to end. Prepares `BEG-003-LAB1`.

**Steps**
1. Run `nslookup example.com` in a terminal. Read the IP address in the answer.
2. Run it on two more domains; notice that some return several addresses.
3. Open the same site in the browser with the Network tab open.
4. Find the main document: method `GET`, status `200`, type `document`.
5. **Planned mistake:** try `nslookup https://example.com`; it fails because a URL is not a domain. Fix: use only the domain name.
