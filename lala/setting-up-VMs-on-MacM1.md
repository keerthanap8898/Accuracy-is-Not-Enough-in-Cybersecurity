# `setting-up-VMs-on-MacM1.md`

## `Compact Runbook: Temporary OS / VM Setup for Vulnerability Detection Scripting Problems`

> Minimal, repeatable setup guide for running the temporary OS targets needed for four scripting problems:
>
> - **Q1** - Windows Workstation software inventory.
> - **Q2** - `log4j-core` detection.
> - **Q3** - Debian package EVR reporting.
> - **Q4** - SSH host-key fetching.

---

## `License`

>     Copyright Ⓒ 2025  Keerthana Purushotham <keep.consult@proton.me>.
>     Licensed under the GNU AGPL v3. See LICENSE for details.
>   [*`see license`*](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license)

---

<a id="index"></a>

## `Index`

- [**`0. Goal & OS Mapping`**](#0-goal--os-mapping)
- [**`1. Reference Links`**](#1-reference-links)
  - [**`1.1 Core Workspace Links`**](#11-core-workspace-links)
  - [**`1.2 Windows VM Links`**](#12-windows-vm-links)
  - [**`1.3 Docker / Container Links`**](#13-docker--container-links)
  - [**`1.4 Problem-Specific References`**](#14-problem-specific-references)
- [**`2. Codespaces Setup for Q2-Q4`**](#2-codespaces-setup-for-q2-q4)
- [**`3. Q1 - Windows 11 Workstation VM on MacBook M1 Pro`**](#3-q1---windows-11-workstation-vm-on-macbook-m1-pro)
  - [**`3.1 One-Time UTM Install`**](#31-one-time-utm-install)
  - [**`3.2 One-Time Windows VM Creation`**](#32-one-time-windows-vm-creation)
  - [**`3.3 One-Time Windows SSH Setup`**](#33-one-time-windows-ssh-setup)
  - [**`3.4 Blind Start / Run / Stop Workflow`**](#34-blind-start--run--stop-workflow)
- [**`4. Q2 - Temporary Ubuntu Container for Log4j`**](#4-q2---temporary-ubuntu-container-for-log4j)
- [**`5. Q3 - Temporary Debian Container for Package EVR`**](#5-q3---temporary-debian-container-for-package-evr)
- [**`6. Q4 - Temporary Ubuntu SSH Server Container`**](#6-q4---temporary-ubuntu-ssh-server-container)
- [**`7. Optional Local Mac Setup for Q2-Q4`**](#7-optional-local-mac-setup-for-q2-q4)
- [**`8. Final Proof Bundle`**](#8-final-proof-bundle)
- [**`9. Cleanup Commands`**](#9-cleanup-commands)

---

<a id="0-goal--os-mapping"></a>

## `0. Goal & OS Mapping`

| Problem | Required Target | Easiest Temporary Setup | Where To Run |
|---|---|---|---|
| `Q1` | Windows Workstation, not Server | Windows 11 ARM VM | MacBook M1 Pro using UTM |
| `Q2` | Any OS for `log4j-core` search | Ubuntu container | GitHub Codespaces or Mac Docker |
| `Q3` | Debian-based machine | Debian 12 container | GitHub Codespaces or Mac Docker |
| `Q4` | Remote SSH machine | Ubuntu container running `sshd` | GitHub Codespaces or Mac Docker |

**Key rule:**  
Use **Mac + UTM** for `Q1`. Use **Docker containers** for `Q2`, `Q3`, & `Q4`.

[***`back to index`***](#index)

---

<a id="1-reference-links"></a>

## `1. Reference Links`

<a id="11-core-workspace-links"></a>

### `1.1 Core Workspace Links`

- [***`GitHub Codespaces overview`***](https://docs.github.com/codespaces/overview)
- [***`Current Codespace workspace`***](https://github.com/codespaces/shiny-garbanzo-rr9gw6gpg652p6v?editor=vscode)
- [***`Target markdown file path`***](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/lala/setting-up-VMs-on-MacM1.md)
- [***`Repository license anchor`***](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main#license)

[***`back to index`***](#index)

---

<a id="12-windows-vm-links"></a>

### `1.2 Windows VM Links`

- [***`UTM official website`***](https://mac.getutm.app/)
- [***`UTM macOS install docs`***](https://docs.getutm.app/installation/macos/)
- [***`UTM scripting / CLI docs`***](https://docs.getutm.app/scripting/scripting/)
- [***`UTM remote-control docs`***](https://docs.getutm.app/advanced/remote-control/)
- [***`Windows 11 download page`***](https://www.microsoft.com/software-download/windows11)
- [***`Windows on Arm ISO docs`***](https://learn.microsoft.com/en-us/windows/arm/iso)
- [***`Windows 11 Enterprise Evaluation`***](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
- [***`Windows OpenSSH optional feature troubleshooting`***](https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features)

[***`back to index`***](#index)

---

<a id="13-docker--container-links"></a>

### `1.3 Docker / Container Links`

- [***`Docker Desktop for Mac install docs`***](https://docs.docker.com/desktop/setup/install/mac-install/)
- [***`Docker Desktop main docs`***](https://docs.docker.com/desktop/)
- [***`Docker Desktop Apple Silicon DMG`***](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
- [***`Ubuntu official Docker image`***](https://hub.docker.com/_/ubuntu)
- [***`Debian official Docker image`***](https://hub.docker.com/_/debian)

[***`back to index`***](#index)

---

<a id="14-problem-specific-references"></a>

### `1.4 Problem-Specific References`

#### `Q1 - Windows inventory`

- [***`Python winreg docs`***](https://docs.python.org/3/library/winreg.html)
- [***`PowerShell Get-AppxPackage`***](https://learn.microsoft.com/en-us/powershell/module/appx/get-appxpackage)
- [***`PowerShell Get-WindowsPackage`***](https://learn.microsoft.com/en-us/powershell/module/dism/get-windowspackage)

#### `Q2 - Log4j`

- [***`Apache Log4j downloads`***](https://logging.apache.org/log4j/2.x/download.html)
- [***`Maven Central log4j-core 2.17.1`***](https://central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar)
- [***`Direct log4j-core 2.17.1 JAR download`***](https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar)
- [***`Python zipfile docs`***](https://docs.python.org/3/library/zipfile.html)
- [***`Oracle JAR file specification`***](https://docs.oracle.com/en/java/javase/22/docs/specs/jar/jar.html)

#### `Q3 - Debian EVR`

- [***`dpkg-query manual`***](https://manpages.debian.org/dpkg-query)
- [***`Debian package search`***](https://packages.debian.org/)
- [***`Debian security tracker`***](https://security-tracker.debian.org/)
- [***`Ubuntu security notices`***](https://ubuntu.com/security/notices)
- [***`Ubuntu OVAL data`***](https://ubuntu.com/security/oval)

#### `Q4 - SSH host keys`

- [***`OpenSSH manual page index`***](https://www.openssh.org/manual.html)
- [***`ssh-keyscan manual`***](https://man.openbsd.org/ssh-keyscan)
- [***`ssh-keygen manual`***](https://man.openbsd.org/ssh-keygen)

[***`back to index`***](#index)

---

<a id="2-codespaces-setup-for-q2-q4"></a>

## `2. Codespaces Setup for Q2-Q4`

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

- `docker version` works.
- `python3 --version` works.
- Workspace path is `/workspaces/vuln-test`.

[***`back to index`***](#index)

---

<a id="3-q1---windows-11-workstation-vm-on-macbook-m1-pro"></a>

## `3. Q1 - Windows 11 Workstation VM on MacBook M1 Pro`

> Q1 needs a real Windows Workstation/client OS.  
> Codespaces is not enough because Codespaces is Linux container-based.

---

<a id="31-one-time-utm-install"></a>

### `3.1 One-Time UTM Install`

Run this on the MacBook M1 Pro terminal:

```bash
brew install --cask utm

sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin/utmctl

utmctl
```

Reference links:

- [***`UTM official website`***](https://mac.getutm.app/)
- [***`UTM install docs`***](https://docs.getutm.app/installation/macos/)
- [***`UTM CLI docs`***](https://docs.getutm.app/scripting/scripting/)

[***`back to index`***](#index)

---

<a id="32-one-time-windows-vm-creation"></a>

### `3.2 One-Time Windows VM Creation`

Download Windows 11 ARM64 ISO:

- [***`Windows 11 download page`***](https://www.microsoft.com/software-download/windows11)
- [***`Windows on Arm ISO docs`***](https://learn.microsoft.com/en-us/windows/arm/iso)
- [***`Windows 11 Enterprise Evaluation`***](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)

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

Then install Python inside Windows:

- [***`Python Windows downloads`***](https://www.python.org/downloads/windows/)

[***`back to index`***](#index)

---

<a id="33-one-time-windows-ssh-setup"></a>

### `3.3 One-Time Windows SSH Setup`

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

Reference link:

- [***`Windows OpenSSH optional feature docs`***](https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features)

[***`back to index`***](#index)

---

<a id="34-blind-start--run--stop-workflow"></a>

### `3.4 Blind Start / Run / Stop Workflow`

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

[***`back to index`***](#index)

---

<a id="4-q2---temporary-ubuntu-container-for-log4j"></a>

## `4. Q2 - Temporary Ubuntu Container for Log4j`

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

Reference links:

- [***`Ubuntu Docker image`***](https://hub.docker.com/_/ubuntu)
- [***`Direct log4j-core JAR download`***](https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar)
- [***`Python zipfile docs`***](https://docs.python.org/3/library/zipfile.html)

[***`back to index`***](#index)

---

<a id="5-q3---temporary-debian-container-for-package-evr"></a>

## `5. Q3 - Temporary Debian Container for Package EVR`

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

Reference links:

- [***`Debian Docker image`***](https://hub.docker.com/_/debian)
- [***`dpkg-query manual`***](https://manpages.debian.org/dpkg-query)
- [***`Debian package search`***](https://packages.debian.org/)
- [***`Debian security tracker`***](https://security-tracker.debian.org/)

[***`back to index`***](#index)

---

<a id="6-q4---temporary-ubuntu-ssh-server-container"></a>

## `6. Q4 - Temporary Ubuntu SSH Server Container`

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

Reference links:

- [***`Ubuntu Docker image`***](https://hub.docker.com/_/ubuntu)
- [***`OpenSSH manual index`***](https://www.openssh.org/manual.html)
- [***`ssh-keyscan manual`***](https://man.openbsd.org/ssh-keyscan)
- [***`ssh-keygen manual`***](https://man.openbsd.org/ssh-keygen)

[***`back to index`***](#index)

---

<a id="7-optional-local-mac-setup-for-q2-q4"></a>

## `7. Optional Local Mac Setup for Q2-Q4`

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

Reference links:

- [***`Docker Desktop Mac install docs`***](https://docs.docker.com/desktop/setup/install/mac-install/)
- [***`Docker Desktop Apple Silicon DMG`***](https://desktop.docker.com/mac/main/arm64/Docker.dmg)

[***`back to index`***](#index)

---

<a id="8-final-proof-bundle"></a>

## `8. Final Proof Bundle`

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

[***`back to index`***](#index)

---

<a id="9-cleanup-commands"></a>

## `9. Cleanup Commands`

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

[***`back to index`***](#index)

---

## `End State`

After following this runbook:

1. `Q1` is tested on a real Windows 11 Workstation VM.
2. `Q2` is tested in a disposable Ubuntu container with controlled Log4j fixtures.
3. `Q3` is tested in a disposable Debian 12 container with real installed packages.
4. `Q4` is tested against a disposable Ubuntu SSH server container.
5. All outputs remain in `outputs/`.
6. All command transcripts & truth files remain in `logs/`.

[***`back to index`***](#index)
