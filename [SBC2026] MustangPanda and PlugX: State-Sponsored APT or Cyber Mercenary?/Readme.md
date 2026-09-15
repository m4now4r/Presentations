**Event:** Security Bootcamp 2026 (Agentic Security) - Location: Buon Ma Thuot City, Dak Lak Province, Vietnam

**Title:** MustangPanda and PlugX: State-Sponsored APT or Cyber Mercenary?

**Abstract:**
MustangPanda remains one of the most persistent and closely monitored APT groups in the Asia-Pacific region, known for conducting cyber espionage campaigns against government agencies, diplomatic entities, NGOs, and critical sectors. A cornerstone of their operations is PlugX—a modular Remote Access Trojan (RAT) that continuously evolves across generations. Despite extensive public research, infrastructure changes, and numerous analyzed samples, PlugX remains a resilient threat in modern campaigns.

Drawing upon years of independent research—including prior analyses on COVID-19-themed campaigns targeting Vietnamese state agencies while at VinCSS (2020–2023)—this presentation provides an in-depth technical analysis of MustangPanda's latest campaigns through Q1 and Q2 2026.

**The presentation will cover:**

- Initial Access & AI-Assisted Analysis: Examining infection chains utilizing .lnk, .hta, .msi, and .exe files, combining traditional reverse engineering with AI-driven methodologies to accelerate early-stage analysis.

- Core Execution Mechanics: Deep-diving into DLL side-loading techniques, malicious DLLs leveraging the RtlRegisterWait API for shellcode execution, shellcode decryption routines to recover the final PlugX DLL, and the use of ReflectiveDllLoader for in-memory execution.

- Automation & Configuration Extraction: Showcasing custom automation scripts developed to detect encrypted payloads, decrypt and extract PlugX DLLs, and parse encrypted configuration structures.

- Recent Discoveries in Vietnam (Q2 2026): Analyzing newly observed PlugX samples targeting Vietnam, highlighting similarities, variations, and payload modifications that required continuous tool updates.

- Practical AI Integration: Sharing real-world insights on leveraging AI to accelerate malware analysis and research tool development.

*Disclaimer: This is an independent research presentation and does not represent the views, stance, or opinions of any company, employer, or organization.*
