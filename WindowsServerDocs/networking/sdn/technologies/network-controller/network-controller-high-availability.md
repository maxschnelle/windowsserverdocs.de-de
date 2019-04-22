---
title: Netzwerkcontroller – Hohe Verfügbarkeit
description: Sie können in diesem Thema verwenden, um mehr über hohe Verfügbarkeit für den Netzwerkcontroller für Software-Defined Networking (SDN) in Windows Server 2016 erfahren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbd3ae9f4c1f1fc3035fae9ace880046312df2f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813351"
---
# <a name="network-controller-high-availability"></a>Netzwerkcontroller – Hohe Verfügbarkeit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, Informationen zu den Netzwerkcontroller hohe Verfügbarkeit und Skalierbarkeit Konfiguration für die Software Defined Networking \(SDN\).

Wenn Sie SDN in Ihrem Datencenter bereitstellen, können Sie den Netzwerkcontroller zentral bereitstellen, überwachen und Verwalten von vielen Netzwerkelemente, einschließlich der RAS-Gateways, Software-Lastenausgleichsmodule, virtuelle Netzwerkrichtlinien für die Kommunikation des Mandanten, Datacenter Firewall Quality of Service-Richtlinien \(QoS\) für SDN-Richtlinien, Hybrid-Netzwerkrichtlinien und mehr.

Da Netzwerkcontroller das Fundament der Verwaltung eines SDN ist, ist es wichtig, für den Netzwerkcontroller-Bereitstellungen für hohe Verfügbarkeit und die Möglichkeit für Sie auf einfache Weise die zentral hoch- oder Herunterskalieren des Netzwerkcontrollers Knoten Ihre Datacenter-Anforderungen bereit.

Obwohl Sie Netzwerkcontroller als Cluster für die einzelnen Computer bereitstellen können, müssen Sie aus für hohe Verfügbarkeit und Failover-Netzwerkcontroller in einem Cluster mit mindestens drei Computer mit mehreren Computern bereitstellen.

>[!NOTE]
>Sie können den Netzwerkcontroller bereitstellen, auf Servercomputern oder auf virtuellen Computern \(VMs\) , Windows Server 2016 Datacenter Edition ausgeführt werden. Wenn Sie den Netzwerkcontroller auf virtuellen Computern bereitstellen, müssen die virtuellen Computer auf Hyper-V-Hosts ausgeführt werden, die auch Datacenter Edition ausgeführt werden. Netzwerkcontroller ist nicht auf Windows Server 2016 Standard Edition verfügbar.

## <a name="network-controller-as-a-service-fabric-application"></a>Der Netzwerkcontroller als Service Fabric-Anwendung

Um hohe Verfügbarkeit und Skalierbarkeit zu erreichen, verwendet Service Fabric des Netzwerkcontrollers. Service Fabric bietet eine Plattform für verteilte Systeme zum Erstellen skalierbarer, zuverlässiger und Anwendungen problemlos verwalten.

Als Plattform bietet Service Fabric-Funktionen, die zum Erstellen von skalierbaren verteilten Systems erforderlich ist. Es bietet-Dienst hostet, auf mehrere Instanzen des Betriebssystems, Synchronisieren von Zustandsinformationen zwischen Instanzen Wahl führend, bei der fehlererkennung, Lastenausgleich und mehr.

>[!NOTE]
>Weitere Informationen zu Service Fabric in Azure finden Sie unter [Übersicht über Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Bei der Bereitstellung des Netzwerkcontrollers auf mehreren Computern wird des Netzwerkcontrollers als eine einzelne Service Fabric-Anwendung in einem Service Fabric-Cluster ausgeführt. Sie können Service Fabric-Cluster bilden, durch einen Satz von Instanzen des Betriebssystems zu verbinden.

Die Netzwerkcontroller-Anwendung besteht aus mehreren zustandsbehafteten Service Fabric-Diensten. Jeder Dienst ist für eine Netzwerkfunktion, z.B. physische netzwerkverwaltung, Verwalten des virtuellen Netzwerks, firewallverwaltung oder Verwalten des Gateways verantwortlich. 

Jeder Service Fabric-Dienst hat ein primäres Replikat und zwei sekundäre Replikate. Das primäre dienstreplikat verarbeitet Anforderungen, während die beiden Replikate für den sekundären Dienst hohen Verfügbarkeit unter Umständen zur Verfügung stellen, in dem das primäre Replikat aus irgendeinem Grund deaktiviert oder nicht verfügbar ist.

Die folgende Abbildung zeigt einen Network Controller Service Fabric-Cluster mit fünf Computern. Vier Diensten, die über die fünf Computer verteilt werden: Firewall-Service, Dienst, den Softwarelastenausgleich \(SLB\) Service und virtual Network \(Vnet\) Service.  Jede der vier Dienste umfasst eine primäre dienstreplikat und zwei sekundärer dienstreplikate.

![Netzwerk-Controller Service Fabric-cluster](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>Vorteile der Verwendung von Service Fabric

Es folgen die wichtigsten Vorteile für die Verwendung von Service Fabric für den Netzwerkcontroller-Cluster.

### <a name="high-availability-and-scalability"></a>Hohe Verfügbarkeit und Skalierbarkeit

Da Netzwerkcontroller den Kern der ein Netzwerk aus Datencentern aufgebaut ist, muss es sowohl robust gegenüber Fehlern und skalierbar genug, um agile Änderungen im Datencenter, Netzwerke im Laufe der Zeit zu ermöglichen. Die folgenden Features bieten diese Fähigkeiten: 

- **Schnelles Failover**. Service Fabric bietet extrem schnelles Failover. Mehrerer sekundärer dienstreplikate "Hot" sind immer verfügbar. Wenn bei einem Hardwareausfall eine Betriebssysteminstanz verfügbar sind, ist eines der sekundären Replikate sofort zum primären Replikat höher gestuft. 
- **Flexibilität der Skalierung**. Sie können schnell und einfach diese zuverlässige Dienste aus wenigen Instanzen auf Tausende von Instanzen skalieren, und anschließend wieder in ein paar-Instanzen je nach ressourcenanforderungen. 

### <a name="persistent-storage"></a>Dauerhafte Speicherung

Die Netzwerkcontroller-Anwendung muss es sich um große speicheranforderungen für die Konfiguration und Status. Die Anwendung muss auch über geplante und ungeplante Ausfälle verwendbar. Zu diesem Zweck bietet Service Fabric ein Schlüssel-Wert-Store \(KVS\) das ist eine replizierte, transaktionale und permanenten Speicher.

### <a name="modularity"></a>Modularität

Netzwerkcontroller ist mit einer modularen Architektur, mit den einzelnen Dienste des Netzwerks konzipiert, z. B. die Service für virtuelle Netzwerke und die Firewall-Dienstes, erstellt\-in als einzelne Dienste. 

Diese Architektur bietet die folgenden Vorteile.

1. Netzwerkcontroller, die Modularität unabhängige Entwicklung aller unterstützten Dienste ermöglicht eine höhere benötigen. Beispielsweise kann der Softwarelastenausgleich-Dienst aktualisiert werden, ohne Auswirkungen auf die anderen Dienste oder den normalen Betrieb des Netzwerkcontrollers.
2. Network Controller Modularität ermöglicht das Hinzufügen neuer Dienste an, der Weiterentwicklung des Netzwerks. Neue Dienste können in den Netzwerkcontroller hinzugefügt werden, ohne Auswirkungen auf vorhandene Dienste.

>[!NOTE]
>In Windows Server 2016 wird das Hinzufügen von Diensten von Drittanbietern für den Netzwerkcontroller nicht unterstützt.

Service Fabric-Modularität verwendet dienstschemas-Modell, um die Einfachheit der Entwicklung, Bereitstellung und Wartung einer Anwendungs zu maximieren.

## <a name="network-controller-deployment-options"></a>Optionen zur netzwerkbereitstellung Controller

Um die Bereitstellung des Netzwerkcontrollers mithilfe von System Center Virtual Machine Manager- \(VMM\), finden Sie unter [richten Sie eine SDN-Netzwerkcontroller im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Skripts finden Sie unter [Bereitstellen von Software definierte Netzwerk-Infrastruktur mithilfe von Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)

Weitere Informationen zu den Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](Network-Controller.md).