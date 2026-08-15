# Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

![SC](./screenshots/sc36.png)

---

### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

Product Owner (PO): Responsible for prioritizing the backlog and deciding which tasks should be completed first. Since this is Solo Mode, I will personally rank the Stories based on their value to the user and the business in Task 4.

Scrum Master (SM): Responsible for ensuring that the Scrum process is followed correctly. This includes managing the sprint timeline, conducting Scrum activities such as planning and retrospectives, and keeping myself accountable to the agreed Scrum practices.

Dev Lead: Responsible for developing and implementing the selected Story. In Task 8, this involves making the required UI changes and ensuring that the implementation works as expected.

DevOps Lead: Responsible for deploying the completed work and verifying the deployment. This includes committing the changes to Git, deploying the application, and confirming that the updated version is live and functioning correctly.

---

# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

![SC](./screenshots/sc37.png)

---

# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

![SC](./screenshots/sc38.png)

---

# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

![SC](./screenshots/sc39.png)

---

#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

![SC](./screenshots/sc40.png)

---

# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

![SC](./screenshots/sc41.png)

---

### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

S1 – Hero Tagline (1 point):
This only requires replacing the existing heading text, making it a small and straightforward change. There is minimal effort and no additional functionality involved.

S2 – Button Colour (1 point):
This involves updating the button colour using CSS. I briefly considered 2 points because multiple buttons are involved, but kept it at 1 point since the styling change itself is simple.

S3 – Job Card Typography (2 points):
This requires changing the font size and font weight, followed by checking the layout across different screen sizes. The combination of styling and responsive testing makes it slightly more involved.

S4 – REMOTE Badge (2 points):
This requires creating a new badge and ensuring it appears only for remote jobs. Because it involves additional display logic rather than a simple text or style change, I estimated it at 2 points.

S5 – Posted On Date (1 point):
This involves adding the posted date as text without requiring additional logic or complex functionality, making it a straightforward 1-point task.

S6 – Search Labels (2 points):
Several labels and placeholders need to be updated, followed by testing to ensure all the changes work correctly. Since multiple UI elements are involved, I estimated it at 2 points.

S7 – Job Detail “Apply Now” Button (1 point):
This requires adding an “Apply Now” button with an email address or placeholder link. Since no complex functionality is required, I estimated it at 1 point.

S8 – Footer Trust Links (1 point):
This involves adding two simple footer links — “About” and “Contact.” It is a small HTML change with no complex functionality, so I estimated it at 1 point.

Total Backlog Estimate: 11 Story Points

1 + 1 + 2 + 2 + 1 + 2 + 1 + 1 = 11 points

---

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

![SC](./screenshots/sc42.png)

---

#### Screenshot 8 — One Story showing the Sub-tasks created

![SC](./screenshots/sc43.png)

---

# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

![SC](./screenshots/sc44.png)

---

# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

![SC](./screenshots/sc48.png)

---

#### Screenshot 11 — Git commit output

![SC](./screenshots/sc47.png)

---

#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

![SC](./screenshots/sc46.png)

---

# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

![SC](./screenshots/sc49.png)

---

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://lnkd.in/p/gQm5YzV3`

---

#### Screenshot 14 — Published LinkedIn post

![SC](./screenshots/sc50.png)

---

# Submission Instructions

- Add all 14 required screenshots
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [x] Task 1: Team Mode or Solo Mode selected and all four roles documented (Screenshot 1 & Notes)
- [x] Task 2: Team-managed Scrum project created with the required name (Screenshot 2)
- [x] Task 3: UI improvement Epic created (Screenshot 3)
- [x] Task 4: 6–8 Stories added under the Epic and ranked by value (Screenshots 4 & 5)
- [x] Task 5: Story Points set (1, 2, or 3) with reasoning recorded (Screenshot 6 & Notes)
- [x] Task 6: Sprint 1 created with Sprint Goal, 3–4 Stories, and Sub-tasks (Screenshots 7 & 8)
- [x] Task 7: Burndown Chart opened (Screenshot 9)
- [x] Task 8: One UI-only increment implemented, committed, deployed, and verified (Screenshots 10–12)
- [x] Task 9: Retro comment with one Scrum pillar and one Scrum value (Screenshot 13)
- [x] Task 10: Mandatory LinkedIn post published with the live URL, backlog refinement, Sprint planning, one shipped increment, proof, and Screenshot 14
- [x] Full Name visible in required screenshots
- [x] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
