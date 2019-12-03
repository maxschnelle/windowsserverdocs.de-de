---
ms.date: 09/27/2019
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, Installation, Setup
contributor: maertendMSFT
author: maertendMSFT
title: Installation von OpenSSH für Windows
ms.openlocfilehash: 3c742e20432d20ea3c402af66f19a803ea1f3a56
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2019
ms.locfileid: "71934929"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Installation von OpenSSH für Windows Server 2019 und Windows 10 #

Der OpenSSH-Client und der OpenSSH-Server sind unter Windows Server 2019 und Windows 10 1809 separat installierbare Komponenten.
Benutzer mit diesen Windows-Versionen sollten die folgenden Anweisungen zum Installieren und Konfigurieren von OpenSSH befolgen. 

> [!NOTE] 
> Benutzer, die OpenSSH aus dem PowerShell-GitHub-Repository (https://github.com/PowerShell/OpenSSH-Portable) ) bezogen haben, sollten die Anweisungen dort und __nicht diese Anweisungen__ befolgen. 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Installieren von OpenSSH unter Windows Server 2019 oder Windows 10 1809

OpenSSH-Client und -Server sind Installierbare Features von Windows 10 1809. 

Zum Installieren von OpenSSH wechseln Sie zu „Einstellungen“ und dann zu „Apps“ > „Apps und Features“ > Optionale Features“. 

Durchsuchen Sie diese Liste, um festzustellen, ob „OpenSSH-Client“ bereits installiert ist. Falls nicht, wählen Sie oben auf der Seite „Feature hinzufügen“ aus. 

* Um den OpenSSH-Client zu installieren, navigieren Sie zu „OpenSSH-Client“, und klicken Sie dann auf „Installieren“. 
* Um den OpenSSH-Server zu installieren, navigieren Sie zu „OpenSSH-Server“, und klicken Sie dann auf „Installieren“. 

Kehren Sie nach der Installation zu „Apps“ > „Apps und Features“ > „Optionale Features“ zurück. Die OpenSSH-Komponenten sollten aufgeführt sein.

> [!NOTE]
> Durch die Installation von OpenSSH-Server wird eine Firewallregel mit dem Namen „OpenSSH-Server-in-TCP“ erstellt und aktiviert. Diese lässt eingehenden SSH-Datenverkehr an Port 22 zu. 

## <a name="installing-openssh-with-powershell"></a>Installieren von OpenSSH mit PowerShell 

Um OpenSSH mithilfe von PowerShell zu installieren, starten Sie zunächst PowerShell als Administrator.
So stellen Sie sicher, dass die OpenSSH-Features für die Installation zur Verfügung stehen

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

Installieren Sie dann die Server- und/oder Clientfeatures:

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
```

## <a name="uninstalling-openssh"></a>Deinstallieren von OpenSSH

Zum Deinstallieren von OpenSSH in den Windows-Einstellungen wechseln Sie zu „Einstellungen“ und dann zu „Apps“ > „Apps und Features“ > Optionale Features“. Wählen Sie in der Liste der installierten Features die Komponente „OpenSSH-Client“ oder „OpenSSH-Server“ und dann „Deinstallieren“ aus.

Führen Sie zum Deinstallieren von OpenSSH mithilfe von PowerShell einen der folgenden Befehle aus:

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

Nach dem Entfernen von OpenSSH ist möglicherweise ein Neustart von Windows erforderlich, wenn der Dienst zum Zeitpunkt der Deinstallation verwendet wird.


## <a name="initial-configuration-of-ssh-server"></a>Erstkonfiguration des SSH-Servers

Um den OpenSSH-Server für die erstmalige Verwendung unter Windows zu konfigurieren, starten Sie PowerShell als Administrator. Führen Sie dann die folgenden Befehle aus, um den SSHD-Dienst zu starten:

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

## <a name="initial-use-of-ssh"></a>Erstmalige Verwendung von SSH

Nachdem Sie den OpenSSH-Server unter Windows installiert haben, können Sie ihn schnell mithilfe von PowerShell auf jedem Windows-Gerät testen, auf dem der SSH-Client installiert ist. Geben Sie in PowerShell folgenden Befehl ein: 

```powershell
Ssh username@servername
```

Die erste Verbindung mit einem beliebigen Server führt zu einer Meldung ähnlich der folgenden:

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

Die Antwort muss entweder „yes“ oder „no“ sein. Wenn Sie mit „Yes“ antworten, wird dieser Server der Liste bekannter SSH-Hosts des lokalen Systems hinzugefügt.

An dieser Stelle werden Sie zur Eingabe des Kennworts aufgefordert. Als Sicherheitsmaßnahme wird Ihr Kennwort nicht angezeigt, während Sie es eingeben. 

Nachdem Sie eine Verbindung hergestellt haben, wird eine Befehlsshell-Eingabeaufforderung ähnlich der folgenden angezeigt:

```
domain\username@SERVERNAME C:\Users\username>
```

Die Standardshell, die vom OpenSSH-Server unter Windows verwendet wird, ist die Windows-Befehlsshell. 

