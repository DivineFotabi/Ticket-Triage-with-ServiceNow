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

# MITR ATT&CK
None

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

# MITRE ATT&CK
None

# Alert CLD-0105

From James holt, email recived from payroll@cloudora with subject "you August payslip is ready" and a clickable link. Reported medium

# Hypothesis

malicious: A phishing attempt spoofing the cloudora domain name
Benign: A payroll email from the HR.

# Evidence

From the email header confirms to be from the real domain the cloudora domain. All authentication header's pass for the cloudora.io domain name. From the recieved header, the message came from the cloudora server and was recieved by thesame cloudora server.

# Verdict

False positive

# Severity

Informational. legit internal email

# Action

Reply to james: This was a genuine mail n keep reporting anything you don't find comfortable.

# Justification

The alert was from a policy set and a proof to show the policy is working.

# MITRE ATT&CK:
None

# Alert CLD-0106

Device LDN-WS-117 with active unresolved threats. Reported medium.

# Hypothesis
malicious:The device LDN-WS-117 is compromise
Benign: Duplicated threat alert.

# Evidence
The defender daily digest for antivirus decords the same trojan : win32/ stealgen B on thesame device LDN-WS-117 at 8:00 UTC
Reported medium but re-rated Informational

# Verdict
Duplicate

# Severity
Same as CLD-0102

# Action

Duplicate and refrence to CLD-0102

# Justification
Presence of an active malware

# MITRE: Same as CLD-0102

# Alert CLD-0107

Mass deleting of files from leavers folders from the HR-Records.  Reported high

# Hypothesis

Malicious: Compromised account deleting files
Benign: Normal clean up process carried out by HR.

# Evidence

From the handover shift notes, HR runs scheduled annual retention clean up this week under tara.kemp's account in the early hours exactly when the alert fied. Activity details showed HR-Retention flow.

# Verdict

False Positive

# Severity

Reported high but re-rated informational as the activity details holds scheduled automation which was stated in the handover notes.

# Action

Close reference the retention schedule. recommend a schedule task security control while continuing to alert on deletion outside the process window.

# Justification

The file deletion action, timing, account all matches the annual schedule automation.

MITRE : None

# Alert CLD-0108
First time successful entra ID sign-in from a user gwen.muir using IMAP4, window 10. Reported low.

# Hypothesis

Malicious: Using known credential and legacy protocol to escape verification
Benign: User trying a deifferent protocol at none working hours

# Evidence

From sign -in logs the user gwem.muir signed in during working hours from macOS 14 through microsoft 365, sharepoint,outlook and not IMAP4 a legacy system. The one time succcessful login shows the credential was known and from the sign-in time the user was not aware.

# Verdict

True positive

# Severity
Reported low but re-rated to high as the logs show the user account might have been compromised

# Action
- Isolate User
- Revoke session
- Audit mail box
- Restrict Legacy sign-in
- Reset credential

# Justification

The baseline log evenys differ from the gwen's established device, mode of access and IP address differ from that use th0ugh the location matches it might be possible known credential.

# MITRE ATT&CK:
T1078.004 ( Valid account: cloudora accounts via legacy protocol to by pass MFA.

# Alert CLD-0109

Three host LDN-WS-104, MAN-LT-033 and AUS-WS-208 experincing outbound connection to 198.18.207

# Hypothesis
Malicious: Potential beaconing to 198.18.207.66 from three different offices.
Benign: Unknown agent trying to connect

# Evidence
Sign-in logs shows all three users having normal sign-in at normal office hours. No handover notes predicting the action.

# Verdict

Escalate

# Severity
Reported medium but re-rated to high as alert got alot of pending confirmation.

# Action

Escalate to VCISO immediately, stating the affected users, destination and Type of connection, time internal an the registration age of the domain

# Justification

The beaconing to 198.18.207 and the normal sign in patterns requires further investigation

# MITRE ATT&CK
Suspected T1071.001 ( Application layer protocol: web protocols) pending confirmation.

# Alert CLD-0110

Three sign-in attempts on daniel.reeve from lagos Nigeria blocked due to IP present in the tenant block list.

# Hypothesis
Malicious: Threat actor attempting known credentials.
Benign: Security control activity preventing unknown Ipaddress.

# Evidence

Sign-in logs shows the error on the daniel.reeve account and a normal sign-in during office hours. The user appears to be a target.

# Verdict
True Positive

# Severity
Reported low but re-rated to high as the logs shows a threat actor attempting authentication

# Action

Monitor the Ipaddress and escalate any successful sign-in by the Ip address. Activity reopens after containment and interest remains thesame

# Justification

The error on the attack shows credential policy is at work and kills it. No evidence of data theft.

# MITRE ATT&CK

T110.003 ( Password spraying). CLD0001 campaign continues

# Alert CLD-0111
Suspicious email recieved by user with subject overdue invoice INV-2214 with attachment. User not sure of supplier and recorded medium.

# Hypothesis

Malicious: Malicious invioce with weaponised attachment.
Benign: Supplier reminder for a transaction

# Evidence

Email header authentication header check passed for SPF, DKIM=none, DMARC=none, but this doesn't say if the mail is malicious or not. Sender's domain and IPaddress, scope, attachment content and if the linked was clicked or not can not be confirmed from the information provided.

# Verdict

Insufficient Information

# Severity
Reported medium but re-rated to high. Neither phishing or a legit mail

# Action
Verify: sender's domain, Ip address, recipient scope, attachment content and if the linked was clicked or not. Using appropraite testing environment check if the supplier is legit, avoid opening the link normally. Checked if he open on device by pulling out antivirus and end point detection status.

# Justification

Reported alerts needs further verification and confirmation.

# Alert CLD-0112

Impossible travel for Omar.farah within 42 minutes for location that is seven hours apart.

# Hypothesis
Malicious: User account is compromised
Benign: Account user might be on holidays

# Evidence
Sign-in logs shows Omar sign-in at 18:22 UTC London using a registered macOS device. First Dubai login using same device at 5:58 with the first time success. The login at 06:40 UTC London showed a non-interactive token  refresh ( possible his office desktop is reveiwing session and not human sign-in). Finally the 7:30 UTC Dubai sign-in from same MacOS device. Travel was documented in CLD-0001 already

# Verdict
False positive

# Severity

Informational, Legit travel pattern and London sign-in is not human

# Action
Closed reference CLD-0001. Recommend control to exclude non-interactive sign-in from logs.

# Justification
A real compromised user will show interaction in the login. Here all the action align a travel pattern and registered device.

# MITRE ATT&CK
None
