---
title: Hinzufügen und Entwickeln von Funktionen
description: System Insights ermöglicht Ihnen das Hinzufügen neuer Vorhersagefunktionen zu System Insights, ohne dass Betriebssystemupdates erforderlich sind. Dadurch können Entwickler, einschließlich Microsoft und Drittanbietern, neue Funktionen in der Mitte der Veröffentlichung erstellen und bereitstellen, um die Szenarios zu berücksichtigen, die Sie interessieren. Neue Funktionen können benutzerdefinierte Daten angeben, die erfasst und analysiert werden sollen, und Sie können auch in die vorhandenen System Insights-Verwaltungsebenen integriert werden.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 0dd4e24197d5a8c438d70a849e435ce28792dfce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858433"
---
# <a name="adding-and-developing-new-capabilities"></a>Hinzufügen und Entwickeln neuer Funktionen

>Gilt für: Windows Server 2019

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
- Weitere Informationen zu den Klassen und Schnittstellen von System Insights [finden Sie](https://aka.ms/systeminsights-api) in der API-Dokumentation. 
- [Verwenden](https://aka.ms/systeminsights-samplecapability) Sie die System Insights-Beispiel Funktion, um Ihnen den Einstieg zu erleichtern. Dadurch wird gezeigt, wie Sie eine Funktion registrieren, die zu sammelnden Datenquellen angeben und mit der Analyse der Systemdaten beginnen.

>[!NOTE]
>Dies ist eine vorab Funktionalität. Es kann geändert werden, da wir neue Funktionen hinzufügen und Feedback integrieren.

## <a name="see-also"></a>Siehe auch
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Übersicht über System Einblicke](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen, Entfernen und Aktualisieren von Funktionen](add-remove-update-capabilities.md)
- [FAQ zu System Insights](faq.md)