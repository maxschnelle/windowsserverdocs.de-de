---
title: Behandeln von Problemen Sie Remotewebzugriff-Verbindung in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: af4725fd3b1861c847434e3ed62c3da030689fb5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Behandeln von Problemen Sie Remotewebzugriff-Verbindung in Windows Server Essentials
 
>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 In der Regel können Windows Server Essentials einen Breitbandrouter automatisch konfigurieren, wenn der Router ein UPnP-zertifiziertes Gerät und die UPnP-Einstellung auf dem Router aktiviert ist.  
  
## <a name="possible-issues"></a>Mögliche Probleme  
 Sie können die folgenden Probleme mit Remote Web Access-Konnektivität auftreten:  
  
-   Der Router ist nicht eingeschaltet oder nicht mit dem Netzwerk verbunden ist.  
  
-   Die UPnP-Einstellung für Ihren Router ist deaktiviert.  
  
-   Der Router kann den UPnP-Standard nicht vollständig unterstützt. Microsoft verwaltet eine Liste der Router, die mit Windows-Betriebssystemen kompatibel. Zum Anzeigen der Liste der Router (einschließlich funkroutern), die mit Windows Server Essentials kompatibel sind, finden Sie auf der [Windows-Kompatibilitätscenter](https://www.microsoft.com/windows/compatibility/CompatCenter/Home).  
  
## <a name="possible-fixes"></a>Mögliche Problembehebungen  
 Die folgenden Aktionen können diese Probleme beheben:  
  
-   Stellen Sie sicher, dass der Router eingeschaltet ist und ordnungsgemäß funktioniert.  
  
-   Stellen Sie sicher, dass der Server direkt mit dem Router verbunden ist oder dass es mit einem Switch verbunden ist, die mit dem Router verbunden ist.  
  
-   Überprüfen Sie, ob das Breitbandgerät, die Verbindung mit Ihrem Internetdienstanbieter (ISP) aktiviert ist, ordnungsgemäß funktioniert und, die der Router mit dem Breitbandgerät verbunden ist.  
  
-   Aktivieren Sie die UPnP-Einstellung für Ihren Router. Verbinden Sie mit der Konfigurationswebseite für Ihren Router, um die UPnP-Einstellung zu aktivieren. Informationen dazu, wie für die Anmeldung bei Ihrem Router und wie Sie die UPnP-Einstellung aktivieren finden Sie in der Dokumentation zu Ihrem Router. Nachdem Sie die UPnP-Einstellung aktivieren, führen Sie die aktivieren Sie auf Assistent für Remotewebzugriff erneut aus, um den Router zu konfigurieren.  
  
-   Wenn Ihr Router den UPnP-Standard nicht vollständig unterstützt, kann es automatisch konfiguriert werden. Sie müssen manuell konfigurieren Sie den Router oder erwerben einen Router, der den UPnP-Standard unterstützt.  
  
     Wenn um Sie den Router manuell zu konfigurieren, müssen führen Sie die folgenden Aufgaben aus:  
  
    -   Erstellen Sie die IP-Adressreservierung für Ihren Windows Server Essentials-Server.  
  
         Bevor Sie den Router für die erforderlichen Ports zu Windows Server Essentials Weiterleitung manuell konfigurieren, müssen Sie eine Reservierung Dynamic Host Configuration-Protokoll (DHCP) für den Server einrichten, auf denen Windows Server Essentials auf dem Router ausgeführt wird. Dieser Schrittwird sichergestellt, dass die IP-Adresse, die Sie die Ports, die sich nicht ändern, weiterleiten.  
  
         Informationen dazu, wie Sie eine DHCP-Reservierung für den Server auf den Router manuell einrichten finden Sie unter der Hersteller-s-Dokumentation für Ihren Router.  
  
    -   Konfigurieren Sie portweiterleitung auf dem Router für die folgenden Ports:  
  
        |Dienst oder Protokoll|Port|  
        |-------------------------|----------|  
        |HTTP|TCP 80|  
        |HTTPS|TCP 443|  
  
     Informationen zum Einrichten der portweiterleitung auf dem Router manuell festlegen finden Sie in der Dokumentation des Herstellers s.  
  
     Eine typische Routerkonfigurationsseite enthält eine Tabelle, die der folgenden ähnelt.  
  
    > [!NOTE]
    >  In dieser Tabelle ist die IP-Adresse des Computers, auf denen Windows Server Essentials ausgeführt wird 192.168.0.100. Sie müssen die IP-Adresse des Computers ermitteln und ersetzen die IP-Adresse für die IP-Adresse, die in der Tabelle aufgeführten.  
  
    |IP-Adresse|Protokoll (TCP/UDP)|Zeitplan|Eingehende Filter|  
    |----------------|---------------------------|--------------|--------------------|  
    |192.168.0.100|TCP 80|Immer|Alle zulassen|  
    |192.168.0.100|TCP 443|Immer|Alle zulassen|  
  
     Nachdem Sie den Router manuell konfigurieren, führen Sie die aktivieren Sie auf Assistent für Remotewebzugriff, um sicherzustellen, dass Sie auswählen, die **routereinrichtung** Option auf der **erste Schritte** Seite.  
  
-   Erwerben Sie einen neuen Router, wenn Ihr Router den UPnP-Standard nicht vollständig unterstützt.  
  
> [!TIP]
>  Stellen Sie sicher, dass der Router die neueste BIOS-Firmware installiert ist. Sie können die BIOS-Firmware oft für den Router auf der Konfigurationswebseite des Routers aktualisieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem Router. Führen Sie nach der Aktualisierung des Routers den Anywhere Access-Assistenten.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwenden von Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten des Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Unterstützung für Windows Server Essentials](Support-Windows-Server-Essentials.md)

-   [Unterstützung für Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

