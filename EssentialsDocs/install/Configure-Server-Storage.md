---
title: Konfigurieren von Serverspeicher
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef7ddcdd-3a74-40ca-9487-c3a6fc5155a5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6de485f6fd46464ba707bc0871f60ac2fec5a1db
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-server-storage"></a>Konfigurieren von Serverspeicher

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

## <a name="sample-hard-disk-configurations"></a>Beispiele für Festplattenkonfigurationen  
 Die folgende Tabelle enthält Beispiele für Festplattenkonfiguration. Die Schätzwerte basieren auf typischer Verwendung und Funktionalität, aber sie keine Aspekte, die optimale Leistung auswirken. Sie können einen beliebigen Typ von unterstützter Festplatte für diese Konfigurationen (z. B. SATA oder SCSI), basierend auf den Vorgaben und Anforderungen des Kunden verwenden.  
  
> [!IMPORTANT]
>   Windows Server Essentials muss als Volume "c:" installiert werden, und die Größe des Volumes muss mindestens 60 GB sein. Es wird empfohlen, zwei Partitionen auf dem Betriebssystemlaufwerk zu erstellen, und nicht C: (Systempartition) zum Speichern von Geschäftsdaten.  
  
|Server-Ebene|Datenträgerkonfiguration|  
|------------------|------------------------|  
|Eintrag|-Zwei physische Datenträger<br /><br /> -Konfiguriert als RAID 1-Spiegelsatz Gruppe, die Folgendes enthält:<br /><br /> -Volume "c:"? 60 GB<br /><br /> – Volume D:? 1000 GB|  
|Mittel|-Drei physische Datenträger<br /><br /> -Konfiguriert als RAID 5-Spiegelsatz, die Folgendes enthält:<br /><br /> -Volume "c:"? 60 GB<br /><br /> – Volume D:? 1500 GB|  
|Hoch|-Fünf oder mehr physische Datenträger<br /><br /> -Zwei Datenträger in einem RAID 1-Spiegelsatz, die das Volume "c:" enthält? 100GB<br /><br /> -Alle verbleibenden Datenträger in einem RAID-5-Satz, der Folgendes enthält:<br /><br /> – Volume D:? 1500 GB<br /><br /> -Volume "e:"? 1500 GB|  
  
 Diese Empfehlungen berücksichtigen die Größe des installierten Betriebssystems, die durchschnittliche Größe der Speicherung von Daten, die der Server verwendet, und die erwarteten Datenwachstum des Datenspeichers die Lebensdauer des Servers. Die Volumes können Partitionen auf einem einzelnen physischen Datenträger sein, oder sie können auf separaten physischen Datenträgern platziert werden. Da der Server für Ihre Kunden wichtige Daten speichert, wird empfohlen, mehrere physische Datenträger zu verwenden und Schützen der Daten Ihrer Kunden durch Verwendung des Hardware-RAID oder Speicherplätzen.  
  
## <a name="configuring-your-server-backup"></a>Konfigurieren der serversicherung  
 Zusätzlich zu den internen Festplatten auf dem Server sollten Kunden externen USB-Festplatten für Sicherungen verwenden. Idealerweise müsste der Kunde mindestens zwei externe Festplatten mit ausreichender Kapazität aller Daten auf dem Server sichern. Wenn externe Festplatten verwendet werden, kann der Kunde einen Datenträger außerhalb des Standorts jede Nacht zum weiteren Schutz der Daten dauern.  
  
## <a name="partition-configuration"></a>Partitionskonfiguration  
 Während der Erstkonfiguration des Servers eine Reihe von standardserverordnern, die freigegebene Ordner und den Client Computer backup-Ordner enthalten in der größten Datenpartition auf Datenträger 0 erstellt.  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

