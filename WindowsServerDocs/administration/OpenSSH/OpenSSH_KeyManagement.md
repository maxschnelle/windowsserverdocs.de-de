---
title: Konfiguration des OpenSSH-Servers für Windows
description: Konfigurieren des OpenSSH-Servers für Windows mithilfe der Windows-Tools oder PowerShell.
ms.date: 09/27/2018
ms.topic: conceptual
contributor: maertendMSFT
author: maertendmsft
ms.product: windows-server
ms.openlocfilehash: 4acb7893f41207de045af7eeaea15efba8221f4a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469845"
---
# <a name="openssh-key-management"></a>OpenSSH-Schlüsselverwaltung

Die meisten Authentifizierungen in Windows-Umgebungen erfolgen mit einem Paar aus Benutzername und Kennwort.
Dies funktioniert besonders gut bei Systemen, die eine gemeinsame Domäne verwenden.
Bei domänenübergreifenden Arbeiten wie beispielsweise zwischen lokalen und in der Cloud gehosteten Systemen gestaltet sich dies schon schwieriger.

Im Vergleich dazu verwenden Linux-Umgebungen für die Authentifizierung häufig Paare aus einem öffentlichen und einem privaten Schlüssel.
OpenSSH enthält Tools zur Unterstützung dieser Authentifizierungsmethoden einschließlich der folgenden:

* __ssh-keygen__ zum Generieren sicherer Schlüssel
* __ssh-agent__ und __ssh-add__ zum sicheren Speichern privater Schlüssel
* __scp__ und __sftp__ zum sicheren Kopieren öffentlicher Schlüssel bei der erstmaligen Verwendung eines Servers

Dieses Dokument bietet eine Übersicht über die Verwendung dieser Tools unter Windows für die Schlüsselauthentifizierung mit SSH.
Wenn Sie mit der SSH-Schlüsselverwaltung nicht vertraut sind, empfehlen wir Ihnen dringend, das [NIST-Dokument IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) mit dem Titel „Security of Interactive and Automated Access Management Using Secure Shell (SSH)“ (Sicherheit der interaktiven und automatisierten Zugriffsverwaltung mit Secure Shell (SSH)) zu lesen.

## <a name="about-key-pairs"></a>Informationen zu Schlüsselpaaren

Schlüsselpaare verweisen auf die Dateien für öffentliche und private Schlüssel, die von bestimmten Authentifizierungsprotokollen verwendet werden.

Bei der SSH-Authentifizierung mit öffentlichem Schlüssel werden asymmetrische Kryptografiealgorithmen verwendet, um zwei Schlüsseldateien (privat und öffentlich) zu generieren. Die Dateien des privaten Schlüssels entsprechen einem Kennwort und sollten unter allen Umständen gut geschützt werden. Wenn jemand Ihren privaten Schlüssel erhält, kann sich diese Person bei jedem beliebigen SSH-Server anmelden, auf den Sie Zugriff haben. Der öffentliche Schlüssel wird auf dem SSH-Server abgelegt und ggf. freigegeben, ohne dass dabei der private Schlüssel kompromittiert wird.

Bei Verwendung der Schlüsselauthentifizierung mit einem SSH-Server vergleichen der SSH-Server und der SSH-Client die öffentlichen Schlüssel für den angegebenen Benutzernamen mit dem privaten Schlüssel. Wenn der serverseitige öffentliche Schlüssel nicht anhand des clientseitigen privaten Schlüssels überprüft werden kann, schlägt die Authentifizierung fehl.

Die mehrstufige Authentifizierung kann mit Schlüsselpaaren implementiert werden, indem gefordert wird, dass eine Passphrase angegeben wird, wenn das Schlüsselpaar generiert wird (siehe Schlüsselgenerierung unten).
Während der Authentifizierung wird der Benutzer zur Eingabe dieser Passphrase aufgefordert. Diese wird zusammen mit dem privaten Schlüssel auf dem SSH-Client verwendet, um den Benutzer zu authentifizieren.

## <a name="host-key-generation"></a>Generierung des Hostschlüssels

Öffentliche Schlüssel weisen bestimmte ACL-Anforderungen auf, die unter Windows nur den Zugriff auf Administratoren und das System erlauben.
Folgende Maßnahmen dienen hierbei der Vereinfachung:

* Das PowerShell-Modul „OpenSSHUtils“ wurde erstellt, um die Schlüssel-ACLs ordnungsgemäß festzulegen. Es muss auf dem Server installiert werden.
* Bei der ersten Verwendung von SSHD wird das Schlüsselpaar für den Host automatisch generiert. Wenn „ssh-agent“ ausgeführt wird, werden die Schlüssel automatisch dem lokalen Speicher hinzugefügt.

Führen Sie über eine PowerShell-Eingabeaufforderung mit erhöhten Rechten die folgenden Befehle aus, um die Authentifizierung mit dem SSH-Server zu vereinfachen:

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Da dem SSHD-Dienst kein Benutzer zugeordnet ist, werden die Hostschlüssel unter „\ProgramData\ssh“ gespeichert.

## <a name="user-key-generation"></a>Generierung des Benutzerschlüssels

Sie müssen für den Client zunächst einige Schlüsselpaare aus öffentlichen und privaten Schlüsseln generieren, um die schlüsselbasierte Authentifizierung verwenden zu können.
Verwenden Sie in PowerShell oder cmd „ssh-keygen“, um einige Schlüsseldateien zu generieren.

```powershell
cd ~\.ssh\
ssh-keygen
```

Anschließend sollte in etwa Folgendes angezeigt werden („Benutzername“ wird dabei durch Ihren Benutzernamen ersetzt):

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Sie können die EINGABETASTE drücken, um die Standardeinstellung zu übernehmen, oder einen Pfad angeben, in dem die Schlüssel generiert werden sollen.
An diesem Punkt werden Sie aufgefordert, eine Passphrase zum Verschlüsseln der Dateien für den privaten Schlüssel zu verwenden.
Zusammen mit der Schlüsseldatei kann mit der Passphrase die zweistufige Authentifizierung bereitgestellt werden.
In diesem Beispiel wird die Passphrase leer gelassen.

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

Nun haben Sie ein ED25519-Schlüsselpaar aus öffentlichen und privaten Schlüsseln (die PUB-Dateien sind öffentliche Schlüssel, und die übrigen sind private Schlüssel):

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

Beachten Sie, dass die Dateien des privaten Schlüssels dem Kennwort entsprechen und daher auf dieselbe Weise geschützt werden müssen wie Ihr Kennwort.
Verwenden Sie hierfür „ssh-agent“, um die privaten Schlüssel innerhalb eines sicheren Windows-Sicherheitskontexts zu speichern, der Ihrem Windows-Anmeldenamen zugeordnet ist.
Starten Sie hierzu den „ssh-agent“-Dienst als Administrator, und verwenden Sie „ssh-add“, um den privaten Schlüssel zu speichern.

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

Nachdem Sie diese Schritte ausgeführt haben, ruft „ssh-agent“ immer automatisch den privaten Schlüssel ab und übergibt ihn an Ihren SSH-Client, wenn für die Authentifizierung dieses Clients ein privater Schlüssel erforderlich ist.

> [!NOTE]
> Es wird dringend empfohlen, dass Sie den privaten Schlüssel an einem sicheren Speicherort verwahren und aus dem lokalen System löschen, *nachdem* Sie ihn zu „ssh-agent“ hinzugefügt haben.
> Der private Schlüssel kann nicht vom Agent abgerufen werden.
> Wenn Sie keinen Zugriff mehr auf den privaten Schlüssel haben, müssten Sie ein neues Schlüsselpaar erstellen und den öffentlichen Schlüssel auf allen Systemen aktualisieren, mit denen Sie interagieren.

## <a name="deploying-the-public-key"></a>Bereitstellen des öffentlichen Schlüssels

Der öffentliche Schlüssel muss auf dem Server in einer Textdatei namens *authorized_keys* unter users\username\\.ssh\\ platziert werden, um den oben erstellten Schlüssel zu verwenden.
Das OpenSSH-Tool umfasst mit scp ein sicheres Dienstprogramm für den Dateitransfer.

Auf diese Weise verschieben Sie den Inhalt Ihres öffentlichen Schlüssels (~\.ssh\id_ed25519.pub) in eine Textdatei namens „authorized_keys“ in „~\.ssh\“ auf Ihrem Server/Host.

In diesem Beispiel wird die Funktion „Repair-AuthorizedKeyPermissions“ im OpenSSHUtils-Modul verwendet, das wie in den obigen Anweisungen beschrieben auf dem Host installiert wurde.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to copy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

Mit diesen Schritten wird die Konfiguration vervollständigt, die für die Verwendung der schlüsselbasierten Authentifizierung mit SSH unter Windows erforderlich ist.
Danach kann der Benutzer von jedem Client, der über den privaten Schlüssel verfügt, eine Verbindung mit dem SSHD-Host herstellen.
