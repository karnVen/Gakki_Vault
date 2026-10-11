# Unit IV: Software Quality Assurance & 11-Step Process
**Subject:** Software Testing Concepts (`BCAFSCO502T23`)  
**Target:** BCA Semester V Examination  

---

## 1. Software Quality Assurance (SQA)

> **Definition:** Software Quality Assurance is a planned and systematic pattern of all actions necessary to provide adequate confidence that an item or product conforms to established technical requirements.

### Quality Control (QC) vs. Quality Assurance (QA):

| Factor | Quality Assurance (QA) | Quality Control (QC) |
| :--- | :--- | :--- |
| **Focus** | Process-oriented (prevent defects). | Product-oriented (identify defects). |
| **Action** | Proactive (defines standards, audits). | Reactive (executes tests on software). |
| **Responsibility**| Entire engineering & process team. | Dedicated testing team. |
| **Activity** | Process definition, quality audits, tool selection.| Unit testing, functional testing, bug reporting. |

---

## 2. William Perry's Eleven-Step Testing Process (Guaranteed 10-Mark Question)

Dr. William E. Perry outlined an 11-step methodology covering testing throughout the entire software lifecycle:

```
┌────────────────────────────────────────────────────────────────────────┐
│             William Perry's 11-Step Software Testing Process           │
├────────────────────────────────┬───────────────────────────────────────┤
│ 1. Assess Development Plan     │ Review requirements and methodologies │
│ 2. Baseline Test Plan          │ Create test objectives and estimates  │
│ 3. Validate Requirements       │ Check testability and ambiguity       │
│ 4. Validate System Design      │ Verify architectural & DB flow        │
│ 5. Validate Program Design     │ Inspect detailed LLD and class logic  │
│ 6. Execute Tests & Validate    │ Perform dynamic functional testing    │
│ 7. Verify Post-Implementation  │ Test post-install configuration & ops │
│ 8. Analyze & Report Tests      │ Log defect density and pass/fail rate │
│ 9. Install Software Changes    │ Verify fixes without regression       │
│ 10. Final Verification         │ Acceptance testing & sign-off         │
│ 11. Evaluate Testing Process   │ Retrospective & process refinement    │
└────────────────────────────────┴───────────────────────────────────────┘
```

### Detailed Breakdown of the 11 Steps:
1. **Assess Development Plan & Status:** Evaluate the project scope, technical stack, and risks before testing begins.
2. **Develop the Test Plan:** Formulate schedules, resource allocations, hardware lab prerequisites, and entry/exit criteria.
3. **Test Software Requirements:** Verify requirements for completeness, clarity, testability, and traceability.
4. **Test Software Design:** Review high-level and detailed architectural models to catch design defects before coding starts.
5. **Test Program Design & Implementation:** Review source code via static analysis, code walkthroughs, and peer inspections.
6. **Execute Tests & Validate Software:** Run black-box, white-box, and regression suites; log bugs in defect tracking tools.
7. **Verify Post-Implementation Operations:** Validate system parameters, batch jobs, and database migrations in staging environments.
8. **Analyze and Report Test Results:** Collate metrics (defect severity, test execution velocity) into management reports.
9. **Test Software Changes (Regression Testing):** Verify bug fixes and ensure unchanged modules continue to function properly.
10. **Final Verification & Production Release:** Conduct business sign-offs and verify release candidate deployment readiness.
11. **Evaluate Test Process Effectiveness:** Document lessons learned and update testing guidelines for future project cycles.

---

## 3. Test Optimization Techniques

* **Combinatorial Testing (Orthogonal Arrays):** Maximizes test coverage while dramatically minimizing the total number of test pairs.
* **Risk-Based Testing:** Allocates test execution effort based on high-impact business transactions.
* **Automated Regression Selection:** Selects only the subset of test cases affected by recent git commit code diffs.

---

## 4. Software Security Testing

### Core Principles of Security (CIA Triad):
1. **Confidentiality:** Data is accessible only to authorized entities.
2. **Integrity:** Information cannot be tampered with or modified without authorization.
3. **Availability:** Systems remain responsive and operational for legitimate users.

### Security Testing Methods:
* **Vulnerability Scanning:** Automated scanners (OWASP ZAP, Nessus) scan for known CVE security weaknesses.
* **Penetration Testing (Ethical Hacking):** Simulated real-world attacks to identify exploit paths.
* **Static Application Security Testing (SAST):** Scans source code for vulnerabilities (SQL Injection, XSS, Buffer Overflow) without executing the code.
* **Dynamic Application Security Testing (DAST):** Tests running web services from the outside against malicious payloads.

---

## 5. University Model Questions
1. **(5 Marks)** Differentiate between Quality Assurance and Quality Control.
2. **(10 Marks)** Describe William Perry's 11-step testing process in sequential order.
3. **(5 Marks)** Explain the CIA triad and why security testing is mandatory in web applications.
