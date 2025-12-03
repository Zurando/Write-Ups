# Day 1 Write-Up — Linux CLI Basics (Shells Bells)  
**Author:** Zurando  
**Room:** https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti  
**Concept:** Linux Command-Line Fundamentals  

---

## Overview  
This write-up covers my approach to completing the *Linux CLI Basics* room on TryHackMe.  
My goal was to get hands-on with core terminal commands and reinforce the basics through practical experience.

---

# Q1 — Which CLI command lists a directory?  
**Answer:** `ls`

### The `ls` Command  
`ls` displays the contents of the current directory. It’s one of the core commands in Linux.

---

# Q2 — What flag did you find inside McSkidy’s guide?

### Steps Taken (My workflow)
1. List the current directory:
```
ls
```
3. Move into the `Guides` directory:
```
cd Guides
```

3. List contents (nothing appears — because the file is hidden).  
4. Reveal hidden files:
```
ls -la
```

5. Read the hidden file: 
```
cat .guide.txt
```

**Answer:** `THM{learning-linux-cli}`

### Hidden Files in Linux  
Files beginning with `.` are hidden. They don’t appear with a standard `ls` command.

### The `cd` Command  
Moves between directories:  
```
cd <directory>
```
### The `cat` Command  
Reads file contents: 
```
cat <filename.txt>
```

---

# Q4 — What flag was inside the Eggstrike script?

### Steps Taken
1. Find the script using:  
```
find / -name eggstrike.sh 2>/dev/null
```
2. Read the file:  
```
cat /home/socmas/2025/eggstrike.sh
```

**Answer:** `THM{sir-carrotbane-attacks}`

### The `find` Command  
Searches for files in the filesystem:  
```
find <directory> -name <filename>
```

### What is `2>/dev/null`?  
Redirects error messages away from the screen (useful when searching the entire system).

---

# Q5 — Which command switches to the root user?  
**Answer:** `sudo su`

### The `su` Command  
Switches to another user:  
```
su <username>
```

### The `sudo` Command  
Runs commands with root privileges.

---

# Q6 — What flag was left in the root bash history?

### Command used:  
```
cat /root/.bash_history
```

**Answer:** `THM{until-we-meet-again}`

### The `.bash_history` File  
Stores previous terminal commands for each user.

---

## Summary  
This TryHackMe room is a useful refresher on essential Linux CLI commands.  
I used it to reinforce my fundamentals with:

- Navigating directories (`ls`, `cd`)  
- Reading files (`cat`)  
- Searching logs (`grep`)  
- Finding files (`find`)  
- Managing privilege escalation (`sudo`, `su`)  
- Accessing hidden and system files  

A clean, practical warm-up for deeper Linux and offensive security work.
