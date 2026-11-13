# Vishnu's Personal ADHD DevOps Runbook
*Rule: Every command has a Full-Form Memory Hook + Clean Interview Sentence.*

---

## Module 1: Linux Production Troubleshooting

### Level 1: Daily Server Health Checks
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `df -h` | **"D-F minus H"** = **D**isk **F**ree, **H**uman-readable (`GB`/`MB`) | *"I will use `df -h` to check free disk space across partitions."* |
| `free -m` / `top` | **"Free minus M"** = Free Memory in **M**egabytes / **T**able **O**f **P**rocesses | *"I will use `free -m` and `top` to check available memory and CPU usage."* |
| `systemctl status nginx` | **"System-Control"** = **System**d **C**on**t**ro**l** | *"I will use `systemctl status nginx` to check if the Nginx service is running."* |

### Level 2: Logs, Folder Sizes & Ports
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `du -sh /var/log/*` | **"D-U minus S-H"** = **D**isk **U**sage, **S**ummary, **H**uman-readable | *"I will use `du -sh /var/log/*` to check which folder or file is taking the most space."* |
| `tail -n 50 /var/log/nginx/error.log` | **"Tail minus N 50"** = Bottom (**Tail**) of file, **N**umber of lines = 50 (`-f` = **F**ollow live) | *"I will use `tail -n 50` to check the last 50 lines of the error log."* |
| `journalctl -u nginx -f` | **"Journal-Control minus U minus F"** = Systemd **J**ournal, **U**nit `nginx`, **F**ollow live | *"I will use `journalctl -u nginx -f` to stream live systemd logs for Nginx."* |
| `ss -tulpn \| grep 80` | **"S-S minus TULPN"** = **S**ocket **S**tatistics (**T**CP, **U**DP, **L**istening, **P**rocess, **N**umeric) | *"I will use `ss -tulpn \| grep 80` to check which process is listening on port 80."* |

### Level 3: Processes, Permissions & The "Deleted File Still Full" Trap
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `sudo kill -9 4512` | **"Kill minus 9"** = Signal 9 (`SIGKILL` = immediate force kill; Windows uses `-f`, Linux uses **`-9`**) | *"I will use `sudo kill -9 4512` to force-kill the stuck process by its PID."* |
| `sudo chown -R www-data:www-data /var/www/html` | **"Change-Own minus R"** = **Ch**ange **Own**er, **R**ecursive (**WHO** first, **WHERE** second!) | *"I will use `chown -R www-data:www-data /var/www/html` to change the owner and group recursively."* |
| `chmod 755` / `chmod 600` | **"Change-Mode"** = **Ch**ange **Mod**e (`4`=Read, `2`=Write, `1`=Execute -> `755` = Owner `rwx`, Group `r-x`, Others `r-x`; `600` = Owner `rw-` only, used for SSH keys!) | *"I will use `chmod 755` to grant read, write, and execute permissions to the owner, and read and execute to group and others."* |
| `lsof \| grep deleted` | **"L-S-O-F"** = **L**i**s**t **O**pen **F**iles (finds deleted files still held open in RAM by a running service like Nginx) | *"When `df -h` still shows 100% after `rm`, I will use `lsof \| grep deleted` to find which running process is holding the deleted log file open, and reload that service."* |

---

## Module 2: Networking, DNS & Reverse Proxy (`sysadmin.co.in` Core)

### Level 1: DNS, `curl` & HTTP Status Codes (Critical Interview Topic!)
| Command / Concept | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `nslookup sysadmin.co.in` / `dig sysadmin.co.in` | **"N-S-Lookup"** = **N**ame **S**erver **Lookup** (`ping` fails if AWS Security Group blocks ICMP, `nslookup`/`dig` always checks DNS!) | *"I will use `nslookup` or `dig` to check which IP address the domain is resolving to."* |
| `curl -I http://localhost:8080` | **"Curl minus Capital I"** = **C**lient **URL**, **`-I`** = **I**nfo / HTTP Headers only (shows `HTTP/1.1 200 OK`) | *"I will use `curl -I http://localhost:8080` to check the HTTP status code and headers from the terminal."* |
| **`2xx` (`200 OK`)** | **200 = Success** | Everything worked (`200 OK`). |
| **`3xx` (`301` vs `302`)** | **300 = Redirection** (Traffic Police pointing to a new road: `http` -> `https`) | **`301`** = **Permanent** Redirect; **`302`** = **Temporary** Redirect. |
| **`4xx` (`401`, `403`, `404`)** | **400 = Client / Permission Mistake** (Security Guard at the door) | **`401`** = Unauthorized (Not logged in); **`403`** = **Forbidden** (No permission); **`404`** = **Not Found** (Wrong URL). |
| **`5xx` (`502` vs `504`)** | **500 = Server / Backend Crash** (Nginx Reverse Proxy talking to Backend App on port 8080) | **`502 Bad Gateway`** = Backend app is **DEAD/DOWN** (refused connection). **`504 Gateway Timeout`** = Backend app is **TOO SLOW** (timed out waiting). |

---

## Module 3: Git Real-World Workflows

### Level 1: Daily Staging, Branching & Stashing
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `git status` -> `git add nginx.conf` -> `git commit -m "msg"` | **`-m`** = **M**essage | *"I will use `git status` to check modified files, `git add` to stage them, and `git commit -m` to commit with a message."* |
| `git checkout -b feature-login` *(or `git switch -c feature-login`)* | **"Checkout minus B"** = Checkout + create new **B**ranch in 1 step (`-c` = **C**reate) | *"I will use `git checkout -b feature-login` to create and switch to a new branch in one command."* |
| `git stash` & `git stash pop` | **Stash** = Put unfinished work in your **pocket**; **Pop** = **Pop** it back out of your pocket onto your desk! | *"I will use `git stash` to temporarily save uncommitted changes, and `git stash pop` to bring them back later."* |

### Level 2: Commit History & Production Rollback (`revert` vs `reset`)
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `git log --oneline` | **"Git Log minus-minus One-Line"** = Shows each commit on **1 short line** (7-character ID + message) instead of filling the whole screen | *"I will use `git log --oneline` to quickly view the commit history and commit IDs."* |
| `git revert a1b2c3d` | **Safe for Shared `main` Branch (Bank Refund Entry):** Creates a **NEW commit** that reverses the bad commit without deleting history | *"On a shared branch like `main`, I will use `git revert <commit-id>` because it creates a new undo commit without rewriting team history."* |
| `git reset --hard HEAD~1` | **Dangerous on Shared Branch (Time Machine Eraser):** Deletes commits from history (only use on your private local branch!) | *"I only use `git reset` on my local unpushed branch because it erases commit history."* |

---

## Module 4: AWS Cloud Architecture (VPC, IAM, Compute)

### Level 1: VPC Networking & Security (Already Strong!)
| Concept | Memory Hook (Opposite Pairs) | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| **Public vs Private Subnet** | **Public** = Route table points `0.0.0.0/0` to **Internet Gateway (`IGW`)**. **Private** = No direct `IGW` route. | *"A Public Subnet has a route to an Internet Gateway (`IGW`), while a Private Subnet does not allow direct inbound internet traffic."* |
| **NAT Gateway vs NAT Instance** | **NAT** = **N**etwork **A**ddress **T**ranslation (lives in **Public Subnet** so **Private Subnet** EC2s can reach the internet outbound). **NAT Gateway** = Managed by AWS; **NAT Instance** = Cheaper for small workloads, but requires manual patching/maintenance. | *"To let Private Subnet EC2s download patches without exposing them, I route outbound traffic through a NAT Gateway in the Public Subnet (or a NAT Instance to save cost)."* |
| **Security Group vs NACL** | **Security Group (Apartment Door Guard):** **Instance** level, **Stateful** (if you let a guest in, they can walk out automatically), **Allow rules only** (Default: Inbound Blocked, Outbound Allowed). <br>**NACL (Society Main Gate Guard):** **Subnet** level, **Stateless** (checks both Inbound & Outbound separately), supports **Allow AND Deny rules** (great for blocking a specific hacker IP!). | *"A Security Group is stateful, works at the instance level, and only supports Allow rules. A NACL is stateless, works at the subnet level, and supports both Allow and Deny rules."* |

### Level 2: IAM Roles, VPC Endpoints, ALB vs NLB & Auto Scaling (ASG)
| Concept | Memory Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| **IAM Role for EC2** | **Never put Access Keys on EC2!** Attach an **IAM Role** (Instance Profile) -> EC2 automatically fetches temporary rotating tokens from **Instance Metadata (`169.254.169.254`)**. | *"Instead of hardcoding AWS keys, I will attach an IAM Role with S3 permissions to the EC2 instance."* |
| **S3 VPC Gateway Endpoint** | **Free Private Tunnel to S3:** Added to the Private Subnet's **Route Table** so S3 traffic stays inside the AWS network and bypasses the expensive NAT Gateway (`$0/GB`!). | *"I will use an S3 Gateway VPC Endpoint in the Route Table so private EC2s can reach S3 privately without paying NAT Gateway data transfer charges."* |
| **ALB vs NLB** | **ALB (Application = HTTP/HTTPS Layer 7):** Smart router—reads URLs (`/api`, `/login`) and hostnames (`sysadmin.co.in`). <br>**NLB (Network = TCP/UDP Layer 4):** Speed & Static IP router—routes raw TCP/UDP packets at millions of requests/sec or gives a fixed Static IP. | *"I use an ALB for HTTP/HTTPS web apps that need path or host routing, and an NLB for raw TCP/UDP traffic, extreme low latency, or when clients require a static IP."* |
| **EC2 Auto Scaling Group (ASG)** | **3-Piece Lego Set (`LT` -> `ASG` -> `Policy`):** <br>1. **Launch Template (`LT`):** The Blueprint (which AMI, `t3.medium`, Security Group, IAM Role). <br>2. **ASG:** The Manager (`Min=2`, `Desired=2`, `Max=6` across 2 AZs, attached to ALB Target Group). <br>3. **Scaling Policy:** The Trigger (*"If average CPU > 70% for 5 mins, add +1 EC2"*). | *"To set up EC2 Auto Scaling, I create a Launch Template with the AMI and instance type, configure an Auto Scaling Group with Min/Max/Desired capacity attached to an ALB Target Group, and set a Target Tracking policy on 70% CPU."* |

---

## Module 5: Docker & Containers (Coolify Under the Hood)

### Level 1: Daily Container Inspection & Debugging
| Command | Pronunciation & Full-Form Hook | Interview Sentence (`Who -> Action -> Tool -> Why`) |
| :--- | :--- | :--- |
| `docker ps` & `docker ps -a` | **"Docker P-S minus A"** = **P**rocess **S**tatus, **`-a`** = **A**ll (including stopped/crashed containers!) | *"I will use `docker ps` to see running containers, and `docker ps -a` to see stopped or crashed containers."* |
| `docker logs -f wordpress-app` | **"Docker Logs minus F"** = Container **Logs** (with an `s`), **`-f`** = **F**ollow live | *"I will use `docker logs -f wordpress-app` to stream the container's live logs."* |
| `docker exec -it wordpress-app bash` | **"Docker Exec minus I-T"** = **Exec**ute inside container, **`-i`** = **I**nteractive, **`-t`** = **T**erminal (TTY), running `bash` | *"I will use `docker exec -it wordpress-app bash` to open an interactive terminal inside the running container."* |







