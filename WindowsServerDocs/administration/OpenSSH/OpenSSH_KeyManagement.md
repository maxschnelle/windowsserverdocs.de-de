---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH "," SSH "," SSHD, installieren, tritt beim setup
contributor: maertendMSFT
author: maertendMSFT
title: OpenSSH-Server-Konfiguration für Windows
ms.product: w10
ms.openlocfilehash: 3e2981cbbdfe34bf28a77d5121bff0b663e0d3bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837151"
---
# <a name="openssh-key-management"></a>OpenSSH-Schlüsselverwaltung

Die meisten in Umgebungen mit Windows-Authentifizierung erfolgt mit einem Paar aus Benutzername und Kennwort.
Dies eignet sich gut für Systeme, die eine gemeinsame Domäne freigeben. Wenn Sie über Domänen hinweg zu arbeiten, wird z. B. zwischen lokalen und cloudbasierten Systemen, es zunehmend schwieriger.

Linux-Umgebungen wird im Vergleich dazu häufig öffentlichem Schlüssel/Private Schlüssel-Paare, die Laufwerk-Authentifizierung verwenden.
OpenSSH enthält Tools, mit denen dies insbesondere unterstützt:

* __SSH-Keygen__ zum sicheren Schlüssel generieren
* __SSH-Agent__ und __ssh-add-__ zum sicheren Speichern von privaten Schlüsseln
* __SCP__ und __Sftp__ sichere Kopieren von Dateien für öffentliche Schlüssel während der ersten Verwendung eines Servers

Dieses Dokument enthält eine Übersicht über diese Tools auf Windows zu verwenden, um zu beginnen, SSH-Schlüsselauthentifizierung mit. Wenn Sie mit der Verwaltung der SSH-Schlüssel nicht vertraut sind, sollten Sie dringend Sie überprüfen, [NIST-Dokument IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) mit dem Titel "Security interaktiv und automatisierte Access Management Using Secure Shell (SSH)."

## <a name="about-key-pairs"></a>Informationen zu Schlüsselpaare

Schlüsselpaare finden Sie in der öffentlichen und privaten Schlüsseldateien, die von bestimmten Authentifizierungsprotokollen verwendet werden. 

Authentifizierung mit SSH öffentlichem Schlüssel verwendet Asymmetrische kryptografische Algorithmen, zum Generieren von zwei Schlüsseldateien – eine "Private" und der andere "öffentlich". Die Dateien mit privaten Schlüsseln entsprechen den ein Kennwort, und Sie sollten unter allen Umständen geschützt. Wenn jemand Ihren privaten Schlüssel abruft, können sie Sie zu einem beliebigen SSH-Server melden Sie sich, die, denen Sie können zugreifen. Der öffentliche Schlüssel wird auf dem SSH-Server befindet, und freigegeben werden kann, ohne Beeinträchtigung des privaten Schlüssels.

Bei Verwendung der Key-Authentifizierung mit einem SSH-Server Vergleichen der SSH-Server und der Client den öffentlichen Schlüssel für den Benutzernamen für den privaten Schlüssel. Wenn der öffentliche Schlüssel für den privaten Schlüssel für die clientseitige nicht überprüft werden kann, schlägt die Authentifizierung fehl. 

Multi-Factor Authentication kann mit Schlüsselpaaren implementiert werden, dadurch, dass eine Passphrase angegeben werden, wenn das Schlüsselpaar generiert wird (siehe unten schlüsselgenerierung). Während der Authentifizierung, die der Benutzer für die Passphrase aufgefordert wird, wird der zusammen mit das Vorhandensein des privaten Schlüssels für den SSH-Client zur Authentifizierung des Benutzers verwendet. 

## <a name="host-key-generation"></a>Host-schlüsselgenerierung

Öffentliche Schlüssel gelten bestimmte ACL, die auf Windows, entsprechen nur erlaubt den Zugriff auf Administratoren und System. Um dies zu vereinfachen, 

* Die OpenSSHUtils-PowerShell-Modul erstellt, um den Schlüssel ACLs ordnungsgemäß festgelegt und sollte auf dem Server installiert werden
* Bei der ersten Verwendung von Sshd wird das Schlüsselpaar für den Host automatisch generiert werden. Wenn ssh-Agent ausgeführt wird, werden die Schlüssel automatisch auf den lokalen Speicher hinzugefügt. 

Führen Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus, um Key-Authentifizierung mit einem SSH-Server zu erleichtern:

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Da kein Benutzer, die den Sshd-Dienst zugeordnet ist, werden die Hostschlüssel unter \ProgramData\ssh gespeichert.


## <a name="user-key-generation"></a>Generierung von Schlüsseln

Um Schlüsselbasierte Authentifizierung verwenden zu können, müssen Sie zunächst einige öffentlichen/privaten Schlüsselpaaren für Ihren Client zu generieren. Verwenden Sie ssh-Keygen über PowerShell oder cmd ein um einige wichtigsten Dateien zu generieren.

```powershell
cd ~\.ssh\
ssh-keygen
```

Dies sollte etwa wie folgt (wobei "Benutzername" ist durch Ihren Benutzernamen ersetzt) anzeigen

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Sie können EINGABETASTE drücken, um die Standardeinstellung übernehmen, oder geben Sie einen Pfad, in dem Sie Ihre Schlüssel generiert werden soll. An diesem Punkt werden Sie aufgefordert, eine Passphrase verwenden, um Ihre Dateien mit privaten Schlüsseln zu verschlüsseln.
Die Passphrase kann mit der Schlüsseldatei zur 2-Faktor-Authentifizierung. In diesem Beispiel werden wir die Passphrase leer lassen. 

```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in C:\Users\username\.ssh\id_ed25519.
Your public key has been saved in C:\Users\username\.ssh\id_ed25519.pub.
The key fingerprint is: 
SHA256:OIzc1yE7joL2Bzy8!gS0j8eGK7bYaH1FmF3sDuMeSj8 username@server@LOCAL-HOSTNAME

The key's randomart image is:
+--[ED25519 256]--+
|        .        |
|         o       |
|    . + + .      |
|   o B * = .     |
|   o= B S .      |
|   .=B O o       |
|  + =+% o        |
| *oo.O.E         |
|+.o+=o. .        |
+----[SHA256]-----+
```

Nun müssen Sie ein öffentliches/privates ED25519 Schlüsselpaar (die pub-Dateien sind die öffentlichen Schlüssel und die übrigen sind private Schlüssel):

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

Denken Sie daran, dass Dateien mit private Schlüsseln sind, dass das Äquivalent eines Kennworts geschützt werden sollten die gleiche Weise, wie Sie Ihr Kennwort schützen.
Um dabei zu unterstützen, verwenden Sie ssh-Agent zum sicheren Speichern von privaten Schlüsseln in einem Windows-Sicherheitskontext, Ihre Windows-Anmeldenamen zugeordnet. Dazu starten Sie den ssh-Agent-Dienst als Administrator aus, und Verwenden von ssh-hinzufügen, um den privaten Schlüssel speichern. 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

Nach Abschluss dieser Schritte an, wenn ein privater Schlüssel für die Authentifizierung von diesem Client benötigt wird ssh-Agent automatisch Abrufen des lokalen privaten Schlüssels und übergeben Sie es an der SSH-Client.

> [!NOTE]
> Es wird dringend empfohlen, dass Sie Ihres privaten Schlüssels an einem sicheren Speicherort sichern, und löschen Sie es aus dem lokalen System, *nach* ssh-Agent hinzugefügt.
> Der private Schlüssel kann nicht vom Agent abgerufen werden.
> Wenn Sie den Zugriff auf den privaten Schlüssel verlieren, müssten Sie ein neues Schlüsselpaar erstellen und aktualisieren Sie den öffentlichen Schlüssel auf allen Systemen interagieren mit.

## <a name="deploying-the-public-key"></a>Bereitstellen von den öffentlichen Schlüssel

Um den Benutzerschlüssel verwenden, die weiter oben erstellt wurde, muss der öffentliche Schlüssel auf dem Server befinden, in eine Textdatei namens *Authorized_keys* unter Users\username\ssh. Die OpenSSH-Tools umfassen scp, bei dem eine sichere Dateiübertragung-Dienstprogramm ist, um dies zu unterstützen.

Verschieben Sie den Inhalt des öffentlichen Schlüssels (~\.ssh\id_ed25519.pub) in einem Text-Datei namens Authorized_keys in ~\.Ssh\ auf dem Server-Host.

In diesem Beispiel verwendet die reparieren-AuthorizedKeyPermissions-Funktion im Modul OpenSSHUtils die zuvor auf dem Host in der oben genannten Anweisungen installiert wurde.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

Diese Schritte ausführen, die Konfiguration erforderlich, um die Schlüsselbasierte Authentifizierung mit SSH für Windows zu verwenden.
Danach kann der Benutzer an den Sshd-Host von jedem Client aus herstellen, auf den privaten Schlüssel.

