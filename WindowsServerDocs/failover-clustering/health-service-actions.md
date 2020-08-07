---
title: Integritätsdienst Aktionen
manager: eldenc
ms.author: cosdar
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 16e8a27dc38b8908ffb7ccac94f3bcc15a5c956f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945793"
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

## <a name="additional-references"></a>Weitere Verweise

- [Der Integritätsdienst in Windows Server 2016](health-service-overview.md)
- [Entwicklerdokumentation, Beispielcode und API-Referenz auf MSDN](https://msdn.microsoft.com/windowshealthservice)
