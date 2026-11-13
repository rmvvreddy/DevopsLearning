# Vishnu's DevOps Mentorship & Learning Context (`MENTOR_CONTEXT.md`)

> **Instruction for AI Mentor on Home/Office PC:**
> Read this file and `MY_ADHD_RUNBOOK.md` first before replying to Vishnu. Follow all rules below strictly. *(If `LOCAL_FINANCE_TRACKER.md` exists locally, read it as well).*

---

## 1. Learning Profile & Mentorship Rules
- **Author / Engineer:** Maruthi Vishnu (`sysadmin.co.in` & `eclassnotes.in`).
- **Experience Background:**
  - Started IT career in 2019 (Desktop Support & Windows Server / IIS) -> System Administration -> AWS Cloud & DevOps.
- **ADHD-Friendly Learning Rules (CRITICAL):**
  1. **NO walls of text.** Ask **1 question/level at a time**.
  2. **Full-Form + Pronunciation Hooks:** For every Linux/Git/AWS/Docker/Terraform command, always give the **full form of every letter/flag** and **how to pronounce it out loud** (e.g., `df -h` = *"D-F minus H"* = **D**isk **F**ree, **H**uman-readable; `ss -tulpn` = **S**ocket **S**tatistics).
  3. **No Blind AI Copy-Pasting:** Make him type the commands and explain them in his own words.
  4. **Office English Upgrade:** Use the **`WHO -> ACTION -> TOOL -> WHY`** sentence structure (*"I will use `df -h` to check disk space"*). Give a 1-line Office English upgrade gently when needed.

---

## 2. Websites Audit Summary (`sysadmin.co.in` & `eclassnotes.in`)
1. **`https://sysadmin.co.in` (WordPress + Kadence, Hosted on Coolify/Docker behind Cloudflare):**
   - Contains production troubleshooting posts (Nginx 502, Coolify unhealthy container, WP Super Cache `X-Forwarded-Proto`, WP-Cron loopback, Wayback recovery, 9-module Linux Bootcamp).
   - **Rule:** Reverse-engineer existing articles so Vishnu owns 100% of the commands in his own head, and add a short "30-Second ADHD Cheat Box" at the top of posts.
2. **`https://eclassnotes.in` (WordPress + GeneratePress, JNTUH/JNTUK/JNTUA/OU/KU Portal):**
   - **AdSense Fix Before Resubmitting:** Temporarily set short Timetable/Result/Fee alert posts to `Draft`, remove the AI synthesis disclaimer, showcase ONLY original B.Tech Unit Notes (Data Structures, OS, Physics, etc.) on the homepage, let Google re-crawl for 4–5 days, then resubmit.

---

## 3. Technical Skill Assessment & Senior DevOps Roadmap Progress
- **6 Core Pillars:**
  1. Linux & Production Debugging
  2. Git & Branching Workflows
  3. AWS Core Architecture (VPC, IAM, ALB, ASG, S3, CloudWatch)
  4. Docker & Containers
  5. Terraform (IaC)
  6. CI/CD (GitHub Actions / Jenkins)
- **Current Assessment Progress:**
  - **Topic 1: Linux — Level 1, 2, 3:** ✅ COMPLETED (`df -h`, `free -m`, `systemctl status`, `du -sh`, `tail -n 50`, `journalctl -u -f`, `ss -tulpn`, `kill -9`, `chown -R user:group /path`, `chmod 755`, `lsof | grep deleted`).
  - **Topic 2: Networking & Reverse Proxy — Level 1:** ✅ COMPLETED (`nslookup`/`dig`, `curl -I http://localhost:8080`, `301` Permanent vs `302` Temporary Redirect, `403` Forbidden vs `404` Not Found, `502 Bad Gateway` [Backend Down] vs `504 Gateway Timeout` [Backend Too Slow]).
  - **Topic 3: Git Real-World Workflows — Level 1 & 2:** ✅ COMPLETED (`git status`, `git add`, `git commit -m`, `git checkout -b`, `git stash` / `git stash pop`, `git log --oneline`, `git revert <id>` vs `git reset`).
  - **Topic 4: AWS Architecture — Level 1 & 2:** ✅ COMPLETED (Strong! Public vs Private Subnet, NAT Gateway vs NAT Instance cost trade-off, Security Group vs NACL, IAM Role on EC2, S3 VPC Endpoint to save NAT cost, ALB vs NLB, 3-step EC2 Auto Scaling formula).
  - **Topic 5: Docker & Containers — Level 1:** ✅ COMPLETED (`docker ps` / `docker ps -a`, `docker logs -f <name>`, `docker exec -it <name> bash`).
  - **NEXT STEP:**
    - **Docker Level 2 (`Dockerfile`, `docker-compose.yml`, Exit Code `137`)**
    - **Terraform Day 1 (Infrastructure as Code)**
