# POLICY EXCEPTION & RISK WAIVER REQUEST FORM

| Document Metadata | Details |
| :--- | :--- |
| **Form ID** | `AP-GOV-FRM-001` |
| **Parent Documents** | `AP-GOV-POL-001 | AP-GOV-STD-001 | AP-GOV-PRO-001` |
| **Version** | `1.0 (Approved Template + Sample Completed Record)` |
| **Effective Date** | `November 15, 2026` |
| **Governance Owner** | `Governance, Risk & Compliance (GRC) Lead` |
| **Framework Mapping** | `ISO/IEC 27001:2022 (Clause 6.1.3, A.5.1) | NIST SP 800-53 (CA-6, PM-9) | PCI-DSS v4.0 (Appendix B - Compensating Controls)` |

---

## 1. EXCEPTION GOVERNANCE RULES
1. **No Silent Non-Compliance:** No business unit, engineer, or vendor may deviate from an AegisPay Policy, Standard, or Procedure SLA without an approved Exception Waiver on file.
2. **Time-Bound Validity:** Exceptions are **never permanent**. A waiver may be granted for a maximum of **180 days (6 months)**, after which the system must either achieve full compliance or undergo formal CISO re-evaluation.
3. **Mandatory Compensating Controls:** An exception request will be automatically rejected unless accompanied by a verified **Compensating Control** that reduces the likelihood or impact of exploitation during the waiver window.

---

## 2. LIVE COMPLETED EXAMPLE (EXCEPTION RECORD #EX-2026-004)

### SECTION A: REQUESTOR & ASSET DETAILS
| Field | Details |
| :--- | :--- |
| **Exception Tracking ID** | `EX-2026-004` |
| **Date Submitted** | `November 15, 2026` |
| **Requested Expiration Date** | `March 15, 2027 (120 Days)` |
| **Requesting Business Unit** | `Core Payment Operations & Infrastructure` |
| **System / Asset Owner** | `Tunde Bakare (VP of Engineering)` |
| **Affected Asset(s) & Hostname** | `Legacy Reconciliation Server (PRD-WIN2016-BILL01 / 10.20.4.18)` |
| **Asset Criticality (FIPS 199)** | `HIGH (Processes daily merchant settlement files)` |

---

### SECTION B: NON-COMPLIANCE & BUSINESS JUSTIFICATION
| Field | Details |
| :--- | :--- |
| **Standard / Policy Violated** | 1. `AP-GOV-STD-001 (Section 3 & 4)`: Mandatory 14-character password & MFA requirement.<br>2. `AP-GOV-PRO-001 (Section 2)`: Critical OS patch SLA (14 days for internal systems). |
| **Description of Non-Compliance** | The legacy merchant settlement application running on `PRD-WIN2016-BILL01` uses a hardcoded proprietary authentication module that truncates passwords at 10 characters and does not natively support SAML/MFA. Additionally, applying the November Windows cumulative kernel patch caused the settlement service to crash in staging. |
| **Business Justification (Why We Cannot Comply Immediately)** | Shutting down `PRD-WIN2016-BILL01` or forcing the kernel patch would halt daily merchant payouts worth ~$1.2M/day. Engineering is actively migrating this service to a modern containerized microservice on AWS, scheduled to go live on **March 1, 2027**, at which point this legacy server will be permanently decommissioned. |

---

### SECTION C: RISK ANALYSIS & COMPENSATING CONTROLS (FILLED BY GRC & SECOPS)
| Assessment Dimension | Details |
| :--- | :--- |
| **Inherent Risk (Without Controls)** | **CRITICAL (Likelihood: 4/5, Impact: 5/5 = Score 20/25)**<br>An attacker who compromises internal network credentials could brute-force the 10-character login or exploit the unpatched kernel vulnerability to alter merchant payout records. |
| **Mandatory Compensating Controls Implemented** | To mitigate risk during the 120-day migration window, SecOps has implemented and verified the following **4 layered compensating controls**:<br>1. **Network Micro-Segmentation:** Isolated `10.20.4.18` into a restricted VLAN; blocked all inbound SMB/RDP traffic except from a single hardened Jump Host.<br>2. **MFA Enforcement at the Jump Host (Bastion):** Engineers cannot reach `PRD-WIN2016-BILL01` directly; they must first authenticate to the Bastion Host using a 16-character password + **FIDO2 Hardware MFA**.<br>3. **Virtual Patching / IPS Signature:** Enabled deep packet inspection on the internal firewall to block exploit payloads targeting the unpatched kernel CVE.<br>4. **Enhanced SIEM Alerting:** Configured high-priority Wazuh/SIEM alerts for any failed login attempt or new process creation (`Event ID 4625 / 4688`) on this host. |
| **Residual Risk (After Compensating Controls)** | **MEDIUM (Likelihood: 2/5, Impact: 4/5 = Score 8/25)** |
| **Risk Register & POA&M Link** | Logged as Risk ID `RR-2026-019` and tracked on POA&M ID `POAM-008` (Decommission server by March 1, 2027). |

---

### SECTION D: FORMAL GOVERNANCE SIGN-OFF (ACCOUNTABILITY)

> *"By signing below, the Business Owner accepts responsibility for maintaining the compensating controls and meeting the remediation deadline, and the Chief Information Security Officer formally accepts the Residual Risk on behalf of AegisPay Technologies until the expiration date."*

| Role | Name | Decision | Signature & Timestamp |
| :--- | :--- | :--- | :--- |
| **System / Business Owner** | `Tunde Bakare, VP of Engineering` | **Submitted & Agreed** | *Signed via Jira Service Desk — 2026-11-15* |
| **GRC Risk Reviewer** | `Christopher Chiwa, GRC Lead` | **Compensating Controls Verified** | *Signed via GRC Portal — 2026-11-15* |
| **Executive Risk Approver** | `Chief Information Security Officer (CISO)` | **APPROVED (Expires 2027-03-15)** | *Signed via DocuSign — 2026-11-15* |
