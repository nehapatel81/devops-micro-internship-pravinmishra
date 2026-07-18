# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![React App](./screenshots/SC45.png)

---

#### Screenshot 2 — Output of `ip a`

![ip](./screenshots/SC46.png)

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

![tulpen](./screenshots/SC50.png)

---

#### Screenshot 4 — Output of `sudo ufw status`

![status](./screenshots/SC51.png)

---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The output shows that Nginx is listening on 0.0.0.0:80 with the LISTEN state.This means the web server is accepting HTTP requests from all network interfaces.It confirms that users can access the React application through the server’s public IP address.


---

**2. What proves SSH is active on port 22?**

The output of sudo ss -tulpen shows sshd listening on port 22 with the LISTEN state.This confirms that the SSH service is running and accepting connections.It allows secure remote access to the server for administration.

---

**3. Did you find any unexpected open ports? Explain briefly.**

No, I did not find any unexpected open ports on the server. The server was only listening on required ports, such as 22 for SSH and 80 for HTTP (Nginx).Keeping only necessary ports open helps reduce security risks and follows good production practices.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

![nginx status](./screenshots/SC52.png)

---

#### Screenshot 2 — Output of `sudo nginx -t`

![sudo nginx](./screenshots/SC54.png)

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

![lptn](./screenshots/SC56.png)

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart, the website may become unavailable, and users maysee errors such as 502 Bad Gateway or Connection Refused.This can cause downtime and negatively impact the user experience.Using nginx -t before restarting helps verify the configuration and prevent service failures.

---

**2. What's your basic rollback plan?**

My first step would be to identify the recent change and restore the last working Nginx configuration.I would then validate the configuration using nginx -t and restart the Nginx service.If the issue continues, I would restore the previous application or server backup to bring the website back online quickly.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

![sudo tail](./screenshots/SC61.png)

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

![tail](./screenshots/SC62.png)

---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

![journa](./screenshots/SC63.png)

---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No, I did not find any errors in the Nginx error logs during my analysis.The logs were empty or did not contain any recent error entries, indicating the server was running normally.Although this does not guarantee future issues, it confirms no problems were recorded during the check.

---

**2. If there were no errors, what does that indicate about the system?**

It indicates that the application and Nginx were working as expected during the monitoring period. Requests were processed successfully, and no server-side errors were recorded. Regular log monitoring is still important to identify and troubleshoot any future issues.Write your answer here.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes, my curl requests were visible in the Nginx access logs.This confirmed that the requests reached the web server and were successfully processed by Nginx.It also verified that the network connection, Nginx configuration, and request logging were working correctly.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

![Uptime](./screenshots/SC64.png)

---

#### Screenshot 2 — Output of `free -h`

![free](./screenshots/SC65.png)

---

#### Screenshot 3 — Output of `df -h`

![df](./screenshots/SC66.png)

---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

![sort](./screenshots/SC67.png)

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Currently, none of the system resources appear to be in a critical state.However, I would monitor disk usage closely because the root partition is around 60% utilized.Disk space can increase over time due to logs, application data, and updates, so regular monitoring helps prevent storage issues.

---

**2. What happens if disk becomes 100% full in a production server?**

If the disk reaches 100% capacity, applications may fail to write files, logs may stop recording, and deployments or updates can fail.
Some services may crash or fail to start, causing downtime and making troubleshooting difficult.Regular disk monitoring and cleanup help prevent these production issues.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

![head](./screenshots/SC68.png)

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

![deployed](./screenshots/SC69.png)

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

![tryfiles](./screenshots/SC70.png)

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

I confirmed the deployment by checking the /var/www/html directory and verifying that the React build files, including index.html and the static folder, were present.I used the grep command to confirm that my personalized changes were included in the deployed build.Finally, I accessed the application using the EC2 public IP and verified that Nginx was serving the correct updated version.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

Add your screenshot here.

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

![curl](./screenshots/SC54.png)

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![curl](./screenshots/SC76.png)

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

The configuration failure occurred because I removed the semicolon (;) from the try_files $uri /index.html; directive.This created a syntax error, preventing Nginx from validating the configuration.As a result, Nginx could not restart until the error was fixed.

---

**2. How did you fix the issue?**

I added the missing semicolon back to the try_files directive and saved the configuration file.I verified the configuration using sudo nginx -t and then restarted the Nginx service.Finally, I confirmed the application was working by receiving an HTTP 200 response.

---

**3. How can you avoid this kind of issue in real production systems?**

I would always validate the configuration with nginx -t before restarting or reloading Nginx. I would also review configuration changes carefully and use version control to track modifications.Testing changes in a staging environment helps catch errors before deploying to production.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

![curl](./screenshots/SC73.png)

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![curl](./screenshots/SC76.png)

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application stopped working because the /var/www/html directory was temporarily replaced with an empty directory. As a result, Nginx could not find the required files, such as index.html, to serve the website.This caused the application to become unavailable.

---

**2. How did you fix the issue and restore the application?**

I restored the original deployment by replacing the empty /var/www/html directory with the backup.After restarting the Nginx service, I verified the application using the server's public IP. A successful HTTP 200 response confirmed that the application was restored.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

I would always create a backup before making changes to the production server.I would use automated deployment pipelines with rollback support instead of making manual changes.Testing in a staging environment and monitoring the application after deployment would help prevent downtime.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH keys are more secure than passwords because they are much harder to guess or steal.They provide a safer way to access the server and reduce the risk of unauthorized logins.They also help protect production systems from password-based attacks.

---

**2. Why should only required ports be open on a production server?**

Keeping only the required ports open reduces security risks.It limits unnecessary access to the server and helps prevent attacks.This follows security best practices for production environments.

---

**3. Why is it important for Nginx to be enabled on boot?**

Enabling Nginx on boot ensures the web server starts automatically after a system restart.This makes the website available without manual intervention.It helps reduce downtime and improves service reliability.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

If secrets or keys are shared publicly, unauthorized users can access your systems.This can lead to data theft, service misuse, or compromised cloud resources.Keeping credentials private is essential for maintaining security.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Unused cloud resources can continue to generate costs even when they are not in use.Stopping or terminating them helps reduce unnecessary expenses.It also keeps the cloud environment organized and easier to manage.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/workwithneha_dmibypravinmishra-agenticai-devops-share-7484080534269214720-QUXT/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADVmLRoB9dJ70xtJ1M6sDVbSBOiVTmQDql0`

---

#### Screenshot — Published LinkedIn post

![curl](./screenshots/SC126.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [x] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [x] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [x] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [x] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [x] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [x] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [x] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [x] Task 8: Security & Reliability Notes answered
- [x] LinkedIn post published and URL submitted
- [x] Full Name visible in all required screenshots
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