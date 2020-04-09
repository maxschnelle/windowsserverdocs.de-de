---
title: Hardwareanforderungen und Empfehlungen zur Leistung
description: Bietet Hardware-und Leistungsanforderungen sowie Empfehlungen für Multipoint Services
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: dcb139cddf6a7838511365c6a85dc12bd06a81eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820343"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>Hardwareanforderungen und Empfehlungen zur Leistung
In diesem Thema wird die Hardware beschrieben, die zum Ausführen eines Multipoint Services-Systems und zum unterstützen von Anwendungsszenarien für Benutzer erforderlich ist. Das Benutzer Szenario wirkt sich direkt auf die CPU-, RAM-und Netzwerk Bandbreitenanforderungen aus.  

## <a name="optimize-multipoint-services-system-performance"></a>Optimieren der Multipoint Services-Systemleistung  
Die Leistung des Multipoint Services-Systems wird direkt von der Kapazität der CPU, der GPU und der RAM-Kapazität, die auf dem Computer verfügbar ist, auf dem Multipoint Services ausgeführt wird, beeinträchtigt.  
  
### <a name="applications-and-internet-content"></a>Anwendungen und Internet Inhalte  
Da Multipoint Services eine Lösung für die gemeinsame Nutzung von Ressourcen ist, können sich der Typ und die Anzahl der Anwendungen, die auf den Stationen ausgeführt werden, auf die Leistung Ihres Multipoint Services-Systems auswirken. Es ist wichtig, die Typen von Programmen zu beachten, die bei der Planung Ihres Systems regelmäßig verwendet werden. Beispielsweise erfordert eine grafikintensive Anwendung einen leistungsfähigeren Computer als eine Anwendung, z. b. ein Textverarbeitungs Tool. Das über Laden des Computers mit Grafik intensiven Anwendungen führt wahrscheinlich zu Verzögerungen beim gesamten System.  
  
Der Inhaltstyp, auf den Anwendungen zugreifen, wirkt sich auch auf die Leistung des Systems aus. Wenn mehrere Stationen Webbrowser für den Zugriff auf Multimedia-Inhalte verwenden, wie z. b. vollbewegungs-Video, können vor der Beeinträchtigung der Systemleistung weniger Stationen verbunden werden. Wenn dagegen mehrere Stationen Webbrowser verwenden, um auf statische Webinhalte zuzugreifen, können mehr Stationen ohne erhebliche Auswirkung auf die Leistung verbunden werden.  
  
### <a name="hardware-recommendations"></a>Hardware-Empfehlungen  
Verwenden Sie die Richtlinien in der folgenden Tabelle, wenn Sie Ihr System planen und testen, um eine gute Leistung mit Ihrem Multipoint Services-System zu erzielen. Dies sind die grundlegenden Anforderungen für die Multipoint-Dienste. Die tatsächliche Konfigurations Größe hängt von Ihrer Systemkonfiguration, der Arbeitsauslastung, die Sie ausführen, und der Hardware Funktion ab. Sie sollten stets validieren, indem Sie Ihre Anwendungen und Hardware testen.  
  
> [!NOTE]  
> 2C = 2 Kerne, 4C = 4 Kerne, 6C = 6 Kerne, MT = Multithreading. Die Prozessorgeschwindigkeit muss mindestens 2,0 Gigahertz (GHz) betragen.  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>Empfohlene Hardware für die Ausführung von Standard-Multipoint-Server Stationen  
  
|Anwendungsszenario|Bis zu 5 Stationen|6-8-Stationen|9-12-Stationen|13-16-Stationen|17-20-Stationen|21-24-Stationen|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**Fak**<p>Office, Webbrowser, Branchen Anwendungen|CPU: 2C<p>RAM: 2 GB|CPU: 2C<p>RAM: 4 GB|CPU: 4C<p>RAM: 6 GB|CPU: 4C<p>RAM: 8 GB|CPU: 4C + MT oder 6C<p>RAM: 10 GB| CPU: 6C + MT<p>RAM: 12 GB|
|**Mischen**<p>Office, Webbrowser, Branchen Anwendungen und gelegentlich von einigen Benutzern verwendete Video Verwendung|CPU: 2C<p>RAM: 2 GB|CPU: 2C<p>RAM: 4 GB|CPU: 4C<p>RAM: 6 GB|CPU: 4C + MT oder 6C<p>RAM: 8 GB|CPU: 6C + MT<p>RAM: 10 GB| CPU: 6C + MT<p>RAM: 12 GB| 
|**Video intensiv**<p>Office, Webbrowser, Branchen Anwendungen und häufig von allen Benutzern verwendende Videos **:** Videotests wurden mit dem Video "360p H. 264" bei der systemeigenen Auflösung ausgeführt.|CPU: 4C + MT<p>RAM: 2 GB|CPU: 6C + MT<p>RAM: 4 GB|CPU: 8c + MT<p>RAM: 6 GB|CPU: 12C + MT<p>RAM: 8 GB|CPU: 16C + MT<p>RAM: 10 GB<p>-Thin Client: remotefx<br />-USB-Video nicht empfehlenswert| CPU: 20C + MT<p>RAM: 12 GB<p>-Thin Client: remotefx<br />-USB-Video nicht empfehlenswert|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>Empfohlene Hardware für die Ausführung vollständiger virtueller Windows 10-Desktops  
Das Ausführen einer vollständigen virtuellen Betriebssystem Instanz für jede Station ist Rechen intensiver als die Ausführung der standardmäßigen Multipoint Desktop-Sitzungen, sodass die Host Hardwareanforderungen pro Station höher sind:  
  
1.  CPU: 1 Kern oder Thread pro Station  
  
2.  Solid State Drive (SSD)  
  
    1.  Kapazitäts > = 20 GB pro Station + 40 GB für das WMS-Host Betriebssystem  
  
    2.  Zufälliger Lese-/Schreib-IOPS-> = 3K pro Station  
  
3.  RAM-> = 2 GB pro Station + 2 GB für das WMS-Host Betriebssystem  
  
Die BIOS-CPU-Einstellung wurde zum Aktivieren der Virtualisierung konfiguriert – Second Level Address Translation (slat)  
  
Wenden Sie sich an Ihren Hardwarehersteller, um weitere Informationen zur Auswahl der optimalen Multipoint Services-Hardware für Ihre Anforderungen zu erhalten.  