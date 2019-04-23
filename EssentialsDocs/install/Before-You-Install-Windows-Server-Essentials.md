---
title: Vor der Installation von Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d0893bd-e2b7-4494-9537-02b1cbbcd57a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e7eb1b7bed780b41f1a87589add4ab015f41624a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828721"
---
# <a name="before-you-install-windows-server-essentials"></a>Vor der Installation von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_BeforeYouBegin"></a> Bevor Sie die Installation von Windows Server Essentials beginnen, führen Sie die folgenden Aufgaben:  

-   **Stellen Sie sicher, dass Ihr Computer die Mindesthardwareanforderungen erfüllt**. Dies schließt auch, ob zusätzlichen Hardware erforderlich, und überprüfen, dass die Treiber für Ihre Hardware von Windows Server Essentials unterstützt werden. Weitere Informationen finden Sie unter [System Requirements for Windows Server Essentials](../get-started/system-requirements.md).   

  
    > [!IMPORTANT]
    >  Bevor Sie Windows Server Essentials auf einem bereits vorhandenen Computer installieren, wird empfohlen, dass Sie vollständig formatieren und dann neu die Festplatten des Computers partitionieren. Dadurch stellen Sie sicher, dass keine versteckten Partitionen auf den Festplatten verbleiben.  
  
-   **Bereiten Sie Ihr Netzwerk** um Ihr Netzwerk für die Installation von Windows Server Essentials vorzubereiten, gehen Sie folgendermaßen vor:  
    
  
    -   **Aktualisieren Sie das Betriebssystem auf den Clientcomputern** Windows Server Essentials unterstützt die folgenden Betriebssysteme:  Windows 8, Windows 7, Windows 10 und Macintosh OS X Lion oder höher. Diese Betriebssysteme stellen die erforderlichen Sicherheitsfunktionen, die erforderliche Zuverlässigkeit und Leistung sowie Funktionen für das lokale Netzwerk bereit.  
  
    -   **Konfigurieren Sie den Router**. Stellen Sie sicher, dass der Router wie folgt konfiguriert ist:  
  
        -   Das UPnP-Framework ist auf dem Router aktiviert.  
  
        -   Der DHCP-Serverdienst (Dynamic Host Configuration Protocol) für das LAN kann aktiviert bzw. deaktiviert werden.  Windows Server Essentials wird sichergestellt, dass DHCP nicht auf dem Server und dem Router ausgeführt wird? Wenn DHCP auf dem Router aktiviert ist, ist DHCP nicht auf dem Server während der Installation aktiviert.  
  
        -   Sie verfügen über eine IP-Adresse für die externe Schnittstelle des Routers, die vom Internetdienstanbieter (ISP) bereitgestellt wird. Die IP-Adresse kann dynamisch vom DHCP-Serverdienst beim ISP zugewiesen werden; andernfalls müssen Sie mithilfe der Routerverwaltungskonsole manuell eine statische IP-Adresse konfigurieren.  
  
        -   Wenn für die Internetverbindung ein Benutzername und ein Kennwort erforderlich sind (Point-to-Point-Protokoll über Ethernet, PPPoE), werden diese Einstellungen auch dann auf dem Router konfiguriert, wenn das Gerät das UPnP-Framework unterstützt.  
  
        -   Der Router ist mit dem LAN und dem Internet verbunden, er ist eingeschaltet, und er funktioniert ordnungsgemäß.  
  
     Wenn der Router das UPnP-Framework nicht unterstützt oder der Router während der Installation nicht konfiguriert werden kann, müssen Sie ihn manuell mit den Einstellungen für das Netzwerk konfigurieren. Stellen Sie sicher, dass folgende Ports geöffnet sind und an die IP-Adresse des Zielservers weitergeleitet werden:  
  
    |Portnummer|Application|  
    |-----------------|-----------------|  
    |Port 80|HTTP-Webdatenverkehr|  
    |Port 443|HTTPS-Webdatenverkehr|  
  

-   **Lesen Sie die Windows Server Essentials-Versionsdokumentation**. Die Versionsdokumentation enthält aktuelle Informationen, die möglicherweise entscheidend für ordnungsgemäß installieren und Konfigurieren von Windows Server Essentials. Zum Anzeigen oder Drucken der Versionsdokumentation, finden Sie unter [Release Documentation for Windows Server Essentials](../get-started/release-notes.md).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

