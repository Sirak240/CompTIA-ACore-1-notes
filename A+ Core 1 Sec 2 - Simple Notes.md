# A+ Core 1 – Section 2: Networking (Complete Beginner Notes)

Think of the internet like a **town with a post office**. Computers are houses, data is mail, and everything below is how the mail gets delivered.

**What's in here**
1. IP, TCP and UDP
2. Ports and protocols (all 15 exam ports)
3. Wireless (Wi-Fi standards, frequencies, Bluetooth, NFC, RFID)
4. Network services (what servers do on a network)
5. DNS records, DHCP details, VLANs and VPNs
6. Network hardware
7. IP addressing (IPv4, IPv6, private ranges, subnet masks)
8. Setting up a small office / home network (SOHO)
9. Internet connection types and network types
10. Networking tools
11. Final exam cheat sheet

> Cables and connectors (Cat 5e/6, RJ45, fiber, T568A/B) are in **Section 3 (Hardware)**, not here.

---

# 1. IP, TCP and UDP

## IP – Internet Protocol 🏠
**IP = the house address.** Every device on a network has an IP address.

Data travels packed like a letter in an envelope:
- **Payload** = the letter (the actual information)
- **Header** = front of the envelope (addresses, where it's going)
- **Trailer** = back flap (checks nothing got damaged)

## TCP and UDP – two ways to deliver
IP gets data to the right **computer**. TCP or UDP decides **how carefully** it's delivered.
Both go to the right IP address **and** the right port. The only difference is whether they **check that the data arrived**.

### TCP – Transmission Control Protocol 📦 (phone call)
- **Connection-oriented:** starts with a **three-way handshake**: **SYN** ("Hi!") → **SYN-ACK** ("Hi, ready!") → **ACK** ("Let's go!")
- **Reliable:** every piece is numbered and acknowledged. Lost pieces get **sent again**.
- **Flow control:** the receiver can say "slow down" or "speed up."
- **Formal goodbye** when finished.
- **Used for:** websites, email, file downloads, remote control (SSH, RDP).

### UDP – User Datagram Protocol 🗞️ (paperboy)
- **Connectionless:** no hello, no goodbye
- **Unreliable:** no checking. Lost pieces are gone.
- **Fast**
- **Used for:** video calls, games, live streams, DNS, DHCP, SNMP, syslog.

> **Choose:** "If a piece goes missing, would it break the whole thing?"
> **Yes** → TCP. **No, it just needs to be fast and live** → UDP.

## Multiplexing 🎧📺📧
Many conversations over **one connection** at the same time. **Port numbers** keep each app's data sorted. Both TCP and UDP do this.

---

# 2. Ports and Protocols 🚪
**IP address = the building. Port number = the apartment door.**
Firewalls use port numbers to decide what to allow or block.

| Port | Protocol | What it does | Simple picture |
|---|---|---|---|
| TCP 20/21 | **FTP** | Transfers files (not encrypted) | 🚚 Moving truck |
| TCP 22 | **SSH** | Secure remote command line | 🔒 Private headset |
| TCP 23 | **Telnet** | Remote command line, plain text (insecure) | 📢 Shouting |
| TCP 25 | **SMTP** | **Sends** email | 📮 Outgoing mailbox |
| UDP/TCP 53 | **DNS** | Names → IP addresses | 📖 Phone book |
| UDP 67/68 | **DHCP** | Hands out IP addresses | 🎟️ Ticket booth |
| TCP 80 | **HTTP** | Websites, not encrypted | 🌐 Postcard |
| TCP 110 | **POP3** | **Receives** email to one device | 📥 Take mail home |
| UDP 137, TCP 139 | **NetBIOS** | Old Windows name lookup & sharing | 🏘️ Old neighborhood |
| TCP 143 | **IMAP** | **Receives** email, synced everywhere | 💌 Mail stays at library |
| UDP 161/162 | **SNMP** | Monitors network devices | 🩺 Device check-up |
| TCP 389 | **LDAP** | Looks up users/computers in a directory (Active Directory) | 📇 Company directory |
| TCP 443 | **HTTPS** | Websites, encrypted | 🔐 Locked envelope |
| TCP 445 | **SMB / CIFS** | Windows file and printer sharing | 🗂️ Shared folder |
| TCP 3389 | **RDP** | Remote Desktop – control a whole Windows screen | 🖥️ Remote screen |

### Memory tricks
- **22 SSH** → "shhh!" 🤫 quiet and secure. **23 Telnet** → its loud brother.
- **25 SMTP** → **S**MTP = **S**end
- **53 DNS** → dial 5-3 in the phone book
- **67/68 DHCP** → server 67 hands out, client 68 takes
- **143 IMAP** → "I love you" (1-4-3), keeps mail on every device
- **161/162 SNMP** → 161 asks devices questions, 162 is where alerts (**traps**) come back
- **443 HTTPS** → **S** = **S**ecure. **445 SMB** → next door, shares files
- **3389 RDP** → big number, big picture (a whole desktop)

### Compare-the-pair (exam favorites)
| Need | Secure / modern ✅ | Insecure / old ❌ |
|---|---|---|
| Remote command line | SSH 22 | Telnet 23 |
| Websites | HTTPS 443 | HTTP 80 |
| Windows file sharing | SMB 445 | NetBIOS 137–139 |
| Remote control | SSH 22 = text only | RDP 3389 = full desktop |

### Email
- **SMTP 25** → sends
- **POP3 110** → downloads to **one** device, usually deletes from server
- **IMAP 143** → stays on server, **syncs** on all devices

---

# 3. Wireless 📶

## 802.11 = Wi-Fi
Like walkie-talkies for the whole building. Every new version has a letter (and newer ones have a number).

| Standard | Wi-Fi name | Frequency | Max speed | Remember |
|---|---|---|---|---|
| **802.11a** | — | 5 GHz | 54 Mbps | Old, 5 GHz only |
| **802.11b** | — | 2.4 GHz | 11 Mbps | Slowest |
| **802.11g** | — | 2.4 GHz | 54 Mbps | "g" fixed b's speed |
| **802.11n** | Wi-Fi 4 | 2.4 **and** 5 GHz | 600 Mbps | First with **MIMO** (multiple antennas) |
| **802.11ac** | Wi-Fi 5 | 5 GHz | ~6.9 Gbps | **MU-MIMO** (talks to several devices at once) |
| **802.11ax** | Wi-Fi 6 / **6E** | 2.4 & 5 GHz (**6E adds 6 GHz**) | ~9.6 Gbps | **OFDMA**, great in crowded places |

> Newest: **802.11be (Wi-Fi 7)**. Know that it exists and is the fastest.

## Frequencies
| | 2.4 GHz | 5 GHz | 6 GHz |
|---|---|---|---|
| Range | **Longest** – goes through walls best | Medium | Shortest |
| Speed | Slowest | Faster | Fastest |
| Interference | **Most** (microwaves, Bluetooth, neighbors) | Less | Least |
| Non-overlapping channels | **1, 6, 11** | Many | Many |

- **Channel** = a lane on the highway. Neighbors on the same lane slow each other down. On 2.4 GHz use **1, 6, or 11**.
- **Channel width** (20/40/80/160 MHz) = how wide the lane is. Wider = faster but more interference.
- **Regulations:** each country decides which channels and power levels are allowed.

## Other wireless
- **Bluetooth** 🎧 – short range (~10 m), 2.4 GHz. Earbuds, mouse, speakers. Makes a **PAN**.
- **NFC (Near Field Communication)** 📱 – a few **centimeters**. Tap to pay, tap to pair.
- **RFID (Radio Frequency Identification)** 🏷️ – tags read by radio. Building badges, store anti-theft tags, inventory tracking, toll passes.
- **ISM band** – radio frequencies anyone can use **without a license** (2.4 GHz and 5 GHz).

---

# 4. Network Services (what servers do) 🖥️

| Service | Job | Simple picture |
|---|---|---|
| **DNS server** | Names → IP addresses | 📖 Phone book |
| **DHCP server** | Hands out IP addresses and settings | 🎟️ Ticket booth |
| **File server / file share** | Central place to store and share files | 🗄️ Shared filing cabinet |
| **Print server** | Manages printers and print jobs for everyone | 🖨️ Print line manager |
| **Mail server** | Stores, sends and receives email | 🏤 Post office |
| **Web server** | Hosts websites | 🏬 Storefront |
| **Syslog server** | Collects **logs** from every device in one place (UDP 514) | 📓 Security guard's logbook |
| **AAA server** | **A**uthentication (who are you?), **A**uthorization (what can you do?), **A**ccounting (what did you do?). Uses RADIUS or TACACS+ | 🛂 Passport control |
| **Spam gateway** | Filters junk and dangerous email before it reaches inboxes | 🗑️ Mail sorter |
| **UTM (Unified Threat Management)** | All-in-one security box: firewall, intrusion prevention, anti-malware, URL/content filter, VPN | 🛡️ Swiss Army knife |
| **Load balancer** | Spreads traffic across several servers so none gets overloaded | 🚦 Traffic cop |
| **Proxy server** | Makes requests **for** you; can filter, cache and hide users | 🧍 Middleman |

### Special systems
- **Legacy / embedded systems** – old or built-in computers still running important things (factory machines, medical devices). Often can't be updated.
- **SCADA (Supervisory Control and Data Acquisition)** – controls industrial equipment: power plants, water treatment, pipelines. Kept on separate, protected networks.
- **IoT (Internet of Things)** – smart devices: thermostats, cameras, doorbells, smart speakers. Often weak security, so put them on their own network.

---

# 5. Network Configuration Concepts

## DNS records 📖
DNS servers keep **records**, like entries in the phone book.

| Record | What it does | Memory trick |
|---|---|---|
| **A** | Name → **IPv4** address | **A** = **A**ddress |
| **AAAA** | Name → **IPv6** address | 4 A's, because IPv6 is 4× longer |
| **CNAME** | Nickname (alias) for another name | **C**anonical **NAME** – "also known as" |
| **MX** | Which server receives email for the domain | **M**ail e**X**changer |
| **TXT** | Text notes, mainly used for email security | Sticky note |

**Email security (all stored in TXT records)** – stops people faking your email address:
- **SPF** – list of servers **allowed** to send email for your domain. ("Only these mail carriers work for us.")
- **DKIM** – a **digital signature** on each email proving it wasn't changed. ("Wax seal on the letter.")
- **DMARC** – tells others **what to do** if SPF/DKIM fail (do nothing, quarantine, reject) and sends reports. ("The rulebook.")

**Troubleshooting:** a website works by IP but **not by name** → DNS problem.

## DHCP details 🎟️
- **DORA:** **D**iscover → **O**ffer → **R**equest → **A**cknowledge
- **Lease** – the address is **borrowed** for a set time, then renewed or returned.
- **Scope** – the **range** of addresses DHCP can hand out (e.g., 192.168.1.100–192.168.1.200), plus settings like subnet mask, gateway and DNS server.
- **Exclusion** – addresses inside the scope that DHCP should **never** hand out (saved for things with static IPs).
- **Reservation** – a device **always** gets the **same** address, matched to its MAC address. Great for printers and servers.
- **APIPA** – no DHCP answer → device gives itself **169.254.x.x**. Means "couldn't reach DHCP."

## VLAN – Virtual LAN 🧱
Splits **one physical switch** into **separate networks**, like putting walls inside one big room.
- Example: HR, Sales and guest Wi-Fi all plug into the same switch but can't see each other's traffic.
- Why: **security** and **organization**.

## VPN – Virtual Private Network 🚇
An **encrypted tunnel** across the internet.
- Example: you work from home and connect securely to your company's network as if you were in the office.
- The device at the office end that handles many VPN users is a **VPN concentrator** (often built into a firewall).

---

# 6. Network Hardware 🔌

| Device | Job | Simple picture |
|---|---|---|
| **Router** | Connects **different** networks (your home ↔ the internet). Uses **IP addresses** | 🛣️ Highway interchange |
| **Switch** | Connects devices on the **same** network. Sends data only to the right port using **MAC addresses** | 📬 Smart mail sorter |
| **Unmanaged switch** | Plug and play, no settings | Basic power strip |
| **Managed switch** | Configurable: VLANs, monitoring, port settings | Smart power strip with an app |
| **Hub** (old) | Sends everything to **everyone** | 📢 Megaphone – replaced by switches |
| **Access point (AP)** | Connects wireless devices to the wired network | 📶 Wi-Fi bridge |
| **Firewall** | Allows or blocks traffic based on rules (IP, port) | 🚧 Security guard at the gate |
| **Patch panel** | A neat panel where all the building's cables end, so you can patch them to the switch | 🔢 Organized cable board |
| **NIC (Network Interface Card)** | The network port inside a computer. Has the **MAC address** | 🪪 Device's ID badge |
| **Cable modem** | Internet over **coax** cable (uses **DOCSIS**) | 📺 TV-cable internet |
| **DSL modem** | Internet over **phone lines** | ☎️ Phone-line internet |
| **ONT (Optical Network Terminal)** | Converts **fiber** light signals into Ethernet at your home | 💡 Fiber box |
| **SDN (Software-Defined Networking)** | Control the network with software instead of configuring each box by hand – common in the cloud | 🎮 Central remote control |

## PoE – Power over Ethernet ⚡
Sends **power and data on the same network cable**. No outlet needed.
- Used for: security cameras, VoIP phones, wireless access points
- **PoE switch** = power built into the switch. **PoE injector** = adds power to one cable.

| Standard | Name | Power |
|---|---|---|
| 802.3af | PoE | 15.4 W |
| 802.3at | PoE+ | 30 W |
| 802.3bt | PoE++ | 60 W (Type 3) / 100 W (Type 4) |

> **Router vs switch:** router = **between** networks (IP). Switch = **inside** one network (MAC).

---

# 7. IP Addressing 🔢

## IPv4
- **32 bits**, written as **four numbers 0–255** separated by dots: `192.168.1.25`
- Each of the four numbers is an **octet**.
- We're running out of IPv4 addresses, which is why NAT and IPv6 exist.

## IPv6
- **128 bits**, written in **hexadecimal** (0–9, a–f), 8 groups separated by colons:
  `2001:0db8:0000:0000:0000:ff00:0042:8329`
- **Shortening rules:** drop leading zeros in a group, and replace **one** run of all-zero groups with `::`
  → `2001:db8::ff00:42:8329`
- Enough addresses for every device on Earth many times over.

## Public vs private addresses
- **Public** – used on the internet, unique in the whole world. Your ISP gives you one.
- **Private** – used **inside** homes and offices. Can't be used on the internet directly.

**Private IPv4 ranges (memorize these!)**
| Range | Simple version |
|---|---|
| **10.0.0.0 – 10.255.255.255** | Anything starting with **10** |
| **172.16.0.0 – 172.31.255.255** | **172.16** through **172.31** |
| **192.168.0.0 – 192.168.255.255** | Anything starting with **192.168** (most home networks) |

- **NAT (Network Address Translation)** – your router swaps your private address for its public one when you go online. One public address can serve your whole house.

## Special addresses
| Address | Meaning |
|---|---|
| **127.0.0.1** | **Loopback** – "myself." Used to test your own network card. IPv6 loopback: **::1** |
| **169.254.x.x** | **APIPA** – DHCP failed |
| **fe80::** | IPv6 **link-local** – like APIPA for IPv6; works only on the local network |

## The settings every device needs
1. **IP address** – the device's own address
2. **Subnet mask** – which part of the address is the **network** and which part is the **device**. Most common: **255.255.255.0** (also written **/24**) → the first three numbers are the neighborhood, the last number is the house.
3. **Default gateway** – the **router's** address. The door out of your network. Wrong gateway = local stuff works, internet doesn't.
4. **DNS server** – where to look up names.

## Static vs dynamic
- **Dynamic** – DHCP gives it automatically. Used for laptops and phones.
- **Static** – typed in by hand and never changes. Used for servers, printers and routers so people can always find them.

---

# 8. SOHO Networks (Small Office / Home Office) 🏡

Setting up a router for a home or small office:
1. **Change the default admin username and password** – the #1 thing to do
2. **Update the firmware**
3. **Set the SSID** (Wi-Fi network name). You *can* hide it, but that's not real security.
4. **Use strong encryption: WPA3** (or WPA2 if devices are older). Never WEP or open.
5. **Set up DHCP** – choose the scope; reserve or make static IPs for printers.
6. **Use a guest network** for visitors and IoT devices.
7. **Turn off WPS** (the push-button connect feature) – it's easy to break into.
8. **Disable UPnP** unless needed – it lets devices open ports by themselves.
9. **Port forwarding** – sends traffic coming in on a certain port to one inside device (e.g., a game server).
10. **DMZ** – puts one device fully outside the firewall's protection. Risky; avoid unless needed.
11. **Content filtering / parental controls** – block certain websites.

---

# 9. Internet Connection Types & Network Types

## Internet connection types 🌍
| Type | How it works | Good to know |
|---|---|---|
| **Fiber** | Light through glass cables | **Fastest**, very reliable, needs an **ONT** |
| **Cable** | TV coax cable | Fast; bandwidth is **shared** with neighbors (slows at busy times); uses **DOCSIS** |
| **DSL** | Telephone lines | Slower; speed drops the farther you are from the phone company (**ADSL** = faster download than upload) |
| **Satellite** | Dish talks to a satellite | Works anywhere rural. Old satellites = **high latency** (lag). Low-earth-orbit (like Starlink) = much lower lag. **Rain fade** – bad weather hurts signal |
| **Cellular** | 4G / 5G mobile network | Hotspots and tethering; data caps |
| **WISP (Wireless ISP)** | Antennas on towers beam internet to your building | Rural areas; usually needs **line of sight** |

**Latency** = delay (lag). **Bandwidth** = how much data at once (speed).

## Network types (smallest → biggest)
| Type | Name | Size | Example |
|---|---|---|---|
| **PAN** | Personal Area Network | Just you | Phone + Bluetooth earbuds |
| **LAN** | Local Area Network | One building | Your home or office network |
| **WLAN** | Wireless LAN | One building, no cables | Your home Wi-Fi |
| **MAN** | Metropolitan Area Network | A city | A city connecting its libraries |
| **WAN** | Wide Area Network | Across the world | The internet; a company linking offices in different states |
| **SAN** | Storage Area Network | Special purpose | A fast network just for storage drives – servers see it like a local drive |

---

# 10. Networking Tools 🧰

| Tool | What it does | When you'd use it |
|---|---|---|
| **Cable stripper** | Removes the outer plastic jacket from a cable | First step before crimping |
| **Crimper** | Squeezes an **RJ45** connector onto the end of a network cable | Making your own Ethernet cable |
| **Punchdown tool** | Pushes wires into a **patch panel** or wall jack (110 block) | Wiring a building |
| **Cable tester** | Checks that all wires in a cable are connected in the right order | "Did I make this cable right?" |
| **Toner probe** (tone generator + probe) | One end makes a sound on the wire; the probe beeps when it finds it | Finding which cable in a big bundle goes to which office |
| **Loopback plug** | Sends a port's signal right back into itself | Testing if a network port or NIC works |
| **Multimeter** | Measures voltage, resistance and continuity | Checking power and basic wiring |
| **Wi-Fi analyzer** | Shows nearby Wi-Fi networks, signal strength and channels | Finding interference; choosing the best channel |
| **Network tap** | Copies all traffic passing through a cable so you can watch it | Monitoring and security analysis |

> **Toner vs tester:** toner = **find** the cable. Tester = **check** the cable.

---

# 11. Final Exam Cheat Sheet ✅

**TCP/UDP**
- Guaranteed delivery / acknowledgments / handshake → **TCP**
- Connectionless / real-time / fast → **UDP**

**Ports**
- Secure remote command line → **SSH 22** (block **Telnet 23**)
- Full remote Windows desktop → **RDP 3389**
- Send email → **SMTP 25** · Email synced everywhere → **IMAP 143** · One device → **POP3 110**
- Windows file sharing → **SMB 445**
- Directory / Active Directory lookups → **LDAP 389**
- Monitor network devices → **SNMP 161/162**
- Lock icon → **HTTPS 443**

**Troubleshooting clues**
- Works by IP but not by name → **DNS**
- **169.254.x.x** → DHCP failed (APIPA)
- Local network works, internet doesn't → check **default gateway**
- Printer IP keeps changing → **DHCP reservation** or static IP
- Slow Wi-Fi in an apartment building → **change channel** (1, 6, 11 on 2.4 GHz) or use 5 GHz

**Wireless**
- Longest range / most interference → **2.4 GHz**
- Wi-Fi 6E → adds **6 GHz**
- Tap to pay → **NFC** · Badge / inventory tag → **RFID**

**Addresses**
- Private ranges → **10.x**, **172.16–31.x**, **192.168.x**
- Loopback → **127.0.0.1** / **::1**
- IPv4 = 32-bit · IPv6 = 128-bit hex

**Hardware**
- Between networks → **router** · Inside one network → **switch**
- Power + data on one cable → **PoE**
- Fiber at home → **ONT** · Coax internet → **cable modem (DOCSIS)**

**DNS records**
- IPv4 → **A** · IPv6 → **AAAA** · Email server → **MX** · Alias → **CNAME**
- Anti-spoofing email → **SPF, DKIM, DMARC** (TXT records)

**Network config**
- Separate networks on one switch → **VLAN**
- Encrypted tunnel from home to office → **VPN**

**Tools**
- Find a cable → **toner probe** · Check a cable → **cable tester**
- Attach RJ45 → **crimper** · Patch panel → **punchdown tool**
- Test a port → **loopback plug** · Wi-Fi channels → **Wi-Fi analyzer**
