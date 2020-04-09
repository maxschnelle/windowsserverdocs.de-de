---
title: Hinzufügen, Entfernen und Aktualisieren von Funktionen
description: Mit System Insights können Sie neue Funktionen erstellen, die die vorhandene Daten Sammlungs-und-Verwaltungs Funktionalität nutzen. Es ist wichtig, dass Sie auch über die Platt Form Unterstützung verfügen, um das Hinzufügen, entfernen und Aktualisieren dieser Funktionen zu verwalten. In diesem Thema werden die Funktionen auf hoher Ebene zum Hinzufügen, entfernen und Aktualisieren von Funktionen in System Insights beschrieben.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 0a760f25de79bc89b2aa67aec6bb1e3a493c1310
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856263"
---
# <a name="adding-removing-and-updating-capabilities"></a>Hinzufügen, Entfernen und Aktualisieren von Funktionen

>Gilt für: Windows Server 2019

Mit System Insights können Sie neue Funktionen erstellen, die die vorhandene Daten Sammlungs-und-Verwaltungs Funktionalität nutzen. Nachdem diese Funktionen erstellt wurden, ist es ebenso wichtig, dass Sie auch über die Platt Form Unterstützung verfügen, um das Hinzufügen, entfernen und Aktualisieren dieser Funktionen zu verwalten. 

In diesem Thema werden die Funktionen auf hoher Ebene zum Hinzufügen, entfernen und Aktualisieren von Funktionen in System Insights beschrieben. 

## <a name="adding-a-capability"></a>Hinzufügen einer Funktion
Mit System Insights können Sie jederzeit neue Funktionen mithilfe des **Add-insightscapability** -Cmdlets hinzufügen. Die **Add-insightscapability** erfordert, dass Sie einen Funktionsnamen und die Funktionsbibliothek angeben. Die Funktionsbibliothek enthält die Beschreibung, Datenquellen und Vorhersage Logik der Funktion.

```PowerShell
Add-InsightsCapability -Name Sample capability -Library C:\SampleCapability.dll
```

Nachdem Sie System Insights eine Funktion hinzugefügt haben, können Sie die Funktion sofort mithilfe von PowerShell oder Windows Admin Center aufrufen und verwalten. 

## <a name="updating-a-capability"></a>Aktualisieren einer Funktion
System Insights ermöglicht Ihnen außerdem, eine Funktion mithilfe des Cmdlets " **Update-insightscapability** " zu aktualisieren.

```PowerShell
Update-InsightsCapability -Name Sample capability -Library C:\SampleCapabilityv2.dll
```

Durch das Aktualisieren einer Funktion können Sie eine neue Funktionsbibliothek angeben, die es Ihnen ermöglicht, die Funktionsbeschreibung, die Datenquellen und die dieser Funktion zugeordnete Vorhersage Logik zu ändern. Wichtig ist, dass das Aktualisieren einer Funktion alle Konfigurations-und Verlaufs Informationen zu dieser Funktion beibehält, einschließlich benutzerdefinierter Zeitpläne, Aktionen und Verlaufs Vorhersage Ergebnisse. 

## <a name="removing-a-capability"></a>Entfernen einer Funktion
Mithilfe des Cmdlets **Remove-insightscapability** können Sie auch Funktionen in System Insights entfernen. 

```PowerShell
Remove-InsightsCapability -Name Sample capability 
```
>[!NOTE]
>Die standardmäßigen Vorhersagefunktionen können nicht entfernt werden.

Durch das Entfernen einer Funktion werden die Funktionen und alle zugehörigen Informationen, einschließlich des Zeitplans, der Wiederherstellungs Aktionen und der bisherigen Vorhersage Ergebnisse, dauerhaft gelöscht. 

>[!TIP]
>Deaktivieren Sie ggf. eine Funktion, anstatt Sie zu entfernen, wenn Sie sich Sorgen machen, dass alle der Funktion zugeordneten Informationen dauerhaft gelöscht werden. 

## <a name="see-also"></a>Siehe auch
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Übersicht über System Einblicke](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)
- [FAQ zu System Insights](faq.md)