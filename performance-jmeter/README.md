# JMeter Performance Testing for QA Challenge App

## Application Under Test
URL: https://qa-challenge.codesubmit.io

---

## 1. Installation: Java & JMeter

### **Install Java**

#### **macOS (Homebrew Recommended)**
```sh
brew install openjdk
# Add Java to your PATH in ~/.zshrc:
echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```
Check Java:
```sh
java -version
```

#### **Windows**
- Download [Adoptium/Eclipse Temurin JDK](https://adoptium.net/) or [Oracle JDK](https://www.oracle.com/java/technologies/downloads/).
- Install using the Windows installer. During install, choose to set JAVA_HOME.
- If needed, set JAVA_HOME manually:
    - Control Panel → System → Advanced System Settings → Environment Variables.
    - Under "System variables," create JAVA_HOME with value like `C:\Program Files\Eclipse Adoptium\jdk-21`.
    - Add `%JAVA_HOME%\bin` to your Path.
- Open new Command Prompt and check:
```bat
java -version
```

---

### **Download & Extract JMeter**

#### **macOS:**
```sh
curl -L https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.6.3.tgz -o apache-jmeter.tgz
tar -xf apache-jmeter.tgz
mv apache-jmeter-5.6.3 ~/Applications/
```
Add JMeter to your PATH (optional):
```sh
echo 'export PATH="$PATH:$HOME/Applications/apache-jmeter-5.6.3/bin"' >> ~/.zshrc
source ~/.zshrc
```

#### **Windows:**
- Download from [JMeter](https://jmeter.apache.org/download_jmeter.cgi)
- Extract zip to e.g. `C:\JMeter\apache-jmeter-5.6.3`
- Optionally, add `C:\JMeter\apache-jmeter-5.6.3\bin` to your system Path for CLI usage.

---

## 2. Creating a Performance Test Plan
- **JMeter GUI (cross-platform):**
    - macOS:
      ```sh
      ~/Applications/apache-jmeter-5.6.3/bin/jmeter
      ```
    - Windows:
      ```bat
      C:\JMeter\apache-jmeter-5.6.3\bin\jmeter.bat
      ```
- Add: Thread Group → HTTP Request.
- Save as `.jmx`. Example plans are provided: `login-test.jmx`, etc.

---

## 3. Running Performance Tests (Headless/CLI)

### **macOS:**
```sh
~/Applications/apache-jmeter-5.6.3/bin/jmeter -n -t login-test.jmx -l login-results.jtl -j login-test.log
```

### **Windows:**
```bat
cd C:\JMeter\apache-jmeter-5.6.3\bin
jmeter.bat -n -t C:\path\to\login-test.jmx -l C:\path\to\login-results.jtl -j C:\path\to\login-test.log
```

- Run all `.jmx` plans in the folder (macOS:)
  ```sh
  for f in *.jmx; do ~/Applications/apache-jmeter-5.6.3/bin/jmeter -n -t "$f" -l "${f%.jmx}-results.jtl"; done
  ```
- Run all `.jmx` plans in the folder (Windows PowerShell):
  ```powershell
  Get-ChildItem *.jmx | ForEach-Object { .\jmeter.bat -n -t $_.FullName -l ("$($_.BaseName)-results.jtl") }
  ```

---

## 4. Generating HTML Reports

### **macOS:**
```sh
~/Applications/apache-jmeter-5.6.3/bin/jmeter -g login-results.jtl -o ./login-report
open ./login-report/index.html
```

### **Windows:**
```bat
jmeter.bat -g C:\path\to\login-results.jtl -o C:\path\to\login-report
start C:\path\to\login-report\index.html
```
Or open the HTML file in your browser.

---

## 5. Performance Strategy & Benchmarks
- **Response Time Targets:**
  - Login: < 2 seconds for 95% requests under load
  - Add-to-Cart: < 2 seconds for 95%
  - Inventory Browsing: < 3 seconds for 95%
  - Checkout: < 3 seconds for 95%
- **Concurrency Targets:**
  - Baseline: 10 concurrent users
  - Load: 25, 50, 100, 200 step-up
  - Stress: up to 400 users
  - Ramp Up/Down: Gradual, graceful
- **Error Rate:** Target < 1% failure
- **Test Types:** Step-up, ramp, stress, spike, soak

---

## 6. Scenarios Mapped per JMeter Test Plan
- `login-test.jmx`: Username + password login (standard_user)
- `inventory-test.jmx`: Open products page, view list, get details
- `cart-test.jmx`: Add products, view cart, remove item, proceed to checkout
- `checkout-test.jmx`: Run through shipping info and purchase

---

## 7. CI/CD Integration
Include the CLI commands above in your pipeline.
Assert reports/thresholds in your build process.

---

## 8. Further Notes
- Use different users or CSV data for more realistic simulation.
- You may edit .jmx files directly or with the JMeter GUI for advanced flows.
- See [JMeter docs](https://jmeter.apache.org/usermanual/index.html) for more features.
