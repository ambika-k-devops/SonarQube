# SonarQube by KK FUNDA

## Flow Diagram Explanation

**Before Maven and Tomcat —> SonarQube**

* SonarQube should be installed and running before Maven and Tomcat integrations.
* Maven projects can be configured to run static analysis using the SonarQube plugin.
* After SonarQube is running, the Maven project can push analysis results to the SonarQube server.
* Tomcat is typically used for deploying Java web applications. SonarQube improves quality before deployment by analyzing the source code.

## Definition

* SonarQube is an open-source platform used for continuous inspection of code quality.
* It performs static code analysis to identify bugs, vulnerabilities, and code smells in your code.

## Key Features

### Code Quality and Security

* **Bugs and Vulnerabilities**: Detect and fix issues that might lead to bugs or security vulnerabilities.
* **Code Smells**: Identify maintainability issues in your code.
* **Code Coverage**: Measure how much of your code is covered by tests.
* **Duplication**: Detect duplicate code blocks.
* **Technical Debt**: Estimate the effort required to fix all the issues in the code.

### Multi-Language Support

* Supports a wide range of programming languages including Java, JavaScript, C#, C++, Python, PHP, and many more.

### Quality Gates

* Set thresholds for quality metrics to ensure code meets the standards before it is integrated into the main branch.

## Similar Tools

* SonarQube
* Checkmarx
* Coverity
* Fortify Static Code Analyzer (SCA)
* Veracode
* PMD
* ESLint
* FindBugs/SpotBugs
* StyleCop
* Pylint
* ReSharper
* Flake8
* Codacy
* CodeClimate
* DeepSource
* Semmle LGTM
* Klocwork
* Infer
* Bandit
* Rubocop
* Brakeman

## Difference Between Code Review and Code Coverage

### Code Coverage

* Refers to the number of lines tested through unit test cases.
* Industry standard requires \~80% code coverage.
* **Benefits**: Helps identify untested areas of code.
* **Tools**: JaCoCo (Java), Istanbul (JavaScript), etc.

### Code Review

* Manual review of code by team members.
* Focused on finding bugs, ensuring adherence to coding standards, and improving code quality.
* **Benefits**: Leads to better software quality, promotes best practices.
* **Tools**: GitHub Pull Requests, Bitbucket, GitLab Merge Requests.

## SonarQube Introduction

* **Type**: Continuous Code Quality
* **Vendor**: Sonar
* **Is it open-source?**: Yes (for some languages)
* **Version**: 9.x
* **Supported OS**: Cross-platform (Linux, Windows, macOS)
* **Executable Software?**: No, downloaded as a zip and extracted

**Download Link**: [SonarQube Downloads](https://www.sonarsource.com/products/sonarqube/downloads/)

## More Information About SonarQube

* Previously called "Sonar"
* Continuously analyzes and measures code quality
* Generates reports in HTML/PDF formats
* Initially developed for Java; now supports many languages
* Supports multiple operating systems and browsers
* Compatible with databases like MySQL, Oracle, PostgreSQL, etc.
* Identifies issues like:

  * Duplicate code
  * Coding standards violations
  * Missing/insufficient unit tests
  * Complex code
  * Missing/inadequate comments
  * Potential bugs (e.g., exception handling)

> **Note**: With SonarQube reports, deployments can be halted if quality criteria are not met.

## Prerequisites for SonarQube Installation

### 1. Hardware Requirements

* **CPU**: Modern multi-core processor
* **RAM**: At least 2GB (4GB recommended); use t2.medium for AWS
* **Disk Space**: 1GB for SonarQube + additional for DB

### 2. Software Requirements

#### Operating System

* Linux (preferred)
* Windows
* macOS

#### Java

* Java JDK 11 or 17 (not just JRE)
* Set `JAVA_HOME` environment variable

#### Database

* Supported: Oracle, PostgreSQL, MS SQL Server
* **MySQL Removed**
* Built-in H2 database (for demo/testing)

## SonarQube Installation Steps

1. **Launch EC2 Instance**: Use t2.medium (4GB RAM)

2. **Connect to Server**

3. **Switch to Root User**:

   ```sh
   sudo su -
   ```

4. **Install Java**:

   ```sh
   sudo yum install java-11-openjdk-devel -y
   javac --version
   ```

5. **Navigate to /opt Directory**:

   ```sh
   cd /opt
   ```

6. **Install Utilities**:

   ```sh
   yum install wget unzip -y
   ```

7. **Download SonarQube**:

   ```sh
   wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.6.1.59531.zip
   ```

8. **Unzip and Rename Directory**:

   ```sh
   unzip sonarqube-9.6.1.59531.zip
   mv sonarqube-9.6.1.59531 sonarqube
   ```

9. **Create Sonar User**:

   ```sh
   useradd sonar
   ```

10. **Grant Sudo Access**:

    ```sh
    visudo
    # Add the following line:
    sonar   ALL=(ALL)       NOPASSWD: ALL
    ```

11. **Set Permissions**:

    ```sh
    chown -R sonar:sonar /opt/sonarqube/
    chmod -R 775 /opt/sonarqube/
    su - sonar
    cd /opt/sonarqube/bin/linux-x86-64/
    ```

12. **Start/Stop SonarQube**:

    ```sh
    sh sonar.sh start
    sh sonar.sh status
    sh sonar.sh stop
    sh sonar.sh restart
    ```

13. **Access SonarQube in Browser**:

    * Default Port: `9000`
    * URL: `http://<your-ip>:9000`
    * Ensure port 9000 is open in firewall/security group

14. **Login Credentials**:

    * Username: `admin`
    * Password: `admin`
    * You will be prompted to change the password

## Troubleshooting

1. Ensure Sonar user is used to start SonarQube
2. Check if port 9000 is open
3. Verify Java is installed and configured
4. Use a machine with at least 4GB RAM (t2.medium or higher)
