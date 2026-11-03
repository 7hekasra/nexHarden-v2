[🇮🇷 فارسی](README.fa.md) | [🇬🇧 English](README.md)

# 🛡️ nexHarden

### Linux Security Auditing & Hardening Tool

**nexHarden** is a lightweight, open-source tool designed to audit Linux systems and identify potentially insecure configurations.

It examines your system, detects potential security issues, and generates easy-to-understand reports with recommendations to improve your system's security.

The goal of nexHarden is simple: **to make Linux security more understandable, accessible, and easier to manage.**

---

## ✨ Features

- 🔍 **Security Audit:** Examine Linux system security configurations.
- 📊 **Security Reports:** Generate detailed HTML and JSON reports.
- 🛡️ **Hardening Profiles:** Provide security recommendations to harden your system.
- 🧪 **Dry Run:** Preview proposed changes before applying them.
- 📚 **Audit History:** Access previously generated audit reports.
- ⚡ **Lightweight:** No complicated installation or unnecessary dependencies.

## 📦 Installation

### 1. Download and Extract

Download the nexHarden archive and extract it:

```bash
unzip nexHarden-v2.zip
cd nexHarden
```

### 2. Make the Program Executable

```bash
chmod +x nexharden
```

That's it! nexHarden is ready to use without any complicated installation process.

> **Requirement:** Python 3.9 or later.

---

## 🚀 Quick Start

To start a basic security audit, simply run:

```bash
./nexharden audit
```

This command performs an initial security assessment of your Linux system.

For a more comprehensive audit, run:

```bash
sudo ./nexharden audit --full
```

Once the audit is complete, a security report will be generated.

## 📊 Viewing Reports

All generated reports are stored in the `reports` directory.

Reports are available in both HTML and JSON formats.

To open an HTML report:

```bash
xdg-open reports/audit-*.html
```

If the command above does not work, you can open the report directly using a browser:

```bash
firefox reports/audit-*.html
```

Or:

```bash
google-chrome reports/audit-*.html
```

### What If the Report Does Not Open?

If you encounter an `ERR_ACCESS_DENIED` error, the issue may be related to file permissions.

First, fix the ownership of the reports directory:

```bash
sudo chown -R "$USER":"$USER" reports/
```

Then, set the appropriate read permissions:

```bash
chmod 644 reports/*.html reports/*.json
```

Try opening the report again.

**Alternative Method:**

If the problem persists, you can start a simple local web server:

```bash
cd reports
python3 -m http.server 8080
```

Then open the following address in your browser:

```text
http://localhost:8080
```

Click on the desired `audit-....html` file to view the report.

To stop the server, press `Ctrl + C`.

---

## 🛠️ Common Commands

| Command | Description |
|---|---|
| `./nexharden audit` | Run a basic security audit |
| `sudo ./nexharden audit --full` | Run a comprehensive security audit |
| `./nexharden system-info` | Display system information |
| `./nexharden version` | Display the current version |
| `./nexharden history` | View previous audit reports |

---

## 🔐 What Is Hardening?

Hardening refers to a set of actions and security configurations designed to reduce potential vulnerabilities and improve overall system security.

In addition to identifying security issues, nexHarden can provide recommendations for improving your system's security configurations.

By default, this feature does not make any changes to your system.

### 1. Preview Proposed Changes (Dry Run)

Before applying any changes, you can preview the expected modifications:

```bash
sudo ./nexharden harden --profile basic --dry-run
```

### 2. Apply Changes (Apply)

After reviewing and approving the proposed changes, you can apply them:

```bash
sudo ./nexharden harden --profile basic --apply
```

> **Warning:** Always carefully review the Dry Run output before applying changes. Modifying security configurations may affect the functionality of certain services and applications.

---

## 🧰 Troubleshooting

### The Program Does Not Start

First, check your Python version:

```bash
python3 --version
```

If Python is not installed, install it using:

```bash
sudo apt update
sudo apt install python3
```

### Permission Denied

Some security checks require administrative privileges to access system information.

Try running the audit with `sudo`:

```bash
sudo ./nexharden audit --full
```

### Module Not Found

Make sure you are running the program from its main directory:

```bash
cd ~/Downloads/nexHarden-v2/nexHarden
```

Then try running it again:

```bash
./nexharden audit
```

If the problem persists, save the complete error output for further investigation.

---

## ⚠️ Important Security Notes

- nexHarden is a security auditing and hardening tool, not a replacement for antivirus software or a firewall.
- A high security score does not guarantee that your system is completely secure.
- Always review the Dry Run output before applying changes.
- Security recommendations may vary depending on your Linux distribution and system configuration.
- Generated reports may contain sensitive system information. Avoid sharing them publicly.
- It is recommended to back up important files and configurations before applying significant changes.

---

## 📋 Project Information

| Specification | Details |
|---|---|
| Project Name | nexHarden |
| Version | 2.0 |
| Programming Language | Python |
| Operating System | Linux |
| Minimum Python Version | 3.9 |
| License | MIT |

---

## 🐧 About Free and Open-Source Software

We believe that security should never be an exclusive feature or something accessible only to a privileged group of people.

Free and open-source software gives everyone the freedom to explore code, learn from it, modify it, and contribute to making it better.

**nexHarden was built with this belief in mind.**

This project is a small contribution toward a world where knowledge is shared freely, tools are accessible to everyone, and security grows through collaboration and community participation.

If you are passionate about Linux, cybersecurity, and open-source software, we invite you to become part of this journey.

**Use freely. Learn openly. Improve together. Share knowledge.**

---

**nexHarden — Security through Knowledge.**
