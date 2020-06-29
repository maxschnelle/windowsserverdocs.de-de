---
title: Übersicht über OpenSSH für Windows
description: Übersicht über die OpenSSH-Tools, die von Administratoren von Linux- und anderen Windows-fremden Produkten für die plattformübergreifende Verwaltung von Remotesystemen verwendet werden.
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendmsft
ms.product: windows-server
ms.type: conceptual
ms.openlocfilehash: a045e2b2d262df2a19d910b54c8e2a6db9f55362
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469745"
---
# <a name="openssh-in-windows"></a>OpenSSH in Windows

OpenSSH ist die Open-Source-Version der SSH-Tools (Secure Shell), die von Administratoren von Linux- und anderen Windows-fremden Produkten für die plattformübergreifende Verwaltung von Remotesystemen verwendet wird.
OpenSSH wurde Windows im Herbst 2018 hinzugefügt und ist in Windows 10 und Windows Server 2019 enthalten.

SSH basiert auf einer Client/Server-Architektur, bei der das System, auf dem der Benutzer arbeitet, der Client und das verwaltete Remotesystem der Server ist.
OpenSSH umfasst verschiedene Komponenten und Tools, die einen sicheren und einfachen Ansatz für die Remotesystemverwaltung ermöglichen, z. B.:

* „sshd.exe“: Dies ist die SSH-Serverkomponente, die auf dem remote verwalteten System ausgeführt werden muss.
* „ssh.exe“: Dies ist die SSH-Clientkomponente, die auf dem lokalen System des Benutzers ausgeführt wird.
* „ssh-keygen.exe“: Dient zum Generieren, Verwalten und Konvertieren von Authentifizierungsschlüsseln für SSH.
* „ssh-agent.exe“: Dient zum Speichern von privaten Schlüsseln für die Authentifizierung mit öffentlichem Schlüssel.
* „ssh-add.exe“: Fügt der Liste mit den zulässigen Elementen des Servers private Schlüssel hinzu.
* „ssh-keyscan.exe“: Dient als Hilfe beim Erfassen der öffentlichen SSH-Hostschlüssel für eine Reihe von Hosts.
* „sftp.exe“: Der Dienst, der das Secure File Transfer Protocol bereitstellt und per SSH ausgeführt wird.
* „scp.exe“: Ein Hilfsprogramm zum Kopieren von Dateien, das unter SSH ausgeführt wird.

In der Dokumentation in diesem Abschnitt geht es darum, wie OpenSSH unter Windows verwendet wird (einschließlich der Installation), und um Windows-spezifische Konfigurationen und Anwendungsfälle. Hier sind die Themen angegeben:

Eine zusätzliche ausführliche Dokumentation zu häufig verwendeten OpenSSH-Features ist unter [OpenSSH.com](https://www.openssh.com/manual.html) online verfügbar.

Das [Open-Source-Hauptprojekt von OpenSSH](https://www.openssh.com) wird von Entwicklern unter dem „OpenBSD Project“ verwaltet.
Die Microsoft-Verzweigung dieses Projekts findest du auf [GitHub](https://github.com/PowerShell/openssh-portable).
Feedback zu Windows OpenSSH ist willkommen und kann bereitgestellt werden, indem in unserem [OpenSSH-GitHub-Repository](https://github.com/PowerShell/openssh-portable) Anfragen zu GitHub-Problemen erstellt werden.
