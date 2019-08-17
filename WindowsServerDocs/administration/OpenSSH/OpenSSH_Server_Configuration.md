---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, sshd, installieren, Setup
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: OpenSSH-Server Konfiguration für Windows
ms.openlocfilehash: ed424c33c4cd2c19a9b5e985ab6083bcbcb9fbdc
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546265"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>OpenSSH-Serverkonfiguration für Windows 10 1809 und Server 2019

In diesem Thema wird die Windows-spezifische Konfiguration für OpenSSH Server (sshd) behandelt. 

OpenSSH verwaltet eine ausführliche Dokumentation für Konfigurationsoptionen online unter [OpenSSH.com](https://www.openssh.com/manual.html), die in diesem Dokumentations Satz nicht dupliziert wird. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Konfigurieren der Standardshell für OpenSSH in Windows

Die standardbefehlsshell ermöglicht dem Benutzer, wenn er über ssh eine Verbindung mit dem Server herstellt. Das erste Standardfenster ist die Windows-Befehlsshell (cmd. exe). Windows umfasst auch PowerShell und bash, und Befehls Shells von Drittanbietern sind auch für Windows verfügbar und können als Standardshell für einen Server konfiguriert werden.

Um die standardbefehlsshell festzulegen, vergewissern Sie sich zunächst, dass sich der OpenSSH-Installationsordner im Systempfad befindet. Der Standard Installationsordner für Windows ist System Drive: windowsdirectory\system32\openssh. Mit den folgenden Befehlen wird die aktuelle Pfad Einstellung angezeigt, und es wird der OpenSSH-Standard Installationsordner hinzugefügt. 

Befehlsshell | Zu verwendenden Befehl
------------- | -------------- 
Befehl | path
PowerShell | $ENV:p ATH

Die Konfiguration der standardssh-Shell erfolgt in der Windows-Registrierung durch Hinzufügen des vollständigen Pfads zur ausführbaren Shell-Datei zu Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH im Zeichen folgen Wert DefaultShell. 

Beispielsweise wird mit dem folgenden PowerShell-Befehl die Standardshell auf "PowerShell. exe" festgelegt:

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>Windows-Konfigurationen in sshd_config 

In Windows liest sshd Konfigurationsdaten standardmäßig aus%ProgramData%\ssh\sshd_config, oder es kann eine andere Konfigurationsdatei angegeben werden, indem "sshd. exe" mit dem Parameter "-f" gestartet wird.
Wenn die Datei nicht vorhanden ist, generiert sshd eine mit der Standardkonfiguration, wenn der Dienst gestartet wird.

Die unten aufgeführten Elemente bieten eine Windows-spezifische Konfiguration durch Einträge in sshd_config. Es sind andere Konfigurationseinstellungen in möglich, die hier nicht aufgeführt sind, da Sie in der Online- [Win32 OpenSSH-Dokumentation](https://github.com/powershell/win32-openssh/wiki)ausführlich behandelt werden. 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers 

Das Steuern, welche Benutzer und Gruppen eine Verbindung mit dem Server herstellen können, erfolgt mithilfe der Anweisungen AllowGroups, AllowUsers, DenyGroups und DenyUsers. Die allow/Deny-Direktiven werden in der folgenden Reihenfolge verarbeitet: DenyUsers, AllowUsers, DenyGroups und schließlich AllowGroups. Alle Kontonamen müssen in Kleinbuchstaben angegeben werden. Weitere Informationen zu Mustern für Platzhalter finden Sie unter Patterns in ssh_config.

Wenn Sie Benutzer-/Gruppenbasierte Regeln mit einem Domänen Benutzer oder einer Gruppe konfigurieren, verwenden ``` user?domain* ```Sie das folgende Format:.
Windows ermöglicht mehrere Formate zum Angeben von Domänen Prinzipale, aber viele Konflikte mit Linux-Standard Mustern. Aus diesem Grund wird * zum abdecken von FQDNs hinzugefügt. Bei diesem Ansatz wird auch "?" anstelle von @ verwendet, um Konflikte mit dem username@host Format zu vermeiden. 

Arbeitsgruppen Benutzer/-Gruppen und mit dem Internet verbundene Konten werden stets in Ihren lokalen Kontonamen aufgelöst (kein Domänen Teil, vergleichbar mit UNIX-Standardnamen). Domänen Benutzer und-Gruppen werden streng in das [namesamcompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) -Format aufgelöst domain_short_name\user_name. Alle Benutzer-/gruppenbasierten Konfigurations Regeln müssen diesem Format entsprechen.

Beispiele für Domänen Benutzer und-Gruppen 

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

### <a name="authenticationmethods"></a>Authenticationmethods 

Für Windows OpenSSH sind die einzigen verfügbaren Authentifizierungsmethoden "Password" und "PublicKey".

### <a name="authorizedkeysfile"></a>Authorizedkeysfile 

Der Standardwert ist ". ssh/authorized_keys. ssh/authorized_keys2". Wenn der Pfad nicht absolut ist, wird er relativ zum Basisverzeichnis des Benutzers (oder Profil Image Pfad) erstellt. Fern. c:\benutzer\benutzername.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (Unterstützung in v 7.7.0.0 hinzugefügt)

Diese Direktive wird nur für SFTP-Sitzungen unterstützt. Eine Remote Sitzung in "cmd. exe" würde dies nicht beachten. Legen Sie für ForceCommand den Wert internal-SFTP fest, um einen nur SFTP-Server zu erstellen. Sie können auch SCP mit chroot einrichten, indem Sie eine benutzerdefinierte Shell implementieren, die nur SCP und SFTP zulässt.

### <a name="hostkey"></a>HostKey

Die Standardwerte sind% Program Data%/SSH/ssh_host_ecdsa_key,% Program Data%/SSH/ssh_host_ed25519_key und% Program Data%/SSH/ssh_host_rsa_key. Wenn die Standardwerte nicht vorhanden sind, generiert sshd diese automatisch bei einem Dienst Start.

### <a name="match"></a>Übereinstimmung

Beachten Sie die Musterregeln in diesem Abschnitt. Benutzer-und Gruppennamen sollten Kleinbuchstaben aufweisen.

### <a name="permitrootlogin"></a>PermitRootLogin

Nicht anwendbar in Windows. Verwenden Sie Administratoren mit der DenyGroups-Direktive, um die Administrator Anmeldung zu verhindern.

### <a name="syslogfacility"></a>Syslogfacility

Wenn Sie dateibasierte Protokollierung benötigen, verwenden Sie LOCAL0. Die Protokolle werden unter%ProgramData%\ssh\logs. generiert.
Jeder andere Wert, einschließlich der Standardwert Authentifizierung, leitet die Protokollierung an etw weiter. Weitere Informationen finden Sie unter Protokollierungs Einrichtungen in Windows.

### <a name="not-supported"></a>Nicht unterstützt. 

Die folgenden Konfigurationsoptionen sind in der OpenSSH-Version, die im Lieferumfang von Windows Server 2019 und Windows 10 1809 enthalten ist, nicht verfügbar:

* Akzeptenv
* Allowstreamlocalforwarding
* Authorizedkeyscommand
* Authorizedkeyscommanduser
* Authorizedprincipalscommand
* Authorizedprincipalscommanduser
* Komprimierung
* Expoabauthinfo
* GSSAPIAuthentication
* Gssapicleanupanmelde Informationen
* Gssapistrictakzeptorcheck
* Hostbasedakzeptedkeytypes
* HostbasedAuthentication
* Hostbasedusesnamefrompacketonly
* IgnoreRhosts
* Ignoreuserknownhosts
* Kbdinteractiveauthentication
* Kerberosauthentication
* Kerberosgetaf stoken
* Kerberosorlocalpasswd
* Kerberosticketcleanup
* Permittunnel
* Permituserenvironment
* Permituserrc
* PidFile
* Printlastlog
* Rdomain
* Streamlocalbindmask
* Streamlocalbindunlink
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XauthLocation

