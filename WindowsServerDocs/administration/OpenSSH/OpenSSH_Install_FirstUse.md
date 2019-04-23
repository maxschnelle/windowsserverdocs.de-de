---
ms.date: 01/07/2019
ms.topic: conceptual
keywords: OpenSSH "," SSH "," SSHD, installieren, tritt beim setup
contributor: maertendMSFT
author: maertendMSFT
title: Installation von OpenSSH für Windows
ms.openlocfilehash: f617b01ee7dabd4897f99e374420f673e209e145
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859561"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Installation von OpenSSH für WindowsServer 2019 und Windows 10 #

OpenSSH-Client und OpenSSH-Server werden separat installierbare Komponenten in Windows Server-2019 und Windows 10-1809.
Benutzer mit dieser Windows-Versionen sollten die Anweisungen verwenden, die zum Installieren und Konfigurieren von OpenSSH folgen. 

> [!NOTE] 
> Benutzer, die OpenSSH erworben, das PowerShell-Github-Repository haben (https://github.com/PowerShell/OpenSSH-Portable) soll, verwenden Sie die Anweisungen aus, und __sollte nicht__ verwenden Sie diese Anweisungen. 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Installieren von OpenSSH von der Einstellungs-Benutzeroberfläche auf WindowsServer 2019 oder Windows 10-1809

Sind installierbaren Features von Windows 10-1809, OpenSSH-Client und Server. 

Um OpenSSH zu installieren, starten Sie die Einstellungen finden Sie unter Apps > Apps und Features > optionale Funktionen verwalten. 

Überprüfen Sie diese Liste, um festzustellen, ob OpenSSH-Client bereits installiert ist. Wenn dies nicht der Fall ist, wählen Sie dann am oberen Rand der Seite "Hinzufügen eines Features", klicken Sie dann: 

* Um den OpenSSH-Client zu installieren, suchen Sie "OpenSSH-Client", und klicken Sie dann "Installieren". 
* Um den OpenSSH-Server installieren, navigieren Sie zu "OpenSSH Server", und klicken Sie auf "Installieren". 

Nach Abschluss der Installation zurück, um Apps > Apps und Features > optionale Funktionen verwalten, und Sie sehen, sollten die OpenSSH-Komponenten aufgeführt.

> [!NOTE]
> Installieren von OpenSSH-Server erstellen und Aktivieren einer Firewallregel mit dem Namen "OpenSSH-Server-In-TCP". Dadurch können eingehende SSH-Datenverkehr über Port 22. 

## <a name="installing-openssh-with-powershell"></a>Installieren von OpenSSH mit PowerShell 

Starten Sie zuerst PowerShell als Administrator, um OpenSSH mithilfe von PowerShell zu installieren.
Um sicherzustellen, dass die OpenSSH-Funktionen für die Installation verfügbar sind:

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

Installieren Sie dann die Server und/oder Client-Funktionen:

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

Um mithilfe der Windows-Einstellungen OpenSSH zu deinstallieren, starten Sie die Einstellungen finden Sie unter Apps > Apps und Features > optionale Funktionen verwalten. Wählen Sie in der Liste der installierten Features die Komponente OpenSSH-Client oder OpenSSH-Server, und wählen Sie dann deinstallieren.

Um OpenSSH mithilfe von PowerShell zu deinstallieren, verwenden Sie einen der folgenden Befehle aus:

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

Ein Windows-Neustart kann erforderlich sein, nach der Deinstallation von OpenSSH, entfernen, wenn der Dienst verwendet, die zum Zeitpunkt wird.


## <a name="initial-configuration-of-ssh-server"></a>Erstkonfiguration von SSH-Server

Klicken Sie zum Konfigurieren des OpenSSH-Servers für die erstmalige Verwendung unter Windows starten Sie PowerShell als Administrator, und führen Sie die folgenden Befehle aus, um die SSHD-Dienst zu starten:

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled 
```

## <a name="initial-use-of-ssh"></a>Erstmalige Verwendung von SSH

Nachdem Sie das OpenSSH-Server unter Windows installiert haben, können Sie mithilfe von PowerShell auf einem beliebigen Windows-Gerät mit dem SSH-Client installiert schnell testen. Geben Sie in PowerShell den folgenden Befehl ein: 

```powershell
Ssh username@servername
```

Die erste Verbindung zu einem beliebigen Server wird eine Meldung ähnlich der folgenden ausgegeben:

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

Die Antwort muss entweder "yes" oder "no". Mit Ja antworten, dieser Server hinzugefügt wird, auf das lokale System die Liste der bekannten ssh Hosts.

Für das Kennwort werden an diesem Punkt Sie aufgefordert. Als Sicherheitsmaßnahme wird Ihr Kennwort nicht angezeigt werden, während der Eingabe. 

Nachdem Sie eine Verbindung herstellen, sehen Sie eine Shell-Eingabeaufforderung, die etwa wie folgt:

```
domain\username@SERVERNAME C:\Users\username>
```

Die Standardshell von Windows OpenSSH-Server verwendet, ist die Windows-Befehlsshell. 

