---
title: Überwachen von Servern, und Konfigurieren von Warnungen mit Azure-Monitor aus dem Windows Admin Center
description: Windows Admin Center (Projekt Honolulu) integriert Azure überwachen
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 6ada708bf7dd8cd08e1bc2620be5244a07beac7d
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297022"
---
# Überwachen von Servern, und Konfigurieren von Warnungen mit Azure-Monitor aus dem Windows Admin Center

[Weitere Informationen über die Integration von Azure finden Sie im Windows Admin Center.](../plan/azure-integration-options.md)

[Azure-Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ist eine Lösung, die sammelt und analysiert Telemetriedaten aus einer Vielzahl von Ressourcen, einschließlich Windows-Servern und VMs sowohl lokal als auch in der Cloud fungiert. Obwohl die Azure-Monitor Daten von Azure-VMs und andere Azure-Ressourcen zieht, geht es um die in diesem Artikel zur Funktionsweise der Azure-Monitor mit lokalen Servern und VMs speziell mit Windows Admin Center. Wenn Sie erfahren möchten, erfahren, wie Sie Azure-Monitor verwenden können, um e-Mail-Warnungen über die zusammengeführte Cluster zu erhalten, informieren Sie sich über die [Verwendung von Azure-Monitor für Health-Service-Fehler-e-Mails senden](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor).

## Wie funktioniert die Azure-Monitor?
![IMG](../media/azure-monitor-diagram.png) Daten aus lokalen Windows Server generiert werden in einem Log Analytics-Arbeitsbereich im Azure-Monitor erfasst. Innerhalb eines Arbeitsbereichs können Sie verschiedene monitoring-Lösungen aktivieren – legt der Logik, die Einblicke für ein bestimmtes Szenario bereitstellen. Azure-Updateverwaltung, Azure Security Center und Azure-Monitor für VMs sind beispielsweise alle monitoring-Lösungen, die innerhalb eines Arbeitsbereichs aktiviert werden können. 

Wenn Sie eine Überwachung Lösung in Log Analytics-Arbeitsbereich alle Berichte für diesen Arbeitsbereich Server aktivieren startet Erfassung von Daten in Bezug auf, die diese Lösung, damit die Lösung Einblicke für alle Server im Arbeitsbereich "" erstellen kann. 

Zum Sammeln von Telemetriedaten auf einem lokalen Server und entscheiden Sie sich für die Log Analytics-Arbeitsbereich, erfordert, dass Azure-Monitor die Installation der Microsoft Monitoring Agent oder den MMA. Bestimmte monitoring-Lösungen erfordern außerdem einen sekundären-Agent. Beispielsweise hängt von Azure-Monitor für VMs auch einen Agent ServiceMap zusätzliche Funktionen, die diese Lösung bietet. 

Einige Lösungen, wie Azure-Updateverwaltung, hängt auch von Azure-Benutzeroberflächenautomatisierung, dem Sie Ressourcen über Azure und nicht-Azure-Umgebungen zentral verwalten können. Beispielsweise verwendet Azure-Updateverwaltung Azure-Automatisierung zu planen und zu koordinieren Installation von Updates auf Computern in Ihrer Umgebung zentral aus dem Azure-Portal.


## Wie ermöglicht Windows Admin Center Azure-Monitor verwenden?

Innerhalb der WAC, können Sie zwei monitoring-Lösungen aktivieren:

- [Azure-Updateverwaltung](azure-update-management.md) (in der Update-Tool)
- Azure-Monitor für VMs (in Server Einstellungen), bzw. virtuellen Computern Einblicke

Sie können beginnen mit der Azure-Monitor aus dieser Tools. Wenn Sie Azure-Monitor vor dem noch nie verwendet haben, WAC wird automatisch bereitstellen einer Log Analytics-Arbeitsbereich (und Automatisierung von Azure-Konto bei Bedarf) sowie installieren und konfigurieren Sie den Microsoft Monitoring Agent (MMA) auf dem Zielserver. Es wird dann die entsprechende Lösung in den Arbeitsbereich installieren. 

Wenn Sie sich zuerst an das Updates-Tool, das Einrichten von Azure-Updateverwaltung hinausgehen, wird z. B. WAC:

1. Installieren Sie den MMA auf dem Computer
2. Erstellen der Log Analytics-Arbeitsbereich und das Azure-Automatisierung-Konto (da ein Azure-Automatisierung-Konto in diesem Fall erforderlich ist)
3. Installieren Sie die Update-Management-Lösung im Arbeitsbereich "neu erstellte".

Wenn Sie einen anderen monitoring-Lösung von innerhalb der WAC auf demselben Server hinzufügen möchten, installiert WAC einfach diese Lösung in den vorhandenen Arbeitsbereich mit dem dieser Server verbunden ist. WAC wird außerdem alle anderen erforderlichen Agenten installieren.

Wenn Sie eine Verbindung mit einem anderen Server herstellen, haben aber bereits Setup ein Log Analytics-Arbeitsbereich (entweder über WAC oder manuell im Azure-Portal), können Sie auch den MMA-Agent auf dem Server installieren und es bis zu einem vorhandenen Arbeitsbereich verbinden. Wenn Sie einen Server in einen Arbeitsbereich verbinden, wird es Erfassung von Daten und Berichte für Lösungen, die in diesem Arbeitsbereich installiert automatisch gestartet.

## Überwachen von Azure für (auch bekannt als virtuelle Computer Virtuelle Computer Einblicke)
>Gilt für: Windows Admin Center Vorschau

Wenn Sie Azure-Monitor für VMs in Server-Einstellungen einrichten, ermöglicht Windows Admin Center der Azure-Monitor für VMs Lösung, auch bekannt als virtuellen Computer Einblicke. Diese Lösung können Sie Überwachung von Serverstatus und Ereignisse, e-Mail-Warnungen zu erstellen, erhalten eine konsolidierte Sicht serverleistung in Ihrer Umgebung und Visualisieren apps, Systeme und Dienste, die mit einem bestimmten Server verbunden.

> [!NOTE]
> Trotz seines Namens funktioniert VM Einblicke für physische Server als auch für virtuelle Computer.

Mit Azure-Monitor kostenlose 5 GB Daten/Monat/Kunden Vergütung, Sie können ganz einfach ausprobieren dies für einen Server oder zwei ohne Gedanken erste in Rechnung gestellt. Lesen Sie weiter, finden Sie weitere Vorteile von Onboarding-Servern in Azure-Monitor, z. B. eine konsolidierte Sicht auf Systemen Leistung über die Server in Ihrer Umgebung abrufen.

### **Richten Sie Ihre Server für die Verwendung mit Azure-Monitor**

In der Übersicht einer Server-Verbindung, klicken Sie auf die neue Schaltfläche "Verwalten von Warnungen" zu oder servereinstellungen > Überwachung und Warnungen. Innerhalb dieser Seite integrieren Ihrer Server auf Azure-Monitor durch Klicken auf "Set up" und dem Abschluss des Setup-Bereichs. Admin Center sorgt dafür, dass der Azure Log Analytics-Arbeitsbereich Bereitstellung Installieren des erforderlichen Agenten und sicherstellen, dass die VM-Insights-Lösung konfiguriert ist. Nach Abschluss sendet Ihrer Server Leistungsindikatordaten auf Azure-Monitor, aktivieren Sie zum Anzeigen und Erstellen von e-Mail-Warnungen basierend auf diesen Server aus dem Azure-Portal.

### **Erstellen von e-Mail-Warnungen**

Nachdem Sie Ihre Server mit Azure-Monitor verbunden haben, können Sie den intelligenten Hyperlinks innerhalb der Seite "Einstellungen > Überwachung und Warnungen" verwenden, um auf das Azure-Portal navigieren. Admin Center aktiviert automatisch Leistungsindikatoren gesammelt, sein, damit Sie ganz einfach [eine neue Warnung erstellen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) , indem Sie eine der vielen vordefinierten Abfragen anpassen oder einen eigenen schreiben können.

### ** Erhalten Sie eine konsolidierte Sicht auf mehreren Servern **

Wenn Sie integrieren mehreren Servern auf einen einzelnen Log Analytics-Arbeitsbereich in Azure überwachen Sie erhalten eine konsolidierte Sicht auf alle dieser Server aus der [virtuelle Computer Einblicke Lösung](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) in Azure-Monitor.  (Beachten Sie, dass nur die Leistung und Karten Registerkarten von virtuellen Computern Einblicke für Azure-Monitor mit lokalen Server – die Integrität Registerkarte Funktionen nur mit Azure-VMs funktioniert.) Um dies im Azure-Portal anzuzeigen, wechseln Sie zu Azure-Monitor > virtuelle Computer (unter Einblicke), und navigieren Sie zu den Registerkarten "Leistung" oder "Karten".

### **Visualisieren Sie apps, Systeme und Dienste, die Verbindung mit einem bestimmten server**

Wenn aufleuchtet Admin Center Onboards einen Server in die VM-Insights-Lösung in Azure-Monitor, es auch eine Funktion namens [Service-Karte](https://docs.microsoft.com/azure/azure-monitor/insights/service-map). Diese Funktion ist automatisch Anwendungskomponenten ermittelt und die Kommunikation zwischen Diensten zugeordnet ist, damit Sie problemlos Verbindungen zwischen den Servern mit ausführlich aus dem Azure-Portal darstellen können. Dies können Sie ermitteln, indem Sie die Azure Portal > Azure-Monitor > virtuelle Computer (unter Einblicke), und navigieren zur Registerkarte "Karten".

> [!NOTE]
> Die Visualisierungen für virtuelle Computer Einblicke für Azure-Monitor werden derzeit in 6 öffentlichen Regionen angeboten.  Überprüfen Sie die neuesten Informationen den [Azure-Monitor für VMs-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics).  Sie müssen die Log Analytics-Arbeitsbereich in einem der unterstützten Regionen abzurufenden zusätzliche Vorteile, die die oben beschriebenen virtuelle Computer Einblicke-Lösung bereitstellen.

## Deaktivieren der Überwachung

Um Ihre Server vollständig aus dem Log Analytics-Arbeitsbereich zu trennen, deinstallieren Sie den MMA-Agent. Dies bedeutet, dass diese Server nicht mehr von Daten in den Arbeitsbereich senden wird und alles, was die Lösungen, die in diesem Arbeitsbereich installiert, nicht mehr werden sammeln und Verarbeiten von Daten von diesem Server. Dies wirkt nicht Arbeitsbereich selbst – alle sich jedoch die Ressourcen erstellt Berichte für diesen Arbeitsbereich weiterhin tun. Um den MMA-Agent innerhalb WAC zu deinstallieren, um Apps & Features, suchen Sie den Microsoft Monitoring Agent, und klicken Sie auf Deinstallieren.

Wenn Sie eine bestimmte Lösung innerhalb eines Arbeitsbereichs deaktivieren möchten, müssen Sie [die Überwachung Lösung aus dem Azure-Portal](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)entfernen. Entfernen einer monitoring Lösung bedeutet, dass die Erkenntnisse durch erstellt, dass die Lösung nicht mehr für _Alle_ Berichte für diesen Arbeitsbereich Servern generiert wird. Beispielsweise, wenn ich den Azure-Monitor für VMs Lösung deinstallieren, sehen ich nicht mehr Einblicke zur Leistung von VM oder Server aus der Computer mit Mein Arbeitsbereich verbunden.