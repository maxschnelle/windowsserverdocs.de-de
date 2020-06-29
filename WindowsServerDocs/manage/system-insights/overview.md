---
title: 'Systemdaten: Übersicht'
description: System Insights ist ein neues Predictive Analytics Feature in Windows Server 2019. Die Vorhersagefunktionen von System Insights, die jeweils durch ein Machine Learning-Modell unterstützt werden, analysieren lokal Windows Server-System Daten (z. b. Leistungsindikatoren und Ereignisse), um Einblicke in die Funktionsweise Ihrer Server zu erhalten und die Betriebskosten zu reduzieren, die mit der reaktiven Verwaltung von Problemen in ihren bereit Stellungen einhergehen.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: b1f0fc5343c5228a02369a64bff2de50ab3f863e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471765"
---
# <a name="system-insights-overview"></a>Systemdaten: Übersicht

>Gilt für: Windows Server 2019

System Insights ist ein neues Predictive Analytics Feature in Windows Server 2019. Die Vorhersagefunktionen von System Insights, die jeweils durch ein Machine Learning-Modell unterstützt werden, analysieren lokal Windows Server-System Daten (z. b. Leistungsindikatoren und Ereignisse), um Einblicke in die Funktionsweise Ihrer Server zu erhalten und die Betriebskosten zu reduzieren, die mit der reaktiven Verwaltung von Problemen in ihren bereit Stellungen einhergehen.

In Windows Server 2019 wird System Insights mit vier Standardfunktionen ausgeliefert, die sich auf die Kapazitäts Vorhersage konzentrieren, und zukünftige Ressourcen für Compute-, Netzwerk-und Speicherressourcen basierend auf Ihren vorherigen Verwendungs Mustern Vorhersagen. System Insights ist auch mit einer [erweiterbaren Infrastruktur](adding-and-developing-capabilities.md)ausgeliefert, sodass von Microsoft und Drittanbietern neue Vorhersagefunktionen zu System Insights hinzugefügt werden können, ohne das Betriebs System zu aktualisieren.

Sie können System Einblicke über eine intuitive [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) -Erweiterung oder [direkt über PowerShell](https://aka.ms/SystemInsightsPowerShell)verwalten. mit System Insights können Sie jede Vorhersagefunktion separat entsprechend den Anforderungen Ihrer Bereitstellung konfigurieren. Alle Vorhersage Ergebnisse werden im Ereignisprotokoll veröffentlicht, sodass Sie [Azure Monitor](https://azure.microsoft.com/services/monitor/) oder [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) verwenden können, um auf einfache Weise Vorhersagen für eine Gruppe von Computern zu aggregieren und anzuzeigen.

![System Insights-Erweiterung im Windows Admin Center und zeigt die Prognose der CPU-Kapazität mit einem Diagramm, das die Vorhersage gezeichnet.](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>Lokale Funktionalität
System Insights wird vollständig lokal unter Windows Server ausgeführt. Mithilfe der neuen Funktionen, die in Windows Server 2019 eingeführt wurden, werden alle Ihre Daten direkt auf Ihrem Computer gesammelt, gespeichert und analysiert, sodass Sie Predictive Analytics Funktionen ohne cloudkonnektivität umsetzen können.

Die Systemdaten werden auf dem Computer gespeichert, und diese Daten werden anhand von Vorhersagefunktionen analysiert, die in der Cloud nicht umgeschult werden müssen. Mit System Insights können Sie Ihre Daten auf Ihrem Computer speichern und weiterhin von Predictive Analytics Funktionen profitieren.

## <a name="get-started"></a>Erste Schritte

<iframe src=https://www.youtube-nocookie.com/embed/AJxQkx5WSaA width=560 height=315 allowfullscreen></iframe>

>[!TIP]
>Sehen Sie sich diese kurzen Videos an, um die Informationen zu erhalten, die Sie für die ersten Schritte und die zuverlässige Verwaltung von System Insights benötigen: [Getting Started with System Insights in 10](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>Anforderungen
System Insights ist auf jeder Windows Server 2019-Instanz verfügbar. Es wird auf Host-und Gast Computern, auf jedem Hypervisor und in jeder Cloud ausgeführt.

### <a name="install-system-insights"></a>Installieren von System Insights
>[!IMPORTANT]
>System Insights sammelt und speichert die Daten in einem Jahr vor einem Jahr. Wenn Sie Ihre Daten beim Upgrade Ihres Betriebssystems beibehalten möchten, **Stellen Sie sicher, dass Sie ein direktes Upgrade verwenden**.

#### <a name="install-the-feature"></a>Installieren des Features
Sie können System Insights mit der Erweiterung im Windows Admin Center installieren:

![Day 0-Vorgang für die System Insights-Erweiterung.](media/day-0-2.png)

Sie können System Insights auch direkt über Server-Manager installieren, indem Sie das **System-Insights** -Feature hinzufügen oder PowerShell verwenden:

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>Feedback geben
Wir freuen uns über Ihr Feedback, um uns bei der Verbesserung dieses Features zu unterstützen. Sie können die folgenden Kanäle verwenden, um Feedback zu senden:
- **Feedback-Hub**: Verwenden Sie das Feedback-Hub-Tool in Windows 10, um einen Fehler oder ein Feedback zu melden. Geben Sie dabei Folgendes an:
    - **Kategorie**: Server
    - **SubCategory**: System Insights
- **UserVoice**: übermitteln Sie Featureanforderungen über unsere [UserVoice-Seite](https://windowsserver.uservoice.com/forums/295071-management-tools). Teilen Sie den Kollegen mit, dass Sie die für Sie wichtigen Elemente upstimmen.
- **E-Mail**: Wenn Sie Ihr Feedback privat an das Featureteam senden möchten, senden Sie eine e-Mail an system-insights-feed@microsoft.com . Beachten Sie, dass wir Sie möglicherweise bitten, Feedback-Hub oder UserVoice zu verwenden.

## <a name="additional-references"></a>Zusätzliche Referenzen
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)
- [FAQ zu System Insights](faq.md)