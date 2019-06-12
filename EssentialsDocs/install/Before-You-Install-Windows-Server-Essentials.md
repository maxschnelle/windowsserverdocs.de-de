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
ms.openlocfilehash: 32b2b37e0d0109b8ad2a991b9f7693139103734d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433709"
---
# <a name="before-you-install-windows-server-essentials"></a>Vor der Installation von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_BeforeYouBegin"></a> Bevor Sie die Installation von Windows Server Essentials beginnen, führen Sie die folgenden Aufgaben:  

-   **Stellen Sie sicher, dass Ihr Computer die Mindesthardwareanforderungen erfüllt**. Dies schließt auch, ob zusätzlichen Hardware erforderlich, und überprüfen, dass die Treiber für Ihre Hardware von Windows Server Essentials unterstützt werden. Weitere Informationen finden Sie unter [System Requirements for Windows Server Essentials](../get-started/system-requirements.md).   


~~~
> [!IMPORTANT]
>  Before you install  Windows Server Essentials on a pre-existing computer, we recommend that you fully format and then repartition the hard disks of the pre-existing computer. By formatting and repartitioning the hard disks, you remove the possibility that hidden partitions remain on the hard disks.  
~~~

- **Bereiten Sie Ihr Netzwerk** um Ihr Netzwerk für die Installation von Windows Server Essentials vorzubereiten, gehen Sie folgendermaßen vor:  


  - **Aktualisieren Sie das Betriebssystem auf den Clientcomputern** Windows Server Essentials unterstützt die folgenden Betriebssysteme:  Windows 8, Windows 7, Windows 10 und Macintosh OS X Lion oder höher. Diese Betriebssysteme stellen die erforderlichen Sicherheitsfunktionen, die erforderliche Zuverlässigkeit und Leistung sowie Funktionen für das lokale Netzwerk bereit.  

  - **Konfigurieren Sie den Router**. Stellen Sie sicher, dass der Router wie folgt konfiguriert ist:  

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


- **Lesen Sie die Windows Server Essentials-Versionsdokumentation**. Die Versionsdokumentation enthält aktuelle Informationen, die möglicherweise entscheidend für ordnungsgemäß installieren und Konfigurieren von Windows Server Essentials. Zum Anzeigen oder Drucken der Versionsdokumentation, finden Sie unter [Release Documentation for Windows Server Essentials](../get-started/release-notes.md).  

## <a name="see-also"></a>Siehe auch  

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

