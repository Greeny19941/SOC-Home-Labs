# Account Lockout Investigation – Active Directory Lab

## 📌 Summary
A simulated account lockout scenario was conducted within a controlled Active Directory environment. The objective was to observe how repeated failed authentication attempts lead to account lockout and how this is reflected in Windows Security logs on the Domain Controller.

---

## 🏗️ Lab Setup and Configuration

This lab was built on top of an existing Active Directory environment (Lab 1).

To configure account lockout behaviour, the following changes were made in the Default Domain Policy:

Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy

The following settings were applied:
- Account lockout duration: 15 minutes  
- Account lockout threshold: 5 invalid login attempts  
- Reset account lockout counter after: 15 minutes  

After configuration, the policy was applied using:
- `gpupdate /force`

---

## ⚔️ Attack Simulation

The simulation was performed from the client machine by intentionally entering incorrect credentials for the domain user account:

- Username: `lab\testuser`  
- 5 consecutive invalid password attempts were made  

This triggered the account lockout policy configured on the domain.

---

## 📊 Log Analysis

Logs were reviewed on the Domain Controller via:

Event Viewer → Windows Logs → Security

The primary event observed was:

### 🔴 Event ID: 4740 – Account Lockout

- This event confirmed that the account was locked out due to repeated failed authentication attempts
- The event included:
  - Target user account (`testuser`)
  - Source machine (client system)

---

## 🧠 Observations and Investigation Notes

During analysis, expected “build-up” authentication failure logs (such as repeated 4771 events) were not clearly visible in a sequential pattern.

This is a common behaviour in Active Directory environments for several reasons:

- Authentication failures may be processed using different authentication paths (Kerberos or NTLM), meaning events may not always appear as a clean, repeated sequence.
- Some failed authentication attempts are aggregated or processed at the domain controller level without producing clearly visible repeated event entries in Security logs.
- Once the account reaches the lockout threshold, Windows prioritises the lockout event (4740), which becomes the primary visible indicator of the attack outcome.

Therefore, while repeated failed login attempts were successfully executed from the client, the Security logs did not present a clearly visible step-by-step “build-up” sequence. Instead, the final lockout event (4740) served as the definitive indicator of repeated authentication failure activity.

---

## 🚨 Conclusion

This lab demonstrates how Active Directory account lockout mechanisms respond to repeated failed authentication attempts.

Key findings:
- Account lockout policy successfully triggered after 5 failed login attempts  
- Event ID 4740 confirmed enforcement of security controls  
- Failed authentication “build-up” logs may not always appear clearly due to how Windows processes authentication events  

This highlights an important SOC concept: analysts must often correlate outcomes (such as account lockouts) rather than relying on perfectly sequential log evidence.

---
