---
title: Hardwareanforderungen und Empfehlungen zur Leistung
description: Stellt Anforderungen an Hardware und Leistung und Empfehlungen für das MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b47f4c224d4a4f6f4aa104b6d5ee5d93590ac0c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823391"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>Hardwareanforderungen und Empfehlungen zur Leistung
In diesem Thema wird beschrieben, die Hardware, die erforderlich sind, führen Sie ein MultiPoint Services-System und Anwendungsszenarien zu unterstützen. Das Benutzerszenario wirkt sich direkt auf die CPU, RAM und Anforderungen an die Netzwerkbandbreite.  

## <a name="optimize-multipoint-services-system-performance"></a>Optimieren der Leistung von MultiPoint Services-Systems  
Die Leistung Ihres MultiPoint Services-Systems sind direkt betroffen, indem Sie die Möglichkeit, die CPU, GPU und die Größe des Arbeitsspeichers, der auf dem Computer verfügbar ist, das MultiPoint Services ausgeführt wird.  
  
### <a name="applications-and-internet-content"></a>Anwendungen und Internet-Inhalt  
Da MultiPoint Services eine freigegebene Ressource-computing-Lösung ist, können der Typ und die Anzahl der Anwendungen, die auf die Stationen ausgeführt werden die Leistung Ihres MultiPoint Services-Systems auswirken. Es ist wichtig, die Typen von Programmen zu berücksichtigen, die regelmäßig auf, wenn Sie, Ihr System planen verwendet werden. So erfordert beispielsweise eine Anwendung für grafikintensive einen leistungsfähigeren Computer als eine Anwendung z. B. ein Textverarbeitungsprogramm. Überladen den Computer mit grafikintensive Anwendungen werden wahrscheinlich Lag Probleme im gesamten System führen.  
  
Der Typ des Inhalts, die von Anwendungen zugegriffen wird, wirkt sich auch auf die Systemleistung aus. Wenn mehrere Stationen multimedia-Inhalte, z. B. Full Motion-Videos, den Zugriff auf Webbrowser verwenden können weniger Stationen verbunden werden, bevor Sie die Systemleistung beeinträchtigen. Im Gegensatz dazu können mehrere Stationen Webbrowser verwenden, um die statische Webinhalte zugreifen, mehrere Stationen ohne erhebliche Auswirkungen auf die Leistung verbunden werden.  
  
### <a name="hardware-recommendations"></a>Hardware-Empfehlungen  
Um gute Leistung mit Ihrem MultiPoint Services-System unter verschiedenen auslastungen zu erreichen, verwenden Sie die Richtlinien in der folgenden Tabelle, wenn Sie planen und Testen Ihr System. Dies sind die grundlegenden Anforderungen ForMultiPoint-Dienste. Die tatsächliche Größe hängt von Ihrer Systemkonfiguration, der arbeitsauslastung, die Sie ausführen und die Hardwarefunktionen ab. Sie sollten immer überprüfen, testen Sie Ihre Anwendungen und Hardware.  
  
> [!NOTE]  
> 2 C = 2 Kerne, 4, C = 4 Kerne, 6, C = 6 Kerne, MT = multithreading. Prozessorgeschwindigkeit sollte über mindestens 2,0 Gigahertz (GHz).  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>Minimale hardwareanforderungen zum Ausführen von standardmäßigen MultiPoint Server-Stationen  
  
|Anwendungsszenario|Bis zu 5 Stationen|6 bis 8 Stationen|9 bis 12 Stationen|13-16-Stationen|17 – 20 Stationen|21.-24. Stationen|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**Produktivität**<br /><br />Office Web durchsuchen, Line-of-Business-Anwendungen|CPU: 2C<br /><br />RAM: 2 GB|CPU: 2C<br /><br />RAM: 4 GB|CPU: 4C<br /><br />RAM: 6 GB|CPU: 4C<br /><br />RAM: 8 GB|CPU: 4C + MT oder 6C<br /><br />RAM: 10 GB| CPU: 6C + MT<br /><br />RAM: 12 GB|
|**Gemischte**<br /><br />Office, Browsen im Web, Line-of-Business-Anwendungen und gelegentliche Video-Nutzung durch einige Benutzer|CPU: 2C<br /><br />RAM: 2 GB|CPU: 2C<br /><br />RAM: 4 GB|CPU: 4C<br /><br />RAM: 6 GB|CPU: 4C + MT oder 6C<br /><br />RAM: 8 GB|CPU: 6C + MT<br /><br />RAM: 10 GB| CPU: 6C + MT<br /><br />RAM: 12 GB| 
|**Intensive Video**<br /><br />Office, Browsen im Web, Line-of-Business-Anwendungen und video verwenden alle Benutzer häufig **beachten:** Video zu testen, wurde die 360p h. 264-Video mit native Auflösung mit ausgeführt.|CPU: 4C + MT<br /><br />RAM: 2 GB|CPU: 6C + MT<br /><br />RAM: 4 GB|CPU: 8C + MT<br /><br />RAM: 6 GB|CPU: 12C + MT<br /><br />RAM: 8 GB|CPU: 16C + MT<br /><br />RAM: 10 GB<br /><br />-Thin-Client: RemoteFX<br />-USB-Video nicht empfohlen.| CPU: 20C + MT<br /><br />RAM: 12 GB<br /><br />-Thin-Client: RemoteFX<br />-USB-Video nicht empfohlen.|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>Minimale hardwareanforderungen zum Ausführen von vollständigen virtuelle Windows 10-desktops  
Ausführen einer vollständigen virtuelles Betriebssystem-Instanz für jede Station ist mehr Compute-ressourcenintensiver als die MultiPoint desktop Standard-Sitzungen ausgeführt, also den Host hardwareanforderungen für einzelne Station höher:  
  
1.  CPU: 1 Kern oder Thread pro station  
  
2.  Solid-State Drive (SSD)  
  
    1.  Kapazität > = 20GB pro Station + 40GB, für das WMS Betriebssystem hosten  
  
    2.  IOPS für zufällige Lese-/Schreibzugriff > = 3K einzelne Station  
  
3.  RAM > = 2GB pro Station + 2GB, für das WMS Betriebssystem hosten  
  
BIOS-CPU-Einstellung wurde konfiguriert, um die Virtualisierung – Second Level Address Translation (SLAT) zu aktivieren.  
  
Weitere Informationen zum Auswählen der besten MultiPoint Services-Hardware für Ihre Anforderungen und wenden Sie sich an Ihren Hardwarehersteller.  