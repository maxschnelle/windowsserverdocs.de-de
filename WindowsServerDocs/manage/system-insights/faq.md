---
title: System Insights – häufig gestellte Fragen
description: System Insights – häufig gestellte Fragen
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
ms.date: 5/23/2018
ms.openlocfilehash: 13767e1336d1ff729d1fbbe6cae3ed57d68cefc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851061"
---
# <a name="system-insights-faq"></a>System Insights – häufig gestellte Fragen

>Gilt für: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Wie können Sie System Insights mit Azure Monitor oder System Center Operations Manager verwenden?

[Azure Monitor](https://azure.microsoft.com/services/monitor/) und [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) bieten Informationen zu Vorgängen innerhalb Ihrer Bereitstellungen helfen Ihnen beim Verwalten Ihrer Infrastruktur. System Insights im Gegensatz dazu ist eine Windows Server-Funktion, die lokalen predictive Analytics-Funktionen eingeführt werden. Zusammen können System Insights und Azure Monitor oder SCOM die Vorhersagen für eine Auffüllung von Geräten Oberfläche:

 Azure Monitor oder SCOM kann aus der Ereignisse, die vom System Insights erstellt gedrückt, während System Insights das Ergebnis der einzelnen Vorhersagen in das Ereignisprotokoll ausgegeben. Sie können diese computerspezifischen Vorhersagen für eine ganze Reihe von Windows-Servern und ermöglicht Ihnen, einen einheitlichen Überblick über diese Vorhersagen für eine Gruppe von Server-Instanzen in Erscheinung treten. 
 
 Finden Sie unter den Kanal und Ereignis-IDs, für jede Vorhersage [hier](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results).

## <a name="how-does-system-insights-relate-to-windows-ml"></a>In welcher Beziehung steht System Insights auf Windows-ML?

[Windows-ML](https://docs.microsoft.com/windows/uwp/machine-learning/) ist eine Plattform, mit der Entwickler zum Importieren und vorab trainierten Machine Learning-Modelle auf Windows-Geräten zu bewerten. Diese Modelle profitieren, die Hardwarebeschleunigung, und sie lokal bewertet werden können. 

System Insights ist ein Feature in Windows Server-2019, die lokale Vorhersagefunktionen sowie eine umfassende Verwaltungsoberfläche, einschließlich der Integration von PowerShell und Windows Admin Center bietet. 

## <a name="can-i-use-system-insights-for-my-cluster"></a>Kann ich für meinen Cluster System Insights verwenden? 

Ja. System-Einblicke können unabhängig voneinander auf jedem einzelnen Failoverclusterknoten und das Standardverhalten des System-Insights-Vorhersagen-Nutzung über den lokalen Speicher, Datenträger, CPU und Netzwerk ausgeführt. **Sie können auch aktivieren, für den Clusterspeicher Prognose**, sodass die Funktionen des forecasting-Nutzung für die gruppierten Volumes und Storage Vorhersagen. 

Sie können diese Einstellungen in Windows Admin Center oder PowerShell verwalten, und ausführlichere Informationen zu dieser Funktionalität ist verfügbar [hier](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/).
 

## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>Wie aufwändig ist die Standardfunktionen ausgeführt?

Jede Standardfunktion ist kostengünstig ausführen. Jede Funktion dauert länger, auszuführen, wie Sie mehr Daten erfassen, aber sie in der Regel sollte in einer nur wenige Sekunden abgeschlossen. 

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
