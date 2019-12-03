---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH, SSH, Win32-OpenSSH
title: OpenSSH in Windows
ms.product: w10
ms.openlocfilehash: c6563fbe4fe69acad4d295a3f7fe166e92d38444
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280052"
---
# <a name="openssh-in-windows"></a>OpenSSH in Windows

OpenSSH ist die Open-Source-Version der SSH-Tools (Secure Shell), die von Administratoren von Linux- und anderen Windows-fremden Produkten für die plattformübergreifende Verwaltung von Remotesystemen verwendet wird. OpenSSH wurde Windows im Herbst 2018 hinzugefügt und ist in Windows 10 und Windows Server 2019 enthalten. 

SSH basiert auf einer Client/Server-Architektur, bei der das System, auf dem der Benutzer arbeitet, der Client und das verwaltete Remotesystem der Server ist. OpenSSH umfasst verschiedene Komponenten und Tools, die einen sicheren und einfachen Ansatz für die Remotesystemverwaltung ermöglichen, z. B.:

* „sshd.exe“: Dies ist die SSH-Serverkomponente, die auf dem remote verwalteten System ausgeführt werden muss. 
* „ssh.exe“: Dies ist die SSH-Clientkomponente, die auf dem lokalen System des Benutzers ausgeführt wird.
* „ssh-keygen.exe“: Dient zum Generieren, Verwalten und Konvertieren von Authentifizierungsschlüsseln für SSH. 
* „ssh-agent.exe“: Dient zum Speichern von privaten Schlüsseln für die Authentifizierung mit öffentlichem Schlüssel.
* „ssh-add.exe“: Fügt der Liste mit den zulässigen Elementen des Servers private Schlüssel hinzu.
* „ssh-keyscan.exe“: Dient als Hilfe beim Erfassen der öffentlichen SSH-Hostschlüssel für eine Reihe von Hosts.
* „sftp.exe“: Der Dienst, der das Secure File Transfer Protocol bereitstellt und per SSH ausgeführt wird.
* „scp.exe“: Ein Hilfsprogramm zum Kopieren von Dateien, das unter SSH ausgeführt wird.

In der Dokumentation in diesem Abschnitt geht es darum, wie OpenSSH unter Windows verwendet wird (einschließlich der Installation), und um Windows-spezifische Konfigurationen und Anwendungsfälle. Hier sind die Themen angegeben:
* Installieren und Deinstallieren von OpenSSH für Windows Server 2019 und Windows 10

Eine zusätzliche ausführliche Dokumentation zu häufig verwendeten OpenSSH-Features ist unter [OpenSSH.com](https://www.openssh.com/manual.html) online verfügbar. 

Das [Open-Source-Hauptprojekt von OpenSSH](https://www.openssh.com) wird von Entwicklern unter dem „OpenBSD Project“ verwaltet. Die Microsoft-Verzweigung dieses Projekts findest du auf [GitHub](https://github.com/PowerShell/openssh-portable).
Feedback zu Windows OpenSSH ist willkommen und kann bereitgestellt werden, indem in unserem [OpenSSH-GitHub-Repository](https://github.com/PowerShell/openssh-portable) Anfragen zu GitHub-Problemen erstellt werden. 
