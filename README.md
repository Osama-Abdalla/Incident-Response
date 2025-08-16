# 🛡️ Incident-Response

## 📌 Overview
This repository showcases my hands-on work in **Incident Response (IR)**.  
It demonstrates the process of detecting, analyzing, containing, and mitigating cybersecurity incidents in a structured and repeatable way.

The repository is designed as a practical portfolio for **SOC analysts, blue teamers, and security enthusiasts**, and documents real-world IR workflows, tools, and methodologies.

---

## 🔄 Incident Response Lifecycle
The project follows the industry-standard **NIST Incident Response lifecycle**:

1. **Preparation**  
   - IR playbooks and policies  
   - Lab setup for detection and response  

2. **Identification**  
   - Log analysis (Splunk, ELK, Sysmon)  
   - Alert triage and false positive reduction  

3. **Containment**  
   - Isolating compromised systems  
   - Blocking malicious IPs/domains  

4. **Eradication**  
   - Removing malware, backdoors, and persistence mechanisms  
   - Closing exploited vulnerabilities  

5. **Recovery**  
   - Restoring systems to normal operation  
   - Verifying security posture post-incident  

6. **Lessons Learned**  
   - Post-incident reporting  
   - Updating playbooks for future incidents
  
   ## 📂 Incident Response Cases

| Case Name | Description | Link |
|-----------|-------------|------|
| **Phishing Attack** | Analysis of malicious email with payload delivery | [View Case](cases/phishing-attack.md) |
| **Brute Force Attack** | Detection of repeated login attempts in logs | [View Case](cases/brute-force.md) |
| **Malware Infection** | Investigating suspicious process & containment steps | [View Case](cases/malware-infection.md) |
| **Privilege Escalation** | Detection & analysis of privilege misuse on Linux host | [View Case](cases/privilege-escalation.md) |
