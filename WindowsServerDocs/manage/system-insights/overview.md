---
title: System-Insights-Übersicht
description: System Insights ist ein neues predictive Analytics-Feature in Windows Server-2019. Die System Insights Vorhersagefunktionen - jeweils von einem Machine Learning-Modell - gesicherten lokal Windows Server Systemdaten analysieren, wie Leistungsindikatoren und Ereignisse, die Einblicke in die Funktionsweise von Ihren Servern und unterstützen Sie reduzieren die Betriebsausgaben reaktiv Verwaltung Probleme in Ihren Bereitstellungen zugeordnet.
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
ms.openlocfilehash: ca471e5e747c7aaa369f5725290e16deab7a6660
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887241"
---
# <a name="system-insights-overview"></a>System-Insights-Übersicht

>Gilt für: Windows Server 2019

System Insights ist ein neues predictive Analytics-Feature in Windows Server-2019. Die System Insights Vorhersagefunktionen - jeweils von einem Machine Learning-Modell - gesicherten lokal Windows Server Systemdaten analysieren, wie Leistungsindikatoren und Ereignisse, die Einblicke in die Funktionsweise von Ihren Servern und unterstützen Sie reduzieren die Betriebsausgaben reaktiv Verwaltung Probleme in Ihren Bereitstellungen zugeordnet. 

In Windows Server-2019 Lieferumfang vier Standardfunktionen konzentriert sich auf Kapazität, Prognosen, Vorhersagen der zukünftigen Ressourcenverwendung für COMPUTE-, Netzwerk- und Speicherressourcen basierend auf Ihren vorherigen Verwendungsmustern System Insights. Außerdem Lieferumfang System Insights eine [erweiterbare Infrastruktur](adding-and-developing-capabilities.md), sodass Microsoft und 3. neue Vorhersagefunktionen System Insights hinzufügen können ohne Aktualisierung des Betriebssystems. 

Sie können System Insights verwalten, über eine intuitive [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) Erweiterung oder [direkt über PowerShell](https://aka.ms/SystemInsightsPowerShell), System Insights können Sie jede Vorhersagefunktion konfigurieren separat entsprechend den Anforderungen Ihrer Bereitstellung. Alle Vorhersageergebnisse werden in das Ereignisprotokoll, die Sie verwenden können veröffentlicht [Azure Monitor](https://azure.microsoft.com/services/monitor/) oder [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) auf einfache Weise zu aggregieren und Vorhersagen für eine Gruppe von Computern angezeigt.

![System-Insights-Erweiterung in Windows Admin Center, CPU-Kapazität, die Funktion mit einem Diagramm zeichnen die Vorhersage Vorhersagen anzeigen](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>Lokale Funktionen
System Insights wird vollständig lokal unter Windows Server ausgeführt. Verwenden neue Funktionen, eingeführt in Windows Server-2019, all Ihre Daten erfasst, beibehalten, und analysiert, die direkt auf Ihrem Computer ermöglichen Ihnen, predictive Analytics-Funktionen, ohne alle Cloud-Konnektivität zu erzielen.

Die Systemdaten auf Ihrem Computer gespeichert und analysiert diese Daten von Vorhersagefunktionen, die keine erfordern das erneute trainieren, in der Cloud. Mit System Einblicke können Sie Ihre Daten auf dem Computer beibehalten und dennoch von predictive Analytics-Funktionen profitieren. 

## <a name="get-started"></a>Beginnen

<iframe src="https://www.youtube-nocookie.com/embed/AJxQkx5WSaA" width="560" height="315" allowfullscreen></iframe>

>[!TIP]
>Sehen Sie sich in diesen kurzen Videos finden Sie die Informationen, die Sie benötigen, zu beginnen und zuverlässig verwalten System Insights: [Erste Schritte mit System Einblicke in 10 Minuten](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>Anforderungen
System Insights ist in einer Instanz von Windows Server-2019 verfügbar. Es wird auf Host- und Gastbetriebssysteme Computern, auf jedem Hypervisor, und klicken Sie in einer Cloud ausgeführt.

### <a name="install-system-insights"></a>Installieren Sie das System Insights
>[!IMPORTANT]
>System Insights sammelt und speichert bis zu den Zeitraum eines Jahres, der auf einem lokalen Computer. Wenn Sie Ihre Daten beibehalten werden soll, wenn das Betriebssystem aktualisieren möchten **stellen sicher, dass Sie ein direktes Upgrade**.

#### <a name="install-the-feature"></a>Installieren Sie das feature
Sie können System-Einblicke, die mit der Erweiterung in Windows Admin Center installieren:

![Day-0-Erfahrung für System-Insights-Erweiterung.](media/day-0-2.png)

Sie können auch System Insights direkt über den Server-Manager installieren, durch das Hinzufügen der **System Insights** Feature oder mithilfe von PowerShell:

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>Feedback bereitstellen
Wir würden gerne erfahren Sie, Ihr Feedback, um dieses Feature zu verbessern. Sie können die folgenden Kanäle verwenden, um Feedback zu senden:
- **Feedback Hub**: Verwenden Sie das Feedback Hub-Tool unter Windows 10, in der Datei ein Fehler oder ein Feedback. Dabei geben:
    - **Kategorie**: Server 
    - **Unterkategorie**: Systemdaten
- **UserVoice**: Übermitteln Sie featureanforderungen durch unsere [UserVoice-Seite](https://windowsserver.uservoice.com/forums/295071-management-tools). Mit Ihren Kollegen gemeinsam auf nach oben zu Voten-Elemente, die für Sie wichtig sind.
- **E-Mail-Adresse**: Wenn Sie Ihr Feedback an das Feature-Team privat übermitteln möchten, senden Sie eine e-Mail an system-insights-feed@microsoft.com. Bewahren Sie bedenken, dass wir Ihnen die Verwendung der Feedback-Hub oder UserVoice weiterhin anfordern kann.

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)