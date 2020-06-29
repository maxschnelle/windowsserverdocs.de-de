---
title: Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 41000915-f6ff-4dbb-b7be-629ef36386d4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1741d514728452a8fd9d1963811d4508ec158d78
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470815"
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows Server Essentials bietet zuverlässige Möglichkeiten für regelmäßige Sicherungen des Servers und Sicherungen der Computer im Netzwerk. Im Fall eines Datenverlusts können Sie Daten aus einer erfolgreichen Sicherung auf dem Server wiederherstellen, ohne den gesamten Computer wiederherstellen. Bei Bedarf können Sie eine vollständige Systemwiederherstellung auf Server- oder Clientcomputern im Netzwerk ausführen. In der folgende Tabelle werden die verschiedenen Sicherungsoptionen und ihre Vorteile beschrieben.

|Sicherungsfunktion|BESCHREIBUNG|Vorteile|
|--------------------|-----------------|----------------|
|Serversicherung|Sichert den Server, auf dem Windows Server Essentials ausgeführt wird. Die Daten werden auf einem externen USB-Laufwerk gesichert.<br /><br /> Weitere Informationen finden Sie unter [Verwalten der Server Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md) und- [Wiederherstellung oder Reparieren des Servers](Restore-or-repair-your-server-running-Windows-Server-Essentials.md).|-Können Dateien und Ordner auf dem Server wiederherstellen.<br /><br /> -Kann die vollständige Systemwiederherstellung des Servers ausführen.|
|Clientcomputersicherung|Sichert die Clientcomputer im Netzwerk. Die Daten werden auf dem Server gesichert, der Windows Server Essentials ausführt.<br /><br /> Weitere Informationen finden Sie unter [Verwalten der Client Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md) und [Wiederherstellen eines vollständigen Systems aus einer vorhandenen Client Computer Sicherung](Restore-a-full-system-from-an-existing-client-computer-backup.md).|-Können Dateien und Ordner auf dem Server wiederherstellen.<br /><br /> -Kann die vollständige Systemwiederherstellung des Client Computers ausführen.|
| Microsoft Azure Backup|Führt eine Onlinesicherung von Dateien oder Ordnern auf dem Server durch. Wenn Sie Azure Backup zum Sichern von Serverdaten verwenden, werden die Informationen mithilfe Ihrer Passphrase verschlüsselt, bevor Sie in ein sicheres Daten Center im Internet hochgeladen werden.<br /><br /> Weitere Informationen finden Sie unter [Verwalten der Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md).|-Können Dateien und Ordner auf dem Server wiederherstellen.<br /><br /> -Bei inkrementellen Sicherungen werden nur Änderungen an Dateien in die Cloud übertragen.<br /><br /> -Sicherungen werden in Microsoft Azure gespeichert und sind Offsite, wodurch die Notwendigkeit zum Sichern und schützen von lokalen Sicherungsmedien verringert wird.|

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
