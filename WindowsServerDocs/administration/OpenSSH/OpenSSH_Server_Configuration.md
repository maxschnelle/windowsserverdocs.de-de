---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, Installation, Setup
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Konfiguration des OpenSSH-Servers für Windows
ms.openlocfilehash: ed424c33c4cd2c19a9b5e985ab6083bcbcb9fbdc
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546265"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Konfiguration des OpenSSH-Servers für Windows 10 1809 und Windows Server 2019

In diesem Thema wird die Windows-spezifische Konfiguration für OpenSSH Server (sshd) behandelt. 

OpenSSH bietet online unter [OpenSSH.com](https://www.openssh.com/manual.html) eine ausführliche Dokumentation der Konfigurationsoptionen, die in dieser Dokumentation nicht dupliziert wird. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Konfigurieren der Standardshell für OpenSSH unter Windows

Die Standardbefehlsshell stellt die Benutzeroberfläche bereit, die einem Benutzer beim Herstellen einer Verbindung mit dem Server über SSH angezeigt wird. Das erste Standardfenster ist die Windows-Befehlsshell (cmd. exe). Windows bietet auch PowerShell und Bash sowie Befehlsshells von Drittanbietern, die auch für Windows verfügbar sind und als Standardshell für einen Server konfiguriert werden können.

Um die Standardbefehlsshell festzulegen, vergewissern Sie sich zunächst, dass sich der OpenSSH-Installationsordner im Systempfad befindet. Der Standardinstallationsordner unter Windows ist SystemDrive:WindowsDirectory\System32\openssh. Die folgenden Befehle zeigen die aktuelle Pfadeinstellung und fügen den Standardordner der OpenSSH-Installation hinzu. 

Befehlsshell | Zu verwendender Befehl
------------- | -------------- 
Befehl | path
PowerShell | $env:path

Die Konfiguration der standardmäßigen SSH-Shell erfolgt in der Windows-Registrierung, indem der vollständige Pfad zur ausführbaren Shell-Datei dem Zeichenfolgenwert DefaultShell in Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH hinzugefügt wird. 

Als Beispiel legt der folgende PowerShell-Befehl die Standardshell auf PowerShell.exe fest:

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>Windows-Konfigurationen in sshd_config 

Unter Windows liest sshd Konfigurationsdaten standardmäßig aus %programdata%\ssh\sshd_config, oder es kann eine andere Konfigurationsdatei angegeben werden, indem sshd.exe mit dem Parameter -f gestartet wird.
Wenn die Datei fehlt, erzeugt sshd beim Start des Diensts eine mit der Standardkonfiguration.

Die unten aufgeführten Elemente bieten eine Windows-spezifische Konfiguration, die durch Einträge in sshd_config möglich ist. Es gibt weitere mögliche Konfigurationseinstellungen, die hier nicht aufgeführt sind, da sie in der [Onlinedokumentation zu Win32 OpenSSH](https://github.com/powershell/win32-openssh/wiki) ausführlich behandelt werden. 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers 

Das Steuern, welche Benutzer und Gruppen eine Verbindung mit dem Server herstellen können, erfolgt mithilfe der Anweisungen AllowGroups, AllowUsers, DenyGroups und DenyUsers. Die Anweisungen zum Zulassen und Verweigern werden in der folgenden Reihenfolge verarbeitet: DenyUsers, AllowUsers, DenyGroups, und schließlich AllowGroups. Alle Kontonamen müssen in Kleinbuchstaben angegeben werden. Weitere Informationen zu Mustern für Platzhalter finden Sie in ssh_config unter PATTERNS.

Wenn Sie benutzer-/gruppenbasierte Regeln mit einem Domänenbenutzer oder einer Domänengruppe konfigurieren, verwenden Sie das folgende Format: ``` user?domain* ```.
Windows lässt mehrere Formate für die Angabe von Domänenprinzipalen zu, aber viele stehen im Konflikt mit Linux-Standardmustern. Aus diesem Grund wird * zum Abdecken von FQDNs hinzugefügt. Außerdem verwendet dieser Ansatz ? anstelle von @, um Konflikte mit dem Format username@host zu vermeiden. 

Arbeitsgruppenbenutzer, Gruppen und mit dem Internet verbundene Konten werden stets in Ihren lokalen Kontonamen aufgelöst (ohne Domänenteil vergleichbar mit UNIX-Standardnamen). Domänenbenutzer und -gruppen werden streng in das Format [NameSamCompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) aufgelöst: Kurzname_der_Domäne\Benutzername. Alle Benutzer-/gruppenbasierten Konfigurationsregeln müssen sich an dieses Format halten.

Beispiele für Domänenbenutzer und -gruppen 

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

Für Windows OpenSSH sind die einzigen verfügbaren Authentifizierungsmethoden „password“ and „publickey“.

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

Der Standardwert ist „.ssh/authorized_keys .ssh/authorized_keys2“. Wenn der Pfad nicht absolut ist, wird er relativ zum Basisverzeichnis des Benutzers (oder Pfad des Profilbilds) erstellt. Beispiel: c:\users\user.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (Unterstützung in v7.7.0.0 hinzugefügt)

Dieses Verzeichnis wird nur für sftp-Sitzungen unterstützt. Eine Remotesitzung in cmd.exe würde es nicht beachten. Um einen chroot-Server für ausschließlich sftp einzurichten, legen Sie ForceCommand auf internal-sftp fest. Sie können scp auch mit chroot einrichten, indem Sie eine benutzerdefinierte Shell implementieren, die nur scp und sftp zulässt.

### <a name="hostkey"></a>HostKey

Die Standardwerte sind %programdata%/ssh/ssh_host_ecdsa_key, %programdata%/ssh/ssh_host_ed25519_key und %programdata%/ssh/ssh_host_rsa_key. Wenn die Standardwerte nicht vorhanden sind, generiert sshd diese automatisch beim Start eines Diensts.

### <a name="match"></a>Übereinstimmung

Beachten Sie die Musterregeln in diesem Abschnitt. Benutzer- und Gruppennamen erfordern Kleinschreibung.

### <a name="permitrootlogin"></a>PermitRootLogin

Gilt nicht unter Windows. Um die Administratoranmeldung zu verhindern, verwenden Sie „Administrators“ mit der DenyGroups-Anweisung.

### <a name="syslogfacility"></a>SyslogFacility

Wenn Sie eine dateibasierte Protokollierung benötigen, verwenden Sie LOCAL0. Protokolle werden unter %programdata%\ssh\logs generiert.
Jeder andere Wert, einschließlich des Standardwerts AUTH, leitet die Protokollierung an ETW. Weitere Informationen finden Sie unter „Protokollierungsmöglichkeiten unter Windows“.

### <a name="not-supported"></a>Nicht unterstützt. 

Die folgenden Konfigurationsoptionen sind in der OpenSSH-Version unter Windows Server 2019 und Windows 10 1809 nicht verfügbar:

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

