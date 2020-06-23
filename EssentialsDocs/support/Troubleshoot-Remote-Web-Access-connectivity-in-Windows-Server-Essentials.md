---
title: Behandeln von Problemen mit der Remotewebzugriff-Verbindung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9fb3628ed519d5faae04787dbb84da37f27d96fb
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217490"
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Behandeln von Problemen mit der Remotewebzugriff-Verbindung in Windows Server Essentials
 
>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Windows Server Essentials kann in der Regel einen Breitbandrouter automatisch konfigurieren, wenn der Router ein UPnP-zertifiziertes Gerät ist und die UPnP-Einstellung auf dem Router aktiviert ist.  
  
## <a name="possible-issues"></a>Mögliche Probleme  
 Die folgenden Probleme können bei der Remotewebzugriff-Verbindung auftreten:  
  
-   Der Router ist nicht eingeschaltet oder nicht mit dem Netzwerk verbunden.  
  
-   Die UPnP-Einstellung für Ihren Router ist deaktiviert.  
  
-   Der Router unterstützt ggf. den UPnP-Standard nicht vollständig. Microsoft führt eine Liste der Router, die mit Windows-Betriebssystemen zusammenarbeiten. Eine Liste der Router (einschließlich Funkroutern), die mit Windows Server Essentials kompatibel sind, finden Sie im [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
## <a name="possible-fixes"></a>Mögliche Korrekturen  
 Über die folgenden Aktionen können diese Probleme behoben werden:  
  
- Stellen Sie sicher, dass der Router eingeschaltet ist und ordnungsgemäß funktioniert.  
  
- Stellen Sie sicher, dass der Server direkt mit dem Router oder einem Switch verbunden ist, der mit dem Router verbunden ist.  
  
- Überprüfen, ob das Breitbandgerät, das die Verbindung mit Ihrem Internetdienstanbieter (ISP) herstellt, aktiviert ist, ordnungsgemäß funktioniert und ob Ihr Router mit dem Breitbandgerät verbunden ist.  
  
- Aktivieren Sie die UPnP-Einstellung für Ihren Router. Öffnen Sie die Konfigurationswebseite für Ihren Router, um die UPnP-Einstellung zu aktivieren. Informationen dazu, wie Sie sich bei Ihrem Router anmelden und die UPnP-Einstellung aktivieren, finden Sie in der Dokumentation zum Router. Nachdem Sie die UPnP-Einstellung aktiviert haben, führen Sie den Assistenten zum Aktivieren von Remote Webzugriff erneut aus, um den Router zu konfigurieren.  
  
- Wenn Ihr Router den UPnP-Standard nicht vollständig unterstützt, kann er nicht automatisch konfiguriert werden. Sie müssen den Router manuell konfigurieren oder einen Router erwerben, der den UPnP-Standard unterstützt.  
  
   Dazu führen Sie die folgenden Schritte aus:  
  
  - Erstellen Sie die IP-Adressreservierung für Ihren Windows Server Essentials-Server.  
  
     Bevor Sie den Router manuell so konfigurieren, dass die erforderlichen Ports an Windows Server Essentials weitergeleitet werden, müssen Sie auf dem Router eine DHCP-Reservierung für Ihren Server mit Windows Server Essentials einrichten. Durch diesen Schritt wird sichergestellt, dass sich die IP-Adresse, an die Sie die Ports weiterleiten, nicht ändert.  
  
     Informationen dazu, wie Sie manuell eine DHCP-Reservierung für den Server auf dem Router einrichten, finden Sie in der Dokumentation des Herstellers für Ihren Router.  
  
  - Konfigurieren Sie die Portweiterleitung auf dem Router für die folgenden Ports:  
  
    |Dienst oder Protokoll|Port|  
    |-------------------------|----------|  
    |HTTP|TCP 80|  
    |HTTPS|TCP 443|  
  
    Informationen zum manuellen Einrichten der Port Weiterleitung auf dem Router finden Sie in der Dokumentation des Herstellers.  
  
    Eine typische Routerkonfigurationsseite enthält eine Tabelle, die der folgenden ähnelt.  
  
  > [!NOTE]
  >  In dieser Tabelle lautet die IP-Adresse des Computer mit Windows Server Essentials 192.168.0.100. Sie müssen die IP-Adresse des Computers ermitteln und diese IP-Adresse durch die IP-Adresse ersetzen, die in der Tabelle angezeigt wird.  
  
  |IP-Adresse|Protokoll (TCP/UDP)|Zeitplan|Eingehender Filter|  
  |----------------|---------------------------|--------------|--------------------|  
  |192.168.0.100|TCP 80|Always|Alle zulassen|  
  |192.168.0.100|TCP 443|Always|Alle zulassen|  
  
   Nachdem Sie den Router manuell konfiguriert haben, führen Sie den Assistenten zum Aktivieren von Remote Webzugriff aus, um sicherzustellen, dass Sie auf **der Seite mit den ersten** Schritten die Option **routereinrichtung überspringen** auswählen  
  
- Erwerben Sie einen neuen Router, falls Ihr Router den UPnP-Standard nicht vollständig unterstützt.  
  
> [!TIP]
>  Stellen Sie sicher, dass auf dem Router die neueste BIOS-Firmware installiert ist. Sie können die BIOS-Firmware für den Router auf der Webseite für die Konfiguration des Routers regelmäßig aktualisieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem Router. Führen Sie nach der Aktualisierung des Routers den Assistenten zum Einrichten von Zugriff überall aus.  
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Verwenden des Remotewebzugriffs](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten der Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von %%amp;quot;Zugriff überall%%amp;quot;](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)  

-   [Unterstützung von Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

