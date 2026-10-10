# A+ Core 1 – Section 2: Networking (Beginner Version)

Think of the internet like a **town with a post office**. Computers are houses, data is mail, and the rules below are how the mail gets delivered.

---

## IP – Internet Protocol
**IP = the house address.**

- Every device on a network has an **IP address**, just like every house has a street address.
- When your laptop sends data to a server over Ethernet, the data is packed like a letter in an envelope:
  - **Payload** = the letter (the actual information)
  - **Header** = the front of the envelope (addresses, where it's going)
  - **Trailer** = the back flap (checks that nothing got damaged)

---

## TCP and UDP – Two Ways to Deliver
IP gets data to the right **computer**. TCP or UDP decides **how carefully** it's delivered.

**Both TCP and UDP:**
- Go to the right IP address (the building)
- Go to the right port number (the apartment door)

The only difference is whether they **check that the data arrived**.

### TCP – Transmission Control Protocol 📦
**Like a phone call.** You say hello, talk, and say goodbye.

- **Connection-oriented:** starts with a **three-way handshake** ("Hi!" / "Hi, ready!" / "Let's go!")
- **Reliable:** every piece is numbered and checked. Lost pieces get **sent again**.
- **Flow control:** the receiver can say "slow down" or "speed up."
- **Formal goodbye:** the connection is properly ended when finished.
- **Used for:** websites, email, file downloads, anything where every piece must arrive.

### UDP – User Datagram Protocol 🗞️
**Like a paperboy throwing newspapers.** He throws and keeps riding.

- **Connectionless:** no hello, no goodbye
- **Unreliable:** no checking. If a piece is lost, it's gone.
- **Fast:** skips all the back-and-forth
- **Used for:** video calls, online games, live streams, DNS, DHCP

### Easy way to choose
> "If a piece goes missing, would it break the whole thing?"
> - **Yes** (file, email, webpage) → **TCP**
> - **No, it just needs to be fast and live** (call, game, stream) → **UDP**

---

## Multiplexing 🎧📺📧
**Lots of conversations over one connection at the same time.**

- You can watch YouTube, download a file, and send an email all at once.
- **Port numbers** keep everything sorted so each app gets the right data.
- Both TCP and UDP do this.

---

## Port Numbers 🚪
**IP address = the building. Port number = the apartment door.**

- Every service has its own port number.
- **Firewalls** use port numbers to decide what traffic to allow or block.

| Port | Protocol | What it does | Simple picture |
|---|---|---|---|
| TCP 20/21 | **FTP** | Transfers files | 🚚 Moving truck |
| TCP 22 | **SSH** | Secure remote control | 🔒 Private coach's headset |
| TCP 23 | **Telnet** | Unsecure remote control | 📢 Shouting – don't use! |
| TCP 25 | **SMTP** | **Sends** email | 📮 Outgoing mailbox |
| UDP/TCP 53 | **DNS** | Turns names into IP addresses | 📖 Phone book |
| UDP 67/68 | **DHCP** | Hands out IP addresses | 🎟️ Ticket booth |
| TCP 80 | **HTTP** | Websites (not encrypted) | 🌐 Postcard anyone can read |
| TCP 110 | **POP3** | **Receives** email to one device | 📥 Take mail home |
| TCP 143 | **IMAP** | **Receives** email, synced everywhere | 💌 Mail stays at the library |
| TCP 443 | **HTTPS** | Websites (encrypted) | 🔐 Locked envelope |

### Memory tricks
- **22 SSH** → "shhh!" 🤫 the quiet, secure one
- **23 Telnet** → SSH's loud brother, one number up
- **25 SMTP** → **S**MTP = **S**end
- **443 HTTPS** → the **S** means **S**ecure
- **143 IMAP** → "I love you" (1-4-3), keeps your mail on every device

---

## SSH vs Telnet
Both let you **control another computer from far away** using a command line.

- **SSH (port 22):** everything is **encrypted**. Nobody can see your password.
- **Telnet (port 23):** everything is sent in **plain text**. Anyone snooping can see your password.
- **Exam tip:** if a question asks for the *secure* way to remotely manage a device, the answer is **SSH**.

**Everyday example:** An IT admin restarts a broken company server from home using SSH.

---

## Email: Sending vs Receiving
- **SMTP (25)** → **sends** email
- **POP3 (110)** → **downloads** email to **one** device and usually deletes it from the server
- **IMAP (143)** → keeps email **on the server** and **syncs** it on all devices (phone, laptop, web)

**Example:** You read an email on your phone and it shows as read on your laptop too. That's IMAP.

---

## HTTP vs HTTPS
- **HTTP (80):** not encrypted. Your browser may show **"Not Secure."**
- **HTTPS (443):** encrypted. Look for the **🔒 lock icon**.

---

## DNS – Domain Name System 📖
**The internet's phone book.**

- Turns names into IP addresses: `www.professormesser.com` → `162.159.246.164`
- Can also work in reverse (IP address → name)
- **Troubleshooting clue:** a website works by IP address but **not by name** → **DNS problem**

---

## DHCP – Dynamic Host Configuration Protocol 🎟️
**The ticket booth that hands out IP addresses automatically.**

- You never have to type in an IP address yourself.
- Example: you join coffee shop Wi-Fi and you're online in seconds. Thank DHCP.
- Networks can have more than one DHCP server, so if one fails, another can take over.

### DORA – how you get an address
1. **D**iscover – "Is anyone handing out addresses?" 🙋
2. **O**ffer – "I am! You can have this one." 🎁
3. **R**equest – "Yes please, I'll take it!" 🙏
4. **A**cknowledge – "It's yours!" 👍

The address is **leased** (borrowed for a set time), not owned forever.

### APIPA – when DHCP fails ⚠️
- If no DHCP server answers, the device gives itself an address starting with **169.254.x.x**.
- **Exam tip:** a **169.254** address means the device **couldn't reach a DHCP server**.

---

## Wireless: Wi-Fi vs Bluetooth
- **802.11 = Wi-Fi.** Like walkie-talkies for the whole building. You can walk around and stay connected. Uses **2.4 GHz, 5 GHz, and 6 GHz**.
- **Bluetooth = short range.** Like a tin-can phone. Only works when devices are close (earbuds, speakers, mouse). Uses **2.4 GHz**.
- **ISM band** (Industrial, Scientific, Medical): radio frequencies anyone can use **without a special license**. Both Wi-Fi and Bluetooth use the 2.4 GHz ISM band.

---

## Network Types (smallest → biggest)
| Type | Name | Size | Example |
|---|---|---|---|
| **PAN** | Personal Area Network | Just you | Phone + Bluetooth earbuds |
| **LAN** | Local Area Network | One building | Your home or office network |
| **WLAN** | Wireless LAN | One building, no cables | Your home Wi-Fi |
| **MAN** | Metropolitan Area Network | A city | A city connecting its libraries |
| **WAN** | Wide Area Network | Across the world | The internet, a company linking offices in different states |
| **SAN** | Storage Area Network | Special purpose | A fast network just for storage drives |

---

## Quick Exam Cheat Sheet ✅
- **Guaranteed delivery / acknowledgments** → TCP
- **Connectionless / real-time / fast** → UDP
- **Secure remote command line** → SSH 22
- **Send email** → SMTP 25
- **Email synced on all devices** → IMAP 143
- **Name works by IP but not by name** → DNS 53
- **169.254.x.x address** → DHCP failed (APIPA)
- **Lock icon in browser** → HTTPS 443
- **Wi-Fi standard** → 802.11
- **Earbuds connected to phone** → PAN / Bluetooth
