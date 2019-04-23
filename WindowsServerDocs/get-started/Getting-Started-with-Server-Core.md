---
title: Installieren von Server Core
description: Informationen zum Abrufen und Installieren einer Server Core-Installations auf Windows Server-2019, Windows Server 2016 oder Windows Server (Halbjährlicher Kanal).
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 1/04/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: d99cd0b028d08d5c3247541ce3a868676b60693d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869021"
---
# <a name="install-server-core"></a>Installieren von Server Core

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)
  
Wenn Sie Windows Server zum ersten Mal installieren, müssen Sie die folgenden Installationsoptionen:

>[!NOTE]
> In der folgenden Liste sind Editionen ohne "Desktopdarstellung" für die Server Core-Installationsoptionen

-   Windows Server Standard
-   Windows Server Standard mit Desktopdarstellung
-   Windows Server Datacenter
-   Windows Server Datacenter mit Desktopdarstellung

Bei der Installation von Windows Server (Halbjährlicher Kanal), einschließlich der Version 1709, 1803 und 1809, haben Sie die folgenden Installationsoptionen:

-   Windows Server Standard 
-   Windows Server Datacenter

Die Option „Server Core“ erfordert weniger Speicherplatz auf dem Datenträger und reduziert die potenzielle Angriffsfläche. Daher empfiehlt es sich, die Server Core-Installation auszuwählen, sofern Sie die zusätzlichen Benutzeroberflächenelemente oder grafischen Verwaltungstools, die in der Option „Server mit Desktopdarstellung“ enthalten sind, nicht unbedingt benötigen. Wenn Sie die zusätzlichen Benutzeroberflächenelemente benötigen, finden Sie weitere Informationen hierzu unter [Installieren von Server mit Desktopdarstellung](Getting-Started-with-Server-with-Desktop-Experience.md). 

Bei dieser Option wird die Standardbenutzeroberfläche (die Desktopdarstellung) nicht installiert. Sie verwalten den Server mithilfe der Befehlszeile, Windows PowerShell oder Remotemethoden.

>[!NOTE]
>
>Im Gegensatz zu einigen früheren Versionen von Windows Server ist eine Konvertierung zwischen Server Core und Servern mit Desktopdarstellung nach der Installation nicht möglich. Wenn Sie Server Core installieren und später Server mit Desktopdarstellung verwenden möchten, sollten Sie eine Neuinstallation durchführen.

**Benutzeroberfläche:** Befehlszeile

**Lokales Installieren, Konfigurieren und Deinstallieren von Serverrollen:** an einer Eingabeaufforderung mit Windows PowerShell

**Installieren, konfigurieren und Deinstallieren von Serverrollen im Remotemodus aus einem Windows-Client-Computer (oder einem Server mit der Desktopdarstellung installiert):** mit Server-Manager, Remoteserver-Verwaltungstools (RSAT), Windows PowerShell oder Windows Admin Center .

>[!NOTE]
>
>Für RSAT müssen Sie die Windows 10-Version verwenden.
>Microsoft Management Console ist lokal nicht verfügbar.

**Beispiel-Serverfunktionen zur Verfügung:**

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

Rollen in Server Core nicht enthalten, finden Sie unter [Rollen, Rollendienste und Features nicht in Windows Server – Server Core](../administration/server-core/server-core-removed-roles.md).

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>Installieren von auf WindowsServer 2019 oder WindowsServer 2016

Allgemeine Installationsschritte und Optionen für die Windows-Server (Long Term Wartungskanal), finden Sie unter [Windows Server-Installation und Upgrade](installation-and-upgrade.md).

## <a name="installing-on-windows-server-semi-annual-channel"></a>Installieren unter WindowsServer (Halbjährlicher Kanal)

Installationsschritte für Windows Server (Halbjährlicher Kanal) sind identisch mit frühere Versionen von Windows Server installieren (von ein. ISO-Abbild) mit den folgenden Ausnahmen:
- Keine unterstützten Upgrades von früheren Versionen von Windows Server auf Windows Server, Version 1709. Eine Neuinstallation ist immer erforderlich.
   Dies bedeutet, dass beim Ausführen von setup.exe auf dem Desktop eines Windows-Computers der Setupvorgang nicht die Option zulässig ist (er ist abgeblendet).
- Es ist keine Auswertung-Version für Windows Server (Halbjährlicher Kanal)
- Es gibt kein OEM oder Einzelhandel. Windows Server (Halbjährlicher Kanal) kann nur über Software Assurance oder Loyalität Programme lizenziert werden.

Informationen zum Erwerb der Version 1709 von Windows Server finden Sie unter [Einführung in Windows Server, Version 1709](get-started-with-1709.md).

Windows Server-Version 1803 finden Sie unter [Einführung in Windows Server, Version 1803](get-started-with-1803.md).

Neuigkeiten in Windows Server, Version 1809, finden Sie unter [Neuigkeiten in Windows Server-Version 1809](whats-new-in-windows-server-1809.md)
