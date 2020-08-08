---
title: FAQ zu System Insights
description: FAQ zu System Insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 2a97fdbc2e2a80c310cac2b770e18f34d53dd983
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997149"
---
# <a name="system-insights-faq"></a>FAQ zu System Insights

>Gilt für: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Wie können Sie System Einblicke mit Azure Monitor oder System Center Operations Manager verwenden?

In [Azure Monitor](https://azure.microsoft.com/services/monitor/) und [System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807) werden Betriebsinformationen für Ihre bereit Stellungen bereitgestellt, um Ihnen die Verwaltung Ihrer Infrastruktur zu erleichtern. System Insights ist dagegen eine Windows Server-Funktion, die lokale Predictive Analytics Funktionen einführt. Mithilfe von System Insights und Azure Monitor oder SCOM können Sie die Vorhersagen über eine Population von Geräten hinweg ermitteln:

 Azure Monitor oder SCOM können die von System Insights erstellten Ereignisse als Schlüssel ausgeben, da System Einblicke das Ergebnis jeder Vorhersage an das Ereignisprotokoll übergibt. Diese computerspezifischen Vorhersagen können über eine Flotte von Windows-Servern hinweg angezeigt werden, sodass Sie über eine einheitliche Ansicht dieser Vorhersagen für eine Gruppe von Server Instanzen verfügen.

 Sehen Sie sich die Kanal-und Ereignis-IDs für [jede Vorhersage](./managing-capabilities.md#retrieving-capability-results)an.

## <a name="how-does-system-insights-relate-to-windows-ml"></a>Wie verhält sich System Insights mit Windows ml?

[Windows ml](/windows/uwp/machine-learning/) ist eine Plattform, die es Entwicklern ermöglicht, vorab trainierte Machine Learning-Modelle auf Windows-Geräten zu importieren und zu bewerten. Diese Modelle profitieren von der Hardwarebeschleunigung und können lokal bewertet werden.

System Insights ist ein Feature in Windows Server 2019, das lokale Vorhersagefunktionen sowie eine komplette Verwaltungs Umgebung bietet, einschließlich der PowerShell-und Windows Admin Center-Integration.

## <a name="can-i-use-system-insights-for-my-cluster"></a>Kann ich für meinen Cluster System Einblicke verwenden?

Ja. System Insights kann unabhängig voneinander auf jedem einzelnen Failoverclusterknoten ausgeführt werden, und das Standardverhalten von System Insights prognostiziert die Verwendung von lokalem Speicher, Volume, CPU und Netzwerk. **Sie können auch die Vorhersage für Cluster Speicher aktivieren**, sodass die Speicher Prognose Funktionen die Nutzung für gruppierte Volumes und Speicher Vorhersagen.

Sie können diese Einstellungen im Windows Admin Center oder PowerShell verwalten. ausführlichere Informationen zu dieser Funktionalität finden Sie [hier](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/).


## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>Wie teuer ist das Ausführen der Standardfunktionen?

Jede Standardfunktion ist für die Durchführung von kostengünstiger. Die Ausführung der Funktionen dauert länger, wenn Sie mehr Daten sammeln, aber Sie sollten in der Regel in wenigen Sekunden fertiggestellt werden.

## <a name="additional-references"></a>Weitere Verweise
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Systemdaten: Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)