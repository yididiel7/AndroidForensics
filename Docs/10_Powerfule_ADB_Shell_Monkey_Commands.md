# 🐒 10 Powerful ADB Shell Monkey Commands
A quick reference for Android security testers using the ADB Monkey tool to perform UI fuzzing, stress testing, and automated input events.

# 1️⃣ Launch a Specific App Instantly

```bash
adb shell monkey -p com.target.app -c android.intent.category.LAUNCHER 1
```

**Purpose**

* Starts an app immediately.
* Useful when testing **malware samples or forensic tools**.

**Security testing use**

* Confirm app launches correctly after installation.

---

# 2️⃣ Controlled Random Testing for One App

```bash
adb shell monkey -p com.target.app --throttle 300 -v 1000
```

**What it does**

* Limits testing to **one app**
* Adds **300ms delay between events**
* Generates **1000 random actions**

**Finds**

* crashes
* UI bugs
* input handling flaws

---

# 3️⃣ Full System Stress Test

```bash
adb shell monkey -v 100000
```

**Effect**

Runs **100,000 random system events** across the entire device.

Security researchers use this to detect:

* **system UI crashes**
* framework vulnerabilities
* memory leaks

⚠️ Can open random apps or change settings.

---

# 4️⃣ Motion/Gesture Stress Test

```bash
adb shell monkey --pct-motion 100 -v 5000
```

**Meaning**

* Generates **100% swipe/drag gestures**

Useful for testing:

* scroll vulnerabilities
* gesture-based exploits
* UI rendering crashes

---

# 5️⃣ Heavy Touch Input Flood

```bash
adb shell monkey --pct-touch 100 -v 5000
```

Simulates **thousands of rapid taps**.

Security testers use this to detect:

* race conditions
* UI thread crashes
* input buffer overflows

---

# 6️⃣ Activity Navigation Stress Test

```bash
adb shell monkey \
-p com.target.app \
--pct-nav 40 \
--pct-touch 30 \
--pct-motion 30 \
-v 10000
```

Creates **frequent activity navigation events**.

Helps reveal:

* broken activity lifecycle
* intent vulnerabilities
* navigation crashes

---

# 7️⃣ App Switching Chaos Test

```bash
adb shell monkey \
--pct-appswitch 40 \
--pct-touch 30 \
--pct-motion 30 \
-v 10000
```

Simulates **constant switching between apps**.

Finds:

* background process crashes
* permission leaks
* lifecycle bugs

---

# 8️⃣ Monkey Test With Crash Ignoring

```bash
adb shell monkey \
-p com.target.app \
--ignore-crashes \
--ignore-timeouts \
--ignore-security-exceptions \
-v 10000
```

Keeps testing even if the app crashes.

Important for:

* long-term fuzz testing
* malware sandbox analysis

---

# 9️⃣ Deterministic Monkey Test (Repeatable)

```bash
adb shell monkey -p com.target.app -s 12345 -v 5000
```

`-s` = **seed value**

This makes the random test **repeatable**.

Security researchers use this to:

* reproduce crashes
* debug vulnerabilities

---

# 🔟 Massive Chaos Test (Real Security Stress Test)

```bash
adb shell monkey \
--throttle 50 \
--pct-touch 35 \
--pct-motion 30 \
--pct-nav 15 \
--pct-appswitch 10 \
--pct-anyevent 10 \
-v 50000
```

Simulates **50,000 mixed user actions**.

This is used in:

* penetration testing
* Android malware analysis
* robustness testing

---

# 🧠 Pro Security Testing Trick

Capture logs while monkey runs:

```bash
adb logcat > monkey_test_log.txt
```

Then run monkey:

```bash
adb shell monkey -p com.target.app -v 10000
```

Afterwards search the log:

```
CRASH
ANR
SecurityException
Fatal signal
```

This helps detect **hidden vulnerabilities**.

---
