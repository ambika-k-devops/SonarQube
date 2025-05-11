Here's your content reformatted in a clean, eye-appealing **Markdown** style without missing any points. This is suitable for internal documentation or knowledge bases like GitHub README, Confluence, or Notion:

---

# 📊 How to Execute the SonarQube Report for Java Projects

## ✅ Step 1: Connect to the Server

Connect to the server where your Java projects are located.

---

## 🛠️ Step 2: Update `pom.xml` with SonarQube Details

```xml
<properties>
    <sonar.host.url>http://13.235.50.5:9000</sonar.host.url>
    <sonar.login>admin</sonar.login>
    <sonar.password>password</sonar.password>
</properties>
```

---

## 📈 Step 3: Generate the SonarQube Report

```bash
mvn sonar:sonar
```

> Format: `[pluginName:goalName]`

---

## 🌐 Step 4: Access SonarQube GUI

* Go to the SonarQube web interface
* Click on the **Projects** tab to see your listed project

---

## 🔍 Step 5: View Full Report

* Open your project to see the complete code analysis report.

---

## ☕ Java Prerequisite

Install Java 11 and configure environment:

```bash
sudo yum install java-11-openjdk-devel

export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```

---

# 🔐 Use SonarQube Token Instead of Username & Password

## 📌 Problem:

Avoid hardcoding `username` and `password` in `pom.xml`.

---

## ✅ Solution:

### 🔑 Step 1: Generate Token

* Go to: `Administration` → `Security` → `Users`
* Click on **Tokens**
* Provide a name and click **Generate**
* Copy the token
  Example: `squ_339becfebb58026cd7ce7b3f16925730d4dd0da4`

---

### 🛠️ Step 2: Update `pom.xml` with Token

```xml
<properties>
    <sonar.host.url>http://43.205.231.25:9000</sonar.host.url>
    <!--
    <sonar.login>admin</sonar.login>
    <sonar.password>kkfunda</sonar.password>
    -->
    <sonar.login>squ_339becfebb58026cd7ce7b3f16925730d4dd0da4</sonar.login>
</properties>
```

---

### 🚀 Step 3: Run Report Again

```bash
mvn clean sonar:sonar
```

---

# 🔄 Change SonarQube Server Port Number

### ⚙️ Default:

* Port: `9000`
* Context Path: `/`

---

### 🔧 Steps:

```bash
cd /opt/sonarqube/conf
vi sonar.properties
```

Uncomment and modify:

```
sonar.web.context=/kkfunda
sonar.web.port=8639
```

Restart SonarQube:

```bash
cd /opt/sonarqube/bin/linux-x86-64
sh sonar.sh restart
```

---

# 📁 SonarQube Sections

## 📂 Projects

Displays all the scanned projects.

## ❗ Issues

Shows all code issues across projects.

## 📜 Rules

Each language has a set of rules that determine code quality checks.

---

# 🧩 Quality Profile

* A **collection of rules** applied during analysis.
* Each language has its own profile.

## 🤔 Can I create a custom Quality Profile?

**Yes!**

### ✨ Steps:

1. Go to `Quality Profiles` → `Create`
2. Provide:

   * Name: `jio-qp`
   * Language: `Java`
   * Parent: `None`
3. Save

> Confirm creation under **Java** section.

---

### 🔄 Assign to Project:

* Go to `Project` → `Project Settings` → `Quality Profiles`
* Select `Java`
* Choose `Always use specific quality profile`
* Save

> Now build with:

```bash
mvn clean sonar:sonar
```

---

# 🚦 Quality Gates

* **Set of conditions** that a project must meet.
* Default: **Sonar way**

---

## 🏗️ How to Create a Custom Quality Gate?

### Steps:

1. Go to `Quality Gates` → `Create`
2. Name it: `jio-qg`
3. Add Conditions:

   * **Coverage**: fails if below `80%`
   * **Duplicate Lines**: fails if above `3%`

---

### 🔗 Assign to Project:

* Go to `Project` → `Settings` → `Quality Gate`
* Choose: `Always use specific quality gate`
* Save

> Run the analysis again:

```bash
mvn sonar:sonar
```

---

# ⚙️ Administration

## 🔧 Configuration

* Navigate to `Languages` to view available extensions

---

## 🔐 Security

### ➕ Create New User

* `Security` → `Users` → `Create User`
* Fill details and create

> Login with new credentials

---

### 🛡️ Grant Admin Access

* Login as `admin`
* Go to: `Security` → `Users`
* Assign `sonar-admin` role to the user
* Optionally:

  * Go to `Groups`
  * Add user to `admin` group

---

## 👥 Create New Group

* Login as `admin`
* Go to: `Security` → `Groups` → `Create Group`

---

Let me know if you want this in a downloadable `.md` file too!
