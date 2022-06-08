![image](https://user-images.githubusercontent.com/51442719/172730126-bc48a2be-6103-45e5-b51a-492af4579be1.png)

# TryHackMe > WriteUp > [CyberHeroes](https://tryhackme.com/room/cyberheroes)

## Want to be a part of the elite club of CyberHeroes? Prove your merit by finding a way to log in!

- `Task 1`  CyberHeroes
  - Want to be a part of the elite club of CyberHeroes? Prove your merit by finding a way to log in!
  - Answer the questions below
    - Uncover the flag!

- Answers: `Task 1` 
  - [1] Start Machine Copy Machine IP: 10.10.202.66
  - [2] Open it in your Attacking Box Browser: http://10.10.202.66/
  - [3] Go to Login page: http://10.10.202.66/login.html
  - [4] Open `View-Source`, to see source of site.
  - [5] <img width="1186" alt="image" src="https://user-images.githubusercontent.com/51442719/170817566-3acdad8d-67f5-4739-a863-bca19e759507.png">
  - [6] You see Function `authenticate`, there is 2 variables (a=name, b=pass)
    - (a.value=="h3ck3rBoi" & b.value==RevereString("54321@terceSrepuS")


