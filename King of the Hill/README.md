<div align="center">

![image](https://user-images.githubusercontent.com/51442719/172729066-1293d382-4a31-4f03-8c23-ab0ea5f611a0.png)

# [King of the Hill](https://tryhackme.com/games/koth) `Beta`

</div>

# What is "King of the Hill"[?](https://docs.tryhackme.com/docs/koth/king-of-the-hill)
## [`KoTH`](https://github.com/Anlominus/TryHackMe/tree/main/King%20of%20the%20Hill/KoTH) ~ King of the Hill 
- King of the Hill (KoTH) is a competitive hacking game, where you play against up to 5 other hackers to compromise a machine and then patch its vulnerabilities to stop other players from also gaining access. 
- The longer you maintain your access, the more points you get.
- Traditionally you are taught how to compromise a machine to claim ownership of it. 
- TryHackMe provides plenty of content on how to do so. 
- However, an often overlooked aspect of hacking is maintaining access.
- KoTH not only inspires you to apply the knowledge gained from the content within the platform in a competitive, timed set way, but also encourages the use of blue-team tactics to prevent others from using similar methods, such as those that you employed to compromise the machine.

---

# Becoming King
- After enumeration and such forth, you will need to add your TryHackMe Username to `/root/king.txt` or king file in ADMINISTRATOR user's directory(Windows machine) on the machine itself to become the latest "King".
- It is then down to you to prevent your competitors from replacing your TryHackMe Username and becoming the new "King", however, you must follow the rules.

---

## Be the first to hack into a machine, and then retain your presence by patching vulnerabilities to stop your foes from taking your position!
### `Attack` then `defend`!

# About
#### King of the Hill (KoTH) is a competitive hacking game, where you play against 10 other hackers to compromise a machine and then patch its vulnerabilities to stop other players from also gaining access. 
#### The longer you maintain your access, the more points you get.

---

# How to play
- When everyone "readies" within the lobby, you will be provided the IP Address of the machine you all have to compete amongst each other to attack. 
- From now on, you will compete to become the first King of the Hill.
- After the lobby has started - the time of which you have specified, the game will last for 60 minutes or 1 Hour. 
- The member with the most points at the end of the game - regardless of the amount of "King Changes" and the like wins!
####
- Join a lobby with up to 10 players
- When everyone is ready, you'll get a machines IP address
- Enumerate and hack into the machine
- Add your TryHackMe username to /root/king.txt
- Patch the machines vulnerabilities to maintain your access
- The longer you're king, the more points you get
- Hunt for flags around the system for extra points
- After 60 minutes, the game ends

---

# How Points are Scored
- There are two main methods of obtaining points. 
- However, it should be noted that any points gained throughout the game are not persistent and will not be reflected on your TryHackMe profile - nor the next lobby you join. 
- These two methods are the following:
  - "`Be King`" 
    - The longer you have your TryHackMe Username in the /root/king.txt file, the more points you get. 
    - You obtain 10 points every full-minute you are the current "King" I.e. 
    - to obtain 10 points, you must be the current "King" for 60 seconds (1 full-minute). 
    - If you are only the king for 50 seconds, you will not be awarded the 10 points, nor will the person who was "King" for the remaining 10 seconds of that minute.
  - "`Submit Flags`" 
    - There are multiple entry points to the machine, some will have flags hidden throughout. 
    - The difficulty of how the value of the flag is obtained will stipulate the points you obtain for it. I.e. 
    - A harder to reach flag will grant more points then a flag that is easier to obtain.

---

## My Tool >>--> ``

---

## ALL Tools
- [CyberChef](https://gchq.github.io/CyberChef)
- [koth-protect-king](https://github.com/MatheuZSecurity/koth-protect-king)
- [Koth-TryHackMe-Tricks](https://github.com/MatheuZSecurity/Koth-TryHackMe-Tricks)
- [thm-vm](https://github.com/f11snipe/thm-vm): TryHackMe - Simple helper script for VPN, VM's, etc
- [Hide a Process in Koth Tryhackme](https://github.com/MatheuZSecurity/hide-a-process)
- [Python tools for penetration testers](https://github.com/Anlominus/PenTest/blob/main/KingMenu.md#python-tools-for-penetration-testers)
- [Pentesting Cheatsheet](PenTest.md): 
* [RustScan](https://github.com/rustscan/rustscan) - Lightweight and quick open-source port scanner designed to automatically pipe open ports into Nmap.

---

# Awesome 
- [Awesome Privilege Escalation](https://github.com/m0nad/awesome-privilege-escalation)
- [Awesome Incident Response](https://github.com/meirwah/awesome-incident-response)
- [Certified ethical hacker in bullet points](https://github.com/Anlominus/HacKingPro/tree/main/CEH%20-%20Certified%20Ethical%20Hacker#certified-ethical-hacker-in-bullet-points)
