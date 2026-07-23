# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

![output1](./screenshots/SC131.png)

---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

![output2](./screenshots/SC132.png)

---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

If the output returns active, it confirms that the Nginx service is running successfully.

---

**2. What proves that the server is listening for HTTP traffic?**

If port 80 appears in the output, it proves that Nginx is listening for HTTP requests.

---

**3. Why must you capture a healthy baseline before simulating an incident?**

I must capture a healthy baseline before simulating an incident because it provides a reference point for how the system normally works. After creating the incident, I can compare the current state with the baseline to identify what changed and troubleshoot the issue more effectively. Once the problem is fixed, I can verify that the system has returned to its normal healthy state.

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

![output3](./screenshots/SC133.png)

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Claude should receive project-specific operational rules because they provide clear instructions about how to work within that specific environment. These rules help Claude understand the project structure, required processes, limitations, and best practices so it can provide safer and more accurate assistance.

---

**2. Why is the human required to execute the recovery command?**

The human is required to execute the recovery command because recovery actions can make important system changes. A human should review and approve the action before running it to prevent accidental damage and ensure the correct decision is being made.

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The rule that prevents Claude from making an unsupported diagnosis is the requirement to verify evidence before making conclusions. Claude must collect information, check logs, and confirm the issue before identifying the root cause instead of guessing.

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

![output](./screenshots/SC138.png)

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The Gather phase is the read-only inspection of the Ubuntu server. Claude collected information about Nginx, port 80, the HTTP response, disk usage, and memory without making any changes.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes,Claude only ran read-only commands and did not create any files. I verified this by checking the workspace and confirming that no new Bash script or other files were created.

---

**3. Why is planning before coding useful in DevOps automation?**

Planning helps identify the required checks, organize the workflow, and avoid mistakes before writing the script. This makes the automation safer and more reliable.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

![output](./screenshots/SC139.png)

---

#### Screenshot 6 — Middle section showing check functions and conditionals

![output](./screenshots/SC140.png)

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

![output](./screenshots/SC141.png)

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

![output](./screenshots/SC143.png)

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the five functions that perform the health checks.

---

**2. How does the `for` loop use that array?**

The for loop goes through each function in the array and runs them one by one to complete all the health checks.

---

**3. Why are the health checks separated into functions?**

Using functions keeps the script organized, easier to read, and simpler to update or troubleshoot.

---

**4. What is the purpose of `$(...)` in this script?**

$(...) runs a command and stores its output, such as the hostname, timestamp, disk usage, or HTTP status.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes show the overall result of the health checks: 0 = Healthy, 1 = Warning, and 2 = Fail. This helps users and automation tools quickly understand the server's status.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

![output](./screenshots/SC144.png)

---

#### Screenshot 10 — Output showing the captured exit code and final summary

![output](./screenshots/SC145.png)

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

HEALTHY. All health checks passed with no failures.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

The report shows Port 80 is listening and the HTTP check returned status code 200, confirming the application is serving traffic.

---

**3. Did your script return exit code 0 or 1? Explain why.**

My script returned exit code 0 because all health checks passed successfully with no warnings or failures.
---

**4. What is the difference between a warning and a failure in this script?**

A warning means the server is still working, but a resource like disk space or memory needs attention. A failure means a critical check, such as Nginx, port 80, or the HTTP response, has failed and requires immediate action.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

![output](./screenshots/SC146.png)

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

![output](./screenshots/SC147.png)

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

It uses Bash to run the health checks, Read to view the report, and Grep to find important results. Write isn't needed because the skill only inspects the server and doesn't modify files.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

It prevents Claude from running the skill automatically, so I stay in control of when the server inspection is performed.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash runs the health checks and generates the report. Claude reads the report, explains the results, and recommends the next steps without making changes.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

It is better because Claude analyzes real server data instead of guessing. This makes the assessment more accurate and reliable.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

![output](./screenshots/SC148.png)

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

![output](./screenshots/SC149.png)

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

![output](./screenshots/SC150.png)

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

The Nginx service, port 80, and local HTTP checks failed.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

The report shows Nginx is inactive, port 80 is not listening, and the HTTP request returned status code 000, confirming Nginx is unavailable.

---

**3. Did Claude execute the recovery command? Why is that important?**

No, Claude only suggested the recovery command. This is important because it lets me review the evidence before making changes to the server.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

The Gather phase.

---

**5. Which phase is represented by Claude's explanation?**

The Analyze phase.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

![output](./screenshots/SC151.png)

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

![output](./screenshots/SC152.png)

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

![output](./screenshots/SC153.png)

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

![output](./screenshots/SC155.png)

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

I manually ran sudo systemctl start nginx.

---

**2. What evidence proves that the service recovered?**

systemctl is-active nginx returned active, the HTTP request returned 200 OK, and the second triage confirmed all checks passed.

---

**3. Why is the second triage run necessary?**

It confirms the server is fully healthy after restarting Nginx by checking all health checks again.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

It could hide the real problem or make the issue worse if the root cause isn't fixed first.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

A chatbot answers questions, while an agentic workflow uses real system data to analyze the situation and recommend actions before I decide what to do.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Neha Patel

**Date:** 22/07/2026

---

**1. Reported Symptom**

The EpicReads React application became unreachable. A local HTTP check using curl failed, showing that the application was not serving traffic.

---

**2. Evidence Collected**

The triage script found three failures:

Nginx service inactive (systemctl is-active nginx returned inactive)
Port 80 not listening (ss showed no port 80 entry)
HTTP check failed (curl returned status 000)

Disk usage and memory checks passed, showing the issue was related to Nginx, not system resources.

---

**3. Most Likely Cause**

The most likely cause was that the Nginx service was stopped. Since Nginx was not running, port 80 was unavailable and the application could not receive HTTP requests.

---

**4. Human-Approved Recovery Action**

sudo systemctl start nginx I reviewed the evidence and manually executed the command.

---

**5. Verification**

Recovery was confirmed because:

systemctl is-active nginx returned active
curl -I http://localhost returned HTTP/1.1 200 OK
A second /linux-triage run showed all checks passed and the system status was HEALTHY

---

**6. Safety Decision**

Claude was limited to read-only tools and was not allowed to restart services. Keeping a human involved prevents unsafe changes and ensures the root cause is reviewed before recovery actions are taken.

---

**7. Agentic Loop Mapping**

Gather: Bash collected server health evidence and created the report.
Analyze: Claude reviewed the report, identified Nginx as the issue, and suggested a fix.
Human Act: I reviewed and manually ran the recovery command.
Verify: A second triage confirmed the server was healthy again.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/workwithneha_devops-networking-cloudcomputing-share-7485904912938131456-e7Uo/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADVmLRoB9dJ70xtJ1M6sDVbSBOiVTmQDql0`

---

#### Screenshot — Published LinkedIn post

![linkedin](./screenshots/SC130.png)

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`https://github.com/nehapatel81/devops-micro-internship-pravinmishra`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [x] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [x] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [x] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [x] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [x] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [x] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [x] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [x] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [x] Incident summary contains all seven required sections
- [x] LinkedIn post published and URL submitted
- [x] Full Name visible in all required screenshots and the Bash report
- [x] Skill does not have Write permission
- [x] Skill did not execute any recovery commands
- [x] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*