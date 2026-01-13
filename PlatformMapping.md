# ServiceNow Oversight Engine — Platform Capability Mapping

This document maps the key ServiceNow modules, tables, and system areas that the **ServiceNow Oversight Engine** will monitor and analyze for platform health, governance, and compliance.

---

## 1. CMDB (cmdb_ci*)

**Purpose:** Stores all configuration items (CIs) and their relationships.  

**Why it matters:** CMDB is the backbone of the platform. Inaccurate or incomplete data leads to poor decision-making, compliance issues, and upgrade risks.  

**Key Risks to Monitor:**
- Missing mandatory CI fields  
- Orphan or disconnected CIs  
- Stale or outdated data  
- Incomplete relationships between CIs  

---

## 2. Business Rules (sys_script)

**Purpose:** Server-side automation triggered by database operations.  

**Why it matters:** Improperly designed business rules can degrade performance, cause unexpected behavior, or create maintenance challenges.  

**Key Risks to Monitor:**
- Rules with no conditions or always true conditions  
- Heavy or inefficient server-side processing  
- Overlapping or conflicting rules  

---

## 3. Client Scripts (sys_script_client)

**Purpose:** Client-side logic executed on forms and UI pages.  

**Why it matters:** Can affect user experience, page load times, and create security or data consistency issues.  

**Key Risks to Monitor:**
- Global scripts running on all forms unnecessarily  
- OnLoad scripts with heavy processing  
- Scripts without proper UI type restrictions  

---

## 4. Script Includes (sys_script_include)

**Purpose:** Reusable server-side code for automation and APIs.  

**Why it matters:** Unused or unsafe code increases maintenance complexity and may introduce security risks.  

**Key Risks to Monitor:**
- Script Includes without protection policies  
- Unused or redundant code  
- Global access that can affect security  

---

## 5. Flows / Flow Designer (sys_flow_context)

**Purpose:** Automations and workflows created in Flow Designer.  

**Why it matters:** Misconfigured flows can cause performance issues, duplicated work, or unexpected triggers.  

**Key Risks to Monitor:**
- Flows with high execution frequency  
- Inefficient triggers causing performance lag  
- Orphaned flows no longer in use  

---

## 6. Update Sets (sys_update_set, sys_update_xml)

**Purpose:** Track and manage customizations and configuration changes.  

**Why it matters:** Critical for upgrade readiness and governance; improper update sets can cause conflicts or system instability.  

**Key Risks to Monitor:**
- Direct core table overrides  
- Untracked or unmanaged updates  
- Conflicting update sets  

---

## 7. Scheduled Jobs (sys_trigger)

**Purpose:** Recurring server-side scripts and scheduled automation.  

**Why it matters:** Poorly designed jobs can degrade system performance or cause unexpected downtime.  

**Key Risks to Monitor:**
- Jobs running too frequently or redundantly  
- Jobs without proper error handling  
- Orphaned or inactive scheduled jobs  

---

## 8. Access Control Rules (sys_security_acl)

**Purpose:** Define platform security and data access rules.  

**Why it matters:** Overly broad or missing ACLs create compliance and security risks.  

**Key Risks to Monitor:**
- ACLs with overly permissive conditions  
- Missing ACLs on critical tables  
- Inefficient or redundant ACL rules  

---

## Notes

This mapping will serve as the **blueprint for all scanning and analytics modules** in the ServiceNow Oversight Engine. Each module’s risk areas will feed into:

- **Health Score calculation**  
- **Risk Score evaluation**  
- **Dashboard visualization**  
- **Remediation guidance and governance reporting**
