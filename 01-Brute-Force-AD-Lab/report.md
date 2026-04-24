# Brute Force Attack Investigation – Active Directory Lab

## 📌 Summary
A simulated brute-force attack was conducted against a domain user account within a controlled Active Directory environment. The objective was to generate failed authentication attempts and analyse how they appear in Windows Security logs from a Domain Controller perspective.

---

## 🏗️ Lab Setup

### Environment
- 2 Virtual Machines (Hyper-V):
  - Domain Controller: Windows Server 2022 (Desktop Experience)
  - Client Machine: Windows 11
 
    

### Configuration
- Active Directory Domain Services (AD DS) installed
- Domain Controller promoted with domain:
  - `lab.local`
- Test user created:
  - `testuser`

### Networking
- Client DNS configured to point to Domain Controller
- Both VMs connected via internal virtual switch
- IPv6 disabled to resolve initial connectivity issues between client and DC
- Client successfully joined to domain

---

## ⚔️ Attack Simulation

A brute-force attack was simulated from the client machine by repeatedly attempting to log in using incorrect credentials for the domain user:

- Username: `lab\testuser`
- Multiple incorrect password attempts were entered within a short timeframe
- Followed by a successful login attempt

---

## 📊 Log Analysis

Logs were analysed on the Domain Controller via:

- Event Viewer → Windows Logs → Security
- Audit logging enabled for:
  - Success
  - Failure

---

### 🔴 Event ID: 4771 – Kerberos Pre-Authentication Failure

- Multiple 4771 events were observed
- These indicate failed authentication attempts using Kerberos
- Occurred in rapid succession within seconds:

Example timestamps:
- 07:34:11  
- 07:34:14  
- 07:34:17  
- 07:34:20  
- 07:34:28  

#### Key Observations:
- Repeated failures targeting authentication  
- Very short time intervals between attempts  
- Consistent with brute-force behaviour  

---

### 🟢 Event ID: 4624 – Successful Logon

- A successful login event was recorded following failed attempts  
- Confirms that valid credentials were eventually used  

---

## 🧠 Analysis

The pattern of repeated authentication failures (Event ID 4771) within a short timeframe indicates a brute-force attack attempt against a domain account.

The presence of a subsequent successful login (Event ID 4624) demonstrates how attackers may eventually gain access if correct credentials are guessed or known.

Although the username is not always explicitly shown in 4771 events, the frequency, timing, and source system provide sufficient evidence of suspicious authentication behaviour.

---

## 🚨 Conclusion

This lab demonstrates how brute-force attacks manifest within Active Directory environments using Kerberos authentication.

Key takeaways:
- Event ID 4771 is a primary indicator of failed authentication attempts in domain environments  
- Repeated failures in short intervals indicate brute-force activity  
- Event correlation (failures followed by success) is key in SOC investigations  

---

## 📸 Evidence

- Multiple Event ID 4771 failures  
- Example Event ID 4771 details  
- Event ID 4624 successful login  

---
