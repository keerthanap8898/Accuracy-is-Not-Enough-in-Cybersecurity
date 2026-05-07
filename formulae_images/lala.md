Below is the same setup workflow with **raw reference links & download links** added where they matter.
## Vuln rx
---

# Link pack

## GitHub Codespaces

Codespaces runs your dev environment in a Docker container on a VM. The default environment is Ubuntu Linux, & Codespaces run in Linux regardless of your local OS. Use it for **Q2-Q4**, not Q1. ([GitHub Docs][1])

```text
https://docs.github.com/codespaces/overview
```

Your Codespace:

```text
https://github.com/codespaces/shiny-garbanzo-rr9gw6gpg652p6v?editor=vscode
```

---

## Windows 11 Workstation VM for Q1

Use this on your **MacBook M1 Pro**, because Q1 requires a Windows Workstation/client target.

Microsoft Windows 11 Enterprise Evaluation:

```text
https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise
```

Microsoft Windows 11 Arm ISO overview:

```text
https://learn.microsoft.com/en-us/windows/arm/iso
```

Windows 11 download page:

```text
https://www.microsoft.com/software-download/windows11
```

UTM official site:

```text
https://mac.getutm.app/
```

UTM macOS install docs:

```text
https://docs.getutm.app/installation/macos/
```

UTM scripting / CLI docs:

```text
https://docs.getutm.app/scripting/scripting/
```

UTM remote-control docs:

```text
https://docs.getutm.app/advanced/remote-control/
```

UTM can be installed from the Mac App Store or GitHub, & its `utmctl` CLI is located at `/Applications/UTM.app/Contents/MacOS/utmctl`. ([UTM Documentation][2])

---

## Docker for Q2-Q4

Docker Desktop for Mac install docs:

```text
https://docs.docker.com/desktop/setup/install/mac-install/
```

Docker Desktop main docs:

```text
https://docs.docker.com/desktop/
```

Docker Desktop direct Apple Silicon DMG link:

```text
https://desktop.docker.com/mac/main/arm64/Docker.dmg
```

Docker Desktop direct Intel Mac DMG link:

```text
https://desktop.docker.com/mac/main/amd64/Docker.dmg
```

Docker Desktop requires a paid subscription for commercial use in larger enterprises, but is free for personal use, education, non-commercial open-source, & smaller businesses under Docker’s threshold. ([Docker Documentation][3])

---

## Container image references

Ubuntu official Docker image:

```text
https://hub.docker.com/_/ubuntu
```

Ubuntu `24.04` is a supported official image tag. ([Docker Hub][4])

Debian official Docker image:

```text
https://hub.docker.com/_/debian
```

Debian `12` / `bookworm` is a supported official image tag. ([Docker Hub][5])

---

## Q1 references

Python `winreg` docs:

```text
https://docs.python.org/3/library/winreg.html
```

Microsoft OpenSSH Server install / Windows capability reference:

```text
https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features
```

Microsoft `Get-AppxPackage` docs:

```text
https://learn.microsoft.com/en-us/powershell/module/appx/get-appxpackage
```

Microsoft `Get-WindowsPackage` docs:

```text
https://learn.microsoft.com/en-us/powershell/module/dism/get-windowspackage
```

OpenSSH Server on Windows can be installed with `Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0` on supported Windows client/server systems where it is available as an optional feature. ([Microsoft Learn][6])

---

## Q2 references

Apache Log4j downloads:

```text
https://logging.apache.org/log4j/2.x/download.html
```

Maven Central Log4j Core 2.17.1 page:

```text
https://central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar
```

Raw Maven Central directory:

```text
https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/
```

Direct JAR download used in the fixture:

```text
https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar
```

Python `zipfile` docs:

```text
https://docs.python.org/3/library/zipfile.html
```

Java JAR file specification:

```text
https://docs.oracle.com/en/java/javase/22/docs/specs/jar/jar.html
```

Maven Central identifies `org.apache.logging.log4j:log4j-core:2.17.1` as the Log4j Core artifact, & the raw Maven repository exposes the actual JAR download path. ([Maven Central][7])

---

## Q3 references

Debian official Docker image:

```text
https://hub.docker.com/_/debian
```

Debian package search:

```text
https://packages.debian.org/
```

Debian security tracker:

```text
https://security-tracker.debian.org/
```

Ubuntu security notices:

```text
https://ubuntu.com/security/notices
```

Ubuntu OVAL data:

```text
https://ubuntu.com/security/oval
```

`dpkg-query` manual:

```text
https://manpages.debian.org/dpkg-query
```

Debian package affectedness should be checked against distro-specific truth sources where vulnerability matching is the goal; your uploaded source inventory specifically calls out Debian/Ubuntu/vendor feeds as required to avoid package-backport false positives. 

---

## Q4 references

OpenSSH manual pages:

```text
https://www.openssh.org/manual.html
```

`ssh-keyscan` manual:

```text
https://man.openbsd.org/ssh-keyscan
```

`ssh-keygen` manual:

```text
https://man.openbsd.org/ssh-keygen
```

OpenSSH lists `ssh-keyscan` as the utility for gathering public host keys. ([openssh.org][8])

---

# Updated blind workflow with raw links

## 0. In Codespaces - prepare workspace

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

Reference:

```text
https://docs.github.com/codespaces/overview
```

---

# 1. Q1 - Windows Workstation VM on MacBook M1 Pro

## One-time install links

Install UTM:

```text
https://mac.getutm.app/
https://docs.getutm.app/installation/macos/
```

Install via Homebrew Cask, optional:

```bash
brew install --cask utm
sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin/utmctl
utmctl
```

Download Windows 11 ARM64 ISO:

```text
https://www.microsoft.com/software-download/windows11
https://learn.microsoft.com/en-us/windows/arm/iso
https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise
```

UTM CLI docs:

```text
https://docs.getutm.app/scripting/scripting/
```

## Create VM manually once

In UTM:

```text
+ -> Virtualize -> Windows -> select Windows 11 ARM64 ISO
Name: vuln-q1-win11
RAM: 8192 MB
CPU: 4 cores
Disk: 64 GB
```

Inside Windows PowerShell as Administrator, enable SSH:

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service -Name sshd -StartupType Automatic
New-NetFirewallRule -Name sshd -DisplayName "OpenSSH Server" -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

Reference:

```text
https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features
```

Create temp user:

```powershell
net user auditor "TempPassw0rd!" /add
net localgroup Administrators auditor /add
```

Confirm workstation/client:

```powershell
Get-CimInstance Win32_OperatingSystem |
  Select-Object Caption, Version, ProductType, OSArchitecture |
  Format-List
```

Expected:

```text
ProductType : 1
```

## Blind start / run / exit

From Mac terminal:

```bash
set -euxo pipefail

utmctl list
utmctl start "vuln-q1-win11"
```

Find VM IP inside Windows:

```powershell
ipconfig
```

Back on Mac:

```bash
export WIN_IP="PUT_WINDOWS_VM_IP_HERE"
export WIN_USER="auditor"

ssh "$WIN_USER@$WIN_IP" 'hostname'
ssh "$WIN_USER@$WIN_IP" 'powershell -NoProfile -Command "Get-CimInstance Win32_OperatingSystem | Select Caption,ProductType,OSArchitecture | Format-List"'

scp scripts/q1_windows_programs.py "$WIN_USER@$WIN_IP:C:/Users/auditor/Desktop/q1_windows_programs.py"

ssh "$WIN_USER@$WIN_IP" 'py -3 C:\Users\auditor\Desktop\q1_windows_programs.py --output C:\Users\auditor\Desktop\q1_output.txt'

scp "$WIN_USER@$WIN_IP:C:/Users/auditor/Desktop/q1_output.txt" outputs/q1_output.txt

head -80 outputs/q1_output.txt

utmctl stop "vuln-q1-win11"
```

Reference links:

```text
https://docs.python.org/3/library/winreg.html
https://learn.microsoft.com/en-us/powershell/module/appx/get-appxpackage
https://learn.microsoft.com/en-us/powershell/module/dism/get-windowspackage
```

---

# 2. Q2 - Temporary Ubuntu container for Log4j

## Links

Ubuntu official Docker image:

```text
https://hub.docker.com/_/ubuntu
```

Log4j Core fixture download:

```text
https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-core/2.17.1/log4j-core-2.17.1.jar
```

Maven Central reference:

```text
https://central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar
```

Python archive handling:

```text
https://docs.python.org/3/library/zipfile.html
```

JAR spec:

```text
https://docs.oracle.com/en/java/javase/22/docs/specs/jar/jar.html
```

## Blind start / run / exit

```bash
docker rm -f q2-log4j 2>/dev/null || true

docker run -it --name q2-log4j \
  -v "$PWD:/work" \
  -w /work \
  ubuntu:24.04 \
  bash
```

Inside container:

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

Delete temp container:

```bash
docker rm -f q2-log4j
```

---

# 3. Q3 - Temporary Debian container for package EVR

## Links

Debian official Docker image:

```text
https://hub.docker.com/_/debian
```

`dpkg-query` manual:

```text
https://manpages.debian.org/dpkg-query
```

Debian packages:

```text
https://packages.debian.org/
```

Debian security tracker:

```text
https://security-tracker.debian.org/
```

Ubuntu security references, useful if the Debian-based test OS is Ubuntu instead:

```text
https://ubuntu.com/security/notices
https://ubuntu.com/security/oval
```

## Blind start / run / exit

```bash
docker rm -f q3-debian 2>/dev/null || true

docker run -it --name q3-debian \
  -v "$PWD:/work" \
  -w /work \
  debian:12 \
  bash
```

Inside container:

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

Delete temp container:

```bash
docker rm -f q3-debian
```

---

# 4. Q4 - Temporary SSH server container

## Links

Ubuntu official Docker image:

```text
https://hub.docker.com/_/ubuntu
```

OpenSSH manual page index:

```text
https://www.openssh.org/manual.html
```

`ssh-keyscan` manual:

```text
https://man.openbsd.org/ssh-keyscan
```

`ssh-keygen` manual:

```text
https://man.openbsd.org/ssh-keygen
```

## Blind start / run / exit

Start disposable SSH server:

```bash
docker rm -f q4-sshd 2>/dev/null || true

docker run -d --name q4-sshd \
  -p 2222:22 \
  ubuntu:24.04 \
  sleep infinity

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

Run your script:

```bash
python3 scripts/q4_ssh_hostkeys.py \
  --host 127.0.0.1 \
  --port 2222 \
  --types rsa,ecdsa,ed25519 \
  --timeout 5 \
  --output outputs/q4_output.txt

cat outputs/q4_output.txt
```

Check proof:

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

Delete temp container:

```bash
docker rm -f q4-sshd
```

---

# Final proof bundle

```bash
find scripts fixtures outputs logs -type f -maxdepth 3 -print | sort

shasum -a 256 scripts/* outputs/* logs/* 2>/dev/null || true
sha256sum scripts/* outputs/* logs/* 2>/dev/null || true
```

Reference basis from your uploaded source inventory: accurate inventory, package identity, distro/vendor affectedness, & validation evidence are the key layers for avoiding incomplete or noisy vulnerability matching. 

[1]: https://docs.github.com/codespaces/overview?utm_source=chatgpt.com "What are GitHub Codespaces? - GitHub Docs"
[2]: https://docs.getutm.app/installation/macos/?utm_source=chatgpt.com "macOS | UTM Documentation"
[3]: https://docs.docker.com/desktop/setup/install/mac-install/?utm_source=chatgpt.com "Install Docker Desktop on Mac | Docker Docs"
[4]: https://hub.docker.com/_/ubuntu/?name=focal&tab=description&utm_source=chatgpt.com "ubuntu - Official Image | Docker Hub"
[5]: https://hub.docker.com/_/debian?...=&tab=description&utm_source=chatgpt.com "debian - Official Image | Docker Hub"
[6]: https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/cant-install-openssh-features?utm_source=chatgpt.com "Can't install OpenSSH Features - Windows Server | Microsoft Learn"
[7]: https://central.sonatype.com/artifact/org.apache.logging.log4j/log4j-core/2.17.1/jar?utm_source=chatgpt.com "Maven Central: org.apache.logging.log4j:log4j-core:2.17.1"
[8]: https://www.openssh.org/manual.html?utm_source=chatgpt.com "OpenSSH: Manual Pages"
