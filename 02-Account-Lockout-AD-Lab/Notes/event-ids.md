# Key Event IDs – Account Lockout Lab

This document lists key Windows Event IDs relevant to account lockout investigations in Active Directory.

---

## 🔴 4740 – Account Lockout
- Triggered when a user account is locked due to repeated failed login attempts  
- Primary indicator of brute-force or repeated authentication failure activity  
- Includes details such as username and source machine  

---

## 🔴 4625 – Failed Logon
- Indicates a failed login attempt  
- May or may not appear depending on authentication method (Kerberos/NTLM)  

---

## 🔴 4776 – NTLM Authentication Failure
- Indicates failed NTLM authentication attempts  
- Alternative to Kerberos failure logs  

---

## 🟢 4624 – Successful Logon
- Indicates successful authentication  
- Useful for confirming access after lockout or recovery  

---

## 🟡 4771 – Kerberos Authentication Failure (if present)
- Indicates failed Kerberos pre-authentication attempts  
- May appear in some domain authentication scenarios  

---
