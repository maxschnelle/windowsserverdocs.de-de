---
title: Integritätsdienst Aktionen
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 541b5cbbc18d3ea8619f34d9bcc8aeb34fd0066b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473127"
---
# <a name="health-service-actions"></a>Integritätsdienst Aktionen

> Gilt für: Windows Server 2019, Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung und Betriebsbereitschaft für Cluster mit direkte Speicherplätze verbessert.

## <a name="actions"></a>Aktionen

Im nächsten Abschnitt werden Workflows beschrieben, die vom Integritätsdienst automatisiert werden. Um sicherzustellen, dass eine Aktivität tatsächlich autonom erfolgt, oder um ihren Fortschritt oder ihr Ergebnis nachzuverfolgen, generiert der Integritätsdienst „Aktionen“. Im Gegensatz zu Protokollen verschwinden Aktionen, kurz nachdem sie erfolgt sind, und dienen hauptsächlich zum Gewinnen von Einblicken in laufende Aktivitäten, die sich auf die Leistung oder Kapazität auswirken können (z. B. Wiederherstellen der Ausfallsicherheit oder Neuverteilen von Daten).

### <a name="usage"></a>Zweck

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Der Integritätsdienst in Windows Server 2016](health-service-overview.md)
- [Entwicklerdokumentation, Beispielcode und API-Referenz auf MSDN](https://msdn.microsoft.com/windowshealthservice)
