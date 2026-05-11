# `Compact Runbook: 
> ## Temporary OS / VM Setup for Vulnerability Detection Scripting Problems
>
> - *Minimal, repeatable setup guide for running the temporary OS targets needed for four scripting problems*:
>
>   - **Q1** - *Windows Workstation software inventory.*
>   - **Q2** - *`log4j-core` detection.*
>   - **Q3** - *Debian package EVR reporting.*
>   - **Q4** - *SSH host-key fetching.*

---

## `License`

>     Copyright Ⓒ 2025  Keerthana Purushotham <keep.consult@proton.me>.
>     Licensed under the GNU AGPL v3. See LICENSE for details.
>   ["**see license**"- *github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license*](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license)

---

<a id="index"></a>

## `Index`

1. [**`Goal & OS Mapping`**](#1-goal--os-mapping)
2. [**`Reference Links`**](#2-reference-links)
   1. [**`Core Workspace Links`**](#21-core-workspace-links)
   2. [**`Windows VM Links`**](#22-windows-vm-links)
   3. [**`Docker / Container Links`**](#23-docker--container-links)
   4. [**`Problem-Specific References`**](#24-problem-specific-references)
3. [**`Codespaces Setup for Q2-Q4`**](#3-codespaces-setup-for-q2-q4)
4. [**`Q1 - Windows 11 Workstation VM on MacBook M1 Pro`**](#4-q1---windows-11-workstation-vm-on-macbook-m1-pro)
   1. [**`One-Time UTM Install`**](#41-one-time-utm-install)
   2. [**`One-Time Windows VM Creation`**](#42-one-time-windows-vm-creation)
   3. [**`One-Time Windows SSH Setup`**](#43-one-time-windows-ssh-setup)
   4. [**`Blind Start / Run / Stop Workflow`**](#44-blind-start--run--stop-workflow)
5. [**`Q2 - Temporary Ubuntu Container for Log4j`**](#5-q2---temporary-ubuntu-container-for-log4j)
6. [**`Q3 - Temporary Debian Container for Package EVR`**](#6-q3---temporary-debian-container-for-package-evr)
7. [**`Q4 - Temporary Ubuntu SSH Server Container`**](#7-q4---temporary-ubuntu-ssh-server-container)
8. [**`Optional Local Mac Setup for Q2-Q4`**](#8-optional-local-mac-setup-for-q2-q4)
9. [**`Final Proof Bundle`**](#9-final-proof-bundle)
10. [**`Cleanup Commands`**](#10-cleanup-commands)

---

<a id="1-goal--os-mapping"></a>

## `1. Goal & OS Mapping`

| Problem | Required Target | Easiest Temporary Setup | Where To Run |
|---|---|---|---|
| `Q1` | Windows Workstation, not Server | Windows 11 ARM VM | MacBook M1 Pro using UTM |
| `Q2` | Any OS for `log4j-core` search | Ubuntu container | GitHub Codespaces or Mac Docker |
| `Q3` | Debian-based machine | Debian 12 container | GitHub Codespaces or Mac Docker |
| `Q4` | Remote SSH machine | Ubuntu container running `sshd` | GitHub Codespaces or Mac Docker |

**Key rule:**  
Use **Mac + UTM** for `Q1`. Use **Docker containers** for `Q2`, `Q3`, & `Q4`.

["***back to index***"- *#index*](#index)

---

<a id="2-reference-links"></a>

## `2. Reference Links`

<a id="21-core-workspace-links"></a>

### `2.1 Core Workspace Links`

1. ["**GitHub Codespaces overview**"- *docs.github.com/codespaces/overview*](https://docs.github.com/codespaces/overview)
2. ["**Current Codespace workspace**"- *github.com/codespaces/shiny-garbanzo-rr9gw6gpg652p6v?editor=vscode*](https://github.com/codespaces/shiny-garbanzo-rr9gw6gpg652p6v?editor=vscode)
3. ["**Target markdown file path**"- *github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/lala/setting-up-VMs-on-MacM1.md*](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/lala/setting-up-VMs-on-MacM1.md)
4. ["**Repository license anchor**"- *github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license*](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license)

["***back to index***"- *#index*](#index)

---

<a id="22-windows-vm-links"></a>

### `2.2 Windows VM Links`

  1. ["**UTM official website**"- *mac.getutm.app*](https://mac.getutm.app/)
  2. ["**UTM macOS install docs**"- *docs.getutm.app/installation/macos*](https://docs.getutm.app/installation/macos/)
  3. ["**UTM scripting / CLI docs**"- *docs.getutm.app/scripting/scripting*](https://docs.getutm.app/scripting/scripting/)
  4. ["**UTM remote-control docs**"- *docs.getutm.app/advanced/remote-control*](https://docs.getutm.app/advanced/remote-control/)
  5. ["**Windows 11 download page**"- *www.microsoft.com/software-download/windows11*](https://www.microsoft.com/software-download/windows11)
  6. ["**Windows on Arm ISO docs**"- *learn.microsoft.com/en-us/windows/arm/iso*](https://learn.microsoft.com/en-us/windows/arm/iso)
  7. ["**Windows 11 Enterprise Evaluation**"- *www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise*](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
  8. ["**Windows OpenSSH optional feature troubleshooting**"- *learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features*](https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features)

["***back to index***"- *#index*](#index)

---

<a id="23-docker--container-links"></a>

### `2.3 Docker / Container Links`

  1. ["**Docker Desktop for Mac install docs**"- *docs.docker.com/desktop/setup/install/mac-install*](https://docs.docker.com/desktop/setup/install/mac-install/)
  2. ["**Docker Desktop main docs**"- *docs.docker.com/desktop*](https://docs.docker.com/desktop/)
  3. ["**Docker Desktop Apple Silicon DMG**"- *desktop.docker.com/mac/main/arm64/Docker.dmg*](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
  4. ["**Ubuntu official Docker image**"- *hub.docker.com/_/ubuntu*](https://hub.docker.com/_/ubuntu)
  5. ["**Debian official Docker image**"- *hub.docker.com/_/debian*](https://hub.docker.com/_/debian)

["***back to index***"- *#index*](#index)

---

<a id="24-problem-specific-references"></a>

### `2.4 Problem-Specific References`

#### `2.4.1 Q1 - Windows inventory`

  1. ["**Python winreg docs**"- *docs.python.org/3/library/winreg.html*](https://docs.python.org/3/library/winreg.html)
  2. ["**PowerShell Get-AppxPackage**"- *learn.microsoft.com/en-us/powershell/module/appx/get-appxpackage*](https://learn.microsoft.com/en-us/powershell/module/appx/get-appxpackage)
  3. ["**PowerShell Get-WindowsPackage**"- *learn.microsoft.com/en-us/powershell/module/dism/get-windowspackage*](https://learn.microsoft.com/en-us/powershell/module/dism/get-windowspackage)

["***back to index***"- *#index*](#index)

#### `2.4.2 Q2 - Log4j`

  1. ["**Apache Log4j downloads**"- *logging.apache.org/log4j/2.x/download.html*](https://logging.apache.org/log4j/2.x/download.html)
  2. ["**Maven Central log4j-core 2.17.1**"- *central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar*](https://central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar)
  3. ["**Direct log4j-core 2.17.1 JAR download**"- *repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar*](https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar)
  4. ["**Python zipfile docs**"- *docs.python.org/3/library/zipfile.html*](https://docs.python.org/3/library/zipfile.html)
  5. ["**Oracle JAR file specification**"- *docs.oracle.com/en/java/javase/22/docs/specs/jar/jar.html*](https://docs.oracle.com/en/java/javase/22/docs/specs/jar/jar.html)

["***back to index***"- *#index*](#index)

#### `2.4.3 Q3 - Debian EVR`

  1. ["**dpkg-query manual**"- *manpages.debian.org/dpkg-query*](https://manpages.debian.org/dpkg-query)
  2. ["**Debian package search**"- *packages.debian.org*](https://packages.debian.org/)
  3. ["**Debian security tracker**"- *security-tracker.debian.org*](https://security-tracker.debian.org/)
  4. ["**Ubuntu security notices**"- *ubuntu.com/security/notices*](https://ubuntu.com/security/notices)
  5. ["**Ubuntu OVAL data**"- *ubuntu.com/security/oval*](https://ubuntu.com/security/oval)

["***back to index***"- *#index*](#index)

#### `2.4.4 Q4 - SSH host keys`

  1. ["**OpenSSH manual page index***"- *www.openssh.org/manual.html*](https://www.openssh.org/manual.html)
  2. ["**ssh-keyscan manual**"- *man.openbsd.org/ssh-keyscan*](https://man.openbsd.org/ssh-keyscan)
  3. ["**ssh-keygen manual**"- *man.openbsd.org/ssh-keygen*](https://man.openbsd.org/ssh-keygen)

["***back to index***"- *#index*](#index)

---

<a id="3-codespaces-setup-for-q2-q4"></a>

## `3. Codespaces Setup for Q2-Q4`

  > Run this inside the GitHub Codespaces terminal.
  
  ```bash
  cd /workspaces
  
  mkdir -p vuln-test/{scripts,fixtures,outputs,logs}
  
  cd vuln-test
  
  exec > >(tee -a logs/session.log) 2>&1
  
  set -euxo pipefail
  
  date -u
  
  uname -a
  
  cat /etc/os-release || true
  
  docker version
  
  python3 --version
  ```
  
  Expected result:
  
  1. `docker version` works.
  2. `python3 --version` works.
  3. Workspace path is `/workspaces/vuln-test`.

["***back to index***"- *#index*](#index)

---

<a id="4-q1---windows-11-workstation-vm-on-macbook-m1-pro"></a>

## `4. Q1 - Windows 11 Workstation VM on MacBook M1 Pro`

  > Q1 needs a real Windows Workstation/client OS.  
  > Codespaces is not enough because Codespaces is Linux container-based.
  
  ---
  
  <a id="41-one-time-utm-install"></a>
  
  ### `4.1 One-Time UTM Install`
  
  Run this on the MacBook M1 Pro terminal:
  
  ```bash
  brew install --cask utm
  
  sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin/utmctl
  
  utmctl
  ```
  
  References:
  
  1. ["**UTM official website**"- *mac.getutm.app*](https://mac.getutm.app/)
  2. ["**UTM install docs**"- *docs.getutm.app/installation/macos*](https://docs.getutm.app/installation/macos/)
  3. ["**UTM CLI docs**"- *docs.getutm.app/scripting/scripting*](https://docs.getutm.app/scripting/scripting/)

["***back to index***"- *#index*](#index)

---

<a id="42-one-time-windows-vm-creation"></a>

### `4.2 One-Time Windows VM Creation`

  Download Windows 11 ARM64 ISO:
  
  1. ["**Windows 11 download page**"- *www.microsoft.com/software-download/windows11*](https://www.microsoft.com/software-download/windows11)
  2. ["**Windows on Arm ISO docs**"- *learn.microsoft.com/en-us/windows/arm/iso*](https://learn.microsoft.com/en-us/windows/arm/iso)
  3. ["**Windows 11 Enterprise Evaluation**"- *www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise*](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
  
  Create the VM in UTM:
  
  ```text
  UTM -> + -> Virtualize -> Windows -> Select Windows 11 ARM64 ISO
  
  Name: vuln-q1-win11
  RAM: 8192 MB
  CPU: 4 cores
  Disk: 64 GB
  Network: Shared Network or Bridged Network
  ```
  
  Finish Windows setup normally.
  
  Install Python inside Windows:
  
  1. ["**Python Windows downloads**"- *www.python.org/downloads/windows*](https://www.python.org/downloads/windows/)

["***back to index***"- *#index*](#index)

---

<a id="43-one-time-windows-ssh-setup"></a>

### `4.3 One-Time Windows SSH Setup`

  Open **PowerShell as Administrator** inside the Windows VM.
  
  Install & start OpenSSH Server:
  
  ```powershell
  Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
  
  Start-Service sshd
  
  Set-Service -Name sshd -StartupType Automatic
  
  New-NetFirewallRule -Name sshd -DisplayName "OpenSSH Server" -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
  ```
  
  Create a temporary admin user:
  
  ```powershell
  net user auditor "TempPassw0rd!" /add
  
  net localgroup Administrators auditor /add
  ```
  
  Confirm the VM is a Windows Workstation/client:
  
  ```powershell
  Get-CimInstance Win32_OperatingSystem |
    Select-Object Caption, Version, ProductType, OSArchitecture |
    Format-List
  ```
  
  Expected:
  
  ```text
  ProductType : 1
  ```
  
  Find the VM IP:
  
  ```powershell
  ipconfig
  ```
  
  Reference:
  
  1. ["**Windows OpenSSH optional feature docs**"- *learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features*](https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features)

["***back to index***"- *#index*](#index)

---

<a id="44-blind-start--run--stop-workflow"></a>

### `4.4 Blind Start / Run / Stop Workflow`

  Run this from the Mac terminal after the one-time VM setup is complete:
  
  ```bash
  set -euxo pipefail
  
  utmctl list
  
  utmctl start "vuln-q1-win11"
  ```
  
  Set the VM connection variables:
  
  ```bash
  export WIN_IP="PUT_WINDOWS_VM_IP_HERE"
  
  export WIN_USER="auditor"
  ```
  
  Test SSH:
  
  ```bash
  ssh "$WIN_USER@$WIN_IP" 'hostname'
  
  ssh "$WIN_USER@$WIN_IP" 'powershell -NoProfile -Command "Get-CimInstance Win32_OperatingSystem | Select Caption,ProductType,OSArchitecture | Format-List"'
  ```
  
  Copy the Q1 script into Windows:
  
  ```bash
  scp scripts/q1_windows_programs.py "$WIN_USER@$WIN_IP:C:/Users/auditor/Desktop/q1_windows_programs.py"
  ```
  
  Run the Q1 script:
  
  ```bash
  ssh "$WIN_USER@$WIN_IP" 'py -3 C:\Users\auditor\Desktop\q1_windows_programs.py --output C:\Users\auditor\Desktop\q1_output.txt'
  ```
  
  Copy the output back:
  
  ```bash
  scp "$WIN_USER@$WIN_IP:C:/Users/auditor/Desktop/q1_output.txt" outputs/q1_output.txt
  
  head -80 outputs/q1_output.txt
  ```
  
  Stop the temporary VM:
  
  ```bash
  utmctl stop "vuln-q1-win11"
  ```

["***back to index***"- *#index*](#index)

---

<a id="5-q2---temporary-ubuntu-container-for-log4j"></a>

## `5. Q2 - Temporary Ubuntu Container for Log4j`
  
  > This creates a temporary Ubuntu OS, downloads a real `log4j-core` JAR, creates renamed/nested/fake fixtures, runs the script, then exits.
  
  Start the temporary OS:
  
  ```bash
  docker rm -f q2-log4j 2>/dev/null || true
  
  docker run -it --name q2-log4j \
    -v "$PWD:/work" \
    -w /work \
    ubuntu:24.04 \
    bash
  ```
  
  Inside the container, run:
  
  ```bash
  set -euxo pipefail
  
  apt-get update
  
  apt-get install -y python3 curl zip unzip ca-certificates findutils
  
  mkdir -p fixtures/q2/direct fixtures/q2/renamed fixtures/q2/nested-app/BOOT-INF/lib fixtures/q2/false outputs logs
  
  curl -fsSLo fixtures/q2/direct/log4j-core-2.17.1.jar \
    https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar
  
  cp fixtures/q2/direct/log4j-core-2.17.1.jar \
    fixtures/q2/renamed/acme-logging-engine.jar
  
  cp fixtures/q2/direct/log4j-core-2.17.1.jar \
    fixtures/q2/nested-app/BOOT-INF/lib/log4j-core-2.17.1.jar
  
  mkdir -p fixtures/q2/nested-app/META-INF
  
  cat > fixtures/q2/nested-app/META-INF/MANIFEST.MF <<'EOF'
  Manifest-Version: 1.0
  Implementation-Title: Student Test App
  Implementation-Version: 9.8.7
  EOF
  
  (cd fixtures/q2/nested-app && zip -qr ../student-app-9.8.7.jar .)
  
  echo "fake log4j-core-9.9.9.jar" > fixtures/q2/false/log4j-core-9.9.9.jar.txt
  
  python3 scripts/q2_find_log4j_core.py \
    --root fixtures/q2 \
    --output outputs/q2_output.txt
  
  cat outputs/q2_output.txt
  
  grep -F "log4j-core-2.17.1.jar" outputs/q2_output.txt
  
  grep -F "acme-logging-engine.jar" outputs/q2_output.txt
  
  grep -F "student-app-9.8.7.jar" outputs/q2_output.txt
  
  ! grep -F "log4j-core-9.9.9.jar.txt" outputs/q2_output.txt
  
  exit
  ```
  
  Delete the temporary OS container:
  
  ```bash
  docker rm -f q2-log4j
  ```
  
  References:
  
  1. ["**Ubuntu Docker image**"- *hub.docker.com/_/ubuntu*](https://hub.docker.com/_/ubuntu)
  2. ["**Direct log4j-core JAR download**"- *repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar*](https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar)
  3. ["**Python zipfile docs**"- *docs.python.org/3/library/zipfile.html*](https://docs.python.org/3/library/zipfile.html)

["***back to index***"- *#index*](#index)

---

<a id="6-q3---temporary-debian-container-for-package-evr"></a>

## `6. Q3 - Temporary Debian Container for Package EVR`
  
  > This creates a temporary Debian 12 OS, installs target packages, runs EVR reporting, then exits.
  
  Start the temporary OS:
  
  ```bash
  docker rm -f q3-debian 2>/dev/null || true
  
  docker run -it --name q3-debian \
    -v "$PWD:/work" \
    -w /work \
    debian:12 \
    bash
  ```
  
  Inside the container, run:
  
  ```bash
  set -euxo pipefail
  
  apt-get update
  
  apt-get install -y python3 apache2 libssh-4 grep mount sed procps php dpkg-dev
  
  mkdir -p outputs logs
  
  python3 scripts/q3_debian_evr.py \
    --output outputs/q3_output.txt
  
  cat outputs/q3_output.txt
  
  for p in apache2 libssh python3 grep mount sed procsp php; do
    dpkg-query -W -f='${binary:Package}\t${Version}\n' "$p" 2>/dev/null || echo "$p MISSING"
  done | tee logs/q3_truth.txt
  
  grep -F "apache2" outputs/q3_output.txt
  
  grep -F "python3" outputs/q3_output.txt
  
  grep -F "grep" outputs/q3_output.txt
  
  grep -F "mount" outputs/q3_output.txt
  
  grep -F "sed" outputs/q3_output.txt
  
  grep -F "php" outputs/q3_output.txt
  
  grep -F "procsp" outputs/q3_output.txt
  
  grep -F "missing" outputs/q3_output.txt
  
  exit
  ```
  
  Delete the temporary OS container:
  
  ```bash
  docker rm -f q3-debian
  ```
  
  References:
  
  1. ["**Debian Docker image**"- *hub.docker.com/_/debian*](https://hub.docker.com/_/debian)
  2. ["**dpkg-query manual**"- *manpages.debian.org/dpkg-query*](https://manpages.debian.org/dpkg-query)
  3. ["**Debian package search**"- *packages.debian.org*](https://packages.debian.org/)
  4. ["**Debian security tracker**"- *security-tracker.debian.org*](https://security-tracker.debian.org/)

["***back to index***"- *#index*](#index)

---

<a id="7-q4---temporary-ubuntu-ssh-server-container"></a>

## `7. Q4 - Temporary Ubuntu SSH Server Container`
  
  > This creates a temporary Ubuntu machine running `sshd`, captures server-side host-key truth, scans it using the Q4 script, then deletes the container.
  
  Start the temporary SSH server OS:
  
  ```bash
  docker rm -f q4-sshd 2>/dev/null || true
  
  docker run -d --name q4-sshd \
    -p 2222:22 \
    ubuntu:24.04 \
    sleep infinity
  ```
  
  Install & start SSH inside the container:
  
  ```bash
  docker exec q4-sshd bash -lc '
  set -euxo pipefail
  apt-get update
  apt-get install -y openssh-server
  mkdir -p /run/sshd
  ssh-keygen -A
  /usr/sbin/sshd
  ls -l /etc/ssh/ssh_host_*_key.pub
  '
  ```
  
  Capture server-side truth:
  
  ```bash
  docker exec q4-sshd bash -lc '
  for f in /etc/ssh/ssh_host_*_key.pub; do
    ssh-keygen -lf "$f" -E sha256
  done
  ' | sort | tee logs/q4_server_truth.txt
  ```
  
  Run the Q4 script from the host/Codespaces terminal:
  
  ```bash
  python3 scripts/q4_ssh_hostkeys.py \
    --host 127.0.0.1 \
    --port 2222 \
    --types rsa,ecdsa,ed25519 \
    --timeout 5 \
    --output outputs/q4_output.txt
  
  cat outputs/q4_output.txt
  ```
  
  Proof checks:
  
  ```bash
  grep -F "Raw host keys" outputs/q4_output.txt
  
  grep -F "SHA256" outputs/q4_output.txt
  
  grep -E "ssh-rsa|ecdsa-sha2|ssh-ed25519" outputs/q4_output.txt
  ```
  
  Graceful failure test:
  
  ```bash
  set +e
  
  python3 scripts/q4_ssh_hostkeys.py \
    --host 127.0.0.1 \
    --port 2299 \
    --timeout 2 \
    --output outputs/q4_unreachable_output.txt
  
  echo "exit_code=$?"
  
  set -e
  
  cat outputs/q4_unreachable_output.txt
  
  grep -E "No host keys|Connection refused|timed out|Errors" outputs/q4_unreachable_output.txt
  ```
  
  Delete the temporary SSH server OS:
  
  ```bash
  docker rm -f q4-sshd
  ```
  
  References:
  
  1. ["**Ubuntu Docker image**"- *hub.docker.com/_/ubuntu*](https://hub.docker.com/_/ubuntu)
  2. ["**OpenSSH manual index***"- *www.openssh.org/manual.html*](https://www.openssh.org/manual.html)
  3. ["**ssh-keyscan manual**"- *man.openbsd.org/ssh-keyscan*](https://man.openbsd.org/ssh-keyscan)
  4. ["**ssh-keygen manual**"- *man.openbsd.org/ssh-keygen*](https://man.openbsd.org/ssh-keygen)

["***back to index***"- *#index*](#index)

---

<a id="8-optional-local-mac-setup-for-q2-q4"></a>

## `8. Optional Local Mac Setup for Q2-Q4`
  
  > Use this only if Codespaces Docker is unavailable or unreliable.
  
  Install Docker Desktop on Mac:
  
  ```bash
  brew install --cask docker
  
  open -a Docker
  ```
  
  Check Docker:
  
  ```bash
  docker version
  ```
  
  If Docker works, the same `Q2`, `Q3`, & `Q4` commands can be run locally from the repo directory.
  
  References:
  
  1. ["**Docker Desktop Mac install docs**"- *docs.docker.com/desktop/setup/install/mac-install*](https://docs.docker.com/desktop/setup/install/mac-install/)
  2. ["**Docker Desktop Apple Silicon DMG**"- *desktop.docker.com/mac/main/arm64/Docker.dmg*](https://desktop.docker.com/mac/main/arm64/Docker.dmg)

["***back to index***"- *#index*](#index)

---

<a id="9-final-proof-bundle"></a>

## `9. Final Proof Bundle`
  
  Run this from the project root after all tests:
  
  ```bash
  find scripts fixtures outputs logs -type f -maxdepth 3 -print | sort
  ```
  
  Hash the proof files:
  
  ```bash
  shasum -a 256 scripts/* outputs/* logs/* 2>/dev/null || true
  
  sha256sum scripts/* outputs/* logs/* 2>/dev/null || true
  ```
  
  Review expected output files:
  
  ```bash
  ls -lah outputs logs
  
  cat outputs/q1_output.txt 2>/dev/null || true
  
  cat outputs/q2_output.txt 2>/dev/null || true
  
  cat outputs/q3_output.txt 2>/dev/null || true
  
  cat outputs/q4_output.txt 2>/dev/null || true
  ```
  
  Minimum expected outputs:
  
  | Output File | Expected Content |
  |---|---|
  | `outputs/q1_output.txt` | Windows OS info, registry source, program names, versions, executable paths |
  | `outputs/q2_output.txt` | direct, renamed, & nested `log4j-core` findings |
  | `outputs/q3_output.txt` | Debian package names, exact versions, missing `procsp` |
  | `outputs/q4_output.txt` | SSH host keys & SHA256 fingerprints |
  | `outputs/q4_unreachable_output.txt` | clean error handling for closed port |

["***back to index***"- *#index*](#index)

---

<a id="10-cleanup-commands"></a>

## `10. Cleanup Commands`
  
  Clean temporary Docker containers:
  
  ```bash
  docker rm -f q2-log4j q3-debian q4-sshd 2>/dev/null || true
  ```
  
  Stop Windows VM:
  
  ```bash
  utmctl stop "vuln-q1-win11"
  ```
  
  Optional Docker cleanup:
  
  ```bash
  docker system prune -f
  ```
  
  Optional fixture cleanup:
  
  ```bash
  rm -rf fixtures/q2
  
  rm -f outputs/q4_unreachable_output.txt
  ```

["***back to index***"- *#index*](#index)

---

## `End State`
  
  After following this runbook:
  
  1. `Q1` is tested on a real Windows 11 Workstation VM.
  2. `Q2` is tested in a disposable Ubuntu container with controlled Log4j fixtures.
  3. `Q3` is tested in a disposable Debian 12 container with real installed packages.
  4. `Q4` is tested against a disposable Ubuntu SSH server container.
  5. All outputs remain in `outputs/`.
  6. All command transcripts & truth files remain in `logs/`.

["***back to index***"- *#index*](#index)
