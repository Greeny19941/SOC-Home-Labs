# Key Event IDs – Active Directory Lab

This document lists key Windows Security Event IDs used during authentication investigations.

---

## 🔴 4771 – Kerberos Pre-Authentication Failure
- Indicates failed authentication attempt in a domain environment
- Common during brute-force or password attacks
- Key indicator in Active Directory environments

---

## 🔴 4625 – Failed Logon
- Indicates a failed login attempt
- More common in local or NTLM-based authentication
- Not always present in domain (Kerberos) scenarios

---

## 🟢 4624 – Successful Logon
- Indicates a successful authentication
- Useful to identify if access was gained after failures

---

## 🟡 4740 – Account Lockout
- Triggered when too many failed login attempts occur
- Indicates account protection mechanisms are working

---

## 🟡 4776 – NTLM Authentication Failure
- Occurs during NTLM authentication attempts
- Alternative failure log to 4771 in some environments

---

## 🟡 4769 – Kerberos Service Ticket Request
- Indicates a request for access to a service
- Useful for tracking lateral movement or service access

---

## 🟡 4672 – Special Privileges Assigned
- Indicates admin-level privileges assigned at logon
- Important for detecting privileged access

---
