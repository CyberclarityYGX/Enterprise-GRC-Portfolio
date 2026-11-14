# IDENTITY, ACCESS MANAGEMENT (IAM) & PASSWORD STANDARD

| Document Metadata | Details |
| :--- | :--- |
| **Document ID** | `AP-GOV-STD-001` |
| **Parent Policy** | `Acceptable Use Policy (AP-GOV-POL-001)` |
| **Version** | `1.0 (Approved)` |
| **Effective Date** | `November 13, 2026` |
| **Review Cycle** | `Annual` |
| **Standard Owner** | `Governance, Risk & Compliance (GRC) Lead` |
| **Executive Approver** | `Chief Information Security Officer (CISO)` |
| **Classification** | `Internal` |
| **Framework Mapping** | `ISO/IEC 27001:2022 (A.5.15, A.5.16, A.5.17, A.5.18, A.8.2, A.8.5) | NIST SP 800-53 (AC-2, IA-2, IA-5) | NIST SP 800-63B | PCI-DSS v4.0 (Req 7, Req 8)` |

---

## 1. PURPOSE AND SCOPE

### 1.1 Purpose
While the Acceptable Use Policy (`AP-GOV-POL-001`) establishes high-level behavioral expectations, this Standard defines the **mandatory technical parameters, configuration baselines, and operational SLAs** for managing digital identities, authentication, and access control across AegisPay Technologies.

### 1.2 Scope
This Standard applies to all IT administrators, cloud engineers, system owners, and users across all AegisPay environments, including:
* Corporate Identity Providers (Active Directory / Microsoft Entra ID / SSO)
* Production & Non-Production Cloud Infrastructure (AWS / Azure / GCP)
* Source Code Repositories & CI/CD Pipelines (GitHub / GitLab)
* Internal Databases, ERP/Financial Systems, and Corporate VPN/Wi-Fi (802.1X)

---

## 2. USER IDENTITY LIFECYCLE (JOINER, MOVER, LEAVER)

All user access must be governed by the **Principle of Least Privilege** (users are granted only the minimum permissions required to perform their job role) and **Role-Based Access Control (RBAC)**.

| Lifecycle Stage | Mandatory Technical & Operational Standard | Target SLA |
| :--- | :--- | :--- |
| **1. Joiner (Onboarding)** | • Accounts may only be provisioned upon receipt of a verified HR onboarding ticket.<br>• Manager approval is required for any permissions beyond the baseline birthright role.<br>• Every human user must be assigned a unique User ID (`firstname.lastname`). **Shared or generic accounts (`admin`, `guest`, `finance-team`) are strictly prohibited.** | Prior to Day 1 orientation |
| **2. Mover (Role Transfer)** | • When an employee changes departments or roles, their existing permissions must be reviewed.<br>• **Anti-Privilege Creep Rule:** Previous department access must be revoked within 24 hours of the role transition unless explicitly re-approved in writing. | Within **24 hours** of transfer |
| **3. Leaver (Involuntary Termination)** | • For high-risk or involuntary terminations, HR must notify IT/Security prior to or during the exit meeting.<br>• All SSO, Active Directory, VPN, email, and cloud sessions must be disabled and active tokens revoked immediately. | Within **1 hour** of notification |
| **4. Leaver (Voluntary Resignation)** | • All logical access across corporate and production systems must be disabled upon the employee's final working hour.<br>• Inactive accounts with no login activity for **45 consecutive days** must be automatically disabled. | Within **24 hours** of final day |

---

## 3. PASSWORD & AUTHENTICATION PARAMETERS

Technical authentication configurations across all Identity Providers (IdP), operating systems, and applications must enforce the following exact parameters aligned with **NIST SP 800-63B** and **PCI-DSS v4.0**:

| Parameter | Standard User Accounts | Privileged / Admin Accounts | Service / API Accounts |
| :--- | :--- | :--- | :--- |
| **Minimum Length** | **14 characters** (Passphrases encouraged) | **16 characters** | **32+ characters** (Randomly generated) |
| **Complexity** | Uppercase, lowercase, numeric, and special characters permitted | Uppercase, lowercase, numeric, and special characters required | Cryptographic API keys / Managed Identities preferred over passwords |
| **Breached Password Check** | Mandatory block against known compromised password lists (e.g., HaveIBeenPwned / Entra Password Protection) | Mandatory block against compromised password lists | N/A |
| **Maximum Password Age (Rotation)** | **No periodic expiration** (Rotation only forced upon suspected compromise, per NIST SP 800-63B) | **Every 90 days** (Unless managed via automated PAM vault rotation) | **Every 90 days** (Automated key/secret rotation) |
| **Password History** | Remember last **12 passwords** | Remember last **24 passwords** | N/A |
| **Account Lockout Threshold** | **5 invalid attempts** | **3 invalid attempts** | Alert triggered to SOC on 3 failed auth attempts |
| **Lockout Duration** | **30 minutes** (or manual IT unlock after identity verification) | Manual unlock by Security Operations only | N/A |
| **Session Idle Timeout** | **15 minutes** (Screen lock / Re-authentication required) | **10 minutes** (Session termination) | Token TTL $\le$ **1 hour** |

---

## 4. MULTI-FACTOR AUTHENTICATION (MFA) STANDARD

### 4.1 Mandatory MFA Enforcement
Multi-Factor Authentication (MFA) is **mandatory (100% enforcement)** for:
1. All remote access and VPN connections.
2. All cloud management consoles (AWS, Azure, M365, Google Workspace) and source code repositories (GitHub).
3. All Privileged / Administrative accounts (both internal and remote).
4. Any access to systems storing, processing, or transmitting Confidential or Customer PII/Financial data.

### 4.2 Approved vs. Prohibited MFA Factors
* **Approved MFA Methods:**
  * Phishing-resistant **FIDO2 / WebAuthn Hardware Security Keys** (e.g., YubiKey) — *Mandatory for all Production Cloud Admins and Domain Admins.*
  * Time-based One-Time Passwords (**TOTP**) via approved Authenticator Apps (Microsoft Authenticator, Google Authenticator, Okta Verify) with Number Matching enabled.
* **Prohibited MFA Methods:**
  * **SMS Text Messages, Voice Calls, and Email OTPs are strictly prohibited** for corporate authentication due to vulnerability to SIM-swapping, SS7 interception, and phishing.

---

## 5. PRIVILEGED ACCESS MANAGEMENT (PAM) & NETWORK ACCESS

### 5.1 Dual-Account Rule for Administrators
System Administrators, Database Administrators (DBAs), Cloud Engineers, and Security Analysts must never use their privileged account for daily tasks (email, web browsing, Slack).
* **Standard Account (`c.chiwa@aegispay.com`):** Used for email, productivity, and general workstation login. Zero admin rights.
* **Privileged Account (`adm-c.chiwa@aegispay.com`):** Used strictly for elevating privileges, server administration, and production changes. Isolated from external email and internet browsing.

### 5.2 Just-In-Time (JIT) Access & Default Password Removal
* Standing administrative access to production databases and cloud environments should be replaced with **Just-In-Time (JIT)** elevation (granted for a maximum window of 4 hours per approved ticket).
* All vendor-supplied **default passwords** and default SNMP community strings on routers, firewalls, databases, and IoT devices must be changed prior to connecting the asset to any AegisPay network.

### 5.3 Wireless (Wi-Fi) & BYOD Authentication
* **Corporate Production Wi-Fi:** Must use **WPA3-Enterprise (802.1X)** authenticating via RADIUS against the corporate Identity Provider using device certificates. Shared Pre-Shared Keys (PSK) are prohibited on corporate VLANs.
* **Guest Wi-Fi:** Must be logically segmented on an isolated VLAN with zero routing access to internal corporate networks.
* **BYOD Conditional Access:** Personal devices may only access corporate SaaS apps (email/Slack) if enrolled in Mobile Application Management (MAM), verified with biometric/PIN screen lock, and disallowing local downloads of corporate data.

---

## 6. USER ACCESS REVIEWS (UAR) & AUDIT LOGGING

To prevent unauthorized access accumulation, System Owners and GRC must conduct formal **User Access Reviews (Attestations)** according to the following schedule:

| System Tier | Review Frequency | Reviewer | Required Audit Evidence |
| :--- | :--- | :--- | :--- |
| **Tier 1: Critical / Production / Privileged (AWS, Prod DBs, Domain Admins, Financial ERP)** | **Quarterly (Every 90 Days)** | System Owner + CISO / GRC | Exported user permission list, signed reviewer attestation, and revocation tickets for any removed access. |
| **Tier 2: Standard Corporate Apps (CRM, HRIS, Internal Wikis, GitHub Standard Users)** | **Semi-Annually (Every 180 Days)** | Department Heads | Signed access review spreadsheet and IT removal confirmation. |

---

## 7. EXCEPTIONS AND NON-COMPLIANCE
Any legacy application or third-party appliance that cannot technically meet the parameters in Section 3 or Section 4 (e.g., an older billing system that only supports 8-character passwords or lacks native MFA) must:
1. Be documented on an approved **Policy Exception Waiver (`AP-GOV-FRM-001`)**.
2. Be placed behind a **Compensating Control** (such as an isolated network VLAN and an MFA-protected Jump Host / Bastion Server).
