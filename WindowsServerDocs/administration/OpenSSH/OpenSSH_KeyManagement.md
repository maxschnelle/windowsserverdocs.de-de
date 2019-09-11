---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, sshd, installieren, Setup
contributor: maertendMSFT
author: maertendMSFT
title: OpenSSH-Server Konfiguration für Windows
ms.product: w10
ms.openlocfilehash: ed9f3653c79f1329b1334f52fe14c1184bc99539
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866866"
---
# <a name="openssh-key-management"></a>OpenSSH-Schlüsselverwaltung

Die meisten Authentifizierung in Windows-Umgebungen erfolgt mit einem Paar aus Benutzername und Kennwort.
Dies funktioniert gut für Systeme, die gemeinsam eine gemeinsame Domäne verwenden. Wenn Domänen übergreifend gearbeitet werden, z. b. zwischen lokalen und in der Cloud gehosteten Systemen, wird es schwieriger.

Im Vergleich dazu verwenden Linux-Umgebungen häufig öffentliche/private Schlüsselpaare, um die Authentifizierung zu steuern.
OpenSSH enthält Tools, mit denen dies unterstützt wird, insbesondere:

* __ssh-keygen__ zum Erstellen von sicheren Schlüsseln
* __SSH-Agent__ und __SSH-Add__ zum sicheren Speichern privater Schlüssel
* __SCP__ und __SFTP__ zum sicheren Kopieren von Dateien für öffentliche Schlüssel während der anfänglichen Verwendung eines Servers

Dieses Dokument enthält eine Übersicht über die Verwendung dieser Tools unter Windows, um mit der Verwendung der Schlüssel Authentifizierung mit SSH zu beginnen. Wenn Sie mit der SSH-Schlüsselverwaltung nicht vertraut sind, empfehlen wir Ihnen dringend, [NIST Document IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) mit dem Titel "Sicherheit der interaktiven und automatisierten Zugriffs Verwaltung mit Secure Shell (SSH)" zu lesen.

## <a name="about-key-pairs"></a>Informationen zu Schlüsselpaaren

Schlüsselpaare verweisen auf die Dateien für öffentliche und private Schlüssel, die von bestimmten Authentifizierungs Protokollen verwendet werden. 

Bei der Authentifizierung mit öffentlichem Schlüssel werden Asymmetrische Kryptografiealgorithmen verwendet, um zwei Schlüsseldateien zu generieren – eine "private" und die andere "Public". Die Dateien des privaten Schlüssels entsprechen einem Kennwort und sollten unter allen Umständen geschützt werden. Wenn jemand Ihren privaten Schlüssel erhält, kann er sich als Sie bei jedem beliebigen SSH-Server anmelden, auf den Sie Zugriff haben. Der öffentliche Schlüssel wird auf dem SSH-Server abgelegt und kann freigegeben werden, ohne dass der private Schlüssel kompromittiert wird.

Bei Verwendung der Schlüssel Authentifizierung bei einem SSH-Server vergleichen der SSH-Server und-Client den öffentlichen Schlüssel für den Benutzernamen, der mit dem privaten Schlüssel bereitgestellt wird. Wenn der öffentliche Schlüssel nicht anhand des Client seitigen privaten Schlüssels überprüft werden kann, schlägt die Authentifizierung fehl. 

Die Multi-Factor Authentication kann mit Schlüsselpaaren implementiert werden, indem gefordert wird, dass eine Passphrase angegeben wird, wenn das Schlüsselpaar generiert wird (siehe Schlüsselgenerierung unten). Während der Authentifizierung wird der Benutzer zur Eingabe der Passphrase aufgefordert. diese wird zusammen mit dem vorhanden sein des privaten Schlüssels auf dem SSH-Client zum Authentifizieren des Benutzers verwendet. 

## <a name="host-key-generation"></a>Generierung von Host Schlüsseln

Öffentliche Schlüssel weisen bestimmte ACL-Anforderungen auf, die unter Windows nur den Zugriff auf Administratoren und Systeme erlauben. Um dies zu vereinfachen, 

* Das PowerShell-Modul opensshutils wurde erstellt, um die Schlüssel-ACLs ordnungsgemäß festzulegen, und muss auf dem Server installiert werden.
* Bei der ersten Verwendung von sshd wird das Schlüsselpaar für den Host automatisch generiert. Wenn SSH-Agent ausgeführt wird, werden die Schlüssel automatisch dem lokalen Speicher hinzugefügt. 

Führen Sie die folgenden Befehle an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus, um die Schlüssel Authentifizierung mit einem SSH-Server zu vereinfachen:

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Da dem sshd-Dienst kein Benutzer zugeordnet ist, werden die Host Schlüssel unter "\programdata\ssh" gespeichert.


## <a name="user-key-generation"></a>Generierung von Benutzer Schlüsseln

Um die Schlüssel basierte Authentifizierung verwenden zu können, müssen Sie zunächst einige öffentliche/private Schlüsselpaare für Ihren Client generieren. Verwenden Sie in PowerShell oder cmd ssh-keygen, um einige Schlüsseldateien zu generieren.

```powershell
cd ~\.ssh\
ssh-keygen
```

Dies sollte in etwa wie folgt angezeigt werden (wobei "username" durch Ihren Benutzernamen ersetzt wird).

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Sie können die EINGABETASTE drücken, um die Standardeinstellung zu übernehmen, oder einen Pfad angeben, in dem die Schlüssel generiert werden sollen. An diesem Punkt werden Sie aufgefordert, eine Passphrase zum Verschlüsseln Ihrer Dateien für den privaten Schlüssel zu verwenden.
Die Passphrase funktioniert mit der Schlüsseldatei, um die zweistufige Authentifizierung bereitzustellen. In diesem Beispiel wird die Passphrase leer gelassen. 

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

Nun haben Sie ein öffentliches/privates ED25519-Schlüsselpaar (die pub-Dateien sind öffentliche Schlüssel und die übrigen privaten Schlüssel):

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

Beachten Sie, dass die Dateien des privaten Schlüssels dem Kennwort entsprechen, das auf dieselbe Weise wie Ihr Kennwort geschützt werden muss.
Um dies zu unterstützen, verwenden Sie SSH-Agent zum sicheren Speichern der privaten Schlüssel innerhalb eines Windows-Sicherheits Kontexts, der Ihrem Windows-Anmelde Namen zugeordnet ist. Starten Sie hierzu den SSH-Agent-Dienst als Administrator, und verwenden Sie SSH-Add, um den privaten Schlüssel zu speichern. 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

Nachdem Sie diese Schritte ausgeführt haben, ruft der SSH-Agent immer dann den lokalen privaten Schlüssel ab und übergibt ihn an Ihren SSH-Client, wenn für die Authentifizierung von diesem Client ein privater Schlüssel erforderlich ist.

> [!NOTE]
> Es wird dringend empfohlen, dass Sie den privaten Schlüssel an einem sicheren Speicherort sichern und ihn dann aus dem lokalen System löschen, *nachdem* Sie ihn dem SSH-Agent hinzugefügt haben.
> Der private Schlüssel kann nicht vom Agent abgerufen werden.
> Wenn Sie den Zugriff auf den privaten Schlüssel verlieren, müssten Sie ein neues Schlüsselpaar erstellen und den öffentlichen Schlüssel auf allen Systemen aktualisieren, mit denen Sie interagieren.

## <a name="deploying-the-public-key"></a>Bereitstellen des öffentlichen Schlüssels

Um den oben erstellten Benutzerschlüssel zu verwenden, muss der öffentliche Schlüssel auf dem Server in eine Textdatei namens " *authorized_keys* " unter "users\benutzername\ssh." eingefügt werden. Zu den OpenSSH-Tools gehört SCP, ein sicheres Datei Übertragungs Dienstprogramm, um dies zu unterstützen.

Um den Inhalt des öffentlichen Schlüssels (~\.ssh\id_ed25519.pub) in eine Textdatei mit dem Namen authorized_keys in ~\.SSH \ auf Ihrem Server/Host zu verschieben.

In diesem Beispiel wird die Funktion Repair-authorizedkey-Berechtigungen im opensshutils-Modul verwendet, das zuvor in den obigen Anweisungen auf dem Host installiert wurde.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

Mit diesen Schritten wird die Konfiguration vervollständigt, die für die Verwendung der Schlüssel basierten Authentifizierung mit SSH unter Windows erforderlich ist.
Danach kann der Benutzer von jedem Client, der über den privaten Schlüssel verfügt, eine Verbindung mit dem sshd-Host herstellen.

