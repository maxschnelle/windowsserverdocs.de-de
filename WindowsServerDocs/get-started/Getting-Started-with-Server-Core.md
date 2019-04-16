---
title: Installieren von Server Core
description: So erhalten und Installieren von Server Core-Installationsoption auf Windows Server 2019, Windows Server 2016 oder Windows Server (Semi-Annual Channel).
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
ms.sourcegitcommit: 7fc7271745e40f110c54918b55624cadd0d7ff98
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/04/2019
ms.locfileid: "8991797"
---
# Installieren von Server Core

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)
  
Wenn Sie Windows Server zum ersten Mal installieren, haben Sie die folgende Optionen:

>[!NOTE]
> In der folgenden Liste sind Editionen ohne "Desktopdarstellung" für die Server Core-Installationsoptionen

-   Windows Server Standard
-   Windows Server Standard mit Desktopdarstellung
-   Windows Server Datacenter
-   Windows Server Datacenter mit Desktopdarstellung

Bei der Installation von Windows Server (Semi-Annual Channel), einschließlich Version 1709, 1803 und 1809, haben Sie die folgende Optionen:

-   Windows Server Standard 
-   Windows Server Datacenter

Die Option „Server Core“ erfordert weniger Speicherplatz auf dem Datenträger und reduziert die potenzielle Angriffsfläche. Daher empfiehlt es sich, die Server Core-Installation auszuwählen, sofern Sie die zusätzlichen Benutzeroberflächenelemente oder grafischen Verwaltungstools, die in der Option „Server mit Desktopdarstellung“ enthalten sind, nicht unbedingt benötigen. Wenn Sie die zusätzlichen Benutzeroberflächenelemente benötigen, finden Sie weitere Informationen hierzu unter [Installieren von Server mit Desktopdarstellung](Getting-Started-with-Server-with-Desktop-Experience.md). 

Bei dieser Option wird die Standardbenutzeroberfläche (die Desktopdarstellung) nicht installiert. Sie verwalten den Server mithilfe der Befehlszeile, Windows PowerShell oder Remotemethoden.

>[!NOTE]
>
>Im Gegensatz zu einigen früheren Versionen von Windows Server ist eine Konvertierung zwischen Server Core und Servern mit Desktopdarstellung nach der Installation nicht möglich. Wenn Sie Server Core installieren und später Server mit Desktopdarstellung verwenden möchten, sollten Sie eine Neuinstallation durchführen.

**Benutzeroberfläche:** Befehlszeile

**Lokales Installieren, Konfigurieren und Deinstallieren von Serverrollen:** an einer Eingabeaufforderung mit Windows PowerShell

**Installieren, konfigurieren, Deinstallieren der Serverrollen auf einem Windows-Client-Computer (oder ein Server mit der Desktop-Umgebung installiert):** mit Server-Manager, Remote Server Administration Tools (RSAT), Windows PowerShell oder Windows Admin Center.

>[!NOTE]
>
>Für RSAT müssen Sie die Windows 10-Version verwenden.
>Microsoft Management Console ist lokal nicht verfügbar.

**Beispiel verfügbare Serverrollen:**

- Active Directory-Zertifikatdienste
- ActiveDirectory-Domänendienste (ADDS)
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

Rollen, die nicht in Server Core enthalten finden Sie unter [Rollen, Rollendienste und Features, die nicht in Windows Server - Server Core](../administration/server-core/server-core-removed-roles.md).

## Installieren unter WindowsServer 2019 oder WindowsServer 2016

Allgemeine Installationsschritte und Optionen für Windows Server (Long-Term Servicing Channel) finden Sie unter [Windows Server-Installation und Upgrade](installation-and-upgrade.md).

## Installieren unter WindowsServer (Semi-Annual Channel)

Die Installationsschritte für Windows Server (Semi-Annual Channel) sind identisch mit der Installation von früheren Versionen von Windows Server (über ein. ISO-Abbild) mit den folgenden Ausnahmen:
- Keine unterstützten Upgrades von früheren Versionen von Windows Server auf Windows Server, Version 1709. Eine Neuinstallation ist immer erforderlich.
   Dies bedeutet, dass beim Ausführen von setup.exe über den Desktop eines Windows-Computers die Setup-Erfahrung nicht die Upgrade-Option ist (es ist deaktiviert).
- Es gibt keine Evaluierungsversion für Windows Server (Semi-Annual Channel)
- Es gibt kein OEM oder Einzelhandel. Windows Server (Semi-Annual Channel) kann nur über Programme Software Assurance oder Treueprogramme lizenziert werden.

Informationen zum Erwerb der Version 1709 von Windows Server finden Sie unter [Einführung in Windows Server, Version 1709](get-started-with-1709.md).

Um Windows Server, Version 1803 zu erhalten, finden Sie unter [Einführung in Windows Server, Version 1803](get-started-with-1803.md).

Was ist neu in der Windows Server, Version 1809, finden Sie unter [Neuigkeiten in Windows Server, Version 1809](whats-new-in-windows-server-1809.md)
