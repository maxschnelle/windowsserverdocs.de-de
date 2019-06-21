---
title: Überwachen von Servern, und Konfigurieren von Warnungen mit Azure Monitor aus Windows Admin Center
description: Windows Admin Center (Projekt Honolulu) ist in Azure Monitor integriert.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 8f7baba465071cc95ab7492037ff25c5cd58219e
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280433"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Überwachen von Servern, und Konfigurieren von Warnungen mit Azure Monitor aus Windows Admin Center

[Weitere Informationen zu Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ist eine Lösung, die erfasst, analysiert und Telemetriedaten aus einer Vielzahl von Ressourcen, einschließlich Windows-Servern und virtuellen Computern, sowohl lokal und in der Cloud dient. Obwohl Azure Monitor Daten aus Azure-VMs und anderen Azure-Ressourcen abruft, liegt der Schwerpunkt in diesem Artikel zur Funktionsweise von Azure Monitor mit lokalen Servern und virtuellen Computern, speziell mit Windows Admin Center. Wenn Sie möchten wissen, um zu erfahren, wie Sie Azure Monitor verwenden können, um e-Mail-Benachrichtigungen zu Ihren hyperkonvergenten Cluster zu erhalten, erfahren Sie, [mithilfe von Azure Monitor zum Senden von e-Mails für Health-Dienstfehler](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor).

## <a name="how-does-azure-monitor-work"></a>Funktionsweise von Azure Monitor
![IMG](../media/azure-monitor-diagram.png) von lokalen Windows-Servern generierte Daten in einem Log Analytics-Arbeitsbereich in Azure Monitor erfasst werden. In einem Arbeitsbereich können Sie verschiedene überwachungslösung in Azure Stack – legt fest, der Logik, die Einblicke für ein bestimmtes Szenario zu bieten. Beispielsweise sind die Verwaltung von Azure, Azure Security Center und Azure Monitor für den virtuellen Computer alle überwachungslösungen, die in einem Arbeitsbereich aktiviert werden können. 

Wenn Sie eine überwachungslösung in Log Analytics-Arbeitsbereich aktivieren, werden alle Server, die an diesem Arbeitsbereich gestartet für diese Lösung, relevante Daten zu sammeln, damit die Lösung Einblicke für alle Server im Arbeitsbereich generieren kann. 

Zum Sammeln von Telemetriedaten auf einem lokalen Server, und per push an Log Analytics-Arbeitsbereich, erfordert die Azure Monitor die Installation von Microsoft Monitoring Agent oder der MMA. Bestimmte überwachungslösungen erfordern auch einen sekundären-Agent. Azure Monitor für den virtuellen Computer hängt beispielsweise auch auf einem Agent ServiceMap für zusätzliche Funktionalität, die diese Lösung bietet. 

Einige Lösungen wie Azure-Updateverwaltung, hängt auch Azure Automation, die Sie Ressourcen auf Azure und nicht-Azure-Umgebungen zentral verwalten können. Beispielsweise verwendet Azure die Verwaltung von Azure Automation zu planen und orchestrieren die Installation von Updates auf Computern in Ihrer Umgebung zentral im Azure-Portal.


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Wie Ihnen die Verwendung von Azure Monitor Windows Admin Center aktivieren?

In WAC, können Sie zwei überwachungslösungen aktivieren:

- [Verwaltung von Azure](azure-update-management.md) (in der Updates-Tool)
- Azure Monitor für virtuelle Computer (in Server-Einstellungen), bzw. VMs insights

Sie können die ersten mithilfe von Azure Monitor von einem dieser Tools. Wenn Sie Azure Monitor vor der nie verwendet haben, WAC wird automatisch bereitgestellt, einen Log Analytics-Arbeitsbereich (und den Azure Automation-Konto bei Bedarf), und installieren und konfigurieren Sie den Microsoft Monitoring Agent (MMA) auf dem Zielserver. Es wird dann die entsprechende Lösung in den Arbeitsbereich installieren. 

Wenn Sie zuerst die Updates-Tool zum Einrichten der Verwaltung von Azure aufrufen, wird z. B. WAC:

1. Installieren des MMA auf dem Computer
2. Erstellen von Log Analytics-Arbeitsbereich und das Azure Automation-Konto (da es sich bei Azure Automation-Konto in diesem Fall erforderlich ist)
3. Installieren Sie die Updateverwaltung-Lösung im neu erstellten Arbeitsbereich aus.

Wenn Sie eine andere Lösung aus in WAC auf dem gleichen Server hinzufügen möchten, installiert WAC einfach die Lösung in den vorhandenen Arbeitsbereich, der diesem Server verbunden ist. WAC werden außerdem alle anderen erforderlichen Agents installiert.

Wenn Sie eine Verbindung mit einem anderen Server herstellen, aber Sie verfügen bereits über Setup Log Analytics-Arbeitsbereich (entweder über WAC oder manuell im Azure-Portal), können Sie auch den MMA-Agent auf dem Server installieren und verbinden Sie es bis zu einem vorhandenen Arbeitsbereich. Wenn Sie einen Server in einem Arbeitsbereich anschließen, startet er automatisch an das Sammeln von Daten und Berichte an Lösungen, die in diesem Arbeitsbereich installiert.

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>Überwachen von Azure für virtuelle Computer (auch als) VM-Informationen)
>Gilt für: Windows Admin Center – Vorschau

Wenn Sie Azure Monitor für virtuelle Computer im Server-Einstellungen einrichten, ermöglicht Windows Admin Center die Azure Monitor für die VMs auch bekannt als VM-Insights-Lösung. Diese Lösung können Sie Serverzustand und Ereignisse überwachen, e-Mail-Warnungen erstellen, erhalten eine konsolidierte Ansicht der Leistung in Ihrer gesamten Umgebung und Visualisieren von apps, Systeme und Dienste miteinander verbunden sind, für einen bestimmten Server.

> [!NOTE]
> Trotz seines Namens VM Insights funktioniert für physische Server als auch für virtuelle Computer.

Mit Azure Monitor die kostenlose 5 GB Daten/Monat/Kunde-Kontingent, die Sie ganz einfach ausprobieren können dies für einen Server oder zwei, ohne dass Gebühren. Lesen Sie weiter, finden Sie weitere Vorteile von Onboarding von Servern in Azure Monitor, z. B. eine konsolidierte Ansicht der Systemleistung zwischen den Servern in Ihrer Umgebung abrufen.

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Einrichten des Servers für die Verwendung mit Azure Monitor**

Aus der Seite "Übersicht" eine Serververbindung, klicken Sie auf die neue Schaltfläche "Warnungen verwalten", oder wechseln Sie zum Server-Einstellungen > Überwachung und Warnungen. Auf dieser Seite, integrieren des Servers zu Azure Monitor, indem Sie auf "einrichten" und im Bereich Setup abschließen. Admin Center kümmert sich der Bereitstellung von Azure Log Analytics-Arbeitsbereich, den erforderlichen Agent installieren und Sicherstellen der VM-Insights-Lösung konfiguriert ist. Nach Abschluss des Vorgangs sendet der Server Leistungsindikatordaten an Azure Monitor ermöglicht Ihnen das Anzeigen und erstellen die e-Mail-Benachrichtigungen basierend auf diesem Server aus dem Azure-Portal.

### <a name="create-email-alerts"></a>**Erstellen von e-Mail-Benachrichtigungen**

Nachdem Sie Ihren Server zu Azure Monitor angehängt haben, können Sie die intelligenten Links in den Einstellungen > Überwachung und Warnungen-Seite zu Azure-Portal navigieren. Admin Center aktiviert automatisch Leistungsindikatoren gesammelt werden sollen, können Sie problemlos [erstellt eine neue Warnung](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) durch eine der vielen vordefinierten Abfragen anpassen, oder Verfassen Ihres eigenen.

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>** Erhalten Sie eine konsolidierte Ansicht über mehrere Server **

Wenn Sie integriert mehrere Server für einen einzelnen Log Analytics-Arbeitsbereich in Azure Monitor erhalten Sie eine konsolidierte Ansicht der alle diese Server von der [VMs Insights-Lösung](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) in Azure Monitor.  (Beachten Sie, dass nur die Registerkarten Leistung und die Zuordnungen von virtuellen Computern Insights für Azure Monitor mit lokalen Servern – die Integrität Registerkarte-funktioniert nur mit virtuellen Azure-Computern verwendet werden kann.) Um dies im Azure-Portal anzuzeigen, wechseln Sie an Azure Monitor > virtuelle Computer (unter Insights), und navigieren Sie zu den Registerkarten "Leistung" oder "Karten".

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**Visualisieren von apps, Systeme und Dienste miteinander verbunden sind, um einen bestimmten Server.**

Wenn Admin Center Integration von einem Server in der VM-Insights-Lösung in Azure Monitor, auch klicke, werden eine Funktion namens [Service Map](https://docs.microsoft.com/azure/azure-monitor/insights/service-map). Diese Funktion automatisch Anwendungskomponenten ermittelt und die Kommunikation zwischen Diensten abbildet, sodass Sie Verbindungen zwischen Servern mit sehr ausführliche Informationen über das Azure-Portal einfach visualisieren können. Sie finden diese auf das Azure-Portal > Azure Monitor > virtuelle Computer (unter Insights), und navigieren zur Registerkarte "Karten".

> [!NOTE]
> Derzeit werden die Visualisierungen für Einblicke in virtuellen Computern für Azure Monitor in 6 öffentlichen Regionen angeboten.  Überprüfen Sie die neuesten Informationen, die [Azure Monitor für die Dokumentation zu virtuellen Computern](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics).  Sie müssen die Log Analytics-Arbeitsbereich in einem der unterstützten Regionen erhalten weitere Vorteile, die der virtuelle Computer-Insights-Lösung, die oben beschriebenen bereitstellen.

## <a name="disabling-monitoring"></a>Deaktivieren der Überwachung

Um Ihre Server vollständig aus dem Log Analytics-Arbeitsbereich zu trennen, deinstallieren Sie den MMA-Agent. Dies bedeutet, dass dieser Server mehr Daten auf den Arbeitsbereich sendet, und alles, was nicht mehr werden von die in diesem Arbeitsbereich installierten Lösungen sammeln und Verarbeiten von Daten von diesem Server. Dies wirkt nicht der Arbeitsbereich selbst – alle sich jedoch die Ressourcen, die mit diesem Arbeitsbereich Berichte weiterhin dazu. Wechseln Sie zum Deinstallieren des MMA-Agents in WAC finden auf Anwendungen und Funktionen, die Microsoft Monitoring Agent, und klicken Sie auf Deinstallieren.

Wenn Sie eine bestimmte Projektmappe in einem Arbeitsbereich deaktivieren möchten, müssen Sie zum [entfernen die Lösung für die vom Azure-Portal](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution). Entfernen eine Lösung für die Remoteüberwachung bedeutet, dass es sich bei die Einblicke, die von der Lösung erstellt nicht mehr für die generiert werden _alle_ der mit diesem Arbeitsbereich reporting-Server. Z. B. wenn ich die Azure Monitor für die Lösung für virtuelle Computer deinstallieren, werden ich nicht mehr Erkenntnisse zur Leistung von virtuellen Computer oder Server von einem Computer mit dem Arbeitsbereich verbunden angezeigt.