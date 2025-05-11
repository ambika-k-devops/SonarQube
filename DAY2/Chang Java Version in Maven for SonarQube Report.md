You're on the right track using the `alternatives` command to switch between Java versions. However, there's a bit of nuance:

### Key Points:

* `java` and `javac` are managed **independently** via `alternatives`.

* You changed the **runtime (`java`) version** using:

  ```
  sudo alternatives --config java
  ```

  That’s why `java -version` now shows Java 11.

* However, `javac -version` is still showing Java 8 because you **haven’t changed the compiler (`javac`) version** yet.

---

### To Change the `javac` Version:

Run the following command:

```bash
sudo alternatives --config javac
```

You'll see a list of installed `javac` versions. Select the one that corresponds to Java 11 (e.g., something like `/usr/lib/jvm/java-11-openjdk-.../bin/javac`).

---

### Summary

* `java -version` shows Java 11 → ✅ already set
* `javac -version` shows Java 8 → ❌ needs updating

Just run:

```bash
sudo alternatives --config javac
```

…and select the Java 11 compiler.

Would you like help verifying that both `java` and `javac` are pointing to the same JDK installation after that?
------------------------------------------------------------------------
Great! Here's how you can **verify** that both `java` and `javac` are pointing to the **same JDK installation** after switching:

---

### ✅ Step-by-Step Verification

#### 1. Check the actual paths for `java` and `javac`:

```bash
which java
which javac
```

#### 2. Check the symlink targets:

```bash
readlink -f $(which java)
readlink -f $(which javac)
```

These commands will show you the full resolved paths of the executables.

#### 3. Compare the paths:

They should both point to the **same base JDK directory**, like:

```
/usr/lib/jvm/java-11-openjdk-11.0.25.0.9-7.el9.x86_64/bin/java
/usr/lib/jvm/java-11-openjdk-11.0.25.0.9-7.el9.x86_64/bin/javac
```

---

### 🧪 Optional Check: JAVA\_HOME

To ensure consistency across tools (like Maven or Gradle), check if `JAVA_HOME` is set:

```bash
echo $JAVA_HOME
```

If it's not pointing to the correct JDK, set it like so (for temporary use):

```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.25.0.9-7.el9.x86_64
export PATH=$JAVA_HOME/bin:$PATH
```

To make this permanent, add those lines to `~/.bashrc` or `~/.bash_profile`.

---

Would you like a quick script to set `JAVA_HOME` correctly based on the active `java` path?
