# Unit 4 Quiz Notes: Vulnerable vs. Subsequent System Impact (CVSS v4.0)

**Q1: In CVSS v4.0, what does the Vulnerable System (VC/VI/VA) metric group measure, in one sentence?**
A1: It measures the confidentiality, integrity, and availability impact that occurs directly on the component where the vulnerability exists, before any pivot to another system.

**Q2: What does the Subsequent System (SC/SI/SA) metric group capture that VC/VI/VA does not?**
A2: It captures impact on other systems, components, or data that are reached only as a downstream consequence of exploiting the original vulnerability — impact beyond the vulnerable component's own security boundary.

**Q3: In the sudo privilege-escalation case, what would count as the Vulnerable-System impact?**
A3: The attacker's ability to execute arbitrary commands as root on the local machine where the flawed sudo binary is installed — full loss of confidentiality, integrity, and availability on that one host.

**Q4: Would the sudo case typically involve Subsequent-System impact? Why or why not?**
A4: Only if root access on that host is then used to reach other systems — for example, extracting stored credentials or SSH keys that let the attacker pivot to a domain controller or a shared file server; without that pivot, impact stays confined to the vulnerable system.

**Q5: If exploiting the sudo flaw only lets an attacker read local files on the same box, how should VC and SC be scored?**
A5: VC should be scored High (or the appropriate level reflecting local confidentiality loss), while SC should be scored None, since no separate system's confidentiality was affected.

**Q6: Why does CVSS v4.0 separate these two metric groups instead of using one combined "impact" score, as earlier CVSS versions did?**
A6: Separating them lets analysts express that a low-severity local bug can still be critical if it enables a pivot to high-value systems, giving more accurate prioritization than a single blended score could.

**Q7: In the Target/Fazio Mechanical breach, what would VI (Vulnerable-System Integrity) reflect?**
A7: The integrity impact on Fazio's own compromised systems or credentials — the initial foothold — rather than the impact on Target's payment infrastructure.

**Q8: In the same Target breach, what would SA (Subsequent-System Availability) or SC (Subsequent-System Confidentiality) reflect?**
A8: SC would reflect the massive confidentiality loss on Target's separate, more sensitive retail network — the ~40 million card numbers and ~70 million customer records exposed after the attackers pivoted beyond the vendor portal.

**Q9: For the sudo case, if a compromised host is later used to move laterally into a corporate Active Directory environment, which metrics would move from None to High, and why?**
A9: SC, SI, and SA could all move from None to High, since Active Directory is a separate system whose confidentiality, integrity, and availability are now impacted as a direct consequence of the original local exploit.

**Q10: What is the general rule of thumb for deciding whether an impact belongs under Vulnerable-System or Subsequent-System metrics?**
A10: Ask whether the affected component shares the same security authority/boundary as the vulnerable component — if yes, score it under VC/VI/VA; if it's a distinct system, dataset, or trust domain reached only through the exploit, score it under SC/SI/SA.
