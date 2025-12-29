# **Waaree Energy Web Application Security Assessment**

**Assessment Performed By:** NuageCX  
**Client:** Waaree Energy  
**Month:** August  
**Year:** 2025

---

### **Client Details**

**Company Name:** Waaree Energy  
**Contact Person:** [Client Contact Person]  
**Address:** [Client Address]  
**Email:** [Client Email]  
**Telephone:** [Client Phone]

---

### **Document History**

| Version | Date       | Author       | Remark               |
|---------|------------|--------------|----------------------|
| 1.0     | 07 Aug 2025 | NuageCX Team | Document Creation    |

---

### **Table of Contents**

1. **About NuageCX**  
2. **Project Details**  
   2.1 Executive Summary  
   2.2 Scope and Objective  
   2.3 Project Timeline  
   2.4 Technological Impact Summary  
   2.5 Business Impact Summary  
   2.6 Testing Environment  
   2.7 Vulnerability Chart  
   2.8 Vulnerabilities by Category  
   2.9 Table of Findings  
   2.10 Application Strengths  
   2.11 Application Weaknesses  
3. **Technical Findings**  
   3.1 **[CRITICAL] Price Manipulation Vulnerability**  
   3.2 **[CRITICAL] Broken Access Control Leads to Unauthorized Privilege Escalation**  
   3.3 **[CRITICAL] Admin Account Takeover On Update Contact Details**  
   3.4 **[HIGH] Missing Rate Limit Checks at Login Endpoint**  
4. **We Prescribe**  
5. **Appendix**  
   5.1 References  
   5.2 Observations  
   5.3 Failed Test Cases  
   5.3.1 SQL Injections  
   5.3.2 OAuth/SSO Misconfiguration  

---

### **1. About NuageCX**

NuageCX is a research-powered security testing service organization specializing in web, mobile, cloud, and infrastructure security assessments, along with in-depth technical security training. Our state-of-the-art research, methodologies, and tools ensure the safety of our client's assets.

At NuageCX, we follow a comprehensive, risk-focused methodology to identify and remediate vulnerabilities in web applications before malicious actors can exploit them. Our approach combines rigorous manual testing (80%) with selective automated scanning (20%), ensuring that every assessment is thorough, accurate, and aligned with industry best practices.

Our goal is to simulate real-world cyberattacks using advanced techniques and tools, uncovering security weaknesses that automated scanners alone often miss. The findings are then translated into clear, actionable remediation guidance for our clients, followed by a post-patching re-test to validate that all vulnerabilities have been effectively resolved.

---

### **2. Project Details**

#### **2.1 Executive Summary**

NuageCX was engaged by **Waaree Energy** to conduct a comprehensive penetration test of the target web application from **03 Aug 2025** to **07 Aug 2025**. This engagement included **80% manual testing** and **20% automated scanning**, performed within the agreed scope.

The assessment was conducted from an external threat actor's perspective with the objective of identifying security flaws, misconfigurations, and logical vulnerabilities that could compromise confidentiality, integrity, or availability.

**Key Findings:**

- A total of **4 vulnerabilities** were identified (3 Critical, 1 High).
- Risk scores ranged from **8.4 to 8.9**.
- The most critical vulnerabilities could lead to **severe financial loss, data exposure, and reputational damage**.

Following remediation, NuageCX performed a **verification retest**, confirming that all reported vulnerabilities had been successfully fixed.

#### **2.2 Scope and Objective**

The scope of this assessment was limited to the following web application:

- **Target:** `https://shop.waaree.com`

#### **2.3 Project Timeline**

The security assessment was performed for **5 days** from **03 Aug 2025** to **07 Aug 2025**.

#### **2.4 Technological Impact Summary**

The NuageCX security team performed real-time security assessments on the web application. It was identified that the application did not implement proper server-side validation, access control, authentication mechanisms, and rate-limiting, leading to critical business risks such as price manipulation, privilege escalation, account takeover, and credential brute-forcing.

#### **2.5 Business Impact Summary**

We identified the following business impacts:

- Severe financial loss due to price manipulation.
- Unauthorized access to administrative functions.
- Account takeover via brute-force attacks.
- Loss of customer trust and regulatory non-compliance (PCI DSS, GDPR).
- Potential for large-scale fraud and inventory damage.

#### **2.6 Testing Environment**

To perform the web application assessment, we used **Burp Suite Professional** for intercepting and manipulating HTTP/HTTPS traffic. Manual exploitation techniques were applied to validate each finding.

#### **2.7 Vulnerability Chart**

| Severity   | Total | Resolved | Pending | Accepted Risk |
|------------|-------|----------|---------|---------------|
| Critical   | 3     | 0        | 0       | 0             |
| High       | 1     | 0        | 0       | 0             |
| Medium     | 0     | 0        | 0       | 0             |
| Low        | 0     | 0        | 0       | 0             |
| Info       | 0     | 0        | 0       | 0             |

#### **2.8 Vulnerabilities by Category**

- **Broken Access Control:** 2  
- **Insecure Design:** 1  
- **Identification & Authentication Failures:** 2

#### **2.9 Table of Findings**

| Vul ID | Target      | Title                                                                  | Severity | Status  |
|--------|-------------|------------------------------------------------------------------------|----------|---------|
| 1      | shop.waaree.com | Price Manipulation Vulnerability                                      | Critical | Pending |
| 2      | shop.waaree.com | Broken Access Control Leads to Unauthorized Privilege Escalation      | Critical | Pending |
| 3      | shop.waaree.com | Admin Account Takeover On Update Contact Details                      | Critical | Pending |
| 4      | shop.waaree.com | Missing Rate Limit Checks at Login Endpoint                           | High     | Pending |

#### **2.10 Application Strengths**

- The application uses HTTPS for all communications.
- Strong session management with immediate token expiration on logout.
- No SQL injection vulnerabilities were found.

#### **2.11 Application Weaknesses**

- Lack of server-side price validation.
- Missing access control checks.
- No email verification during account creation.
- Insufficient input validation and business logic flaws.
- No rate-limiting on authentication endpoints.

---

### **3. Technical Findings**

#### **3.1 [CRITICAL] Price Manipulation Vulnerability**

**Potential Impact:** HIGH  
**Description:**  
A Price Manipulation Vulnerability was discovered in the application's checkout process, allowing an attacker to alter the price of any product before payment by intercepting and modifying client-side requests.

**Affected Resources:**  
- `https://shop.waaree.com`  
- `https://shop.waaree.com/checkout`

**CVSS Score:**  
CVSS Base Score: 8.4  
CVSS Temporal Score: 7.6  
CVSS Environmental Score: 8.1

**CVSS Vector:**  
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L/E:P/RL:O/RC:C/CR:H/IR:H/AR:H/MAV:N/MAC:L/MPR:N/MUI:N/MS:U/MC:H/MI:H/MA:L

**Business Risk:**  
Severe financial loss, inventory damage, reputational harm, and PCI DSS non-compliance.

**Technical Risk:**  
Successful exploitation enables purchasing high-value products at extremely low or zero cost without detection.

**Remediation:**  
- Implement server-side price validation.  
- Use HMAC or digital signatures for parameter integrity.  
- Enable real-time fraud detection and alerting.  
- Conduct regular PCI DSS audits.

**Steps to Reproduce:**  
1. Log in with a valid user account.  
2. Add a product to cart and proceed to checkout.  
3. Intercept the request using Burp Suite.  
4. Modify price parameters (e.g., change `16389` to `1`).  
5. Complete payment at the manipulated price.

---

#### **3.2 [CRITICAL] Broken Access Control Leads to Unauthorized Privilege Escalation**

**Potential Impact:** HIGH  
**Description:**  
The application lacks proper access controls, allowing unauthorized users to escalate privileges and access administrative functions.

**Affected Resources:**  
- Admin endpoints and sensitive functionalities

**CVSS Score:**  
CVSS Base Score: 8.9  
CVSS Temporal Score: 8.0  
CVSS Environmental Score: 8.5

**CVSS Vector:**  
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H/E:P/RL:O/RC:C/CR:H/IR:H/AR:H/MAV:N/MAC:L/MPR:L/MUI:N/MS:U/MC:H/MI:H/MA:H

**Business Risk:**  
Unauthorized administrative access, data breach potential, and compliance violations.

**Technical Risk:**  
Attackers can perform actions reserved for higher-privileged users, leading to full system compromise.

**Remediation:**  
- Implement role-based access control (RBAC).  
- Validate user permissions on every request.  
- Use centralized authorization checks.

**Steps to Reproduce:**  
1. Log in as a low-privilege user.  
2. Intercept requests to admin endpoints.  
3. Modify user ID or role parameters to gain elevated access.

---

#### **3.3 [CRITICAL] Admin Account Takeover On Update Contact Details**

**Potential Impact:** HIGH  
**Description:**  
The application allows any authenticated user to update contact details of other users, including administrators, leading to account takeover.

**Affected Resources:**  
- User profile update endpoints

**CVSS Score:**  
CVSS Base Score: 8.7  
CVSS Temporal Score: 7.8  
CVSS Environmental Score: 8.3

**CVSS Vector:**  
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H/E:P/RL:O/RC:C/CR:H/IR:H/AR:H/MAV:N/MAC:L/MPR:L/MUI:N/MS:U/MC:H/MI:H/MA:H

**Business Risk:**  
Full account compromise, identity theft, and business disruption.

**Technical Risk:**  
Attackers can modify administrator contact information, leading to complete account takeover.

**Remediation:**  
- Validate that users can only modify their own profiles.  
- Implement session-based ownership checks.  
- Log all profile update attempts.

**Steps to Reproduce:**  
1. Log in as a regular user.  
2. Intercept the contact update request.  
3. Change the user ID to an admin’s ID and modify contact details.

---

#### **3.4 [HIGH] Missing Rate Limit Checks at Login Endpoint**

**Potential Impact:** MEDIUM  
**Description:**  
It has been observed during the assessment that the application does not properly implement rate-limiting on the login endpoint. This allows an attacker to brute-force the password for a known email address.

**Affected Resources:**  
- `https://shop.waaree.com/login`

**CVSS Score:**  
CVSS Base Score: 5.3  
CVSS Temporal Score: 4.8  
CVSS Environmental Score: 6.8

**CVSS Vector:**  
CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N/E:P/RL:T/RC:C/CR:H/IR:H/AR:L/MAV:N/MAC:L/MPR:N/MUI:N/MS:U/MC:L/MI:L/MA:N

**Business Risk:**  
Successful exploitation of this vulnerability allows an attacker to successfully take over a user account.

**Technical Risk:**  
An attacker can brute-force the user's credentials.

**Remediation:**  
- Add a limit on the number of unsuccessful attempts for an account within a specific time.  
- Implement CAPTCHA to prevent automated brute-force attacks (e.g., reCAPTCHA).  
- Enforce account lockout after multiple failed attempts.

**Steps to Reproduce:**  
1. Navigate to `https://shop.waaree.com/login`.  
2. Enter a known username and an incorrect password.  
3. Intercept the request using Burp Suite Proxy.  
4. Send the request to Burp Intruder.  
5. Configure payload positions on the password field.  
6. Launch a brute-force attack with a password list.  
7. Observe successful login attempts without rate-limiting or lockout.

---

### **4. We Prescribe**

| Vul ID | Recommendation |
|--------|----------------|
| 1      | Implement server-side validation, HMAC signing, and fraud monitoring. |
| 2      | Enforce RBAC and centralize authorization logic. |
| 3      | Restrict profile updates to own account only; implement audit logs. |
| 4      | Implement rate-limiting, CAPTCHA, and account lockout policies. |

**General Recommendations:**  
- Conduct secure code training for developers.  
- Perform regular security assessments and penetration tests.  
- Adopt a secure SDLC with security gates at each phase.

---

### **5. Appendix**

#### **5.1 References**  
- OWASP Top 10 2021  
- NIST SP 800-115  
- PCI DSS v4.0

#### **5.2 Observations**  
No significant operational or configuration issues were observed outside the reported vulnerabilities.

#### **5.3 Failed Test Cases**  
##### **5.3.1 SQL Injections**  
All tested endpoints were found to be protected against SQL injection attacks.

##### **5.3.2 OAuth/SSO Misconfiguration**  
The application properly handled OAuth token validation and error responses.

---

**Report End.**

---
**Confidentiality Notice:** This document is intended solely for the use of the client organization and may contain sensitive information. Unauthorized distribution is prohibited.
