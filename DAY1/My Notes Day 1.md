# 🚀 SonarQube by KK FUNDA

---

## 🌍 Flow Overview: Before Maven & Tomcat → SonarQube

```mermaid
graph LR
  A[Developer Code] --> B[Push to Repository]
  B --> C[Maven Build]
  C --> D[Run SonarQube Analysis]
  D --> E[Send Results to SonarQube Server]
  E --> F[Deploy via Tomcat]
```

* **SonarQube sits between development and deployment** to ensure only high-quality code is pushed forward.

---

## 🔍 What is SonarQube?

> SonarQube is an **open-source platform** for **continuous inspection** of code quality.

* Performs **static code analysis** to identify:

  * Bugs
  * Vulnerabilities
  * Code Smells

---

## 📊 Key Features

### 🛡️ Code Quality & Security

* ✉ **Bugs & Vulnerabilities**: Prevent potential production issues
* ⚡ **Code Smells**: Improve maintainability
* 📈 **Code Coverage**: Check test coverage
* ♻️ **Duplication**: Reduce redundant code
* ⏳ **Technical Debt**: Estimate effort to improve codebase

### 📚 Multi-Language Support

> Java, JavaScript, Python, C#, C++, PHP, and many more

### 🏛 Quality Gates

* Define pass/fail criteria based on coverage, duplication, and critical issues

---

## 📄 Similar Tools to SonarQube

| Static Analysis | Linters & Style Checkers |
| --------------- | ------------------------ |
| Checkmarx       | PMD                      |
| Coverity        | ESLint                   |
| Fortify SCA     | StyleCop                 |
| Veracode        | Pylint, Flake8           |
| Semmle LGTM     | Rubocop, Brakeman        |
| Codacy          | ReSharper, Infer         |

---

## 📝 Code Review vs. Code Coverage

| Category | Code Review                            | Code Coverage                |
| -------- | -------------------------------------- | ---------------------------- |
| Method   | Manual peer review                     | Automated via test execution |
| Goal     | Ensure quality, readability, standards | Check which lines are tested |
| Benefits | Fewer bugs, better practices           | Identify untested paths      |
| Tools    | GitHub PRs, Bitbucket                  | JaCoCo, Istanbul, Clover     |

---

## 🧰 SonarQube Introduction

* **Type**: Continuous Code Quality Tool
* **Vendor**: Sonar
* **License**: Open source (for most languages)
* **Version**: 9.x
* **Platform**: Cross-Platform (Linux, macOS, Windows)
* **Installer**: ZIP package (not executable)

[Download SonarQube ⬇️](https://www.sonarsource.com/products/sonarqube/downloads/)

---

## 📚 Detailed Info

* Originally named **Sonar**
* Supports multiple languages & databases
* Produces **HTML/PDF reports**
* Integrates with multiple browsers
* Detects:

  1. Duplicate Code
  2. Standards Violations
  3. Unit Test Gaps
  4. Complex Code
  5. Poor Commenting
  6. Potential Bugs

> ⚠️ SonarQube can block deployments based on report failures

---

## 🚀 Prerequisites for Installation

### Hardware ⚙️

* CPU: Multi-core
* RAM: Min 2GB (Recommended: 4GB)
* Disk: 1GB+ free

### Software 🌐

* **OS**: Linux (preferred), Windows, macOS
* **Java**: JDK 11 or 17 *(set JAVA\_HOME)*
* **DB**: PostgreSQL, Oracle, SQL Server *(MySQL deprecated)*
* **Optional**: H2 embedded DB for testing

---

## 🛠️ SonarQube Installation Guide

1. **Launch EC2 (t2.medium)**
2. **Connect via SSH**
3. **Switch to root**

   ```bash
   sudo su -
   ```
4. **Install Java**

   ```bash
   sudo yum install java-11-openjdk-devel -y
   javac --version
   ```
5. **Navigate to /opt**

   ```bash
   cd /opt
   ```
6. **Install Utilities**

   ```bash
   yum install wget unzip -y
   ```
7. **Download SonarQube**

   ```bash
   wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.6.1.59531.zip
   unzip sonarqube-9.6.1.59531.zip
   mv sonarqube-9.6.1.59531 sonarqube
   ```
8. **Create Non-root Sonar User**

   ```bash
   useradd sonar
   visudo
   # Add: sonar   ALL=(ALL) NOPASSWD: ALL
   ```
9. **Change Permissions**

   ```bash
   chown -R sonar:sonar /opt/sonarqube/
   chmod -R 775 /opt/sonarqube/
   su - sonar
   cd /opt/sonarqube/bin/linux-x86-64/
   ```
10. **Manage SonarQube**

    ```bash
    sh sonar.sh start | status | stop | restart
    ```
11. **Access Web UI**

    * URL: `http://<your-ip>:9000`
    * Port: `9000` (Allow in security group)
12. **Login**

    * Username: `admin`
    * Password: `admin` (Change on first login)
    * It will ask to change the password

---

## ⚠️ Troubleshooting Tips

* Use **sonar** user to start service
* Ensure **port 9000** is open
* Check **Java installation**
* Use machine with **4GB RAM** minimum

---

> ⭐ With SonarQube integrated, your CI/CD pipelines gain a powerful guard against bad code. Automate quality checks and build confidence in every release.
