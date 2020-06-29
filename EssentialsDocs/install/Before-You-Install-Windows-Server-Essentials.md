---
title: Vor der Installation von Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 8d0893bd-e2b7-4494-9537-02b1cbbcd57a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a1a927533497cdd451b9f3a045463889390012b7
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471045"
---
# <a name="before-you-install-windows-server-essentials"></a>Vor der Installation von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="before-you-begin-your-installation-of--windows-server-essentials-perform-the-following-tasks"></a><a name="BKMK_BeforeYouBegin"></a>Bevor Sie mit der Installation von Windows Server Essentials beginnen, führen Sie die folgenden Aufgaben aus:

-   **Stellen Sie sicher, dass Ihr Computer die Mindesthardwareanforderungen erfüllt**. Dies umfasst die Bestimmung, ob zusätzliche Hardware erforderlich ist und ob die Treiber für Ihre Hardware von Windows Server Essentials unterstützt werden. Weitere Informationen finden Sie unter [System Anforderungen für Windows Server Essentials](../get-started/system-requirements.md).

> [!IMPORTANT]
> Vor der Installation von Windows Server Essentials auf einem bereits vorhandenen Computer wird empfohlen, dass Sie die Festplatten des bereits vorhandenen Computers vollständig formatieren und neu partitionieren. Dadurch stellen Sie sicher, dass keine versteckten Partitionen auf den Festplatten verbleiben.

- **Vorbereiten Ihres Netzwerks** Gehen Sie folgendermaßen vor, um Ihr Netzwerk für die Installation von Windows Server Essentials vorzubereiten:


  - **Aktualisieren des Betriebssystems auf den Client Computern**  Windows Server Essentials unterstützt die folgenden Betriebssysteme: Windows 8, Windows 7, Windows 10 und Macintosh OS X Lion oder höher. Diese Betriebssysteme stellen die erforderlichen Sicherheitsfunktionen, die erforderliche Zuverlässigkeit und Leistung sowie Funktionen für das lokale Netzwerk bereit.

  - **Konfigurieren Sie den Router**. Stellen Sie sicher, dass der Router wie folgt konfiguriert ist:

    -   Das UPnP-Framework ist auf dem Router aktiviert.

    -   Der DHCP-Serverdienst (Dynamic Host Configuration Protocol) für das LAN kann aktiviert bzw. deaktiviert werden.  Windows Server Essentials stellt sicher, dass DHCP nicht sowohl auf dem Server als auch auf dem Router ausgeführt wird? Wenn DHCP auf dem Router aktiviert ist, wird DHCP auf dem Server während der Installation nicht aktiviert.

    -   Sie verfügen über eine IP-Adresse für die externe Schnittstelle des Routers, die vom Internetdienstanbieter (ISP) bereitgestellt wird. Die IP-Adresse kann dynamisch vom DHCP-Serverdienst beim ISP zugewiesen werden; andernfalls müssen Sie mithilfe der Routerverwaltungskonsole manuell eine statische IP-Adresse konfigurieren.

    -   Wenn für die Internetverbindung ein Benutzername und ein Kennwort erforderlich sind (Point-to-Point-Protokoll über Ethernet, PPPoE), werden diese Einstellungen auch dann auf dem Router konfiguriert, wenn das Gerät das UPnP-Framework unterstützt.

    -   Der Router ist mit dem LAN und dem Internet verbunden, er ist eingeschaltet, und er funktioniert ordnungsgemäß.

    Wenn der Router das UPnP-Framework nicht unterstützt oder der Router während der Installation nicht konfiguriert werden kann, müssen Sie ihn manuell mit den Einstellungen für das Netzwerk konfigurieren. Stellen Sie sicher, dass folgende Ports geöffnet sind und an die IP-Adresse des Zielservers weitergeleitet werden:

  |Portnummer|Application|
  |-----------------|-----------------|
  |Port 80|HTTP-Webdatenverkehr|
  |Port 443|HTTPS-Webdatenverkehr|


- **Lesen Sie die Dokumentation zur Windows Server Essentials-Version**. Die releasedokumentation enthält die neuesten Informationen, die für eine ordnungsgemäße Installation und Konfiguration von Windows Server Essentials von entscheidender Bedeutung sein können. Informationen zum Anzeigen oder Drucken der releasedokumentation finden Sie in der Versions [Dokumentation für Windows Server Essentials](../get-started/release-notes.md).

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

