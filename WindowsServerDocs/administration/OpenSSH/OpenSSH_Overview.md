---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH, SSH, Win32-OpenSSH
title: OpenSSH in Windows
ms.product: w10
ms.openlocfilehash: 68ced1ff133495d7658e486e7e72321e18857b21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843361"
---
# <a name="openssh-in-windows"></a>OpenSSH in Windows

OpenSSH ist, die Open-Source-Version der Secure Shell (SSH)-Tools, die Administratoren von Linux und anderen nicht-Windows für die plattformübergreifende Verwaltung von remote-Systemen verwendet wird. OpenSSH zu Windows ab Herbst 2018 hinzugefügt wurde, und befindet sich im Windows 10 und Windows Server-2019. 

SSH basiert auf einer Client / Server-Architektur, in denen das System, dem der Benutzer gerade arbeitet der Client und das remote System verwaltet wird, ist der Server. OpenSSH umfasst eine Reihe von Komponenten und Tools zum Bereitstellen eines sicheren und unkomplizierten Ansatzes Remotesystem-Verwaltung, einschließlich:

* sshd.exe, d.h. die SSH-Serverkomponente, die auf dem System, die Remoteverwaltung ausgeführt werden müssen 
* SSH.exe, wird die SSH-Client-Komponente, die auf dem lokalen System des Benutzers ausgeführt wird.
* SSH-keygen.exe generiert, verwaltet und SSH-Authentifizierungsschlüssel konvertiert 
* SSH-agent.exe speichert die privaten Schlüssel für die Authentifizierung des öffentlichen Schlüssels verwendet
* SSH-add.exe fügt der private Schlüssel in die Liste der Server zulässt
* SSH-keyscan.exe Hilfsmittel zum Sammeln von den öffentlichen SSH-Hostschlüssel aus einer Reihe von hosts
* SFTP.exe ist der Dienst, der das Secure File Transfer Protocol und führt über SSH
* SCP.exe ist ein kopierhilfsprogramm, der auf SSH ausgeführt wird.

Dokumentation in diesem Abschnitt konzentriert sich auf wie OpenSSH für Windows, einschließlich Installation und die Windows-spezifischen Konfiguration und Anwendungsfällen verwendet wird. Hier sind die Themen:
* Installieren und deinstallieren OpenSSH für WindowsServer 2019 und Windows 10

Zusätzliche ausführliche Dokumentation hinsichtlich allgemeinen OpenSSH-Funktionen steht online im [OpenSSH.com](https://www.openssh.com/manual.html). 

Der Master [OpenSSH-öffnen-Source-Projekt](https://www.openssh.com) wird von Entwicklern am des OpenBSD-Projekts verwaltet. Die Microsoft-Verzweigung dieses Projekts befindet sich in [Github](https://github.com/PowerShell/openssh-portable).
Feedback zu Windows OpenSSH ist willkommene und kann angegeben werden, durch das Erstellen von Github-Probleme in unseren [OpenSSH-Github-Repository](https://github.com/PowerShell/openssh-portable). 
