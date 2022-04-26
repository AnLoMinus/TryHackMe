
<img width="40" height="40" src="https://user-images.githubusercontent.com/51442719/165321194-11522102-f0ad-4867-8523-960262d6fa42.png"> <a href="https://tryhackme.com/module/introduction-to-offensive-security"> Introduction to Offensive Security</a> 



<details>

<summary>
  <a href="https://tryhackme.com/room/introtooffensivesecurity"> Intro to Offensive Security</a>
</summary>  

![image](https://user-images.githubusercontent.com/51442719/165321005-15b3e841-6b07-4163-b9fb-9f9cf829d5c2.png)

  <br><li> <H3>Hack your first website (legally in a safe environment) and experience an ethical hacker's job. </H3></li>
  
  <div id="taskContent">

  <br>
</div>
<details>
  <summary>
    Task 1  Hacking your first machine
  </summary>
  <div class="card" id="task-1">
    <div class="card-header task-header collapsed"  href="#collapse1" aria-expanded="false">
      <a class="card-link">
      <span class="task-dropdown-title red">Task 1 <span ><i class="far fa-circle text-lgray"></i></span></span> Hacking your first machine
      </a>
    </div>
    <div id="collapse1" class="collapse"  style="">
      <div >
        <div >
          <div >
            <p><span>Before going into cyber security careers and what offensive security is, let's get you hacking (and yes, its&nbsp;</span><span style="font-size:1rem">legal,&nbsp;</span><span style="font-size:1rem">all exercises are fake simulations)</span></p>
            <p><span style="font-size:24px">Your first hack</span></p>
            <p>Click the "Start Machine" button. Once loaded, you will have access to a machine you'll use to hack a fake bank application called FakeBank.<br></p>
            <p><span>We will use a <a class="TeyNIYsb glossary-term" onclick="initPopOver('command-line application', 'TeyNIYsb')">command-line application</a> called "GoBuster" to brute-force FakeBank's website to find hidden directories and pages. GoBuster will take a list of potential page or directory names and tries accessing a website with each of them; if the page exists, it tells you.</span><span style="font-size:1rem"><br></span></p>
            <p><span style="font-size:20px">Step 1) Open a terminal</span></p>
            <p><span style="font-size:1rem">A terminal, also known as the command-line, allows us to interact with a computer without using a graphical user interface.</span>On the machine, open the terminal using the Terminal icon:&nbsp;<img style="font-size:1rem;width:0px;height:0px"><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5bec5dfd73790a7d06282266/room-content/443d573c553e59e4897aa99d2e77b679.png" style="font-size:1rem;width:23.2422px;height:23.2422px"><span style="font-size:1rem">&nbsp;</span></p>
            </span>
            </span>
            <p><span style="font-size:20px">Step 2) Find hidden website pages</span></p>
            <p>Most companies will have an admin portal page, giving their staff access to basic admin controls for day-to-day operations. For a bank, an employee might need to transfer money to and from client accounts. Often these pages are not made private, allowing attackers to find hidden pages that show, or give access to, admin controls or sensitive data.</p>
            <p><span style="font-size:1rem">Type the following command into the terminal to find potentially hidden pages on FakeBank's website using GoBuster (a command-line security application)</span><span style="font-size:20px"><br></span></p>
            </span>
            </span>
            <p style="text-align:right"><i>Don't worry if you have not used a terminal before - TryHackMe walks you through everything!</i></p>
            <p >In the command above, <code>-u</code> is used to state the website we're scanning, <code>-w</code> takes a list of words to iterate through to find hidden pages.</p>
            <p>You will see that GoBuster scans the website with each word in the list, finding pages that exist on the site. GoBuster will have told you the pages it found in the list of page/directory names (indicated by Status: 200).</p>
            <p ></p>
            <p ><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5bec5dfd73790a7d06282266/room-content/73103edfb588a260fb9d336094ad5253.png"><br><br></p>
            <p ><span style="font-size:20px">Step 3) Hack the bank</span><br></p>
            <p >You should have found a secret bank transfer page that allows you to transfer money between accounts at the bank (/bank-transfer).&nbsp;<span style="font-size:1rem">Type the hidden page into the FakeBank website on the machine.</span></p>
            </span>
            <details>
              <summary>Stuck? See video</summary>
              <iframe width="500" height="500" frameborder="0" src="https://assets.tryhackme.com/additional/introtooffensivesecurity/terminal-to-site.mp4">
              </iframe>
            </details>
            </span>
            <p ><br>This page allows an attacker to steal money from any bank account, which is a critical risk for the bank. As an ethical hacker, you would (with permission) find vulnerabilities in their application and report them to the bank to fix before a hacker exploits them.<br></p>
            <p ><span style="font-size:1rem">Transfer $2000 from the bank account 2276, to your account (account number 8881).</span></p>
          </div>
        </div>
        <div class="room-questions-split vertical-align-custom red">
          <div>Answer the questions below</div>
        </div>
        <div class="room-task-questions"> 
          When you've transferred money to your account, go back to your bank account page. What is the answer shown on your bank balance page?
        </div>
      </div>
      <div >
      </div>
      <div class="room-task-input-answer">
        <button type="button" class="btn btn-outline-success task-answer" onclick="answerQuestion(this)">
        <i class="far fa-paper-plane"></i> Submit
        </button>
      </div>
      <div class="room-task-input-hint">
        <button type="button" class="btn btn-outline-dorange btn-noline task-hint" onclick="getHint(this)">
        <i class="fal fa-lightbulb"></i> Hint
        </button>
      </div>
    </div>
    <div class="room-task-questions">
      <p>If you were a penetration tester or security consultant, this is an exercise you’d perform for companies to test for vulnerabilities in their web applications; find hidden pages to investigate for vulnerabilities.<br></p>
    </div>
  </div>
  <div class="room-task-input-answer">
    <button type="button" class="btn btn-outline-success task-answer" onclick="answerQuestion(this)">
    <i class="far fa-paper-plane"></i> Completed
    </button>
  </div>
  </div>
  <div class="room-task-questions">
    <p>Terminate the machine by clicking the red "Terminate" button at the top of the page.<br></p>
  </div>
  </div>
  <div >
    <div >
      <input type="text" class="form-control room-answer-field" placeholder="No answer needed" value="" disabled="">
      <input value="3">
      <input >
    </div>
    <div class="room-task-input-answer">
      <button type="button" class="btn btn-outline-success task-answer" onclick="answerQuestion(this)">
      <i class="far fa-paper-plane"></i> Completed
      </button>
    </div>
  </div>
  </div>
  </div>
  </div>
</details>
<details>
  <summary>
    Task 2  What is Offensive Security?
  </summary>
  <div class="card" id="task-2">
    <div   href="#collapse2">
      <a class="card-link">
      <span class="task-dropdown-title red">Task 2 <span ><i class="far fa-circle text-lgray"></i></span></span> What is Offensive Security?
      <span class="float-right"><i class="fas fa-chevron-down"></i></span>
      <span class="task-resources"></span>
      </a>
    </div>
    <div id="collapse2" class="collapse " >
      <div >
        <div >
          <div >
            <p><img src="https://tryhackme.com/img/network/unknown_infected.png" style="width:154.958px;float:left;height:120.242px" class="note-float-left">In short, offensive security is the process of breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access to them.</p>
            <p>To beat a hacker, you need to behave like a hacker, finding vulnerabilities and recommending patches before a cybercriminal does, as you did in this room!</p>
            <p><img src="https://tryhackme.com/img/general/computerdefend.png" style="width:160.106px;float:right;height:124.242px" class="note-float-right">On the flip side, there is also defensive security, which is the process of protecting an organization's network and computer systems by analyzing and securing any potential digital threats; learn more in the digital forensics room.<br></p>
            <p>In a defensive cyber role, you could be investigating infected computers or devices to understand how it was hacked, tracking down cybercriminals, or monitoring infrastructure for&nbsp;<span style="background-color:rgb(250, 250, 250);font-size:1rem">malicious activity.</span></p>
          </div>
        </div>
        <div class="room-questions-split vertical-align-custom red">
          <div>Answer the questions below</div>
        </div>
        <div class="room-task-questions">
          <div class="room-task-question-details">
            Read the above.
          </div>
        </div>
        <div >
          <div >
            <input type="text" class="form-control room-answer-field" placeholder="No answer needed" value="" disabled="">
            <input >
            <input value="2">
          </div>
          <div class="room-task-input-answer">
            <button type="button" class="btn btn-outline-success task-answer" onclick="answerQuestion(this)">
            <i class="far fa-paper-plane"></i> Completed
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</details>
<details>
  <summary>
    Task 3  Careers in cyber security
  </summary>
  <div class="card" id="task-3">
    <div   href="#collapse3">
      <a class="card-link">
      <span >Task 3 <span ><i class="far fa-circle text-lgray"></i></span></span> Careers in cyber security
      <span ><i class="fas fa-chevron-down"></i></span>
      <span ></span>
      </a>
    </div>
    <div  >
      <div >
        <div >
          <div >
            <p><span style="font-size:24px">How can I start learning?</span></p>
            <p>People often wonder how others become hackers (security consultants) or defenders (security analysts fighting cybercrime), and the answer is simple. Break it down, learn an area of cyber security you're interested in, and regularly practice using hands-on exercises. Build a habit of learning a little bit each day on TryHackMe, and you'll acquire the knowledge to get your first job in the industry.</p>
            <p>Trust us; you can do it! Just take a look at some people who have used TryHackMe to get their first security job:</p>
            <ul>
              <li>Paul went from a construction worker to a security engineer. <a href="https://tryhackme.com/resources/blog/construction-worker-to-security-engineer-how-paul-used-tryhackme-to-land-his-first-job-in-security" target="_blank">Read more</a>.<br></li>
              <li>Kassandra went from a music teacher to a security professional. <a href="https://tryhackme.com/resources/blog/the-teacher-becomes-the-student" target="_blank">Read more</a>.</li>
              <li>Brandon used TryHackMe while at school to get his first job in cyber. <a href="https://tryhackme.com/resources/blog/brandons-success-story" target="_blank">Read more</a>.</li>
            </ul>
            <p><span style="font-size:24px">What careers are there?</span></p>
            <p>The cyber careers room goes into more depth about the different careers in cyber. However, here is a short description of a few offensive security roles:</p>
            <ul>
              <li>Penetration Tester - Responsible for testing technology products for finding exploitable security vulnerabilities.</li>
              <li>Red Teamer - Plays the role of an adversary, attacking an organization and providing feedback from an enemy's perspective.</li>
              <li>Security Engineer - Design, monitor, and maintain security controls, networks, and systems to help prevent cyberattacks.</li>
            </ul>
          </div>
        </div>
        <div class="room-questions-split vertical-align-custom red">
          <div>Answer the questions below</div>
        </div>
        <div class="room-task-questions">
          <div class="room-task-question-details">
            Read the above, and continue with the next room!
          </div>
        </div>
      </div>
    </div>
  </div>
</details>
  
</details>

---

<details>

<summary>
  <a href="https://tryhackme.com/room/introwebapplicationsecurity">Web Application Security</a>
</summary>  

  <br><li> Learn about web applications and explore some of their common security issues. </li>
  
</details>

---

<details>

<summary>
  Intro to Offensive Security
</summary>  

  <br><li> Hack your first website (legally in a safe environment) and experience an ethical hacker's job. </li>
  
</details>

---

<details>

<summary>
  Intro to Offensive Security
</summary>  

  <br><li> Hack your first website (legally in a safe environment) and experience an ethical hacker's job. </li>
  
</details>

---
