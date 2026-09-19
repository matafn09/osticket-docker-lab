# osTicket Lab: Test Ticket Log

These are lab scenarios written to practice the full help desk ticket lifecycle in osTicket (intake, triage, assignment, internal notes, replies, resolution). Users are fictional and the actions described are simulated.

**Priorities:** osTicket's default levels are Low, Normal, High and Emergency.

**How to use this file:** For each ticket, paste the *Internal note* into **Post Internal Note** and the *Reply* into **Post Reply**. Each scenario below has a ready-to-paste internal note and reply.

## Lab status (what I actually did)

| Ticket | Requester | Subject | Priority | Assigned to | Status |
|---|---|---|---|---|---|
| 611545 | Jonathan Crawford | Locked out of account after failed logins | High | - | Closed |
| 526366 | Trevor Murray | Suspicious email reported (phishing) | High | - | Closed (transferred to Support) |
| 189852 | Louise Watson | Laptop won't boot, possible drive failure | Normal | Joseph Clark | Open |
| 123333 | Noah Kim | New hire starting Monday needs accounts and equipment | Normal | Joseph Clark | Open |
| 761977 | Olivia Brown | Request to install Adobe Acrobat Pro | Normal | - | Open |
| - | Gregory Smith | Submitted through the portal | - | - | Open, not yet worked |

Six test tickets were submitted, two were assigned to a second staff account, and two were resolved with staff replies. The rest were left open. The scenario library below includes extra scenarios I have not run.

## Scenario library

Planned outcomes for each scenario. Only the boxes ticked in **Done** were completed in the lab.

| # | Requester | Subject | Priority | Root cause | Outcome | Planned status | Done | Time to resolve |
|---|---|---|---|---|---|---|---|---|
| 1 | Jonathan Crawford | Locked out of account after failed logins | High | Lockout policy triggered by repeated failed logins | Account unlocked, temp password issued | Resolved | [x] | |
| 2 | Marcus Johnson | Forgot my password and reset email never arrives | Low | Reset email sent to an old address on file | Address corrected, password reset | Resolved | [ ] | |
| 3 | Priya Patel | Laptop can't connect to office Wi-Fi | Normal | Stale Wi-Fi profile after a Windows update | Network forgotten and rejoined, IP renewed | Resolved | [ ] | |
| 4 | David Okafor | Computer extremely slow since last week | Normal | Too many startup apps, low disk space, pending updates | Startup trimmed, disk cleaned, updates installed | Resolved | [ ] | |
| 5 | Emily Rodriguez | Constant pop-ups and browser homepage changed | High | Adware bundled with a free PDF converter | Adware removed, browser reset, scans clean | Resolved (escalated to Tier 2) | [ ] | |
| 6 | Trevor Murray | Suspicious email reported (phishing) | High | Look-alike sender domain (phishing), nothing clicked | Sender blocked, similar messages removed, no reset needed | Resolved | [x] | |
| 7 | Aisha Rahman | Second-floor printer shows offline | Low | Printer lost its network connection; stuck jobs in queue | Printer reconnected, spooler cleared | Resolved | [ ] | |
| 8 | Noah Kim | New hire starting Monday needs accounts and equipment | Normal | Onboarding request | Checklist started, waiting on manager approvals | Open | [ ] | |
| 9 | Olivia Brown | Request to install Adobe Acrobat Pro | Low | Software request, manager approved | License assigned, software installed | Resolved | [ ] | |
| 10 | Louise Watson | Laptop won't boot, possible drive failure | Emergency | Suspected failing hard drive | Data recovered, drive replaced | Resolved | [ ] | |
| 11 | Sofia Martinez | Work email stopped updating on my phone | Normal | Expired sign-in session and background restrictions on the phone | Account re-added, sync restored | Resolved | [ ] | |
| 12 | Tyler Brooks | "Access denied" opening the Marketing shared folder | Normal | Group access requires new manager's approval | Waiting on approval from Grace Lee | Open | [ ] | |

Varied outcomes to try in the admin panel: assign #5 to a second staff account, ask a follow-up question on #3 before resolving, and reopen one resolved ticket (for example #7) and resolve it again.

---

## 1. Locked out of account after failed logins (High)

**Requester:** Jonathan Crawford | **Topic:** Report a Problem

**What the user wrote:** Repeated failed logins led to a lockout. Unsure if he forgot his credentials or if there is a problem on our end. Has a meeting at 9:00 am and needs access ASAP.

**Internal note**
> User reports repeated failed logins and a lockout, and is unsure whether the cause is a forgotten password or a system problem. Checked for outages or authentication issues on our end: none found. Account was locked automatically after repeated failed sign-in attempts. Verified identity by calling back the number on file and confirming employee ID and manager name before making any changes. Unlocked the account, issued a temporary password by phone (not email), and set it to require a change at next sign-in. Failed attempts came from the user's own device with no suspicious sign-in locations. Likely cause: forgotten or mistyped password, not a system fault. Advised the user not to keep retrying and suggested a password manager.

**Reply**
> Hi Jonathan,
>
> Thanks for getting in touch. We'll get you back in before your 9:00 am meeting.
>
> I checked, and there's no problem on our end. Your account was locked automatically after several failed sign-in attempts, which is a security feature. That most likely means the password was forgotten or mistyped.
>
> I've verified your identity, unlocked your account, and given you a temporary password over the phone. You'll be asked to choose a new password the first time you sign in.
>
> A few tips:
> - Check that Caps Lock is off when you type your password.
> - Wait until you have the new password before trying again, since more failed attempts can lock the account again.
> - If your email is saved on your phone or another device, update the password there too.
> - A password manager can save you from forgotten passwords.
>
> If anything doesn't work, reply here right away.
>
> IT Support

**Status:** Resolved

---

## 2. Forgot my password and reset email never arrives (Low)

**Requester:** Marcus Johnson | **Topic:** General Inquiry

**Internal note**
> Reset emails were being sent to an old address still on his account. Verified identity by employee ID, updated the recovery email to his current address, and triggered a new reset. Confirmed with the user that the email arrived and the new password works.

**Reply**
> Hi Marcus,
>
> The reset email was going to an old address still on your account, which is why it never showed up. I've updated it to your current address and sent a new reset link. Please use the link within an hour, choose a new password, and reply here if it works.
>
> Tip: a password manager makes forgotten passwords much less common.
>
> IT Support

**Status:** Resolved once the user confirms.

---

## 3. Laptop can't connect to office Wi-Fi (Normal)

**Requester:** Priya Patel | **Topic:** Report a Problem

**Reply 1 (follow-up question, send first)**
> Hi Priya,
>
> Thanks for the details. To narrow this down, could you tell me:
> 1. The exact error message you see.
> 2. Whether it happens in every room or only some.
> 3. Whether other Wi-Fi networks (for example your phone hotspot) work on the laptop.
>
> In the meantime, please try turning Wi-Fi off and on and restarting the laptop.
>
> IT Support

**Internal note (after her reply)**
> User's phone connects but the laptop does not, after a Windows update, so the problem is on the laptop, not the network. Likely a stale Wi-Fi profile. Removed the saved network, rejoined, then ran `ipconfig /release`, `ipconfig /renew` and `ipconfig /flushdns`. Connection restored and internet access confirmed. Checked the Wi-Fi adapter driver, which is current.

**Reply 2 (resolution)**
> Hi Priya,
>
> This looks like a saved Wi-Fi profile that broke during the Windows update. Here's the fix, in case it happens again:
> 1. Open Settings > Network & internet > Wi-Fi > Manage known networks.
> 2. Select the office network and choose **Forget**.
> 3. Reconnect and enter the Wi-Fi password.
>
> I also refreshed your laptop's network settings. You're connected now, so I'm marking this resolved. Reply if it comes back.
>
> IT Support

**Status:** Resolved

---

## 4. Computer extremely slow since last week (Normal)

**Requester:** David Okafor | **Topic:** Report a Problem

**Internal note**
> Startup impact was high, with many apps launching at sign-in. C: drive was over 90% full. Windows updates had been pending for several weeks. Ran a full Microsoft Defender scan (clean). Disabled unneeded startup apps, ran Storage cleanup and removed temporary files, installed pending updates. Checked drive health, no errors found. Boot time is down to about a minute. Advised that a 3-year-old laptop with a mechanical drive would benefit from an SSD.

**Reply**
> Hi David,
>
> I found the main causes: too many programs starting with Windows, a nearly full drive, and updates that hadn't been installed. I've disabled the unneeded startup apps, cleared space, installed the updates, and run a full virus scan (no threats found). Startup should be much faster now.
>
> If it slows down again, let me know. An SSD upgrade would make a big difference on this laptop, and I'm happy to look at options.
>
> IT Support

**Status:** Resolved

---

## 5. Constant pop-ups and browser homepage changed (High)

**Requester:** Emily Rodriguez | **Topic:** Report a Problem

**Internal note (assign to second staff account, Tier 2)**
> Symptoms began after installing a free PDF converter, consistent with a bundled potentially unwanted program (adware and browser hijacker). Had the user disconnect from the network and stop using the machine. Uninstalled the converter and unknown programs, removed suspicious browser extensions, reset browser settings and homepage, checked startup entries and scheduled tasks. Ran a full Microsoft Defender scan plus an offline scan. No sign of data theft. As a precaution, asked the user to change passwords for accounts used since the install. Advised installing software only from approved sources.

**Reply**
> Hi Emily,
>
> Thanks for reporting this quickly. The pop-ups came from adware bundled with the PDF converter. We removed it, reset your browser settings, and ran two full scans, both of which came back clean.
>
> Please do two things: change the passwords for your main accounts (email, banking, work systems) from a different device or now that the laptop is clean, and only install software from the approved list or after asking us. If we can help you find a safe PDF tool, let us know.
>
> IT Support

**Status:** Resolved

---

## 6. Suspicious email reported (phishing) (High)

**Requester:** Trevor Murray | **Topic:** Report a Problem

**What the user wrote:** Received a suspicious email this morning. The content seems legitimate, but the sender address is one he has never seen, and he is waiting for a similar email. Asks whether it is spam.

**Reply 1 (send first)**
> Hi Trevor,
>
> Thanks for checking before acting on it. Please don't click any links or open any attachments in that email.
>
> Could you forward it to us as an attachment so we can check the sender and the message details? It would also help to know who or what you're expecting an email from, so we can compare the sender address with the real one.
>
> IT Support

**Internal note**
> Sender address is unfamiliar although the content looks legitimate, and the user is expecting a similar email, so this could be a look-alike (impersonation) message. User has not clicked anything. Asked for the message as an attachment to preserve the headers. Checks: compare the sender's domain with the real vendor's domain, compare From vs Reply-To and Return-Path, review SPF/DKIM/DMARC results in the headers, and inspect link destinations by hovering only (no clicking). Result: sender domain is a look-alike of the real one and the link points to a different site, so it is a phishing attempt. Blocked the sender domain, searched other mailboxes for the same message, and reported the URL. No password reset needed because the user did not click or enter anything.

**Reply 2 (resolution)**
> Hi Trevor,
>
> We checked the email. The sender's address is a look-alike of the real one, and the link goes to a different website, so it was a phishing attempt. Good call reporting it.
>
> We've blocked the sender and removed similar messages from other mailboxes. Please delete the email and don't forward it. Since you didn't click anything, no further action is needed on your account. If you did click the link or enter any information, tell us right away.
>
> To get the message you're actually waiting for, use the vendor's official website or an address you already know, not the link in this email.
>
> IT Support

**Status:** Resolved

---

## 7. Second-floor printer shows offline (Low)

**Requester:** Aisha Rahman | **Topic:** Report a Problem

**Internal note**
> A coworker also can't print, so the problem is the printer, not one PC. Printer had lost its network connection after a power cycle. Reconnected it to the network and confirmed it responds. Cleared the stuck queue on the print server (stop the spooler, delete the files in the spool folder, restart the spooler). Test page printed successfully from two computers.

**Reply**
> Hi Aisha,
>
> The printer had dropped off the network after a power cycle. I've reconnected it and cleared the stuck print jobs. A test page printed fine from two computers. Please resubmit your three documents, and let your coworker know it should work for her too.
>
> IT Support

**Status:** Resolved. Reopen this one once for practice if you like.

---

## 8. New hire starting Monday needs accounts and equipment (Normal)

**Requester:** Noah Kim | **Topic:** General Inquiry

**Internal note**
> Onboarding checklist for Jessica Lee (Accounting, manager Mark Davis):
> - [ ] Create user account and email
> - [ ] Add to Accounting security group (needs manager approval)
> - [ ] Access to the Accounting shared drive (needs manager approval)
> - [ ] Prepare and image a laptop
> - [ ] Add the second-floor printer
> - [ ] Set up multi-factor authentication on first day
> Started the account and laptop. Waiting on written approval from Mark Davis for group and shared drive access.

**Reply**
> Hi Noah,
>
> Thanks for the details. I've started on Jessica Lee's account and laptop, and they'll be ready before Monday. To finish the access, I need written approval from her manager, Mark Davis, for the Accounting group and shared drive. Could he reply to this ticket to confirm?
>
> We'll also set up her multi-factor authentication with her on the first day.
>
> IT Support

**Status:** Leave Open, waiting on approval. To close it, add a final reply once the approval arrives.

---

## 9. Request to install Adobe Acrobat Pro (Low)

**Requester:** Olivia Brown | **Topic:** General Inquiry

**Internal note**
> Manager approval from Mark Davis confirmed in writing. License available in the software pool. Assigned a license to the user, installed Acrobat Pro remotely, and verified she can open and sign a test PDF.

**Reply**
> Hi Olivia,
>
> Acrobat Pro is installed on your computer and licensed to you, and Mark's approval is on file. Please sign in with your work account the first time you open it. I tested editing and signing a PDF and both work. Let me know if you run into any issues.
>
> IT Support

**Status:** Resolved

---

## 10. Laptop won't boot, possible drive failure (Emergency)

**Requester:** Louise Watson | **Topic:** Report a Problem

**Reply 1 (send immediately)**
> Hi Louise,
>
> Please power the laptop off completely and don't try to start it again. If the hard drive is failing, every restart can make data loss worse, so please don't reinstall Windows or run repair tools yet.
>
> Please bring the laptop to IT as soon as you can. Our first step is to copy your files off the drive before we repair anything. I'll update you as soon as we've checked what's recoverable.
>
> IT Support

**Internal note**
> Failed boot with a suspected failing mechanical hard drive. Priority is recovering the data. Do not run repair tools or reinstall Windows on the failing drive. Remove the drive, connect it to a working computer through a USB dock (read-only), and copy or image the files first. Then replace the drive with an SSD, reinstall Windows, install the standard software, and restore the files. Verified the recovered files with the user and set up a backup.

**Reply 2 (resolution)**
> Hi Louise,
>
> Good news: we recovered your files from the old drive and confirmed them with you. The drive was failing, so we replaced it with a new SSD, reinstalled Windows and your standard software, and restored your files.
>
> To avoid this happening again, we've set up automatic backups for your Documents and Desktop. Please check that your files are all there and reply if anything is missing.
>
> IT Support

**Status:** Resolved

---

## 11. Work email stopped updating on my phone (Normal)

**Requester:** Sofia Martinez | **Topic:** Report a Problem

**Internal note**
> Desktop and webmail work, so the account is fine and the problem is the phone. Sign-in session had expired, and background data was restricted for the mail app by battery saver. Removed the account from the phone, re-added it with the current password, and turned off the background restriction for the app. New mail arrives within a minute.

**Reply**
> Hi Sofia,
>
> Your phone's sign-in session had expired, and battery saver was stopping the mail app from updating in the background. I re-added your account and allowed background activity for the app. Please check that new mail is arriving, and reply if it stops again.
>
> IT Support

**Status:** Resolved

---

## 12. "Access denied" opening the Marketing shared folder (Normal)

**Requester:** Tyler Brooks | **Topic:** General Inquiry

**Internal note**
> User moved to Marketing this week, and the folder needs membership in the Marketing security group. Access to shared data requires approval from the new manager (Grace Lee). Asked the user to have her confirm in the ticket. Do not add him until it's approved.

**Reply 1**
> Hi Tyler,
>
> Access to the Marketing shared folder needs approval from your new manager. I've asked Grace Lee to confirm in this ticket. Once she does, I'll add you to the group, and you'll need to sign out and back in for it to take effect.
>
> IT Support

**Reply 2 (after approval)**
> Hi Tyler,
>
> Grace's approval came through and I've added you to the Marketing group. Please sign out and back in, then open the folder and let me know it works.
>
> IT Support

**Status:** Leave Open until approval arrives, then resolve.
