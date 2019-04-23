---
title: Integrität von Dienstaktionen
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843021"
---
# <a name="health-service-actions"></a>Integrität von Dienstaktionen

> Gilt für Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, die die tägliche Überwachung verbessert und Erfahrungen für Cluster "direkte Speicherplätze".

## <a name="actions"></a>Aktionen  

Im nächsten Abschnitt werden Workflows beschrieben, die vom Integritätsdienst automatisiert werden. Um sicherzustellen, dass eine Aktivität tatsächlich autonom erfolgt, oder um ihren Fortschritt oder ihr Ergebnis nachzuverfolgen, generiert der Integritätsdienst „Aktionen“. Im Gegensatz zu Protokollen verschwinden Aktionen, kurz nachdem sie erfolgt sind, und dienen hauptsächlich zum Gewinnen von Einblicken in laufende Aktivitäten, die sich auf die Leistung oder Kapazität auswirken können (z. B. Wiederherstellen der Ausfallsicherheit oder Neuverteilen von Daten).  

### <a name="usage"></a>Verwendung  

Mit einem neuen PowerShell-Cmdlet werden alle Aktionen angezeigt:  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>Abdeckung  

In Windows Server 2016 die **Get-StorageHealthAction** Cmdlet kann die folgenden Informationen zurück:  

-   Außerbetriebnahme misslungen, Verbindung verloren oder nicht reagierender physischer Datenträger  

-   Wechsel des Speicherpools, um physischen Austauschdatenträger zu verwenden  

-   Wiederherstellen der vollständigen Ausfallsicherheit für Daten  

-   Neuverteilen von Speicherpools  

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
- [Dokumentation für Entwickler, Beispielcode und API-Referenz auf MSDN](https://msdn.microsoft.com/windowshealthservice)
