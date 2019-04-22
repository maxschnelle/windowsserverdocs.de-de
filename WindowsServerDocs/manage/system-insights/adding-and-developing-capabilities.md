---
title: Hinzufügen und Entwickeln von Funktionen
description: System Insights können Sie System-Einblicke, ohne dass alle Betriebssystemupdates neue Vorhersagefunktionen hinzufügen. Dadurch können Entwickler, einschließlich von Microsoft und Drittanbietern, zum Erstellen und Bereitstellen von neuen Funktionen Mid-Version um die Szenarien, die Sie interessieren. Neue Funktionen können die benutzerdefinierte Daten zu sammeln und analysieren Sie angeben, und sie auch mit den vorhandenen Ebenen von Insights von System Management integrieren.
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
ms.openlocfilehash: 8caddead774ac69a38906f3c0a0d2eaf005c1d28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817481"
---
# <a name="adding-and-developing-new-capabilities"></a>Hinzufügen und neue Funktionen entwickeln

>Gilt für: Windows Server 2019

System Insights können Sie System-Einblicke, ohne dass alle Betriebssystemupdates neue Vorhersagefunktionen hinzufügen. Dadurch können Entwickler, einschließlich von Microsoft und Drittanbietern, zum Erstellen und Bereitstellen von neuen Funktionen Mid-Version um die Szenarien, die Sie interessieren. 

Eine neue Funktion kann integriert und erweitert die vorhandene Infrastruktur von System Insights:

- Neue Funktionen können **Geben Sie Leistung des Indikators oder der System-Ereignis**, der erfasst, lokal gespeichert, und für die Funktion für die Analyse zurückgegeben wird, wenn die Funktion aufgerufen wird.  
- Neue Funktionen können **nutzen Sie die vorhandene Windows Admin Center und PowerShell Management-Ebenen**. Nicht nur werden neue Funktionen in System Insights ermittelt werden, profitieren sie auch benutzerdefinierte Zeitpläne und Aktionen zur Problembehebung. 

## <a name="manage-new-capabilities"></a>Verwalten von neuen Funktionen
- [Erfahren Sie,](add-remove-update-capabilities.md) wie hinzufügen, entfernen und Aktualisieren von Funktionen, die mithilfe von PowerShell. 

## <a name="develop-a-capability"></a>Entwickeln Sie eine Funktion
Verwenden Sie die folgenden Ressourcen können Sie beginnen das Schreiben von eigenen benutzerdefinierten Funktionen:
- [Erfahren Sie,](data-sources.md) zu den Datenquellen, die Sie sammeln können.
- [Herunterladen](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/) das System-Insights-NuGet-Paket enthält die Klassen und Schnittstellen, die Sie eine Funktion schreiben müssen.
- [Besuchen Sie](https://aka.ms/systeminsights-api) der API-Dokumentation erfahren Sie die System-Insights-Klassen und Schnittstellen. 
- [Verwendung](https://aka.ms/systeminsights-samplecapability) beginnen Sie die System-Insights-Beispiel-Funktion, die Ihnen helfen. Dadurch erfahren Sie, wie eine Funktion zu registrieren, geben Sie die Datenquellen zum Sammeln und Systemdaten mit der Analyse beginnen.

>[!NOTE]
>Dies ist eine Vorabversion-Funktion. Es unterliegt, wie wir die neue Funktionalität hinzufügen und integrieren Feedback.

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen, entfernen und Aktualisieren von Funktionen](add-remove-update-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)