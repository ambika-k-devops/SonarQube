* Version Compatability 
* Build Failure Reason
  
--> The error you're encountering:

```
SonarQubeMojo has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0
```

means you're using a **Java Runtime (JDK 8)** to run a plugin (Sonar Maven Plugin 4.0.0.4121) that was compiled with **Java 11**.

### 💡 Class file versions:

* 52.0 = Java 8
* 55.0 = Java 11

---

### ✅ Steps to Resolve the Issue In Ubanu

1. **Upgrade your Java version to Java 11 or newer**:

   * Make sure your system and `JAVA_HOME` environment variable use **JDK 11+**.
   * On Ubuntu/Debian:

     ```bash
     sudo apt update
     sudo apt install openjdk-11-jdk
     sudo update-alternatives --config java
     java -version  # Confirm version is 11+
     ```

2. **Update `JAVA_HOME` (if needed)**:

   * Example (Linux/macOS):

     ```bash
     export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
     export PATH=$JAVA_HOME/bin:$PATH
     ```
   * On Windows:

     * Go to System Properties → Environment Variables.
     * Update `JAVA_HOME` to point to your Java 11 installation.
     * Restart your terminal/IDE.

3. **Verify the Java version used by Maven**:

   ```bash
   mvn -v
   ```

   Ensure it shows Java 11 or higher.

4. **Re-run the Sonar analysis**:

   ```bash
   mvn clean verify sonar:sonar
   ```

---
Let me know if you're working in a Docker container or CI environment, and I can give you environment-specific instructions.

Sure! Here are the commands to **upgrade to Java 11** and configure it on a **Red Hat Enterprise Linux (RHEL)** machine:

---

### ✅ Step-by-Step Commands for RHEL

#### 1. **Install OpenJDK 11**

```bash
sudo yum install java-11-openjdk-devel -y
```

#### 2. **Set Java 11 as the default**

```bash
sudo alternatives --config java
```

* You'll see a list of installed Java versions.
* Enter the number corresponding to `java-11-openjdk`.

#### 3. **Set `JAVA_HOME` environment variable**

Add this to your shell config (e.g., `.bashrc`, `.bash_profile`, or `.zshrc`):

```bash
export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
export PATH=$JAVA_HOME/bin:$PATH
```

Then apply the changes:

```bash
source ~/.bashrc
```

#### 4. **Verify Java version**

```bash
java -version
```

Expected output:

```
openjdk version "11.x.x" ...
```

#### 5. **Verify Maven uses Java 11**

```bash
mvn -v
```

Expected:

```
Java version: 11
```

---

Now you can rerun the SonarQube analysis:

```bash
mvn clean verify sonar:sonar
```

Do you also need to install Maven or SonarQube Scanner on this machine?
