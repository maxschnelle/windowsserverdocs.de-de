---
title: Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41000915-f6ff-4dbb-b7be-629ef36386d4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6f6f0d27472664cd1cc538897d3d525fad506282
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 Windows Server Essentials bietet zuverlässige Möglichkeiten für regelmäßige Sicherungen des Servers und Sicherungen der Computer im Netzwerk ausführen. Im Fall eines Datenverlusts können Sie Daten aus einer erfolgreichen Sicherung auf dem Server wiederherstellen, ohne den gesamten Computer wiederherstellen. Bei Bedarf können Sie eine vollständige Systemwiederherstellung auf Server- oder Clientcomputern im Netzwerk ausführen. In der folgende Tabelle werden die verschiedenen Sicherungsoptionen für Sie und ihre Vorteile beschrieben.  
  
|Sicherungsfeature|Beschreibung|Vorteile|  
|--------------------|-----------------|----------------|  
|Server-Sicherung|Sichert den Server mit Windows Server Essentials. Die Daten werden auf einem externen USB-Laufwerk gesichert.<br /><br /> Weitere Informationen finden Sie unter [Manage Server Backup](Manage-Server-Backup-in-Windows-Server-Essentials.md) und [wiederherstellen oder Reparieren des Servers](Restore-or-repair-your-server-running-Windows-Server-Essentials.md).|-Können Dateien und Ordner auf Ihrem Server wiederherstellen.<br /><br /> – Vollständige Systemwiederherstellung des Servers möglich.|  
|Client Computer Backup|Sichert die Clientcomputer im Netzwerk. Die Daten werden auf dem Server mit Windows Server Essentials gesichert.<br /><br /> Weitere Informationen finden Sie unter [Client-Sicherung verwalten](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md) und [Wiederherstellen eines vollständigen Systems aus einer vorhandenen clientcomputersicherung](Restore-a-full-system-from-an-existing-client-computer-backup.md).|-Können Dateien und Ordner von Ihrem Server wiederherstellen.<br /><br /> – Vollständige Systemwiederherstellung des Servers möglich.|  
| Microsoft Azure Backup|Führt eine onlinesicherung von Dateien oder Ordnern auf dem Server. Wenn Sie Azure Backup Sichern von Serverdaten verwenden, werden die Informationen mithilfe Ihrer Passphrase, bevor sie in ein sicheres Datacenter im Internet hochgeladen werden verschlüsselt.<br /><br /> Weitere Informationen finden Sie unter [Manage Online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md).|-Können Dateien und Ordner von Ihrem Server wiederherstellen.<br /><br /> -Mit inkrementellen Sicherungen werden nur Änderungen an Dateien in die Cloud übertragen.<br /><br /> -Sicherungen werden in Microsoft Azure und sind extern gespeichert Reduzieren der Notwendigkeit zum Sichern und Schützen der Sicherungsmedien.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
