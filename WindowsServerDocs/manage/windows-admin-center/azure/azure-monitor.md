---
title: Überwachen von Servern und Konfigurieren von Warnungen mit Azure Monitor aus dem Windows Admin Center
description: Windows Admin Center (Project Honolulu) ist in Azure Monitor integriert
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.date: 03/24/2019
ms.openlocfilehash: 81501cb5f4255b7a65ebc5f9f6cb9413938864f0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940121"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Überwachen von Servern und Konfigurieren von Warnungen mit Azure Monitor aus dem Windows Admin Center

[Erfahren Sie mehr über die Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ist eine Lösung, die Telemetriedaten aus einer Vielzahl von Ressourcen sammelt, analysiert und bearbeitet, einschließlich Windows-Servern und-VMS, sowohl lokal als auch in der Cloud. Obwohl Azure Monitor Daten von Azure-VMS und anderen Azure-Ressourcen abruft, konzentriert sich dieser Artikel auf die Funktionsweise von Azure Monitor mit lokalen Servern und VMS, insbesondere mit Windows Admin Center. Wenn Sie wissen möchten, wie Sie Azure Monitor verwenden können, um e-Mail-Benachrichtigungen über Ihren hyperkonvergenten Cluster zu erhalten, informieren Sie sich über die [Verwendung Azure Monitor, um e-Mails zu Integritätsdienst Fehlern zu senden](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor).

## <a name="how-does-azure-monitor-work"></a>Funktionsweise von Azure Monitor
![IMG ](../media/azure-monitor-diagram.png) -Daten, die von lokalen Windows-Servern generiert werden, werden in einem Log Analytics Arbeitsbereich in Azure Monitor gesammelt. Sie können in einem Arbeitsbereich verschiedene Überwachungslösungen aktivieren. Dies sind Sätze von Logik, die Erkenntnisse für ein bestimmtes Szenario bieten. Überwachungslösungen, die in einem Arbeitsbereich aktiviert werden können, sind beispielsweise die Azure-Updateverwaltung, Azure Security Center und Azure Monitor für VMs.

Wenn Sie eine Überwachungslösung in einem Log Analytics-Arbeitsbereich aktivieren, beginnen alle Server, die an diesen Arbeitsbereich berichten, mit dem Sammeln von Daten, die für diese Lösung relevant sind, damit die Lösung Erkenntnisse für alle Server im Arbeitsbereich generieren kann.

Zum Sammeln von Telemetriedaten auf einem lokalen Server und zum Übertragung per Push an den Arbeitsbereich Log Analytics Azure Monitor muss die Microsoft Monitoring Agent oder MMA installiert werden. Bestimmte Überwachungslösungen erfordern zudem einen sekundären Agent. Beispielsweise benötigt Azure Monitor für VMs auch einen ServiceMap-Agent für zusätzliche Funktionalität, die von dieser Lösung bereitgestellt wird.

Einige Lösungen, z. B. die Azure-Updateverwaltung, benötigen auch Azure Automation, damit Ressourcen sowohl in Azure-Umgebungen als auch in Umgebungen außerhalb von Azure zentral verwaltet werden können. Beispielsweise verwendet die Azure-Updateverwaltung Azure Automation, um die Installation von Updates auf allen Computern in Ihrer Umgebung zentral über das Azure-Portal zu planen und zu orchestrieren.


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Wie ermöglicht Ihnen Windows Admin Center die Verwendung von Azure Monitor?

Im WAC können Sie zwei Überwachungslösungen aktivieren:

- [Azure-Updateverwaltung](azure-update-management.md) (im Tool Updates)
- Azure Monitor für VMS (in Servereinstellungen), a. k. a Virtual Machines Insights

Sie können Azure Monitor von einem dieser Tools aus verwenden. Wenn Sie noch nie Azure Monitor verwendet haben, stellt WAC automatisch einen Log Analytics Arbeitsbereich bereit (und ggf. Azure Automation Konto) und die Microsoft Monitoring Agent (MMA) auf dem Zielserver zu installieren und zu konfigurieren. Anschließend wird die entsprechende Lösung im Arbeitsbereich installiert.

Wenn Sie zum Beispiel das Tool Updates zum Einrichten von Azure Updateverwaltung aufrufen, führt der WAC folgende Schritte aus:

1. Installieren des MMA auf dem Computer
2. Erstellen Sie den Log Analytics Arbeitsbereich und das Azure Automation Konto (da in diesem Fall ein Azure Automation Konto erforderlich ist).
3. Installieren der Updateverwaltungslösung im neu erstellten Arbeitsbereich

Wenn Sie eine weitere Überwachungslösung von WAC auf demselben Server hinzufügen möchten, wird diese Lösung von WAC einfach im vorhandenen Arbeitsbereich installiert, mit dem dieser Server verbunden ist. WAC installiert zusätzlich alle weiteren erforderlichen Agents.

Wenn Sie eine Verbindung mit einem anderen Server herstellen, aber bereits einen Log Analytics Arbeitsbereich eingerichtet haben (entweder über WAC oder manuell im Azure-Portal), können Sie auch den MMA-Agent auf dem Server installieren und ihn mit einem vorhandenen Arbeitsbereich verbinden. Wenn Sie einen Server mit einem Arbeitsbereich verbinden, beginnt er automatisch mit dem Sammeln von Daten und der Berichterstellung in Lösungen, die in diesem Arbeitsbereich installiert sind.

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>Azure Monitor für virtuelle Computer (auch als „Virtual Machine Insights“ bezeichnet)
>Gilt für: Windows Admin Center (Vorschau)

Wenn Sie Azure Monitor für VMs in den Servereinstellungen einrichten, aktiviert das Windows Admin Center die Azure Monitor für VMS Lösung, auch bekannt als Virtual Machine Insights. Mit dieser Lösung können Sie die Integrität und Ereignisse des Servers überwachen, E-Mail-Warnungen erstellen, eine konsolidierte Ansicht der Serverleistung in Ihrer Umgebung erhalten und Apps, Systeme und Dienste visualisieren, die mit einem bestimmten Server verbunden sind.

> [!NOTE]
> Trotz seines Namens funktioniert VM Insights sowohl für physische Server als auch für virtuelle Computer.

Dank des kostenlosen Azure Monitor-Kontingents von 5 GB Daten pro Monat und Kunde können Sie dies problemlos für einen oder zwei Server ausprobieren, ohne dass Kosten für Sie anfallen. Nachfolgend werden weitere Vorteile des Onboardings von Servern in Azure Monitor beschrieben, darunter eine konsolidierte Ansicht der Systemleistung der Server in Ihrer Umgebung.

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Einrichten des Servers für die Verwendung mit Azure Monitor**

Klicken Sie auf der Übersichtsseite einer Server Verbindung auf die neue Schaltfläche "Warnungen verwalten", oder wechseln Sie zu Servereinstellungen > Überwachung und Warnungen. Integrieren Sie auf dieser Seite den Server in die Azure Monitor, indem Sie auf "einrichten" klicken und den Setup Bereich abschließen. Admin Center übernimmt die Bereitstellung des Azure Log Analytics-Arbeitsbereichs, die Installation des erforderlichen Agents und die Konfiguration der VM Insights-Lösung. Sobald der Vorgang beendet ist, sendet der Server Leistungsindikatordaten an Azure Monitor, sodass Sie über das Azure-Portal E-Mail-Warnungen auf Grundlage dieses Servers anzeigen und erstellen können.

### <a name="create-email-alerts"></a>**E-Mail erstellen**

Nachdem Sie den Server an Azure Monitor angefügt haben, können Sie die intelligenten Hyperlinks auf der Seite Einstellungen > Überwachung und Warnungen verwenden, um zum Azure-Portal zu navigieren. Das Admin Center aktiviert automatisch die zu sammelnden Leistungsindikatoren, sodass Sie problemlos [eine neue Warnung erstellen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) können, indem Sie eine von vielen vordefinierten Abfragen anpassen oder eigene Abfragen erstellen.

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>* * Konsolidierte Ansicht über mehrere Server hinweg erhalten * *

Wenn Sie mehrere Server innerhalb Azure Monitor in einen einzelnen Log Analytics Arbeitsbereich integrieren, können Sie in Azure Monitor eine konsolidierte Ansicht aller dieser Server aus der [Virtual Machines Insights-Lösung](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) erhalten.  (Beachten Sie, dass nur die Registerkarten "Leistung" und "Karten" von Virtual Machines Insights für Azure Monitor mit lokalen Servern funktionieren – die Registerkarte "Integrität" funktioniert nur mit Azure-VMS.) Um dies im Azure-Portal anzuzeigen, wechseln Sie zu Azure Monitor > Virtual Machines (unter Einblicke), und navigieren Sie zu den Registerkarten "Leistung" oder "Maps".

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**Visualisieren von apps, Systemen und Diensten, die mit einem bestimmten Server verbunden sind**

Wenn Admin Center einen Server in der VM Insights-Lösung innerhalb Azure Monitor einrichtet, wird auch eine Funktion mit dem Namen " [Dienstzuordnung](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)" angezeigt. Diese Funktion ermittelt automatisch Anwendungskomponenten und ordnet die Kommunikation zwischen Diensten zu, sodass Sie problemlos über das Azure-Portal Verbindungen zwischen Servern detailliert visualisieren können. Sie finden dies, indem Sie die Azure-Portal > Azure Monitor > Virtual Machines (unter Einblicke) aufrufen und zur Registerkarte "Maps" navigieren.

> [!NOTE]
> Die Visualisierungen für Virtual Machines Insights für Azure Monitor werden derzeit in 6 öffentlichen Regionen angeboten.  Aktuelle Informationen finden Sie in der [Dokumentation zu Azure Monitor für VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics).  Sie müssen den Log Analytics-Arbeitsbereich in einer der unterstützten Regionen bereitstellen, um die zusätzlichen Vorteile der oben beschriebenen Virtual Machines Insights-Lösung zu erhalten.

## <a name="disabling-monitoring"></a>Deaktivieren der Überwachung

Deinstallieren Sie den MMA-Agent, um den Server vollständig vom Log Analytics Arbeitsbereich zu trennen. Dies bewirkt, dass dieser Server keine Daten mehr an den Arbeitsbereich sendet und alle in diesem Arbeitsbereich installierten Lösungen keine Daten mehr von diesem Server sammeln und verarbeiten. Dies wirkt sich jedoch nicht auf den Arbeitsbereich selbst aus – alle Ressourcen, die diesem Arbeitsbereich melden, werden dies weiterhin tun. Wenn Sie den MMA-Agent innerhalb von Windows Admin Center deinstallieren möchten, stellen Sie eine Serververbindung her, navigieren Sie dann zu **Installierte Apps**, suchen Sie den Microsoft Monitoring Agent, und wählen Sie dann **Entfernen** aus.

Wenn Sie eine bestimmte Lösung in einem Arbeitsbereich deaktivieren möchten, müssen Sie [die Überwachungslösung aus dem Azure-Portal entfernen](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution). Das Entfernen einer Überwachungslösung bedeutet, dass die von dieser Lösung erstellten Erkenntnisse für _keinen_ der Server mehr generiert werden, die an diesen Arbeitsbereich berichten. Wenn ich beispielsweise die Azure Monitor für VMS Lösung deinstalliere, sehe ich keine Einblicke in die VM-oder Serverleistung von Computern, die mit dem Arbeitsbereich verbunden sind.
