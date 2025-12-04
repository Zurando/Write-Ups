# TryHackMe Write-Up — Phishing  
**Author:** Zurando  
**Room:** https://tryhackme.com/room/phishing-aoc2025-h2tkye9fzU  
**Concept:** Phishing & Social Engineering  

---

## Overview  
The goal of this room is to strengthen my understanding of phishing techniques, social engineering workflows, and credential harvesting in a controlled environment.  
This write-up covers my approach to the *Phishing* room on TryHackMe (AoC2025), including how I set up the phishing server, used the Social Engineering Toolkit (SET), and captured credentials through a simulated attack scenario.

---

# Method of Solve  

## Setting Up the Phishing Server  
For this challenge, I'm assuming the AttackBox environment.

1. Navigate to the challenge directory:  
```
cd /Rooms/AoC2025/Day02
```
2. Run the phishing server script:  
```
./server.py
```

This spins up a web server on the AttackBox, which we will use as our phishing landing page.  
Once a target is lured to this page, any submitted credentials will appear in the terminal.

---

## Using the Social Engineering Toolkit (SET)

Start SET:
```
setoolkit
```

Then follow this path:

1. **1** → Social-Engineering Attacks  
2. **5** → Mass Mailer Attack  
3. **1** → E-Mail Attack Single Email Address  
4. Enter: `factory@wareville.thm`  
5. Choose **2** → Use your own server or open relay  
6. Sender address: `updates@flyingdeer.thm`  
7. Sender name: `Flying Deer`  
8. Username: *(leave blank)*  
9. Password: *(leave blank)*  
10. SMTP server: `<YOUR_VICTIM_MACHINE_IP>`  
11. Port: `25`  
12. High priority email? → `no`  
13. Attach a file? → `n`  
14. Attach an inline file? → `n`  
15. Email subject: `Shipping Schedule Changes`  
16. Message type: `p` → plain text  

Email body:
```
We've had to make some changes to the shipping schedule. Click the link to see the changes. 
http://10.48.182.11:8000

Regards,
Flying Deer
END
```
Make sure `END` is on a separate line.

---

# Q1 — What is the password used to access the TBFC portal?

After sending the phishing email, captured credentials will appear in the terminal running `server.py`.  
Example output:
```
Captured -> username: admin    password: unranked-wisdom-anthem    from: 10.48.182.11
```
(IP will vary.)

---

# Q2 — What is the total number of toys expected for delivery?

1. Navigate to the TBFC portal using the IP shown in the capture:  
```
http://10.48.182.11
```
2. Log in as the **factory** user:
```
username: factory
password: unranked-wisdom-anthem
```
3. Open the email titled:  
**Urgent: Production & Shipping Request - 1984000 Units (Next 2 Weeks)**  

---

## Status  
This write-up is still in progress.  
Once the room is fully completed, I’ll update the solutions, methodology, and final conclusions.

