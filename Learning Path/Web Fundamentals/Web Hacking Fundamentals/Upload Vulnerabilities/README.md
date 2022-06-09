![image](https://user-images.githubusercontent.com/51442719/172671036-28090dd7-b737-427e-a2de-3687d0cbd503.png)
- [ ] [Upload Vulnerabilities](https://tryhackme.com/room/uploadvulns)
  - Tutorial room exploring some basic file-upload vulnerabilities in websites
      - [x] Task 1  Getting Started
      - [x] Task 2  Introduction
      - [x] Task 3  General Methodology
      - [x] Task 4  Overwriting Existing Files
        - Overwrite the image. What is the flag you receive?
          > `THM{OTBiODQ3YmNjYWZhM2UyMmYzZDNiZjI5}`
      - [x] Task 5  Remote Code Execution
        - Run a Gobuster scan on the website using the syntax from the screenshot above. What directory looks like it might be used for uploads?
          > `/resources`
      - [x] Task 6  Filtering
        - What is the traditionally predominant server-side scripting language?
          > `PHP`
        - When validating by file extension, what would you call a list of accepted extensions (whereby the server rejects any extension not in the list)?
          > `Whitelist`
        - [Research] What MIME type would you expect to see when uploading a CSV file?
          > `text/csv`
      - [ ] Task 7  Bypassing Client-Side Filtering
      - [ ] Task 8  Bypassing Server-Side Filtering: File Extensions
      - [ ] Task 9  Bypassing Server-Side Filtering: Magic Numbers
      - [ ] Task 10  Example Methodology
      - [ ] Task 11  Challenge
      - [ ] Task 12  Conclusion
