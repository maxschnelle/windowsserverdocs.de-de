---
title: Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828521"
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Windows Server Essentials bietet zuverlässige Möglichkeiten für regelmäßige Sicherungen des Servers und Sicherungen der Computer im Netzwerk. Im Fall eines Datenverlusts können Sie Daten aus einer erfolgreichen Sicherung auf dem Server wiederherstellen, ohne den gesamten Computer wiederherstellen. Bei Bedarf können Sie eine vollständige Systemwiederherstellung auf Server- oder Clientcomputern im Netzwerk ausführen. In der folgende Tabelle werden die verschiedenen Sicherungsoptionen und ihre Vorteile beschrieben.  
  
|Sicherungsfunktion|Beschreibung|Vorteile|  
|--------------------|-----------------|----------------|  
|Serversicherung|Sichert den Server, auf dem Windows Server Essentials ausgeführt wird. Die Daten werden auf einem externen USB-Laufwerk gesichert.<br /><br /> Weitere Informationen finden Sie unter [Manage Server Backup](Manage-Server-Backup-in-Windows-Server-Essentials.md) und [wiederherstellen oder Reparieren des Servers](Restore-or-repair-your-server-running-Windows-Server-Essentials.md).|– Sie können Dateien und Ordner auf Ihrem Server wiederherstellen.<br /><br /> – Sie können die vollständige Systemwiederherstellung des Servers führen.|  
|Clientcomputersicherung|Sichert die Clientcomputer im Netzwerk. Die Daten werden auf dem Server gesichert, der Windows Server Essentials ausführt.<br /><br /> Weitere Informationen finden Sie unter [Client-Sicherung verwalten](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md) und [Wiederherstellen eines vollständigen Systems aus einer vorhandenen clientcomputersicherung](Restore-a-full-system-from-an-existing-client-computer-backup.md).|– Sie können Dateien und Ordner von Ihrem Server wiederherstellen.<br /><br /> – Sie können die vollständige Systemwiederherstellung des Servers führen.|  
| Microsoft Azure Backup|Führt eine Onlinesicherung von Dateien oder Ordnern auf dem Server durch. Wenn Sie Azure Backup zum Sichern der Serverdaten verwenden, wird die Informationen verschlüsselt mithilfe Ihrer Passphrase aus, bevor sie in ein sicheres Datacenter im Internet hochgeladen werden.<br /><br /> Weitere Informationen finden Sie unter [Verwalten der Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md).|– Sie können Dateien und Ordner von Ihrem Server wiederherstellen.<br /><br /> -Bei inkrementellen Sicherungen werden nur Änderungen an Dateien in die Cloud übertragen.<br /><br /> -Sicherungen werden gespeichert, in Microsoft Azure und externen, wodurch der Bedarf zum Sichern und Schützen von internen Sicherungsmedien reduziert.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
