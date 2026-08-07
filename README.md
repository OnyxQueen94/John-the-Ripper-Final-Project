
# BCYB644 Final-Project #
## Password Auditing and Incident Response using John the Ripper ##
### **Course** BCYB 644 ###
### Siera Evans ###

## _What_ is John the Ripper? ##
Not to be confused with "Jack" the Ripper of course! 
_John the Ripper_ is a free open-source software tool that's used for password security auditing, and password recovery. It's designed to identify weak passwords by attempting to crack password hashes on a network. The software was originally developed for Unix systems however it now supports Windows, macOs, Linux, and hundreds of hash formats.

## _Why _is John the Ripper Used? ## 
As mentioned previously, John the Ripper is primarily used to detect weak passwords _before_ attackers do, and to test an organization's password policies. The software is also used to recover forgotten passwords when _authorized _ and to assist digital forensic and incident response investigations.

## _Who_ uses John the Ripper? ##
John the Ripper is commonly used by cybersecurity professionals to improve password security, but others include,
1. System Administrators
   ### _Specifically IT staff use John the Ripper to audit user passwords and enforce rules for stronger security protocols concerning password creations._ ###
2. Penetration Testers
3. Incident Responders
4. Digital Forensic Analysts
   and finally Security Auditors

## Putting it all Together ##
After a company experiences a data breach, investigators recover password hashes from a compromised server. They use John the Ripper to determine whether employee passwords were weak enough to be cracked. If many passwords are recovered quickly, the company knows it needs stronger password policies.

### Tool Requirements, Setup, and Workflow ###

## Requirements ##
1. Kali Linux or another Linux distribution
2. John the Ripper Jumbo edition
3. Terminal access 
4. Password hash file
5. Wordlist (RockYou.txt)

## Why? ## 
Linux - Provides the environment John the Ripper runs.
Terminal - Is used to execute John the Ripper commands.
Hash files - Contain encrypted passwords that John the Ripper can test and attempt to recover.  ex: MD5 hashes, or NTLM hashes
Wordlist - Provides common passwords for _dictionary attacks_, and is a text file that identifies commonly used passwords and quickly identifies weak or commonly used passwords.

### Lets Start our Workflow! ###
## Step 1. Obtain Password Hashes ##
# What's the Purpose? #
