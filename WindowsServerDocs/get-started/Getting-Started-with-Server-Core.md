---
title: Installieren von Server Core
description: Abrufen und Installieren einer Server Core-Installation unter Windows Server 2019, Windows Server 2016 oder Windows Server (halbjährlicher Kanal).
ms.prod: windows-server
ms.date: 05/21/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: e6264a59a837003e49e82529750cfb153cc37b92
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360336"
---
# <a name="install-server-core"></a>Installieren von Server Core

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)
  
Wenn du Windows Server zum ersten Mal installierst, stehen dir folgende Installationsoptionen zur Verfügung:

>[!NOTE]
> In der folgenden Liste sind Editionen ohne „Desktopdarstellung“ die Server Core-Installationsoptionen.

-   Windows Server Standard
-   Windows Server Standard mit Desktopdarstellung
-   Windows Server Datacenter
-   Windows Server Datacenter mit Desktopdarstellung

Wenn du Windows Server (halbjährlicher Kanal) installierst, stehen dir folgende Installationsoptionen zur Verfügung:

-   Windows Server Standard 
-   Windows Server Datacenter

Die Option „Server Core“ erfordert weniger Speicherplatz auf dem Datenträger und reduziert die potenzielle Angriffsfläche. Daher empfiehlt es sich, die Server Core-Installation auszuwählen, sofern du die zusätzlichen Benutzeroberflächenelemente oder grafischen Verwaltungstools, die in der Option „Server mit Desktopdarstellung“ enthalten sind, nicht unbedingt benötigst. Wenn du die zusätzlichen Benutzeroberflächenelemente benötigst, findest du Informationen dazu unter [Installieren des Servers mit Desktopdarstellung](Getting-Started-with-Server-with-Desktop-Experience.md). 

Bei der Server Core-Option wird die Standardbenutzeroberfläche (die Desktopdarstellung) nicht installiert. Du verwaltest den Server per Befehlszeile, Windows PowerShell oder Remotemethoden.

>[!NOTE]
>
>Im Gegensatz zu einigen früheren Versionen von Windows Server ist eine Konvertierung zwischen Server Core und Servern mit Desktopdarstellung nach der Installation nicht möglich. Wenn Sie Server Core installieren und später Server mit Desktopdarstellung verwenden möchten, sollten Sie eine Neuinstallation durchführen.

**Benutzeroberfläche:** Befehlszeile

**Lokales Installieren, Konfigurieren und Deinstallieren von Serverrollen:** an einer Eingabeaufforderung mit Windows PowerShell

**Installieren, Konfigurieren, Deinstallieren der Serverrollen remote auf einem Windows-Clientcomputer (oder einem Server mit installierter Desktopdarstellung)** : mit Server-Manager, Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT), Windows PowerShell oder Windows Admin Center.

>[!NOTE]
>
>Für RSAT müssen Sie die Windows 10-Version verwenden.
>Die Microsoft Management Console ist lokal nicht verfügbar.

**Beispiele für verfügbare Serverrollen**:

- Active Directory-Zertifikatdienste
- Active Directory Domain Services
- DHCP-Server
- DNS-Server
- Dateidienste (einschließlich Ressourcen-Manager für Dateiserver)
- Active Directory Lightweight Directory Services (ADLDS)
- Hyper-V
- Druck- und Dokumentdienste
- Streaming Media-Dienste
- Webserver (einschließlich einer Teilmenge von ASP.NET)
- Windows Server Update Services
- Active Directory-Rechteverwaltungsserver
- Routing- und RAS-Server und folgende Unterrollen:
   - Verbindungsbroker für Remotedesktopdienste
   - Lizenzierung
   - Virtualisierung
   - Volumenaktivierungsdienste

Informationen zu Rollen, die in Server Core nicht enthalten sind, findest du unter [Rollen, Rollendienste und Features, die in Windows Server – Server Core nicht enthalten sind](../administration/server-core/server-core-removed-roles.md).

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>Installieren unter Windows Server 2019 oder Windows Server 2016

Allgemeine Installationsschritte und -optionen für Windows Server (Long-Term Servicing Channel) findest du unter [Windows Server-Installation und -Upgrade](installation-and-upgrade.md).

## <a name="installing-on-windows-server-semi-annual-channel"></a>Installieren unter Windows Server (halbjährlicher Kanal)

Die Installationsschritte für Windows Server (halbjährlicher Kanal) sind die gleichen wie für die Installation früherer Versionen von Windows Server (aus einem ISO-Image) mit folgenden Ausnahmen:

- Keine unterstützten Upgrades von früheren Windows Server-Versionen auf Windows Server, Version 1709. Eine Neuinstallation ist immer erforderlich.
   Dies bedeutet, dass beim Ausführen von „setup.exe“ vom Desktop eines Windows-Computers das Setupprogramm keine Upgrade-Option ermöglicht (diese ist deaktiviert).
- Es gibt keine Evaluierungsversion für Windows Server (halbjährlicher Kanal).
- Es gibt keine OEM- oder Einzelhandelsversion. Windows Server (halbjährlicher Kanal) kann nur über Software Assurance oder Treueprogramme lizenziert werden.

Weitere Informationen zum halbjährlichen Kanal findest du unter [Windows Server-Wartungskanäle](../get-started-19/servicing-channels-19.md).

Informationen zu den Neuerungen im halbjährlichen Kanal für Windows Server findest du unter [Neuerungen in Windows Server](whats-new-in-windows-server.md).
