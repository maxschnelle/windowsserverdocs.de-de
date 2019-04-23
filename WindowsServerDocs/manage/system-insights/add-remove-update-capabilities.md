---
title: Hinzufügen, Entfernen und Aktualisieren von Funktionen
description: System-Insights können Sie neue Funktionen zu erstellen, die vorhandenen Datensammlung und Verwaltungsfunktionen zu nutzen. Es ist wichtig, dass auch die Plattform unterstützt das Hinzufügen, entfernen, und Updates für diese Funktionen zu verwalten. Dieses Thema beschreibt die allgemeine Funktionalität zum Hinzufügen, entfernen und Aktualisieren von Funktionen in System Insights.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 07fb036d1c4aa4a63107594ec1f81cb5be1c7724
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880161"
---
# <a name="adding-removing-and-updating-capabilities"></a>Hinzufügen, Entfernen und Aktualisieren von Funktionen

>Gilt für: Windows Server 2019

System-Insights können Sie neue Funktionen zu erstellen, die vorhandenen Datensammlung und Verwaltungsfunktionen zu nutzen. Nachdem dieser Funktionen erstellt wurden, ist es jedoch ebenso wichtig, dass auch die Plattform unterstützt das Hinzufügen, entfernen, und Updates für diese Funktionen zu verwalten. 

Dieses Thema beschreibt die allgemeine Funktionalität zum Hinzufügen, entfernen und Aktualisieren von Funktionen in System Insights. 

## <a name="adding-a-capability"></a>Eine Funktion hinzufügen
System Insights können Sie zum Hinzufügen neuer Funktionen, die jederzeit mithilfe der **hinzufügen-InsightsCapability** Cmdlet. Die **hinzufügen-InsightsCapability** müssen Sie einen Namen für die Funktion und die Funktion-Bibliothek angeben. Die Funktion-Bibliothek enthält die Beschreibung der Funktion, Datenquellen und Vorhersage Logik.

```PowerShell
Add-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapability.dll"
```

Nachdem eine Funktion zum System Insights hinzugefügt wurde, können Sie direkt aufrufen und die Möglichkeit, die mithilfe von PowerShell oder Windows Admin Center verwalten. 

## <a name="updating-a-capability"></a>Eine Funktion wird aktualisiert.
System Insights können Sie eine mithilfe der Funktion aktualisiert auch die **Update-InsightsCapability** Cmdlet.

```PowerShell
Update-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapabilityv2.dll"
```

Eine Funktion wird aktualisiert, können Sie eine neue Bibliothek für die Funktion angeben, die Ihnen ermöglicht, die Beschreibung der Funktion, die Datenquellen und die Vorhersage Logik für diese Funktion zu ändern. Aktualisieren eine Funktion behält wichtig ist, dass alle Konfigurations- und Verlaufsinformationen zu dieser Funktion, einschließlich benutzerdefinierte Zeitpläne, Aktionen und historische Vorhersageergebnisse. 

## <a name="removing-a-capability"></a>Entfernen eine Funktion
Sie können auch Funktionen entfernen, im System Insights verwenden die **Remove-InsightsCapability** Cmdlet. 

```PowerShell
Remove-InsightsCapability -Name "Sample capability" 
```
>[!NOTE]
>Der Standardwert Prognosefunktionen kann nicht entfernt werden.

Eine Funktion dauerhaft zu entfernen, löscht der Funktion und alle zugehörigen Informationen, einschließlich des Zeitplans, alle Aktionen zur Problembehebung und letzten Vorhersageergebnisse. 

>[!TIP]
>Erwägen Sie eine Funktion zu deaktivieren, anstatt ihn zu entfernen, wenn Sie über alle Informationen im Zusammenhang mit der Funktion dauerhaft zu löschen. 

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)