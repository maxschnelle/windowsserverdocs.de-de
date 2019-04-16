---
title: Health Service-Aktionen
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-actions"></a>Health Service-Aktionen

> Gilt für WindowsServer 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung verbessert und betriebliche Erfahrung für Cluster mit "direkte Speicherplätze".

## <a name="actions"></a>Aktionen  

Im nächste Abschnitt wird beschrieben, Workflows, die vom Integritätsdienst automatisiert werden. Stellen Sie sicher, dass eine Aktivität tatsächlich autonom erfolgt, oder den Fortschritt oder Ihr Ergebnis nachzuverfolgen, generiert der Integritätsdienst "Aktionen". Im Gegensatz zu Protokollen verschwinden Aktionen, kurz nachdem abgeschlossen ist, und dienen in erster Linie zur Einblicken in laufende Aktivitäten bereitstellen, die Leistung oder Kapazität (z. B. Wiederherstellen der ausfallsicherheit oder Neuverteilen von Daten) auswirken können.  

### <a name="usage"></a>Verwendung  

Eine neue PowerShell-Cmdlet werden alle Aktionen angezeigt:  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>Abdeckung  

In Windows Server 2016 die **Get-StorageHealthAction** Cmdlet kann die folgenden Informationen zurück:  

-   Zurückziehen von misslungen, Verbindung verloren oder nicht reagierender physischer Datenträger  

-   Wechsel des Speicherpools, um physischen austauschdatenträger zu verwenden  

-   Wiederherstellen der vollständigen ausfallsicherheit für Daten  

-   Neuverteilen von Speicherpools  

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
- [Entwicklerdokumentation, Beispielcode und API-Referenz auf MSDN](https://msdn.microsoft.com/windowshealthservice)
