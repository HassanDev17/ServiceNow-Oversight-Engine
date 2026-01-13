# ServiceNow Oversight Engine — Module Scanning Plan

This document defines how each ServiceNow module will be scanned, what checks will be performed, and the metrics/output for the **ServiceNow Oversight Engine**. This forms the foundation for the **Platform Health Scanner**.

---

## 1. CMDB (`cmdb_ci*`)

**Scanner:** CMDB Scanner  

**Checks / What to Monitor:**
- Missing mandatory fields  
- Orphan or disconnected CIs  
- Stale / outdated CIs  
- Incomplete CI relationships  

**Output / Metric:**
- **CMDB Trust Score (0–100)**  
- Breakdown by CI class  
- List of top 10 high-risk CIs

---

## 2. Business Rules (`sys_script`)

**Scanner:** Business Rule Scanner  

**Checks / What to Monitor:**
- Rules with no conditions or always true conditions  
- Heavy server-side execution  
- Conflicting or redundant rules  

**Output / Metric:**
- **Business Rule Risk Score (0–100)**  
- List of top risky rules  
- Execution impact indicator

---

## 3. Client Scripts (`sys_script_client`)

**Scanner:** Client Script Scanner  

**Checks / What to Monitor:**
- Global scripts executing on all forms unnecessarily  
- OnLoad scripts with heavy processing  
- Scripts without proper UI type restrictions  

**Output / Metric:**
- **Client Script Risk Score (0–100)**  
- Top scripts impacting performance  
- Potential UX impact notes

---

## 4. Script Includes (`sys_script_include`)

**Scanner:** Script Include Scanner  

**Checks / What to Monitor:**
- Unused Script Includes  
- Missing protection policies  
- Global access that may affect security  

**Output / Metric:**
- **Script Include Risk Score (0–100)**  
- List of unprotected or risky script includes  

---

## 5. Flows / Flow Designer (`sys_flow_context`) & Scheduled Jobs (`sys_trigger`)

**Scanner:** Flow / Job Scanner  

**Checks / What to Monitor:**
- High execution frequency  
- Misconfigured triggers  
- Orphaned or inactive flows/jobs  
- Inefficient processing  

**Output / Metric:**
- **Flow / Job Execution Risk Score (0–100)**  
- List of high-risk or redundant flows/jobs  

---

## 6. Access Control Rules (`sys_security_acl`)

**Scanner:** Compliance Scanner  

**Checks / What to Monitor:**
- Overly permissive ACLs  
- Missing ACLs on critical tables  
- Redundant or inefficient ACLs  

**Output / Metric:**
- **Compliance Score (0–100)**  
- Table-level risk details  

---

## 7. Update Sets (`sys_update_set`, `sys_update_xml`)

**Scanner:** Update Set Scanner  

**Checks / What to Monitor:**
- Direct overrides of core tables  
- Untracked or unmanaged updates  
- Conflicting update sets  

**Output / Metric:**
- **Upgrade Risk Score (0–100)**  
- List of risky updates / potential conflicts  

---

## 8. Scoring Logic (Initial / Conceptual)

- **CMDB Trust Score** = (Mandatory Fields Complete % * 0.4) + (Relationships Complete % * 0.4) + (Freshness % * 0.2)  
- **Customization Risk Score** = (Business Rules Risk % * 0.3) + (Client Scripts Risk % * 0.2) + (Script Includes Risk % * 0.5)  
- **Compliance Score** = (ACL Compliance % * 0.7) + (Update Set Compliance % * 0.3)  

> These are initial conceptual weights. They will be refined once the engine is implemented and tested in the PDI instance.

---

## Notes

- Each scanner will feed results into the **Risk & Health Scoring Engine**, which aggregates scores across modules.  
- Outputs will be visualized in **dashboards** for executive, platform owner, and architect views.  
- This document will guide the implementation of **script includes, scheduled jobs, and dashboards** in later stages.
