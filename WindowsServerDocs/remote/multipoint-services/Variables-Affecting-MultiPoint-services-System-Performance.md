---
title: Variablen mit Auswirkung auf die Leistung von MultiPoint Services-Systemen
description: Leistungsinformationen für Multipoint Services
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 0f3e8875-1b5e-4789-b16c-d06d6e31f38e
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 44f268c958ed32e527b66cebe1a10d33652eb9b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858913"
---
# <a name="variables-affecting-multipoint-services-system-performance"></a>Variablen mit Auswirkung auf die Leistung von MultiPoint Services-Systemen
Viele Variablen können sich auf die Gesamtleistung Ihres Multipoint Services-Systems auswirken. Sie sollten diese beim Entwerfen Ihres Systems in Erwägung gezogen werden.  
  
## <a name="usage"></a>Verwendung  
  
-   **Anwendungen** Der Typ und die Anzahl der Anwendungen, die gleichzeitig ausgeführt werden, insbesondere Grafiken\-starker oder Speicher intensiver Anwendungen, wirken sich auf die Gesamtleistung des Systems aus. Weitere Informationen finden Sie unter [Anwendungen und Internet Inhalte](hardware-and-performance-recommendations.md#applications-and-internet-content).  
  
-   **Internet Nutzung** Stellen Sie sich vor, wenn Ihre Benutzer Multimedia-Inhalte oder Webseiten anzeigen, die Videos mit vollständiger Bewegung verwenden. Dieser Inhaltstyp kann das System überladen, wenn zu viele Benutzer gleichzeitig anzeigen.  
  
    > [!NOTE]  
    > Das Projektions Feature in Multipoint Services, das es Lehrkräften ermöglicht, ihre Bildschirme auf ihren Studenten Monitoren zu projizieren, ist nicht für das Projizieren von voll bewegungsvideos konzipiert. Die Projektions Funktion ist für Demonstrationszwecke konzipiert, wie z. b. die Darstellung einer Prozedur.  
  
-   **Hoch Geschwindigkeits Geräte** Wenn zu viele Benutzer gleichzeitig ein hoch Geschwindigkeits Gerät wie eine Webkamera oder einen DVD-Player verwenden, wirkt sich dies auf die Gesamtleistung des Systems aus.  
  
## <a name="configuration"></a>Konfiguration  
  
-   **CPU, GPU und RAM** Weitere Informationen zu den Empfehlungen für CPU, GPU und RAM finden Sie unter [Optimieren der Multipoint Services-System Leistung](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance) in diesem Handbuch.  
-   **Netzwerkbandbreite** Bei verbundenen RDP-over-LAN-Stationen sind die Netzwerkbandbreite und die Funktionsfähigkeit des Clients (z. b. ein Thin Client, ein Desktop-PC oder ein Laptop) wichtig, insbesondere dann, wenn das Video in der Sitzung des Benutzers ausgeführt wird. Wenn Sie USB-over-Ethernet-Clients verwenden, sollte auch die Netzwerkbandbreite berücksichtigt werden. Video Daten für alle Geräte werden über die gleiche Ethernet-Verbindung gesendet. Sie sollten daher bei der Verwendung dieser Geräte ein separates Gigabit-Ethernet-Netzwerk einrichten.  
-   **Remotefx** Bei verbundenen RDP-over-LAN-Stationen können Sie remotefx verwenden, um die Bereitstellung von Multimedia-Inhalten mit hoher Definition erheblich zu verbessern.  
-   **Bildschirmauflösung** Wenn Sie eine hohe voll Bild Grafik verwenden, sollten Sie die Auflösung des Monitors verringern, um die Leistung zu maximieren.  
-   **Anzahl der USB-Clients** Die Gesamtanzahl der USB-Clients auf einem einzelnen Stammhub auf dem Server wirkt sich direkt auf die Leistung des Videos aus. Weitere Informationen finden Sie unter [Layout für mit USB-Clients verbundene Stationen](MultiPoint-services-Site-Planning.md#layout-for-usb-zero-client-connected-stations). Die Anzahl der unterstützten USB-over-Ethernet-Client Stationen kann geringfügig niedriger sein als die Anzahl der USB-Clients.  
-   **USB-Bandbreite** Beachten Sie beim Entwerfen des Systems die USB-Bandbreite.  Dies ist insbesondere bei USB-Clients wichtig, von denen Videodaten über die USB-Verbindung gesendet werden. Um die Bandbreite zu optimieren, minimieren Sie die Anzahl der Geräte, die mit einem einzelnen USB-Anschluss auf dem Server verbunden sind. Dies gilt für nicht verkettete Stationen und zwischen Hubs. Weitere Informationen finden Sie unter [Stations Hubs](MultiPoint-services-Site-Planning.md#station-hubs) und [zwischen Hubs](MultiPoint-services-Site-Planning.md#intermediate-hubs).  
  
-   **USB-Typ** Die Verwendung von USB 3,0 anstelle von USB 2,0 erhöht die verfügbare Bandbreite zwischen dem Server und dem Zwischenhub, wenn Sie mehr als drei USB-Clients mit dem Hub verbinden oder wenn Sie USB-Geräte mit hoher Bandbreite verwenden.  
  
-   **Stationen** Die Gesamtanzahl der Stationen wirkt sich auf die Leistung aus. Wenn Sie über hohe Grafik-, Verarbeitungs-oder Video Anforderungen verfügen, empfiehlt es sich, die Gesamtanzahl der Stationen einzuschränken. Weitere Informationen finden Sie unter [Optimieren der Multipoint Services-System Leistung](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance).