# 🐍 Python for Cybersecurity – Complete 3‑Week Plan

> Your Mission: Build a working port scanner + recon tool.  

> Rule: No theory-only learning. Code every single day.

---

## 📅 Week 1 – Python Fundamentals (Days 1–7)

| Day | Topic | Resource | Hands-On Task |

|-----|-------|----------|---------------|

| Day 1 | Variables, Data Types, Basic I/O | [Python for Cyber Security (first 1hr)](https://www.youtube.com/watch?v=3Kq1MIfTWCE) | Write a script that takes user input and prints it |

| Day 2 | Lists, Tuples, Dictionaries | Same video (1–1.5hr) | Build a simple contacts list app (add, view, delete) |

| Day 3 | Conditionals (`if`/`else`, elif) | Same video (1.5–2hr) | Build a login simulator with username/password check |

| Day 4 | Loops (`for`, while) | Same video (2–2.5hr) | Create a script that loops through a list of IPs and pings them |

| Day 5 | Functions & Error Handling | Same video (2.5–3hr) | Refactor your ping script into functions with try/except |

| Day 6 | File I/O (`open`, read, write) | [Real Python – Reading and Writing Files](https://realpython.com/read-write-files-python/) | Write a script that saves scan results to a .txt file |

| Day 7 | Review + Mini Project | — | Build a dictionary wordlist generator that saves to file |

---

## 📅 Week 2 – Networking + Socket Programming (Days 8–14)

| Day | Topic | Resource | Hands-On Task |

|-----|-------|----------|---------------|

| Day 8 | socket module basics – client/server | [Python Socket Programming (freeCodeCamp)](https://www.youtube.com/watch?v=3QiPPX-KeSc) | Build a TCP client that connects to scanme.nmap.org on port 80 |

| Day 9 | Building a TCP Client + Server | Same video | Build a TCP server that echoes back messages |

| Day 10 | Build a Single‑Port Scanner | [The Cyber Mentor Python Playlist](https://www.youtube.com/playlist?list=PLLKT__MCUeiwBa7d7F_vN1GUwz_2TmVQj) | Write a script that checks if port 22 is open on scanme.nmap.org |

| Day 11 | Multi‑port scanning (`for` loop) | Same playlist | Extend your scanner to check ports 1–1024 |

| Day 12 | Add Threading (make it fast!) | [Real Python – Intro to Threading](https://realpython.com/intro-to-python-threading/) | Add threading to scan 100 ports simultaneously |

| Day 13 | Add Banner Grabbing | [GitHub – Port Scanner with Banner Grabbing](https://github.com/DillanR1/PortScanner) | After identifying open ports, grab service banners (e.g., SSH, HTTP) |

| Day 14 | Add argparse + Output to File | [Real Python – argparse Guide](https://realpython.com/command-line-interfaces-python-argparse/) | Your scanner now accepts -t (target) and -p (ports) args. Save results to .txt |

---

## 📅 Week 3 – Advanced Tools + Recon (Days 15–21)

| Day | Topic | Resource | Hands-On Task |

|-----|-------|----------|---------------|

| Day 15 | requests module – HTTP recon | [Real Python – Requests Guide](https://realpython.com/python-requests/) | Write a script that fetches headers from a website |

| Day 16 | Build a Subdomain Finder | [Sublist3r – Subdomain Enumeration Tool](https://github.com/aboul3la/Sublist3r) | Use a wordlist to check for subdomains on a target domain |

| Day 17 | subprocess module – call Nmap from Python | [Real Python – Subprocess Guide](https://realpython.com/python-subprocess/) | Write a script that runs nmap -sV and parses the output |

| Day 18 | Build an Nmap Wrapper | [Real Python – Subprocess Guide](https://realpython.com/python-subprocess/) | Combine subprocess + argparse to create your own Nmap frontend |

| Day 19 | Combine All Tools into One Recon Suite | — | Menu-driven script: 1) Port Scanner 2) Subdomain Finder 3) Nmap Wrapper |

| Day 20 | Refactor + Clean Code | — | Add comments, error handling, logging. Make it professional. |

| Day 21 | Push to GitHub + Write README | — | Create a GitHub repo, upload your code, write a detailed README |

---

## 🎯 Your Final Deliverable

By the end of Week 3, you will have a GitHub repository containing:

📅 Simplified 3-Week Schedule (Prioritized)

Week 1 – Python Basics (Days 1–7)

Day

Watch This

Do This

Day 1

Python Course (0:00–0:45)

Write a "Hello World" + user input script

Day 2

Python Course (0:45–1:30)

Build a simple contacts list

Day 3

Python Course (1:30–2:15)

Build a login simulator

Day 4

Python Course (2:15–3:00)

Write a script that loops through IPs

Day 5

Python Course (Finish)

Refactor with functions + try/except

Day 6

File I/O Guide (15min read)

Write results to .txt file

Day 7

—

Build a wordlist generator (mini project)

📺 Watch: Python for Cyber Security (3hr)

Week 2 – Building Your Port Scanner (Days 8–14)

Day

Watch This

Do This

Day 8

Socket Tutorial (0–15min)

TCP client that connects to scanme.nmap.org:80

Day 9

Same video (15–30min)

TCP server that echoes back messages

Day 10

Cyber Mentor Playlist – Episode 1

Single‑port scanner (port 22)

Day 11

Cyber Mentor Playlist – Episode 2

Multi‑port scanner (1–1024)

Day 12

Threading Guide (15min read)

Add threading to your scanner

Day 13

Cyber Mentor Playlist – Episode 3

Add banner grabbing

Day 14

Argparse Guide (20min read)

Add CLI arguments + file output

📺 Watch: The Cyber Mentor Python Playlist (Only Episodes 1–4)

Week 3 – Recon Tools + Polish (Days 15–21)

Day

Watch/Read This

Do This

Day 15

Requests Guide (20min read)

Fetch HTTP headers from a website

Day 16

Sublist3r Guide (10min read)

Build a subdomain finder

Day 17

Subprocess Guide (20min read)

Call Nmap from Python

Day 18

—

Build an Nmap wrapper (combine subprocess + argparse)

Day 19

—

Combine all tools into one recon suite (menu-driven)

Day 20

—

Refactor + clean code

Day 21

—

Push to GitHub + write README

📊 Total Watch Time: ~4 Hours Only

Resource

Time Needed

Python for Cyber Security (3hr)

3 hours

Socket Programming (30min)

30 min

Cyber Mentor Playlist (4 episodes)

1 hour

TOTAL

~4.5 hours

The rest is hands-on coding – that's where you actually learn.

🗓️ Your Daily Routine (Simple)

Watch – 30–60 minutes of the video.

Code – 60–90 minutes typing everything yourself.

Push – 5 minutes commit to GitHub.

Write – 5 minutes notes (what you learned, errors fixed).

⚠️ Golden Rule

Stop watching when you understand enough to code.
The goal is to build, not to finish videos.

If you can write the code without looking at the video, you're done watching for the day.

🚀 Your Next Step – TODAY

Time

Action

0–5 min

Open YouTube, search "Python for Cyber Security FULL Course in 3 Hours"

5–60 min

Watch the first hour. Pause and type EVERY line.

60–120 min

Play with the code – change it, break it, fix it.

120–125 min

Push to GitHub.
