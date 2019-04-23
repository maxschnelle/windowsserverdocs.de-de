---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH "," SSH "," SSHD, installieren, tritt beim setup
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: OpenSSH-Server-Konfiguration für Windows
ms.openlocfilehash: 8e6476e4005bd5bbc2d40c8a59d39510ca1beb70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827281"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>OpenSSH-Server-Konfiguration für Windows 10-1809 und Server 2019#

Dieses Thema behandelt die Windows-spezifische Konfiguration für OpenSSH-Server (Sshd). 

OpenSSH verwaltet, ausführliche Dokumentation hinsichtlich der Konfigurationsoptionen online auf [OpenSSH.com](https://www.openssh.com/manual.html), die in dieser Dokumentation nicht dupliziert werden. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Konfigurieren die Standardshell für OpenSSH in Windows

Die Standard-Befehlsshell bietet die Benutzeroberfläche, die ein Benutzer erhält bei der an den Server mithilfe von SSH eine Verbindung herstellen. Der anfängliche Standardwert Windows ist die Windows-Befehlsshell (cmd.exe). Windows enthält auch die PowerShell- und Bash und Drittanbieter-Befehlsshells sind auch für Windows verfügbar und können als die Standardshell für einen Server konfiguriert werden.

Zum Festlegen der Standard-Befehlsshell bestätigen Sie, dass der OpenSSH-Installationsordner unter dem Systempfad befindet. Für Windows ist der Standardinstallationsordner SystemDrive:WindowsDirectory\System32\openssh. Die folgenden Befehle, zeigt die aktuelle Einstellung für den Pfad, und fügen Sie den standardmäßigen OpenSSH-Installationsordner hinzu. 

Befehls-shell | Befehl verwendet
------------- | -------------- 
Befehl | path
PowerShell | $env:\path

Konfigurieren der standardmäßigen ssh Shell in der Windows-Registrierung erfolgt durch den vollständigen Pfad der ausführbaren Datei Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH im Zeichenfolgenwert DefaultShell Shell hinzufügen. 

Beispielsweise legt die folgende Powershell-Befehl die Standardshell PowerShell.exe sein:

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshdconfig"></a>Windows-Konfigurationen in "sshd_config" 

In Windows Sshd liest Konfigurationsdaten aus %programdata%\ssh\sshd_config standardmäßig oder eine anderen Konfigurationsdatei kann angegeben werden, indem starten sshd.exe mit dem -f-Parameter.
Wenn die Datei nicht vorhanden ist, generiert Sshd mit der Standardkonfiguration, wenn der Dienst gestartet wurde.

Die unten aufgeführten Elemente bieten die Windows-spezifischen Konfiguration möglich über Einträge in "sshd_config". Es gibt andere Konfigurationseinstellungen in möglich, die hier nicht aufgelistet werden, wie sie in der online-ausführlich behandelt werden [Win32 OpenSSH Dokumentation](https://github.com/powershell/win32-openssh/wiki). 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers 

Steuern, welche Benutzer und Gruppen, mit dem Server verbinden können erfolgt mithilfe der Direktiven AllowGroups, AllowUsers, DenyGroups und DenyUsers. Die Zulassen/Verweigern-Direktiven werden in der folgenden Reihenfolge verarbeitet: DenyUsers, AllowUsers, DenyGroups und schließlich AllowGroups. Alle Kontonamen müssen in Kleinbuchstaben angegeben werden. Muster in Ssh_config für Weitere Informationen zu Mustern für Platzhalter angezeigt.

Beim Konfigurieren von Benutzer-/Gruppenkonten Regeln mit einem Domänenbenutzer oder-Gruppen basieren, verwenden Sie das folgende Format: ``` user?domain* ```.
Windows ermöglicht mehrere Formate zum Angeben von Domänenprinzipale viele mit Linux-Standardmuster in Konflikt stehen. Aus diesem Grund * wird hinzugefügt, um FQDNs abzudecken. Dieser Ansatz verwendet außerdem "?", statt @, zur Vermeidung von Konflikten mit der username@host Format. 

Arbeit Gruppe Benutzer/Gruppen und Konten Internetverbindung werden immer auf ihre lokalen Account-Name (kein Teil der Domäne, ähnlich wie standard-Unix-Namen) aufgelöst werden. Domänen-Benutzer und Gruppen werden ausschließlich in aufgelöst [NameSamCompatible](https://docs.microsoft.com/en-us/windows/desktop/api/secext/ne-secext-extended_name_format) Format auf: Domain_short_name\user_name. Alle Benutzer/Gruppe basieren, Konfiguration, die Regeln in dieses Format entsprechen müssen.

Beispiele für Domänenbenutzer und Gruppen 

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

Beispiele für lokale Benutzer und Gruppen 

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods 

Für Windows-OpenSSH sind die einzige verfügbare Authentifizierungsmethoden "Password" und "Publickey".

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

Der Standardwert ist "".SSH "/ Authorized_keys".SSH "/ authorized_keys2". Wenn der Pfad kein absoluter ist, wird diese relativ zum Basisverzeichnis des Benutzers (oder Image-Profilpfad) übernommen. Beispiel: c:\users\user.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (hinzugefügt in v7.7.0.0-Unterstützung)

Diese Richtlinie wird nur mit Sftp-Sitzungen unterstützt. Eine Remotesitzung in cmd.exe wäre nicht dies berücksichtigt. Um eine reine Sftp Chroot-Server-setup aus, legen Sie ForceCommand auf interne Sftp fest. Sie können auch einrichten scp mit Chroot, durch die Implementierung einer benutzerdefinierten Shell, die nur scp und Sftp zulassen würde.

### <a name="hostkey"></a>HostKey

Die Standardwerte sind % programdata%/ssh/ssh_host_ecdsa_key, %programdata%/ssh/ssh_host_ed25519_key und % programdata%/ssh/ssh_host_rsa_key. Wenn die Standardwerte nicht vorhanden sind, generiert Sshd automatisch auf einen Dienst starten.

### <a name="match"></a>Übereinstimmung

Beachten Sie, die Regeln in diesem Abschnitt des Musters. Benutzer-und Gruppennamen muss in Kleinbuchstaben.

### <a name="permitrootlogin"></a>PermitRootLogin

In Windows nicht anwendbar. Um die Anmeldeinformationen des Administrators zu verhindern, verwenden Sie Administratoren DenyGroups Richtlinie aus.

### <a name="syslogfacility"></a>SyslogFacility

Wenn Sie dateibasierte Protokollierung benötigen, verwenden Sie LOCAL0. Protokolle werden unter % programdata%\ssh\logs generiert.
Jeder andere Wert ist, einschließlich des Standardwerts AUTH weist ETW-Protokollierung. Weitere Informationen finden Sie in der Protokollierung von Funktionen in Windows.

### <a name="not-supported"></a>Nicht unterstützt. 

Die folgenden Konfigurationsoptionen sind nicht verfügbar, in der OpenSSH-Version, die in Windows Server-2019 und Windows 10-1809 bereitgestellt wird:

* AcceptEnv
* AllowStreamLocalForwarding
* AuthorizedKeysCommand
* AuthorizedKeysCommandUser
* AuthorizedPrincipalsCommand
* AuthorizedPrincipalsCommandUser
* Komprimierung
* ExposeAuthInfo
* GSSAPIAuthentication
* GSSAPICleanupCredentials
* GSSAPIStrictAcceptorCheck
* HostbasedAcceptedKeyTypes
* HostbasedAuthentication
* HostbasedUsesNameFromPacketOnly
* IgnoreRhosts
* IgnoreUserKnownHosts
* KbdInteractiveAuthentication
* KerberosAuthentication
* KerberosGetAFSToken
* KerberosOrLocalPasswd
* KerberosTicketCleanup
* PermitTunnel
* PermitUserEnvironment
* PermitUserRC
* PidFile
* PrintLastLog
* RDomain
* StreamLocalBindMask
* StreamLocalBindUnlink
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XAuthLocation

