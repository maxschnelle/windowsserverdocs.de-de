---
title: Hinzufügen und Entwickeln von Funktionen
description: System Insights ermöglicht Ihnen das Hinzufügen neuer Vorhersagefunktionen zu System Insights, ohne dass Betriebssystemupdates erforderlich sind. Dadurch können Entwickler, einschließlich Microsoft und Drittanbietern, neue Funktionen in der Mitte der Veröffentlichung erstellen und bereitstellen, um die Szenarios zu berücksichtigen, die Sie interessieren. Neue Funktionen können benutzerdefinierte Daten angeben, die erfasst und analysiert werden sollen, und Sie können auch in die vorhandenen System Insights-Verwaltungsebenen integriert werden.
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: d85016fd3f338ab87d6516815ee04c652875bdf5
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766763"
---
# <a name="adding-and-developing-new-capabilities"></a>Hinzufügen und Entwickeln neuer Funktionen

>Gilt für: Windows Server 2019

System Insights ermöglicht Ihnen das Hinzufügen neuer Vorhersagefunktionen zu System Insights, ohne dass Betriebssystemupdates erforderlich sind. Dadurch können Entwickler, einschließlich Microsoft und Drittanbietern, neue Funktionen in der Mitte der Veröffentlichung erstellen und bereitstellen, um die Szenarios zu berücksichtigen, die Sie interessieren.

Jede neue Funktion kann in die vorhandene System Insights-Infrastruktur integriert und erweitert werden:

- Neue Funktionen können **jeden Leistungs-oder System Ereignis Wert angeben**, der gesammelt, lokal gespeichert und an die Analysefunktion zurückgegeben wird, wenn die Funktion aufgerufen wird.
- Neue Funktionen können **das vorhandene Windows Admin Center und die PowerShell-Verwaltungsebenen nutzen**. In System Insights können nicht nur neue Funktionen erkannt werden, sondern Sie profitieren auch von benutzerdefinierten Zeitplänen und Wiederherstellungs Aktionen.

## <a name="manage-new-capabilities"></a>Verwalten neuer Funktionen
- [Erfahren Sie](add-remove-update-capabilities.md) , wie Sie Funktionen mithilfe von PowerShell hinzufügen, entfernen und aktualisieren.

## <a name="develop-a-capability"></a>Entwickeln einer Funktion
Verwenden Sie die folgenden Ressourcen, um Ihnen den Einstieg in die Erstellung eigener benutzerdefinierter Funktionen zu erleichtern:
- [Erfahren Sie mehr](data-sources.md) über die Datenquellen, die Sie erfassen können.
- [Laden](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/) Sie das System Insights-nuget-Paket herunter, das die Klassen und Schnittstellen enthält, die Sie zum Schreiben einer Funktion benötigen.
- Weitere Informationen zu den Klassen und Schnittstellen von System Insights [finden Sie](/dotnet/api/microsoft.systeminsights.capability) in der API-Dokumentation.
- [Verwenden](https://aka.ms/systeminsights-samplecapability) Sie die System Insights-Beispiel Funktion, um Ihnen den Einstieg zu erleichtern. Dadurch wird gezeigt, wie Sie eine Funktion registrieren, die zu sammelnden Datenquellen angeben und mit der Analyse der Systemdaten beginnen.

>[!NOTE]
>Dies ist eine vorab Funktionalität. Es kann geändert werden, da wir neue Funktionen hinzufügen und Feedback integrieren.

## <a name="additional-references"></a>Weitere Verweise
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Systemdaten: Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen, Entfernen und Aktualisieren von Funktionen](add-remove-update-capabilities.md)
- [FAQ zu System Insights](faq.md)