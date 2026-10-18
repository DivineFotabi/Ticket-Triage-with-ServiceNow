## Ticket-Triage-with-ServiceNow

## Objective
I built a live ticket queue in serviceNow and imported a live alert to it. I worked the mixed with explanation, evidence, severity over time. Noticed and active credential stealer and contained it, clear the false positive with proof.

## Skill Learned
-  Alert Triage
-  severity assessment (impact x confidence)
-  True vs False positive
-  Judgment
-  Duplicate handling
-  Escalation discipline
-  Evidence pivoting
-  Verdict writing
-  ServiceNow fundamentals (import sets, incidents, work notes, resolution
-  MITRE ATT&ck mapping
- 

## Tools 
- ServiceNow
- Sign-in Logs
- MITRE ATT&CK Framework
- Header analysis

## Setup/ Steps
- Imported the live tickets.
- I Wrote the alert.
- I wrote the verdict.
- Wrote the severity and where I Overruled the report.
- Action taken, close, escalate or gather more information, monitor.
- Justification.


<img width="2071" height="1345" alt="image" src="https://github.com/user-attachments/assets/6e6ceb90-6d1d-4c7a-b9d8-2733a698e90e" />

AV. Detection

<img src= "https://github.com/DivineFotabi/Ticket-Triage-with-ServiceNow/blob/02a771d2521180d9e62284923c35874a5011f080/av%20detection.png" />

Handover Notes

<img src= "https://github.com/DivineFotabi/Ticket-Triage-with-ServiceNow/blob/2d8464576ba2551007a14c71150ae18be7e09927/Handover%20Notes.png" />

## Triage Verdict

# Alert CLD-0101: 

Multiple authentication entra Id failures for SVC-backup between 23:41 and 00:03 UTC followed by a successful sign-in at 00:14 UTC. Reported high

# Hypothesis

Malicious: Multiple brute force attempts on svc-backup account
Benign: Backup platform credential rotation running

# Evidence

From Handover Notes the activity CHG-2088 mentioned a backupcredential running at the same time interval of the alert with brief authentication failures. The sign-in logs shows source LDN-SRV-BK1 ( 203.0.113.20 ) is and internal host server address

# Verdict

False Positive

# Severity

Reported high was re-rated Informational. Activity was scheduled at the expected time interval.

# Action

Closed with reference CHG-2008 and recommend reviewing the login flow and implimenting clear error handling and security controls during scheduled passwords rotations.

# Justification

Source host, alert time, all matches on the handover notes. A brute force attempt is not initiated by by the internal server and cannnot end immediately as the password rotation occured. 

# Alert CLD-0102

Trojan Win32/stealgen.B ( credential stealer ) detected on user ( liam.doyle ) followed by faile quarantine each time and recreates itself. Reported high

# Hypothesis

Malicious: Credential stealer malware installed on user liam. doyle machine and recreats as a means to stay in the system.
Benign: Alert about and already treated problem.

# Evidence

Detection Av logs shows that a clean scan completed at 22:14 UTC , second scan logs shows the presence of a trojan in the APPdata folder as an executable file ( wsync.exe) with a failed quarantine and file in use. The access denied log at 2:27 UTC and a subsequent recreation of the file as wsync_upd.exe at 2:41 UTC and file becomes in use again in the same folder.No such activity in the handover notes and no suspicious login from user.

# Verdict

True Positive

# Severity

 Sev 2. File recreating faster than the antivirus can kill it.

 # Action

 - Isolate the user
 - Revoke session
 - Restrict the User
 - Eradicate the malware
 - Change login credentials of the user

# Justification

Multiple quarantine failures and file recreation shows the presence of a malware in action.

# MITRE ATT&CK

T1204.002 ( User execution : Malicious file ) 

# Alert CLD-0103

Probed 4000+ TCP port scan across 180 internal host between 22:10 and 02:05 UTC

# Hypothesis

malicious: Identification of entry point for exploitation.
Benign: Routine testing carried out by the administrator.

# Evidence
Handover schedule scan activity on the network at thesame time of the alert on all offices and source address matches. No activity of data moving hence scanner behavior.

# verdict

False positive

# serverity

Reported medium but re-rated informational. Scheduled activity recorded.

# Action

Close reference schedule scan. Recommend security controls during approved or authorised scans

# Justification
Host, action, address and time matches the scheduled action of weekly scan. No data moving indicates scanner behavior.

# Alert CLD-0104

Five MFA failures for a user and followed by a successful sign-in at 6:52 UTC and a new device register for authentication.

# Hypothesis
Malicious: MFA attempts on user
Benign: Company policy on staff for new devices, lockout and travel.

# Evidence:
Sign-in logs shows all events came thesame source 198.51.100.22 from usual device. Helpdesk ticket raised at 7.05 HD-4471 and Handover notes shows a Helpdesk activity that states staff shouls contact helpdesk incase of new device.

# verdict
False Positive

# Severity
Reported medium but re-rated informational as the action was stated in the handovershift notes.

# Action
close with reference Helpdesk and ticket reference HD.

# Justification

Ticket referenced, action time and account matches the Helpdesk notes. Event matches baseline and shows a users fighting her own authentication.
