# ACCEPTABLE USE POLICY (AUP)

| Document Metadata | Details |
| :--- | :--- |
| **Document ID** | `AP-GOV-POL-001` |
| **Version** | `1.0 (Approved)` |
| **Effective Date** | `November 12, 2026` |
| **Review Cycle** | `Annual` |
| **Policy Owner** | `Governance, Risk & Compliance (GRC) Lead` |
| **Executive Approver** | `Chief Information Security Officer (CISO)` |
| **Classification** | `Internal` |
| **Framework Mapping** | `ISO/IEC 27001:2022 (A.5.10) | NIST SP 800-53 (PL-4) | PCI-DSS v4.0 (Req 12.3)` |

---

## 1. FOUNDATION AND SCOPE (THE CONTEXT)

### 1.1 Purpose and Objectives
The purpose of this Acceptable Use Policy (AUP) is to define the acceptable and unacceptable use of AegisPay Technologies’ information systems and physical assets. These rules exist to protect the confidentiality, integrity, and availability of company and customer data, maintain operational continuity, and ensure compliance with applicable regulatory mandates (including Nigeria's NDPA, GDPR, and PCI-DSS).

### 1.2 Audience and Applicability
This policy applies globally to all individuals granted access to AegisPay information resources, including full-time and part-time employees, contractors, interns, consultants, temporary staff, and third-party vendors (collectively referred to as **"Authorized Users"**).

### 1.3 Covered Assets
You do not need an itemized hardware inventory to apply this policy; rather, this policy governs all interactions across the following **Asset Categories**:
* **Endpoint Hardware:** Company-issued laptops, desktops, mobile phones, servers, and storage media.
* **BYOD Assets:** Personal devices (laptops, tablets, smartphones) enrolled in or used to access corporate email, messaging, or cloud applications.
* **Network Infrastructure:** Corporate Wi-Fi, wired local area networks (LAN), Virtual Private Networks (VPN), and cloud virtual networks.
* **Cloud & SaaS Platforms:** Corporate email, collaboration tools, source code repositories, CRM databases, and production cloud environments (AWS/Azure/M365).
* **Data Assets:** All digital and physical records generated, received, or stored as part of business operations, including customer PII, financial records, intellectual property, and credentials.

---

## 2. BEHAVIORAL RULES AND CONTROLS (THE CORE)

### 2.1 Acceptable and Authorized Use
* **Primary Business Purpose:** All covered assets are provided to conduct authorized company business.
* **Incidental Personal Use:** Limited, occasional personal use (such as brief web browsing or personal communication) is permitted provided it does not interfere with work duties, consume excessive network bandwidth, violate any law, or introduce security risks.
* **Authorized Storage:** All company files and sensitive data must be stored strictly within approved corporate cloud storage and repositories.

### 2.2 Prohibited Activities
Authorized Users must never engage in the following activities on any covered asset:
* **Credential Sharing:** Sharing passwords, PINs, API keys, SSH keys, hardware tokens, or approving Multi-Factor Authentication (MFA) prompts for another person.
* **Bypassing Security Controls:** Disabling, tampering with, or attempting to bypass endpoint detection and response (EDR) agents, antivirus software, firewalls, mobile device management (MDM), or logging mechanisms.
* **Shadow IT & Unapproved Software:** Installing unlicensed software, peer-to-peer file sharing tools, browser extensions, or connecting unvetted third-party SaaS applications to corporate accounts without prior IT/GRC approval.
* **Unapproved AI Data Exposure:** Uploading, pasting, or inputting customer PII, source code, credentials, financial data, or internal documentation into public Artificial Intelligence models or unapproved LLMs.
* **Personal Cloud Exfiltration:** Forwarding corporate emails or uploading business documents to personal email accounts, personal cloud drives (e.g., personal Google Drive, Dropbox, iCloud), or unencrypted USB drives.
* **Unauthorized Security Testing:** Running port scanners, vulnerability scanners, packet capture tools, or exploitation frameworks against internal or external networks without explicit, written authorization under a scoped security engagement.
* **Unlawful or Abusive Conduct:** Accessing, storing, or transmitting illegal, pirated, defamatory, harassing, or sexually explicit material.

### 2.3 Security Hygiene Requirements
All Authorized Users must practice the following baseline security duties daily:
* **Identity & MFA Compliance:** Comply with all password complexity, rotation, and Multi-Factor Authentication (MFA) requirements detailed in the *Identity & Access Management (IAM) Standard (`AP-GOV-STD-001`)*.
* **Clear Desk & Clear Screen:** Lock workstation screens (`Win+L` or `Cmd+Ctrl+Q`) immediately upon stepping away from a desk, and lock sensitive physical documents in secure cabinets when unattended.
* **Secure Remote Connectivity:** Use the corporate VPN or Zero-Trust client whenever accessing internal company resources from public Wi-Fi or untrusted networks (airports, hotels, cafes).
* **Mandatory Incident Reporting:** Immediately report any suspected phishing email, social engineering attempt, accidental data leak, or lost/stolen device to the Security Operations team (`security@aegispay.internal`) within 1 hour of discovery.

---

## 3. GOVERNANCE AND ACCOUNTABILITY (THE ENFORCEMENT)

### 3.1 Monitoring and Privacy Notice
AegisPay reserves the legal right to monitor, inspect, log, and audit all network traffic, email communications, web browsing history, and files stored or transmitted on company-issued devices and corporate cloud accounts. Authorized Users have **no expectation of personal privacy** when using company systems or networks, to the fullest extent permitted by applicable law.

### 3.2 Policy Exceptions
If a critical business operation cannot comply with a requirement in this policy, the responsible Department Head must submit a formal **Policy Exception Request (`AP-GOV-FRM-001`)** to the GRC team. Deviations are strictly prohibited until the risk is evaluated, a Compensating Control is verified, and written approval is granted by the CISO. All approved exceptions expire automatically after a maximum of 6 months unless renewed.

### 3.3 Consequences of Violations
Compliance with this policy is a mandatory condition of employment and contract engagement. Violations will result in tiered disciplinary action proportionate to the severity and intent of the breach:
1. **Minor / First-Time Unintentional Infraction:** Mandatory remedial security training and formal written warning.
2. **Repeated or Negligent Violation:** Revocation of system privileges, suspension, or formal HR disciplinary proceedings.
3. **Severe, Reckless, or Malicious Violation:** Immediate termination of employment or vendor contract, forfeiture of access, and referral to law enforcement or civil legal counsel for prosecution.

### 3.4 User Acknowledgment and Review
This policy is reviewed and updated annually by the GRC team. Every Authorized User must sign or digitally attest to the acknowledgment statement below upon onboarding and annually thereafter.

---

### USER ACKNOWLEDGMENT SIGN-OFF
> *"I acknowledge that I have received, read, and understood the AegisPay Technologies Acceptable Use Policy (`AP-GOV-POL-001`). I agree to comply with all rules and security hygiene duties stated herein, and I understand that my activity on corporate systems is subject to monitoring and that violations may result in disciplinary action up to and including termination."*

* **Employee / Contractor Name:** `___________________________`
* **Role & Department:** `___________________________`
* **Signature / Digital Attestation:** `___________________________`
* **Date:** `___________________________`
