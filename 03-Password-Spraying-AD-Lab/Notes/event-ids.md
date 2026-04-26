# Key Event IDs – Password Spraying Lab

This document lists key Windows Security Event IDs relevant to password spraying investigations in Active Directory environments.

---

## 🔴 4625 – Failed Logon
- Indicates a failed authentication attempt  
- Primary event used to detect password spraying activity  
- Useful for identifying multiple failed attempts across different user accounts  

---

## 🟢 4624 – Successful Logon
- Indicates successful authentication  
- Can be used to determine if access was eventually gained  

---

## 🟡 4776 – NTLM Authentication Failure
- Indicates failed NTLM authentication attempts  
- May appear instead of 4625 depending on authentication method  

---

## 🟡 4768 / 4769 – Kerberos Authentication Events
- Related to ticket granting and service access  
- Can help identify authentication activity patterns in domain environments  

---

## 🔴 Detection Insight
Password spraying is typically identified by:
- Low number of attempts per account  
- Multiple accounts targeted  
- Same source system  
- No account lockouts triggered  

---
