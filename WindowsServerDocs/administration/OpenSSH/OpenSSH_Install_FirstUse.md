---
ms.date: 09/27/2019
ms.topic: conceptual
keywords: OpenSSH, SSH, sshd, installieren, Setup
contributor: maertendMSFT
author: maertendMSFT
title: OpenSSH-Installation für Windows
ms.openlocfilehash: 3c742e20432d20ea3c402af66f19a803ea1f3a56
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2019
ms.locfileid: "71934929"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Installation von OpenSSH für Windows Server 2019 und Windows 10 #

Der OpenSSH-Client und der OpenSSH-Server sind separat installierbare Komponenten in Windows Server 2019 und Windows 10 1809.
Benutzer mit diesen Windows-Versionen sollten die folgenden Anweisungen zum Installieren und Konfigurieren von OpenSSH verwenden. 

> [!NOTE] 
> Benutzer, die OpenSSH aus dem PowerShell-GitHub- https://github.com/PowerShell/OpenSSH-Portable) Repository erworben haben (sollten die Anweisungen von dort verwenden und sollten diese Anweisungen __nicht__ verwenden. 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Installieren von OpenSSH über die Benutzeroberfläche für Einstellungen unter Windows Server 2019 oder Windows 10 1809

OpenSSH Client und Server sind Installierbare Features von Windows 10 1809. 

Zum Installieren von OpenSSH wechseln Sie zu Apps > apps und Features > Verwalten optionaler Features. 

Scannen Sie diese Liste, um festzustellen, ob OpenSSH Client bereits installiert ist. Wenn dies nicht der Grund ist, wählen Sie oben auf der Seite "Feature hinzufügen" aus, und klicken Sie dann auf: 

* Um den OpenSSH-Client zu installieren, suchen Sie nach "OpenSSH Client", und klicken Sie dann auf "installieren". 
* Um den OpenSSH-Server zu installieren, suchen Sie nach "OpenSSH Server", und klicken Sie dann auf "installieren". 

Wenn die Installation abgeschlossen ist, kehren Sie zu Apps > apps und Features > Verwalten optionaler Features zurück, und die OpenSSH-Komponente sollte aufgeführt werden.

> [!NOTE]
> Durch die Installation von OpenSSH Server wird eine Firewallregel mit dem Namen "OpenSSH-Server-in-TCP" erstellt und aktiviert. Dies ermöglicht eingehenden SSH-Datenverkehr an Port 22. 

## <a name="installing-openssh-with-powershell"></a>Installieren von OpenSSH mit PowerShell 

Um OpenSSH mithilfe von PowerShell zu installieren, starten Sie zunächst PowerShell als Administrator.
So stellen Sie sicher, dass die OpenSSH-Funktionen für die Installation zur Verfügung stehen:

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

Installieren Sie dann die Server-und/oder Client Features:

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

## <a name="uninstalling-openssh"></a>OpenSSH wird deinstalliert.

Wenn Sie OpenSSH mithilfe der Windows-Einstellungen deinstallieren möchten, wechseln Sie zu Apps > apps und Features > Verwalten optionaler Features. Wählen Sie in der Liste der installierten Features die Komponente OpenSSH Client oder OpenSSH Server aus, und wählen Sie dann deinstallieren aus.

Verwenden Sie zum Deinstallieren von OpenSSH mithilfe von PowerShell einen der folgenden Befehle:

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

Nach dem Entfernen von OpenSSH ist möglicherweise ein Windows-Neustart erforderlich, wenn der Dienst zum Zeitpunkt der Installation verwendet wird.


## <a name="initial-configuration-of-ssh-server"></a>Anfängliche Konfiguration des SSH-Servers

Um den OpenSSH-Server für die anfängliche Verwendung unter Windows zu konfigurieren, starten Sie PowerShell als Administrator, und führen Sie dann die folgenden Befehle aus, um den sshd-Dienst zu starten:

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

## <a name="initial-use-of-ssh"></a>Anfängliche Verwendung von SSH

Nachdem Sie den OpenSSH-Server unter Windows installiert haben, können Sie ihn schnell mithilfe von PowerShell auf jedem Windows-Gerät testen, auf dem der SSH-Client installiert ist. Geben Sie in PowerShell den folgenden Befehl ein: 

```powershell
Ssh username@servername
```

Die erste Verbindung mit einem beliebigen Server führt zu einer Meldung, die der folgenden Meldung ähnelt:

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

Die Antwort muss entweder "yes" oder "No" lauten. Wenn Sie auf Ja antworten, wird dieser Server der Liste bekannter SSH-Hosts des lokalen Systems hinzugefügt.

An dieser Stelle werden Sie zur Eingabe des Kennworts aufgefordert. Als Sicherheitsmaßnahme wird Ihr Kennwort nicht angezeigt, wenn Sie eingeben. 

Nachdem Sie eine Verbindung hergestellt haben, wird eine Befehlsshell-Eingabeaufforderung ähnlich der folgenden angezeigt:

```
domain\username@SERVERNAME C:\Users\username>
```

Die Standardshell, die von Windows OpenSSH Server verwendet wird, ist die Windows-Befehlsshell. 

