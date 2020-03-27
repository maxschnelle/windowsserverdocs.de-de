---
title: Netzwerkcontroller – Hohe Verfügbarkeit
description: In diesem Thema erfahren Sie mehr über die Netzwerk Controller-Hochverfügbarkeit für Software-Defined Networking (SDN) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ce3a0dd33ff105fa7cc36305048b8a311577aa21
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317067"
---
# <a name="network-controller-high-availability"></a>Netzwerkcontroller – Hohe Verfügbarkeit

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Netzwerk Controller-Hochverfügbarkeit und Skalierbarkeits Konfiguration für Software-Defined Networking \(Sdn-\).

Wenn Sie Sdn in Ihrem Rechenzentrum bereitstellen, können Sie mithilfe des Netzwerk Controllers viele Netzwerkelemente zentral bereitstellen, überwachen und verwalten, darunter RAS-Gateways, Software Lastenausgleich, Richtlinien für virtuelle Netzwerke für Mandanten Kommunikation, Datacenter Firewall-Richtlinien, Quality of Service \(QoS\) für Sdn-Richtlinien, Hybrid Netzwerk Richtlinien usw.

Da der Netzwerk Controller der Eckpfeiler der Sdn-Verwaltung ist, ist es wichtig, dass Netzwerk Controller Bereitstellungen Hochverfügbarkeit bereitstellen und die Netzwerk Controller Knoten problemlos zentral hoch-oder herunterskaliert werden können.

Obwohl Sie den Netzwerk Controller als Cluster mit einem einzelnen Computer bereitstellen können, müssen Sie für Hochverfügbarkeit und Failover den Netzwerk Controller in einem Cluster mit mehreren Computern mit mindestens drei Computern bereitstellen.

>[!NOTE]
>Sie können den Netzwerk Controller entweder auf Server Computern oder auf virtuellen Computern \(VMS\) bereitstellen, auf denen Windows Server 2016 Datacenter Edition ausgeführt wird. Wenn Sie einen Netzwerk Controller auf virtuellen Computern bereitstellen, müssen die VMs auf Hyper-V-Hosts ausgeführt werden, auf denen auch die Datacenter Edition ausgeführt wird. Der Netzwerk Controller ist unter Windows Server 2016 Standard Edition nicht verfügbar.

## <a name="network-controller-as-a-service-fabric-application"></a>Netzwerk Controller als Service Fabric Anwendung

Zum Erreichen von Hochverfügbarkeit und Skalierbarkeit basiert der Netzwerk Controller auf Service Fabric. Service Fabric bietet eine Plattform für verteilte Systeme zum Erstellen skalierbarer, zuverlässiger und einfach verwalteter Anwendungen.

Als Plattform bietet Service Fabric Funktionen, die zum Aufbau eines skalierbaren verteilten Systems erforderlich sind. Sie ermöglicht das Hosting von Diensten auf mehreren Betriebssystem Instanzen, das Synchronisieren von Zustandsinformationen zwischen Instanzen, das Überprüfen von Spitzen, Fehlererkennung, Lastenausgleich und mehr.

>[!NOTE]
>Informationen zu Service Fabric in Azure finden Sie unter [Übersicht über Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Wenn Sie den Netzwerk Controller auf mehreren Computern bereitstellen, wird der Netzwerk Controller als einzelne Service Fabric Anwendung auf einem Service Fabric Cluster ausgeführt. Sie können einen Service Fabric Cluster erstellen, indem Sie eine Gruppe von Betriebssystem Instanzen verbinden.

Die Netzwerk Controller Anwendung besteht aus mehreren Zustands behafteten Service Fabric-Diensten. Jeder Dienst ist für eine Netzwerkfunktion zuständig, wie z. b. die physische Netzwerkverwaltung, die Verwaltung virtueller Netzwerke, die Firewallverwaltung oder die Gatewayverwaltung. 

Jeder Service Fabric Dienst verfügt über ein primäres Replikat und zwei sekundäre Replikate. Das primäre Dienst Replikat verarbeitet Anforderungen, während die beiden sekundären Dienst Replikate Hochverfügbarkeit bieten, wenn das primäre Replikat aus irgendeinem Grund deaktiviert oder nicht verfügbar ist.

In der folgenden Abbildung wird ein Netzwerk Controller Service Fabric Cluster mit fünf Computern dargestellt. Vier Dienste werden auf die fünf Computer verteilt: Firewalldienst, Gatewaydienst, Software Lastenausgleich \(SLB-\) Dienst und virtuelles Netzwerk \(vnet\)-Dienst.  Jeder der vier Dienste umfasst ein primäres Dienst Replikat und zwei sekundäre Dienst Replikate.

![Netzwerk Controller Service Fabric-Cluster](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>Vorteile der Verwendung von Service Fabric

Im folgenden sind die Hauptvorteile der Verwendung von Service Fabric für Netzwerk Controller Cluster zu finden.

### <a name="high-availability-and-scalability"></a>Hohe Verfügbarkeit und Skalierbarkeit

Da der Netzwerk Controller das Kernstück eines Rechenzentrums Netzwerks ist, muss es beide anfällig für Ausfallzeiten und skalierbar sein, um Agile Änderungen in Rechenzentrums Netzwerken über einen Zeitraum zuzulassen. Die folgenden Funktionen bieten folgende Möglichkeiten: 

- **Schnelles Failover**. Service Fabric bietet ein sehr schnelles Failover. Es sind immer mehrere heiße sekundäre Dienst Replikate verfügbar. Wenn eine Betriebssystem Instanz aufgrund eines Hardwarefehlers nicht mehr verfügbar ist, wird eines der sekundären Replikate sofort zum primären Replikat herauf gestuft. 
- **Agilität der Skalierung**. Sie können diese zuverlässigen Dienste problemlos und schnell von einigen wenigen Instanzen bis zu Tausenden von Instanzen skalieren und dann je nach Ihren Ressourcenanforderungen auf einige Instanzen zurücksetzen. 

### <a name="persistent-storage"></a>Permanenter Speicher

Die Netzwerk Controller Anwendung hat große Speicheranforderungen für die Konfiguration und den Status. Die Anwendung muss auch für geplante und ungeplante Ausfälle verwendbar sein. Zu diesem Zweck stellt Service Fabric einen Schlüssel-Wert-Speicher \(KVS\) dar, bei dem es sich um einen replizierten, transaktionalen und beibehaltenen Speicher handelt.

### <a name="modularity"></a>Modularität

Der Netzwerk Controller wurde mit einer modularen Architektur entworfen, wobei jeder der Netzwerkdienste (z. b. der Dienst für virtuelle Netzwerke) und der Firewalldienst, der in als einzelner Dienst\-erstellt wurde. 

Diese Anwendungsarchitektur bietet die folgenden Vorteile:

1. Die Netzwerk Controller-Modularität ermöglicht die unabhängige Entwicklung der einzelnen unterstützten Dienste, wenn sich die Anforderungen weiterentwickeln. Beispielsweise kann der Software Lastenausgleich-Dienst aktualisiert werden, ohne dass dies Auswirkungen auf andere Dienste oder den normalen Betrieb des Netzwerk Controllers hat.
2. Durch die Netzwerk Controller-Modularität können neue Dienste hinzugefügt werden, wenn sich das Netzwerk weiterentwickelt. Neue Dienste können dem Netzwerk Controller ohne Beeinträchtigung vorhandener Dienste hinzugefügt werden.

>[!NOTE]
>In Windows Server 2016 wird das Hinzufügen von Drittanbieter Diensten zum Netzwerk Controller nicht unterstützt.

Service Fabric modulität verwendet Dienstmodell Schemas, um die einfache Entwicklung, Bereitstellung und Wartung einer Anwendung zu maximieren.

## <a name="network-controller-deployment-options"></a>Optionen für die Netzwerk Controller Bereitstellung

Informationen zum Bereitstellen eines Netzwerk Controllers mithilfe System Center Virtual Machine Manager \(VMM-\)finden Sie unter [Einrichten eines Sdn-Netzwerk Controllers im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Informationen zum Bereitstellen eines Netzwerk Controllers mithilfe von Skripts finden Sie unter Bereitstellen [einer Software definierten Netzwerkinfrastruktur mit Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

Informationen zum Bereitstellen eines Netzwerk Controllers mit Windows PowerShell finden Sie unter Bereitstellen eines [Netzwerk Controllers mit Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md) .

Weitere Informationen zum Netzwerk Controller finden Sie unter [Netzwerk Controller](Network-Controller.md).