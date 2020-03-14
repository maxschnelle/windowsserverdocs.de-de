---
title: Überwachen von Servern und Konfigurieren von Warnungen mit Azure Monitor aus dem Windows Admin Center
description: Windows Admin Center (Project Honolulu) ist in Azure Monitor integriert
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 03/24/2019
ms.openlocfilehash: 28108a79bbdc654f6437a698c158a3f74d4423ba
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322942"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Überwachen von Servern und Konfigurieren von Warnungen mit Azure Monitor aus dem Windows Admin Center

[Erfahren Sie mehr über die Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ist eine Lösung, die Telemetriedaten aus einer Vielzahl von Ressourcen sammelt, analysiert und bearbeitet, einschließlich Windows-Servern und-VMS, sowohl lokal als auch in der Cloud. Obwohl Azure Monitor Daten von Azure-VMS und anderen Azure-Ressourcen abruft, konzentriert sich dieser Artikel auf die Funktionsweise von Azure Monitor mit lokalen Servern und VMS, insbesondere mit Windows Admin Center. Wenn Sie wissen möchten, wie Sie Azure Monitor verwenden können, um e-Mail-Benachrichtigungen über Ihren hyperkonvergenten Cluster zu erhalten, informieren Sie sich über die [Verwendung Azure Monitor, um e-Mails zu Integritätsdienst Fehlern zu senden](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor).

## <a name="how-does-azure-monitor-work"></a>Wie funktioniert Azure Monitor?
![IMG](../media/azure-monitor-diagram.png) Daten, die von lokalen Windows-Servern generiert werden, werden in Azure Monitor in einem Log Analytics Arbeitsbereich gesammelt. In einem Arbeitsbereich können Sie verschiedene Überwachungslösungen – Sätze von Logik zur Bereitstellung von Informationen für ein bestimmtes Szenario aktivieren. Beispielsweise sind Azure Updateverwaltung, Azure Security Center und Azure Monitor für VMS alle Überwachungslösungen, die in einem Arbeitsbereich aktiviert werden können. 

Wenn Sie eine Überwachungslösung in einem Log Analytics-Arbeitsbereich aktivieren, beginnen alle Server, die an diesen Arbeitsbereich Berichten, mit dem Sammeln von Daten, die für diese Lösung relevant sind, damit die Lösung Einblicke für alle Server im Arbeitsbereich generieren kann. 

Zum Sammeln von Telemetriedaten auf einem lokalen Server und zum Übertragung per Push an den Arbeitsbereich Log Analytics Azure Monitor muss die Microsoft Monitoring Agent oder MMA installiert werden. Bestimmte Überwachungslösungen erfordern auch einen sekundären Agent. Beispielsweise ist Azure Monitor für VMS auch von einem Service Map-Agent abhängig, um zusätzliche Funktionen zu erhalten, die von dieser Lösung bereitstellt werden. 

Einige Lösungen, wie z. b. Azure Updateverwaltung, sind auch von Azure Automation abhängig, sodass Sie Ressourcen zentral in Azure und in nicht-Azure-Umgebungen verwalten können. Beispielsweise verwendet Azure Updateverwaltung Azure Automation, um die Installation von Updates auf allen Computern in Ihrer Umgebung zentral aus dem Azure-Portal zu planen und zu orchestrieren.


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Wie ermöglicht Windows Admin Center Ihnen die Verwendung von Azure Monitor?

Im WAC können Sie zwei Überwachungslösungen aktivieren:

- [Azure-Updateverwaltung](azure-update-management.md) (im Update-Tool)
- Azure Monitor für VMS (in Servereinstellungen), a. k. a Virtual Machines Insights

Sie können Azure Monitor von einem dieser Tools aus verwenden. Wenn Sie noch nie Azure Monitor verwendet haben, stellt WAC automatisch einen Log Analytics Arbeitsbereich bereit (und ggf. Azure Automation Konto) und die Microsoft Monitoring Agent (MMA) auf dem Zielserver zu installieren und zu konfigurieren. Anschließend wird die entsprechende Lösung im Arbeitsbereich installiert. 

Wenn Sie zum Beispiel das Tool Updates zum Einrichten von Azure Updateverwaltung aufrufen, führt der WAC folgende Schritte aus:

1. Installieren des MMA auf dem Computer
2. Erstellen Sie den Log Analytics Arbeitsbereich und das Azure Automation Konto (da in diesem Fall ein Azure Automation Konto erforderlich ist).
3. Installieren Sie die Updateverwaltung Lösung im neu erstellten Arbeitsbereich.

Wenn Sie eine weitere Überwachungslösung von WAC auf demselben Server hinzufügen möchten, wird diese Lösung von WAC einfach im vorhandenen Arbeitsbereich installiert, mit dem dieser Server verbunden ist. WAC installiert zusätzlich alle weiteren erforderlichen Agents.

Wenn Sie eine Verbindung mit einem anderen Server herstellen, aber bereits einen Log Analytics Arbeitsbereich eingerichtet haben (entweder über WAC oder manuell im Azure-Portal), können Sie auch den MMA-Agent auf dem Server installieren und ihn mit einem vorhandenen Arbeitsbereich verbinden. Wenn Sie einen Server mit einem Arbeitsbereich verbinden, beginnt er automatisch mit der Erfassung von Daten und der Berichterstellung an Lösungen, die in diesem Arbeitsbereich installiert sind

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>Azure Monitor für virtuelle Computer (auch bekannt als Einblicke in Virtual Machine
>Gilt für: Windows Admin Center (Vorschau)

Wenn Sie Azure Monitor für VMs in den Servereinstellungen einrichten, aktiviert das Windows Admin Center die Azure Monitor für VMS Lösung, auch bekannt als Virtual Machine Insights. Mit dieser Lösung können Sie die Integrität und Ereignisse des Servers überwachen, e-Mail-Benachrichtigungen erstellen, eine konsolidierte Ansicht der Serverleistung in Ihrer Umgebung erhalten und apps, Systeme und Dienste visualisieren, die mit einem bestimmten Server verbunden sind.

> [!NOTE]
> Trotz seines Namens funktioniert VM Insights sowohl für physische Server als auch für virtuelle Computer.

Dank der kostenlosen Azure Monitor 5 GB Daten/Monat/Kunden Kontingent können Sie dies problemlos für einen oder zwei Server ausprobieren, ohne sich um die Kosten kümmern zu müssen. Lesen Sie weiter, um weitere Vorteile des Onboarding von Servern in Azure Monitor anzuzeigen, wie z. b. das Erzielen einer konsolidierten Ansicht der Systemleistung auf den Servern in Ihrer Umgebung.

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Einrichten des Servers für die Verwendung mit Azure Monitor**

Klicken Sie auf der Übersichtsseite einer Server Verbindung auf die neue Schaltfläche "Warnungen verwalten", oder wechseln Sie zu Servereinstellungen > Überwachung und Warnungen. Integrieren Sie auf dieser Seite den Server in die Azure Monitor, indem Sie auf "einrichten" klicken und den Setup Bereich abschließen. Admin Center übernimmt die Bereitstellung des Azure Log Analytics-Arbeitsbereichs, die Installation des erforderlichen Agents und die Konfiguration der VM Insights-Lösung. Sobald der Vorgang beendet ist, sendet der Server Leistungsdaten an Azure Monitor und ermöglicht Ihnen, e-Mail-Benachrichtigungen basierend auf diesem Server aus dem Azure-Portal anzuzeigen und zu erstellen.

### <a name="create-email-alerts"></a>**E-Mail erstellen**

Nachdem Sie den Server an Azure Monitor angefügt haben, können Sie die intelligenten Hyperlinks auf der Seite Einstellungen > Überwachung und Warnungen verwenden, um zum Azure-Portal zu navigieren. Das Admin Center aktiviert automatisch die zu sammelnden Leistungsindikatoren, sodass Sie problemlos [eine neue Warnung erstellen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) können, indem Sie eine von vielen vordefinierten Abfragen anpassen oder eigene Abfragen erstellen.

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>\* * Konsolidierte Ansicht über mehrere Server hinweg erhalten * *

Wenn Sie mehrere Server innerhalb Azure Monitor in einen einzelnen Log Analytics Arbeitsbereich integrieren, können Sie in Azure Monitor eine konsolidierte Ansicht aller dieser Server aus der [Virtual Machines Insights-Lösung](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) erhalten.  (Beachten Sie, dass nur die Registerkarten "Leistung" und "Karten" von Virtual Machines Insights für Azure Monitor mit lokalen Servern funktionieren – die Registerkarte "Integrität" funktioniert nur mit Azure-VMS.) Um dies im Azure-Portal anzuzeigen, wechseln Sie zu Azure Monitor > virtual machines (unter Einblicke), und navigieren Sie zu den Registerkarten "Leistung" oder "Maps".

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**Visualisieren von apps, Systemen und Diensten, die mit einem bestimmten Server verbunden sind**

Wenn Admin Center einen Server in der VM Insights-Lösung innerhalb Azure Monitor einrichtet, wird auch eine Funktion mit dem Namen " [Dienstzuordnung](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)" angezeigt. Diese Funktion ermittelt automatisch Anwendungskomponenten und ordnet die Kommunikation zwischen Diensten zu, sodass Sie problemlos Verbindungen zwischen Servern mit großen Details aus dem Azure-Portal visualisieren können. Sie finden dies, indem Sie die Azure-Portal > Azure Monitor > virtual machines (unter Einblicke) aufrufen und zur Registerkarte "Maps" navigieren.

> [!NOTE]
> Die Visualisierungen für Virtual Machines Insights für Azure Monitor werden derzeit in 6 öffentlichen Regionen angeboten.  Die neuesten Informationen finden Sie in der [Azure Monitor für VMS-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics).  Sie müssen den Log Analytics-Arbeitsbereich in einer der unterstützten Regionen bereitstellen, um die zusätzlichen Vorteile der oben beschriebenen Virtual Machines Insights-Lösung zu erhalten.

## <a name="disabling-monitoring"></a>Deaktivieren der Überwachung

Deinstallieren Sie den MMA-Agent, um den Server vollständig vom Log Analytics Arbeitsbereich zu trennen. Dies bedeutet, dass dieser Server keine Daten mehr an den Arbeitsbereich sendet und alle in diesem Arbeitsbereich installierten Lösungen die Daten von diesem Server nicht mehr erfassen und verarbeiten. Dies wirkt sich jedoch nicht auf den Arbeitsbereich selbst aus – alle Ressourcen, die diesem Arbeitsbereich melden, werden dies weiterhin tun. Wenn Sie den MMA-Agent innerhalb von WAC deinstallieren möchten, wechseln Sie zu Apps & Features, suchen Sie die Microsoft Monitoring Agent, und klicken Sie dann auf

Wenn Sie eine bestimmte Lösung in einem Arbeitsbereich deaktivieren möchten, müssen Sie [die Überwachungslösung aus dem Azure-Portal entfernen](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution). Das Entfernen einer Überwachungslösung bedeutet, dass die von dieser Lösung erstellten Erkenntnisse nicht mehr für _einen_ der Server generiert werden, die an diesen Arbeitsbereich Berichten. Wenn ich beispielsweise die Azure Monitor für VMS Lösung deinstalliere, sehe ich keine Einblicke in die VM-oder Serverleistung von Computern, die mit dem Arbeitsbereich verbunden sind.