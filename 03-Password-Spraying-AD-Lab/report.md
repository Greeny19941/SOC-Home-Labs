# Password Spraying Investigation – Active Directory Lab

## 📌 Summary
This lab simulated a password spraying attack within an Active Directory environment. The objective was to observe how low-frequency authentication attempts across multiple user accounts appear in Windows Security logs and how this behaviour differs from traditional brute-force attacks.

---

## 🏗️ Lab Setup

This lab was conducted using the existing Active Directory environment from previous labs.

For the purpose of this simulation:
- 5 user accounts were created:
  - `user1`, `user2`, `user3`, `user4`, `user5`
- All accounts were configured with the same password

> Note: The environment was not structured into organisational units (OUs), as the focus of this lab was authentication behaviour rather than directory design.

---

## ⚔️ Attack Simulation

A password spraying attack was simulated from the client machine by attempting a single incorrect login for each user account.

- One failed login attempt per account  
- Attempts were distributed across multiple users rather than repeated on a single account  

This approach mimics real-world password spraying techniques, where attackers avoid account lockouts by limiting the number of attempts per user.

---

## 📊 Log Analysis

Logs were analysed on the Domain Controller via:

Event Viewer → Windows Logs → Security

### 🔴 Event ID: 4625 – Failed Logon

- Multiple 4625 events were observed  
- Each event corresponded to a different user account  
- All attempts originated from the same client machine  
- Events occurred within a similar timeframe  

#### Key Observations:
- Single failed authentication attempt per account  
- Multiple accounts targeted in sequence  
- No account lockouts triggered  

---

## 🧠 Analysis

The observed pattern of authentication failures differs from traditional brute-force attacks.

Instead of repeated attempts against a single account, the activity involved single failed attempts across multiple accounts. This behaviour is consistent with password spraying techniques, which are designed to avoid detection and prevent account lockouts.

By reviewing individual 4625 events and confirming that each corresponded to a different user, it was possible to identify this pattern of distributed authentication attempts.

---

## 📸 Evidence

The following screenshots are included:

- Event Viewer showing multiple Event ID 4625 failed logon attempts  
- Expanded 4625 event showing account name and source machine  
- Evidence of multiple users being targeted  

---

## 🚨 Conclusion

This lab demonstrates how password spraying attacks manifest within Active Directory environments.

Key findings:
- Multiple user accounts were targeted with single authentication attempts  
- Event ID 4625 provided clear visibility of failed logon attempts  
- No account lockouts occurred, reflecting the stealthy nature of password spraying attacks  

This highlights an important SOC principle: attackers may distribute authentication attempts across multiple accounts to avoid detection, requiring analysts to identify patterns across users rather than focusing on a single account.

---
