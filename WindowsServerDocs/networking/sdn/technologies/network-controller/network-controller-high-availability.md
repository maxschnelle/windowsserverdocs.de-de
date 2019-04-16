---
title: Netzwerk-Controller mit hoher Verfügbarkeit
description: In diesem Thema können Sie Informationen zu Netzwerkcontroller hohe Verfügbarkeit für die Software Defined Networking (SDN) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f260f3e4d8ca5fcd998824327478c2fbe3c81875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller-high-availability"></a>Netzwerk-Controller mit hoher Verfügbarkeit

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Netzwerkcontroller hohe Verfügbarkeit und Skalierbarkeit Konfiguration für die Software Defined Networking \(SDN\) Informationen.

Wenn Sie in Ihrem Rechenzentrum SDN bereitstellen, können Sie Netzwerkcontroller zentral bereitstellen, überwachen und Verwalten von vielen Netzwerkelemente, z. B. RAS-Gateways, Software Load Balancers, virtuelle Netzwerkrichtlinien für Mandanten Kommunikation, Datacenter Firewall-Richtlinien, Quality of Service \(QoS\) SDN-Richtlinien, Hybrid-Netzwerkrichtlinien und vieles mehr.

Da Netzwerkcontroller das Herzstück der SDN-Verwaltung ist, ist es wichtig für Netzwerkcontroller Bereitstellungen mit hoher Verfügbarkeit und die Möglichkeit für Sie so leicht nach oben oder unten Netzwerkcontroller Knoten mit Ihren Bedürfnissen Datencenter bereitstellen.

Obwohl Sie Netzwerkcontroller als Cluster für die einzelnen Computer bereitstellen können, müssen für hohe Verfügbarkeit und Failover Sie Netzwerkcontroller in einem Cluster mit mehreren Computern mit mindestens drei Computer bereitstellen.

>[!NOTE]
>Auf beiden Servern oder auf virtuellen Maschinen \(VMs\), auf denen Windows Server 2016 Datacenter Edition ausgeführt werden, können Sie Netzwerkcontroller bereitstellen. Wenn Sie Netzwerkcontroller auf virtuellen Computern bereitstellen, müssen die virtuellen Maschinen auf Hyper-V-Hosts ausgeführt werden, die auch Datacenter Edition ausgeführt wird. Netzwerkcontroller ist nicht in Windows Server 2016 Standard Edition zur Verfügung.

## <a name="network-controller-as-a-service-fabric-application"></a>Netzwerkcontroller als Service Fabric-Anwendung

Um eine hohe Verfügbarkeit und Skalierbarkeit zu erzielen, nutzt Netzwerkcontroller Service Fabric. Service Fabric bietet eine Plattform verteilte Systeme erstellen skalierbarer, zuverlässig und leicht zu verwaltendes Anwendungen.

Als eine Plattform bietet Service Fabric-Funktionen, die für die Erstellung einer skalierbare verteilte Systeme erforderlich ist. Es enthält-Dienst hostet, auf mehrere Instanzen von Betriebssystem, Synchronisieren von Informationen zwischen Instanzen Benutzerzahl führend, Erkennen eines Startfehlers, Lastenausgleich und vieles mehr.

>[!NOTE]
>Informationen zu Service Fabric in Azure, finden Sie unter [Übersicht der Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Wenn Sie Netzwerkcontroller auf mehreren Computern bereitstellen, wird Netzwerkcontroller als eine einzelne Service Fabric-Anwendung auf einem Service Fabric-Cluster ausgeführt. Sie können einen Service Fabric-Cluster bilden, durch eine Reihe von Betriebssysteminstanzen verbinden.

Die Netzwerk-Controller-Anwendung umfasst mehrere zustandsbehaftete Service Fabric-Dienste. Jeder Dienst ist verantwortlich für eine Netzwerkfunktion, z. B. des physischen Netzwerks des virtuellen Netzwerks, Firewall oder den Gateway-Management. 

Jeder Service Fabric-Dienst verfügt über eine primäre Replikat und zwei sekundäre Replikate. Das Replikat primären Dienst verarbeitet Anforderungen, die zwei sekundäre Service Replikate mit hoher Verfügbarkeit unter Umständen bereit, in dem das primäre Replikat aus irgendeinem Grund deaktiviert oder nicht verfügbar ist.

Die folgende Abbildung zeigt einen Netzwerk-Controller Service Fabric-Cluster mit fünf Computern. Vier Dienste auf diese fünf Computer verteilt werden: Firewall-Dienst, Gatewaydienst, Lastenausgleich \(SLB\) Service und virtuellen \(Vnet\) Netzwerkdienst.  Die vier Dienste enthält ein Replikat der primären Dienst und zwei sekundäre Replikate.

![Netzwerk-Controller Service Fabric-cluster](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>Vorteile der Verwendung von Service Fabric

Im folgenden werden die wichtigsten Vorteile für die Verwendung von Service Fabric für Netzwerkcontroller Cluster.

### <a name="high-availability-and-scalability"></a>Hohe Verfügbarkeit und Skalierbarkeit

Da Netzwerkcontroller das Kernstück von einem rechenzentrumsnetzwerk ist, muss es sowohl flexibel in Bezug auf Fehler und skalierbar agile Änderungen im Datencenter-Netzwerke mit der Zeit zu ermöglichen. Die folgenden Features bieten diese Möglichkeiten: 

- **Schnelles Failover**. Service Fabric bietet extrem schnelles Failover. Mehrere hot sekundäre Replikate sind immer verfügbar. Wenn eine Betriebssystem-Instanz aufgrund eines Hardwarefehlers nicht verfügbar ist, wird eine sekundäre Replikate sofort auf das primäre Replikat heraufgestuft. 
- **Flexibilität der Skalierung**. Sie können schnell und einfach skaliert diese zuverlässige Dienste in einigen Fällen bis zu Tausende von Instanzen und dann wieder nach unten für einige Instanzen je nach Bedarf Ressource. 

### <a name="persistent-storage"></a>Permanenten Speicher

Die Anwendung Netzwerkcontroller hat großen speicheranforderungen für die Konfiguration und den Status. Die Anwendung muss über geplante und ungeplante Ausfälle auch verwendet werden. Zu diesem Zweck bietet Service Fabric ein Schlüssel-Wert-Speicher-\(KVS\), das einen replizierten, Transaktions- und dauerhaften Speicher ist.

### <a name="modularity"></a>Modularität

Netzwerkcontroller ist eine modulare Architektur, mit jeder der Netzwerkdienste, z. B. virtuelle Netzwerke und Firewall-Dienst, integrierten eingehend als einzelne Dienste ausgelegt. 

Diese Anwendungsarchitektur bietet die folgenden Vorteile.

1. Netzwerkcontroller Modularität als unabhängige Entwicklung der einzelnen unterstützten Dienste ermöglicht muss weiterentwickelt. Beispielsweise kann der Lastenausgleichsdienst für Software ohne Auswirkung auf die Dienste oder den normalen Betrieb des Netzwerkcontroller aktualisiert werden.
2. Network Controller Modularität ermöglicht das Hinzufügen neuer Dienste im Netzwerk weiterentwickelt. Neue Dienste können ohne Auswirkungen auf vorhandene Dienste Netzwerkcontroller hinzugefügt werden.

>[!NOTE]
>Das Hinzufügen von Drittanbieter-Diensten auf Netzwerk-Controller ist in Windows Server 2016 nicht unterstützt.

Service Fabric Modularität verwendet Service-Modell Schemas, um die einfache Entwicklung, Bereitstellung und Wartung einer Anwendung zu maximieren.

## <a name="network-controller-deployment-options"></a>Netzwerk-Controller-Bereitstellungsoptionen

Zum Bereitstellen von Netzwerkcontroller mithilfe von System Center Virtual Machine Manager-\(VMM\) finden Sie unter [richten Sie ein SDN-Netzwerkcontroller in der VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Skripts finden Sie unter [Bereitstellen einer Software definiert Netzwerk-Infrastruktur mithilfe von Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)

Weitere Informationen zu dem Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](Network-Controller.md).