---
title: Konfigurieren des Serverspeichers
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433744"
---
# <a name="configure-server-storage"></a>Konfigurieren des Serverspeichers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="sample-hard-disk-configurations"></a>Beispiele für Festplattenkonfigurationen  
 Die folgende Tabelle enthält Beispiele für Festplattenkonfiguration. Die Schätzwerte basieren auf typischer Verwendung und Funktionalität, berücksichtigen jedoch keine Aspekte, die sich auf die optimale Leistung auswirken. Sie können unter Berücksichtigung der Vorgaben und Anforderungen des Kunden einen beliebigen Typ von unterstützter Festplatte für diese Konfigurationen verwenden (z. B. SATA oder SCSI).  
  
> [!IMPORTANT]
>   Windows Server Essentials muss als Volume "c:" installiert werden, und die Größe des Volumes muss mindestens 60 GB sein. Es wird empfohlen, zwei Partitionen auf dem Betriebssystemlaufwerk zu erstellen und ":C" (Systempartition) nicht zum Speichern von Geschäftsdaten zu verwenden.  
  
|Serverebene|Datenträgerkonfiguration|  
|------------------|------------------------|  
|Eingabe|-Zwei physische Datenträger<br /><br /> -Konfiguriert als RAID 1-Spiegelsatz Gruppe, die Folgendes enthält:<br /><br /> -"C:" Volume? 60 GB<br /><br /> -D: Volume? 1000 GB|  
|Mittel|-Drei physische Datenträger<br /><br /> -Konfiguriert als RAID 5-Spiegelsatz, das Folgendes enthält:<br /><br /> -"C:" Volume? 60 GB<br /><br /> -D: Volume? 1500 GB|  
|Hoch|– Fünf oder mehr physische Datenträger<br /><br /> – Es werden zwei Datenträger in einem RAID 1-Spiegelsatz, die das Volume "c:" enthält? 100 GB<br /><br /> – Alle verbleibenden Datenträger in einem RAID 5-Spiegelsatz mit den folgenden Komponenten:<br /><br /> -D: Volume? 1500 GB<br /><br /> -E: Volume? 1500 GB|  
  
 Diese Empfehlungen berücksichtigen die Größe des installierten Betriebssystems, die durchschnittliche Größe des vom Server verwendeten Datenspeichers sowie das während der Lebensdauer des Servers erwartete Wachstum des Datenspeichers. Die Volumes können Partitionen auf einem physischen Datenträger sein, oder sie können sich auf separaten physischen Datenträgern befinden. Da der Server wichtige Daten für Ihre Kunden gespeichert werden, wird empfohlen, mehrere physische Datenträger zu verwenden und den Schutz Ihrer Kunden s-Daten mithilfe von Hardware-RAID oder Speicherplätzen zu verwenden.  
  
## <a name="configuring-your-server-backup"></a>Konfigurieren der Serversicherung  
 Neben den internen Festplatten auf dem Server sollten Kunden die Verwendung externer USB-Festplatten für Datensicherungen in Betracht ziehen. Idealerweise besitzt der Kunde mindestens zwei externe Festplatten mit ausreichender Kapazität zum Sichern aller Daten auf dem Server. Wenn externe Festplatten verwendet werden, kann der Kunde jeweils eine Festplatte an einem anderen Standort aufbewahren, um die Daten noch besser zu schützen.  
  
## <a name="partition-configuration"></a>Partitionskonfiguration  
 Während der Erstkonfiguration des Servers wird in der größten Datenpartition auf Datenträger 0 eine Reihe von Standardordnern erstellt, zu denen freigegebene Ordner und Ordner für die Clientcomputersicherung gehören.  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

