# Sysinternals Lab Project 

This repository contains a structured Windows Sysinternals lab designed to demonstrate practical system investigation, monitoring, and incident response skills.  
The project is divided into five phases, starting with environment setup and ending with advanced automation scenarios.

The goal is simple: show real, hands-on capability with Windows internals and Sysinternals tools in a way that’s easy to follow and easy to evaluate.

---

## Project Structure

Each phase has its own folder with documentation, walkthroughs, logs, and any supporting files.

| Phase | Folder | Description |
|-------|--------|-------------|
| Phase 0 – Environment Setup | `phases/phase0-environment-setup/` | Build the Windows VM, baseline the system, create users, configure snapshots, prepare tools |
| Phase 1 – Sysinternals Fundamentals | `phases/phase1-sysinternals-basics/` | Install Sysinternals Suite, practice the core tools, document basic system triage |
| Phase 2 – Monitoring and Analysis | `phases/phase2-monitoring-and-analysis/` | Capture and analyze process, registry, file, and network activity |
| Phase 3 – Forensics and Incident Response | `phases/phase3-forensics-and-incident-response/` | Investigate simulated incidents, track persistence, build incident timelines |
| Phase 4 – Advanced and Automation | `phases/phase4-advanced-and-automation/` | Automate workflows using Sysinternals and PowerShell; build repeatable scenarios |

```
├── README.md
├── docs/
│ └── (screenshots, diagrams, exported logs, notes)
└── phases/
├── phase0-environment-setup/
├── phase1-sysinternals-basics/
├── phase2-monitoring-and-analysis/
├── phase3-forensics-and-incident-response/
└── phase4-advanced-and-automation/
```

---

## Skills Demonstrated

This project highlights practical experience with:

### Sysinternals Tools
- Process Explorer  
- Process Monitor  
- Autoruns  
- TCPView  
- PsTools (PsExec, PsList, PsKill, etc.)  
- AccessChk, SigCheck, Strings, Handle, RAMMap  

### Technical Focus Areas
- Windows internals fundamentals  
- Process, registry, and file activity analysis  
- Network connection triage  
- Startup and persistence mechanism analysis  
- Memory and handle inspection  
- Incident response workflow  
- Evidence collection and documentation  
- Automation using PowerShell combined with Sysinternals tools  

---

## Lab Workflow

All phases follow the same general workflow:

1. Define a scenario or task.  
2. Use Sysinternals tools to observe or investigate.  
3. Capture logs, screenshots, or exports as evidence.  
4. Analyze and explain what happened.  
5. Commit findings in a clear, organized way.

This approach keeps the project consistent and makes it easier for anyone reviewing the repository to follow the logic behind each investigation.

---

## How to Navigate This Repository

If you’re reviewing the project:

- Start with Phase 0 to understand the lab configuration.  
- Move through the phases in order to see how the complexity increases.  
- Each folder contains a README with detailed steps and findings.

If you’re building the project:

- Complete phases sequentially.  
- Document everything thoroughly.  
- Commit often with meaningful messages.  
- Store screenshots, diagrams, or logs in the `docs` directory when needed.

---

## Project Status

- Repository structure created  
- Phase 0 setup in progress  
- Later phases to be completed after environment prep  

---
