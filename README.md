
# 🗡️ John the Ripper

## Password Auditing and Incident Response

### BCYB 644 Final Project

**Student:** Siera Evans

# Introduction 

Passwords remain one of the weakest points in cybersecurity. Weak, reused, or easily guessed passwords continue to contribute to data breaches across organizations of all sizes. Security professionals use password auditing tools like **John the Ripper** to identify weak passwords before attackers can exploit them. This project explores the features, capabilities, and real-world applications of John the Ripper through a realistic Incident Response scenario. By the end of this demonstration, readers will understand how password auditing helps organizations strengthen authentication policies and reduce the risk of unauthorized access. 

## Table of Contents

- [Introduction](#introduction)
- [What is John the Ripper?](#what-is-john-the-ripper)
- [Why is John the Ripper Used?](#why-is-john-the-ripper-used)
- [Who Uses John the Ripper?](#who-uses-john-the-ripper)
- [Putting It All Together](#putting-it-all-together)
- [Tool Requirements](#tool-requirements-setup-and-workflow)
- [Workflow](#workflow)
- [Core Features](#core-features)
- [Practical Demonstration](#practical-demonstration)
- [Incident Response Lifecycle](#incident-response-lifecycle)
- [Strengths and Limitations](#strengths-and-limitations)
- [Recommendations](#recommendations)
- [References](#references)

# _What_ is John the Ripper? 
Not to be confused with "Jack" the Ripper of course! 
_John the Ripper_ is a free open-source software tool that's used for password security auditing and password recovery. It's designed to identify weak passwords by attempting to crack password hashes on a network. The software was originally developed for Unix systems however, it now supports Windows, macOS, Linux, and hundreds of hash formats.

# _Why_ is John the Ripper Used? 
As mentioned previously, John the Ripper is primarily used to detect weak passwords _before_ attackers do, and to test an organization's password policies. The software is also used to recover forgotten passwords when _authorized _ and to assist digital forensic and incident response investigations.

# _Who_ uses John the Ripper? 
Cybersecurity professionals commonly use John the Ripper to improve password security, but others include,

### System Administrators
- Audit employee passwords.
- Enforce password policies.
- Identify weak passwords

### Penetration Testers
- Test password strength during security assessments.

### Incident Responders
- Evaluate compromised password hashes after a breach.

## Digital Forensic Analysts
- Recover passwords from legally obtained evidence.

## Security Auditors
- Verify compliance with password policies.

# Putting it all Together 
After a company experiences a data breach, investigators recover password hashes from a compromised server. They use John the Ripper to determine whether employee passwords were weak enough to be cracked. If many passwords are recovered quickly, the company knows it needs stronger password policies.

# Tool Requirements, Setup, and Workflow #

## Requirements ##
1. Kali Linux or another Linux distribution
2. John the Ripper Jumbo edition
3. Terminal access 
4. Password hash file
5. Wordlist (RockYou.txt)

# _Why?_ # 
1. Linux - Provides the environment John the Ripper runs.
2. Terminal - Is used to execute John the Ripper commands.
3. Hash files - Contain encrypted passwords that John the Ripper can test and attempt to recover.  ex: MD5 hashes, or NTLM hashes
4. Wordlist - Provides common passwords for _dictionary attacks_, and is a text file that identifies commonly used passwords and quickly identifies weak or commonly used passwords.

# Installation

John the Ripper was installed on a MacBook Air using Homebrew.

## Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Install John the Ripper

```bash
brew install john-jumbo
```

## Verify Installation

```bash
john --list=build-info
```

![John the Ripper Installation](images/john-installed.png)

# Workflow #

# Step 1. Obtain Password Hashes #
## What's the Purpose? ##
To collect password hashes from an authorized source for security testing.

## Examples Include ##
1. Linux /etc/shadow
2. Windows SAM database
3. Password audit
4. Database backup

# Step 2. Identify the Hash Type #

## What's the Purpose? ##
To determine which hashing algorithm was used so John the Ripper can know how to process the password hashes.

## Common Hash Types ##
1. MD5
2. SHA-1
3. SHA-256
4. NTLM
5. bcrypt

# Step 3. Select an Attack Method #

## What's the Purpose? ##
To determine which encryption algorithm was used, let's choose the best password recovery technique based on the available information and investigation objectives.

The three most common attack methods include:

1. Dictionary Attack (which we mentioned earlier!)
2. Single Crack Mode
3. Incremental (Brute Force) Mode

The following section explains these features in greater detail before demonstrating how they are used during an Incident Response investigation.

# Core Features

John the Ripper includes several powerful password auditing features that help cybersecurity professionals evaluate password strength, recover passwords, and assess organizational security during authorized security assessments and Incident Response investigations.

The following features will be demonstrated throughout this project.
 
# Core Features

John the Ripper includes several powerful password auditing features that help cybersecurity professionals evaluate password strength, recover passwords, and assess organizational security during authorized security assessments and Incident Response investigations.

---

## 1. Dictionary Attack

### Description

A Dictionary Attack compares password hashes against a wordlist containing millions of commonly used passwords instead of trying every possible password combination.

### Why It Is Important

- Quickly identifies weak passwords.
- Faster than a brute-force attack.
- Commonly used during password audits and Incident Response investigations.

### Command

```bash
john --wordlist=rockyou.txt sample_hashes/md5.txt
```

### Real-World Example

After a company experiences a data breach, investigators recover password hashes from a compromised server. They use a password dictionary to determine whether employees are using weak passwords that attackers could easily recover.

---

## 2. Single Crack Mode

### Description

Single Crack Mode generates password guesses using information such as usernames, names, or other account details.

### Why It Is Important

- Tests predictable passwords based on user information.
- Useful when investigating targeted attacks.

### Command

```bash
john --single sample_hashes/md5.txt
```

### Real-World Example

An employee named Sarah creates the password **Sarah2026**. John the Ripper can automatically generate similar password guesses using account information.

---

## 3. Incremental (Brute Force) Mode

### Description

Incremental Mode attempts every possible password combination until the correct password is found.

### Why It Is Important

- Can recover passwords that are not found in a dictionary.
- Useful for testing password strength.

### Command

```bash
john --incremental sample_hashes/md5.txt
```

### Real-World Example

A randomly generated password such as **Q7!Lm2@Xp9** is unlikely to appear in a wordlist. Incremental Mode attempts many possible character combinations to recover it, although this process can take much longer.

---

## 4. Multiple Hash Support

### Description

John the Ripper supports hundreds of password hash formats.

### Common Hash Types

- MD5
- SHA-1
- SHA-256
- SHA-512
- NTLM
- bcrypt

### Why It Is Important

Different operating systems store passwords using different hashing algorithms. John the Ripper can analyze many of these formats.

---

## 5. Display Recovered Passwords

### Description

Displays any passwords that John the Ripper successfully recovers during the password audit.

### Command

```bash
john --show sample_hashes/md5.txt
```

### Why It Is Important

This allows investigators to quickly determine which accounts need immediate password resets.

---

## 6. Session Recovery

### Description

If a password audit is interrupted, John the Ripper can resume from where it stopped.

### Command

```bash
john --restore
```

### Why It Is Important

Large password audits may take hours or even days. Session recovery prevents investigators from restarting the entire process if the computer shuts down or the session is interrupted.
# Practical Demonstration

## Incident Response Scenario

🪼 **Jello Financial** recently detected unauthorized logins to several employee accounts after suspicious authentication attempts were identified on one of its Linux servers.

During the investigation, the Incident Response (IR) team recovered password hashes from the compromised server's `/etc/shadow` file. Although the attackers had not yet recovered the original passwords, management wanted to determine whether the stolen password hashes could be cracked if they fell into the wrong hands.

To assess the organization's password security, the Incident Response team selected **John the Ripper** to perform a password audit.

---

## Investigation Objectives

The objectives of this investigation are to:

- Determine whether employee passwords are vulnerable to password-cracking attacks.
- Identify accounts requiring immediate password resets.
- Evaluate the effectiveness of the company's password policy.
- Recommend improvements to strengthen password security.

---

## Investigation Timeline

1. Verify John the Ripper installation.
2. Generate a sample password hash.
3. Save the password hash.
4. Identify the password hash type.
5. Perform a Dictionary Attack.
6. Review recovered passwords.
7. Analyze the findings.
8. Recommend security improvements.

---

# Step 1 – Verify John the Ripper Installation

## Objective

Verify that John the Ripper is installed correctly before beginning the password audit.

## Command

```bash
john --list=build-info
```

## Explanation

This command displays information about the installed version of John the Ripper, including the build version, supported password hash formats, and available features. Running this command confirms that John the Ripper is installed correctly and ready for use.

## Screenshot

![John the Ripper Installation](images/john-installed.png)

## Why This Matters

Before beginning any password audit, security analysts must verify that their tools are functioning properly. Confirming the installation helps prevent errors during an investigation and ensures John the Ripper can successfully process password hashes.

---

# Step 2 – Generate a Sample Password Hash

## Objective

Generate a password hash that simulates credentials recovered during a cybersecurity investigation.

## Password Used

```
Password123
```

## Command

```bash
echo -n "Password123" | openssl md5
```

## Explanation

This command converts the plaintext password into an MD5 hash using OpenSSL. During a real-world incident, investigators typically recover password hashes rather than plaintext passwords. Generating a hash allows us to simulate that scenario in a safe lab environment.

## Screenshot

![Generate MD5 Hash](images/create-md5-hash.png)

## Why This Matters

John the Ripper does not crack plaintext passwords directly. Instead, it analyzes password hashes recovered from compromised systems and attempts to determine the original password.

---

# Step 3 – Save the Password Hash

## Objective

Save the generated password hash into a text file that John the Ripper can analyze.

## File Created

```
sample_hashes/md5.txt
```

## Verification Command

```bash
cat sample_hashes/md5.txt
```

## Explanation

The generated MD5 hash was copied into a file named `md5.txt` inside the `sample_hashes` folder. The `cat` command is used to verify that the file contains the correct hash before beginning the password recovery process.

## Screenshot

![Hash File](images/hash-file.png)

## Why This Matters

During Incident Response investigations, password hashes are commonly recovered from sources such as Linux `/etc/shadow`, Windows SAM databases, or compromised authentication databases. Storing the hash in a text file simulates how investigators prepare evidence for password auditing using John the Ripper.


# Step 4 – Identify the Hash Type

## Objective

Identify the hashing algorithm before attempting password recovery.

## Hash Type

MD5

## Explanation

The password hash used in this demonstration was generated using the MD5 hashing algorithm.

Before John the Ripper can attempt password recovery, investigators must identify the type of password hash they are working with. Different operating systems and applications use different hashing algorithms, such as MD5, SHA-256, NTLM, and bcrypt.

Since the hash in this demonstration was created using the `openssl md5` command, its hash type is already known to be MD5.

## Screenshot

![Generate MD5 Hash](images/create-md5-hash.png)

## Why This Matters

Identifying the correct hash type allows John the Ripper to apply the appropriate password-cracking technique. Using the wrong hash type may prevent successful password recovery.

# Step 5 – Perform a Dictionary Attack

## Objective

Determine whether the recovered password hash can be cracked using a password dictionary.

## Command

```bash
john --format=Raw-MD5 --wordlist=wordlists/custom_wordlist.txt sample_hashes/md5.txt
```

## Explanation

John the Ripper compares the recovered password hash against every password contained in the custom wordlist. When a matching password is found, John successfully recovers the original plaintext password.

## Screenshot

![Dictionary Attack](images/dictionary-attack.png)

## Why This Matters

Weak passwords can often be recovered within seconds using a dictionary attack. This demonstrates why organizations should enforce strong password policies and avoid commonly used passwords.


# Step 6 – Display the Recovered Password

## Objective

Display any passwords successfully recovered during the password audit.

## Command

```bash
john --show --format=Raw-MD5 sample_hashes/md5.txt
```

## Explanation

The `--show` option displays passwords that John the Ripper successfully recovered during the audit. This allows investigators to identify compromised accounts that require immediate password resets.

## Screenshot

![Recovered Password](images/john-show.png)

## Why This Matters

Incident Response teams use recovered passwords to assess the impact of a breach and determine which user accounts should be secured immediately.


# Investigation Results

## Findings

The password audit successfully recovered the password **Password123** using a dictionary attack and a custom password wordlist.

The results demonstrate that weak or commonly used passwords can often be recovered within seconds after an attacker obtains password hashes.

## Risks Identified

- Weak password selection.
- Common password usage.
- Increased risk of unauthorized access.
- Potential password reuse across multiple systems.

## Why This Matters

If attackers obtained password hashes during a real-world data breach, weak passwords such as **Password123** could be recovered quickly, allowing attackers to gain unauthorized access to sensitive systems and data.


# Incident Response Lifecycle

John the Ripper supports multiple phases of the Incident Response Lifecycle by helping security teams identify weak passwords after a security incident.

## 1. Preparation

- Develop strong password policies.
- Enforce Multi-Factor Authentication (MFA).
- Conduct regular password audits.
- Train employees on password security best practices.

## 2. Detection and Analysis

- Detect suspicious login activity.
- Recover password hashes from compromised systems.
- Identify the password hash type.
- Analyze password strength using John the Ripper.

## 3. Containment

- Reset compromised passwords.
- Disable affected user accounts.
- Block unauthorized access.

## 4. Eradication

- Remove weak passwords from the environment.
- Strengthen password policies.
- Eliminate reused credentials.

## 5. Recovery

- Restore user access using stronger passwords.
- Enable Multi-Factor Authentication.
- Verify that compromised accounts are secure.

## 6. Lessons Learned

Following the investigation, organizations should:

- Schedule regular password audits.
- Encourage the use of password managers.
- Educate employees on creating strong passwords.
- Continuously review authentication policies.


# Strengths and Limitations

## Strengths

- Free and open-source.
- Supports hundreds of password hash formats.
- Fast password recovery using dictionary attacks.
- Cross-platform support for Windows, macOS, and Linux.
- Useful for penetration testing, password auditing, and Incident Response.
- Large cybersecurity community and extensive documentation.

## Limitations

- Can only crack weak passwords within a reasonable amount of time.
- Strong passwords combined with modern hashing algorithms may take years to recover.
- Requires authorized access to password hashes.
- Effectiveness depends on the quality of the wordlist used.
- Should only be used for authorized security testing.


# Recommendations

Based on the results of this password audit, the following security recommendations are made:

- Require passwords to contain at least 14 characters.
- Enforce Multi-Factor Authentication (MFA) for all users.
- Prevent password reuse across multiple accounts.
- Encourage employees to use password managers.
- Conduct routine password audits using authorized security tools.
- Provide annual cybersecurity awareness training focused on password security.
- Monitor authentication logs for suspicious login attempts.



# References

Openwall. (n.d.). *John the Ripper Password Cracker*. https://www.openwall.com/john/

Openwall. (n.d.). *John the Ripper Documentation*. https://www.openwall.com/john/doc/

MITRE ATT&CK®. (n.d.). *Credential Access*. https://attack.mitre.org/

National Institute of Standards and Technology. (2024). *Digital Identity Guidelines (SP 800-63B).* https://pages.nist.gov/800-63-3/

OWASP Foundation. (n.d.). *Authentication Cheat Sheet*. https://cheatsheetseries.owasp.org/



