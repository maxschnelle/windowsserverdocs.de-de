---
title: Integritätsdienst Aktionen
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 519f0321f36fb7afc86962950aeab729d7a38adb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361097"
---
# <a name="health-service-actions"></a>Integritätsdienst Aktionen

> Gilt für: Windows Server 2019, Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung und Betriebsbereitschaft für Cluster mit direkte Speicherplätze verbessert.

## <a name="actions"></a>Aktionen  

Im nächsten Abschnitt werden Workflows beschrieben, die vom Integritätsdienst automatisiert werden. Um sicherzustellen, dass eine Aktivität tatsächlich autonom erfolgt, oder um ihren Fortschritt oder ihr Ergebnis nachzuverfolgen, generiert der Integritätsdienst „Aktionen“. Im Gegensatz zu Protokollen verschwinden Aktionen, kurz nachdem sie erfolgt sind, und dienen hauptsächlich zum Gewinnen von Einblicken in laufende Aktivitäten, die sich auf die Leistung oder Kapazität auswirken können (z. B. Wiederherstellen der Ausfallsicherheit oder Neuverteilen von Daten).  

### <a name="usage"></a>Verwendung  

Mit einem neuen PowerShell-Cmdlet werden alle Aktionen angezeigt:  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>Abdeckung  

In Windows Server 2016 kann das Cmdlet **Get-storagehealthaction** die folgenden Informationen zurückgeben:  

-   Außerbetriebnahme misslungen, Verbindung verloren oder nicht reagierender physischer Datenträger  

-   Wechsel des Speicherpools, um physischen Austauschdatenträger zu verwenden  

-   Wiederherstellen der vollständigen Ausfallsicherheit für Daten  

-   Neuverteilen von Speicherpools  

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in Windows Server 2016](health-service-overview.md)
- [Entwicklerdokumentation, Beispielcode und API-Referenz auf MSDN](https://msdn.microsoft.com/windowshealthservice)
