---
title: Vor der Installation von Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="before-you-install-windows-server-essentials"></a>Vor der Installation von Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_BeforeYouBegin"></a>Vor dem Beginn der Installations von Windows Server Essentials führen Sie die folgenden Aufgaben aus:  

-   **Stellen Sie sicher, dass Ihr Computer die Mindestanforderungen erfüllt**. Dazu gehören auch, ob zusätzlichen Hardware erforderlich ist und ob die Treiber für Ihre Hardware von Windows Server Essentials unterstützt werden. Weitere Informationen finden Sie unter [System Requirements for Windows Server Essentials](../get-started/system-requirements.md).   

  
    > [!IMPORTANT]
    >  Bevor Sie Windows Server Essentials auf einem bereits vorhandenen Computer installieren, wird empfohlen, dass Sie vollständig formatieren und neu der Festplatten des Computers partitionieren. Formatieren und die Festplatten Neupartitionierung, entfernen Sie die Möglichkeit, die versteckte Partitionen auf den Festplatten verbleiben.  
  
-   **Bereiten Sie Ihr Netzwerk** um Ihr Netzwerk für die Installation von Windows Server Essentials vorzubereiten, gehen Sie folgendermaßen vor:  
    
  
    -   **Aktualisieren Sie das Betriebssystem auf den Clientcomputern** Windows Server Essentials unterstützt die folgenden Betriebssysteme: Windows 8, Windows 7, Windows 10 und Macintosh OS X Lion oder höher. Diese Betriebssysteme bieten die erforderlichen Sicherheitsfunktionen, Zuverlässigkeit, Leistung und Funktionalität für das lokale Netzwerk.  
  
    -   **Konfigurieren Sie den Router** stellen Sie sicher, dass der Router wie folgt konfiguriert ist:  
  
        -   Das UPnP-Framework ist auf dem Router aktiviert.  
  
        -   Das Dynamic Host Configuration-Protokoll (DHCP) Server-Dienst für das LAN kann aktiviert oder deaktiviert werden.  Windows Server Essentials wird sichergestellt, dass DHCP nicht auf dem Server und dem Router ausgeführt wird? Wenn DHCP auf dem Router aktiviert ist, wird DHCP nicht auf dem Server während der Installation aktiviert.  
  
        -   Sie haben eine IP-Adresse für die externe Schnittstelle des Routers, die von Ihrem Internetdienstanbieter (ISP) bereitgestellt wird. Die IP-Adresse kann dynamisch durch den DHCP-Serverdienst beim ISP zugewiesen werden, oder Sie müssen manuell eine statische IP-Adresse mithilfe der routerverwaltungskonsole konfigurieren.  
  
        -   Wenn Ihre Internet-Verbindung erforderlich ist, einen Benutzernamen und ein Kennwort Point Protocol over Ethernet (PPPoE), werden diese Einstellungen auf dem Router konfiguriert, auch wenn das Gerät das UPnP-Framework unterstützt.  
  
        -   Der Router ist mit dem LAN und dem Internet verbunden, eingeschaltet ist und ordnungsgemäß funktioniert.  
  
     Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn der Router während der Installation konfiguriert werden kann, müssen Sie manuell es mit den Einstellungen für Ihr Netzwerk konfigurieren. Stellen Sie sicher, dass folgende Ports geöffnet sind und der IP-Adresse des Zielservers weitergeleitet werden:  
  
    |Portnummer|Anwendung|  
    |-----------------|-----------------|  
    |Port 80|HTTP-Webdatenverkehr|  
    |Port 443|HTTPS-Webdatenverkehr|  
  

-   **Lesen Sie die Dokumentation zu dieser Version der Windows Server Essentials**. Die Versionsdokumentation enthält aktuelle Informationen, die möglicherweise für die ordnungsgemäße Installation und Konfiguration von Windows Server Essentials. Zum Anzeigen oder Drucken der Versionsdokumentation, finden Sie unter [freigeben Documentation for Windows Server Essentials](../get-started/release-notes.md).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

