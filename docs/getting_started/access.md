# Access from laptop

How to setup your developer environment so that you can check out code and start working.
## Device-specific installation steps
### Windows Installation
You can either work directly from Windows or use WSL in order to develop in a Linux context from you Windows laptop
#### Native Windows setup using Scoop

Script that will install the basics for working with Salesforce on a clean Windows PC
```powershell
echo Install Scoop
call Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
call irm get.scoop.sh | iex

clear
echo Add scoop buckets
call scoop bucket add java
call scoop bucket add extras

clear
echo Install Java, nodejs, git and vsCode
call scoop install temurin17-jdk
call scoop install nodejs-lts
call scoop install git
call scoop install vscode

clear
echo Install SF-cli
call npm install -global @salesforce/cli


clear
echo Install Salesforce Extension Pack (Expanded)
call code --install-extension "salesforce.salesforcedx-vscode-expanded"

clear
echo Set Java path for the plugin salesforcedx-vscode-apex.java.home in settings.json

$scoopAppsHome = "$HOME\scoop\apps"
$javaPath = "$scoopAppsHome\temurin17-jdk\current"
$jsonVscodeUserSettingsPath = "$scoopAppsHome\vscode\current\data\user-data\User\settings.json"

$vscodeUserSettingsJson = Get-Content "$jsonVscodeUserSettingsPath" -Raw | ConvertFrom-Json
$vscodeUserSettingsJson | Add-Member -Force -MemberType NoteProperty -Name "salesforcedx-vscode-apex.java.home" -Value "$javaPath"
$vscodeUserSettingsJson | ConvertTo-Json | Out-File "$jsonVscodeUserSettingsPath" -Encoding utf8

clear
echo Salesforce utviklingsmiljøet er satt opp.
echo Neste steg er å konfigurere git samt sjekke ut repoet du skal jobbe med
```

### Windows with WSL Installation
Before starting with this setup you should spend some time to familiarise yourself with WSL and remote development with WSL.

#### Resources
- [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
    - [Get started using Visual Studio Code with Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode)
    - [Get started using Git on Windows Subsystem for Linux]( https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git)
        - [Git Credential Manager setup](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git#git-credential-manager-setup)
- [VS Code Documentation](https://code.visualstudio.com/docs)
    - [Developing in WSL](https://code.visualstudio.com/docs/remote/wsl)

#### Install git and VS Code
1. Install [Scoop](https://scoop.sh) unless you already have it. 
 Scoop makes it possible to install and maintain programs from the command line.
2. Add buckets
   ```powershell
   scoop bucket add extras
   ```
3. Install GIT
   ```powershell
   scoop install git
   ```
4. Install vscode
   ```powershell
   scoop install vscode
   ```

#### Setup WSL
1. Open NAV Programvaresenter
2. Install "Windows Subsytem for Linux (WSL) - Vil restarte!"
3. Update WSL
   ```powershell
   wsl --update
   ```
4. Install your preferred Linux distro
#### Setup Ubuntu WSL
1. Installer GIT
    ```
    add-apt-repository ppa:git-core/ppa
    ```
    ```
    apt update
    ```
    ```
    apt install git
    ```
    ```
    git config --global credential.helper "/mnt/c/Users/<NAVIDENT>/scoop/apps/git/current/mingw64/bin/git-credential-manager.exe"
    ```
2. Install Node
    1. Add sf-cli to Node
   ```
   npm install @salesforce/cli --global
   ```
3. Install Java
    1. The Salesforce plugin for VS Code requires Java version 8,11 or 17. You can read more about it [here](https://developer.salesforce.com/tools/vscode/en/vscode-desktop/java-setup). The following example uses temurin17
    ```
    wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo apt-key add -
    ```
    ```
    apt-get update
    ```
    ```
    apt-get install temurin-17-jdk
    ```
#### Setup VS Code
1. Install the Remote Development extension
    ```
    code --install-extension "ms-vscode-remote.vscode-remote-extensionpack"
    ```
2. Installer Salesforce Extension
   ```
    code --install-extension "salesforce.salesforcedx-vscode-expanded"
    ```
3. Oppdater Apex pluginen med Java Home
    1. Gå til Settings
    2. Velg "Remote [WSL:Ubuntu]" (eller den versjonen du har lagt inn)
    3. Extensions => Salesforce Apex Configuration
    4. Sett Java Home til => `/usr/lib/jvm/temurin-17-jdk-amd64 (dersom du har et annet oppsett en det som er beskrevet her så legg inn den pathen du hadde.`


#### Install and setup GPG for WSL
The repositories requires signed commits, here is a description of how to set this up with the WSL setup
In Windows install GPG with Scoop
```powershell
scoop install gpg
```
Then switch to your WSL installation and to GPG
```
sudo apt-get install gpg gnupg gpg-agent
```
Edit or create the config file `~/.gnupg/gpg-agent.conf` with the content below. IMPORTANT: set `pinentry-program` to point to your Windows installation of pinentry-basic.exe, [USER] must be set to your user.
```
default-cache-ttl 34560000
max-cache-ttl 34560000
pinentry-program "/mnt/c/Users/[USER]/scoop/apps/gpg/current/bin/pinentry-basic.exe"
```
The `pinentry-program` configuration explicitly tells GPG to use the pin entry app installed in Windows. 

Restart gpg
```
gpgconf --kill gpg-agent
```

Proceed to generate GPG key pairs and add the key to your GitHub user.