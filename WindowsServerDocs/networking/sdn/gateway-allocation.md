---
title: Gateway-Bandbreite-Zuordnung
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: 3c259b96e1a8ee27888a5cccc50b285a2f7cb8c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850431"
---
# <a name="gateway-bandwidth-allocation"></a>Gateway-Bandbreite-Zuordnung

>Gilt für: Windows Server

In Windows Server 2016 wurde die einzelne tunnelbandbreite für die IPSec-GRE und L3 ein Verhältnis der Gesamtanzahl gatewaykapazität. Aus diesem Grund würden Kunden die gatewaykapazität basierend auf der standardmäßigen TCP-Bandbreite, die erwartet wird dies von der Gateway-VM bereitstellen.

Maximale IPSec-tunnelbandbreite auf dem Gateway wurde auch auf (3/20) begrenzt\*Gatewaykapazität, die vom Kunden bereitgestellt. Also z. B. wäre wenn Sie die gatewaykapazität auf 100 Mbit/s festgelegt haben, klicken Sie dann die Kapazität der IPsec-Tunnel 150 Mbit/s. Die entsprechenden Verhältnisse für GRE und L3-Tunnel sind 1/5 "und" 1/2, bzw.

Obwohl dies für den Großteil der Bereitstellungen gearbeitet haben, ist das Modell festgelegtes Verhältnis nicht geeignet für Umgebungen mit hohem Durchsatz. Auch wenn die Kosten für Datenübertragungen hoher wurden (z. B. mehr als 40 Gbit/s), den maximalen Durchsatz des SDN-Gateway-Tunnel aufgrund interner Faktoren begrenzt.

In Windows Server-2019 ist für einen Tunneltyp, der maximale Durchsatz behoben:

-   IPsec = 5 Gbit/s

-   GRE = 15 Gbps

-   L3 = 5 Gbit/s

Also auch wenn Ihre Gateway-Host/VM-NICs mit viel höheren Durchsatz unterstützt, ist der Durchsatz von maximal verfügbaren Tunnel fest. Ein weiteres Problem, die, dem dies erledigt, ist nach dem Zufallsprinzip Gateways, findet die übermäßige Bereitstellung der Fall, wenn eine sehr hohe Anzahl für die gatewaykapazität bereitstellen.

## <a name="gateway-capacity-calculation"></a>Berechnung der Gateway-Kapazität

Im Idealfall legen Sie die Durchsatzkapazität des Gateways, um den Durchsatz für die Gateway-VM verfügbar. Daher kann z. B. Wenn Sie ein einzelnes Gateway-VM und der zugrunde liegenden Host-NIC-Durchsatz 25 Gbit/s ist, die Gateway-Durchsatz bis 25 Gbit/s sowie festgelegt werden.

Wenn Sie einen Gateway nur für die IPsec-Verbindungen verwenden, ist die maximale Kapazität des verfügbaren feste 5 Gbit/s an. Also z. B. können Wenn Sie IPsec-Verbindungen auf dem Gateway bereitstellen, Sie nur auf eine aggregierte Bandbreite (eingehende und ausgehende) als 5 Gbit/s bereitstellen.

Wenn Sie das Gateway für sowohl IPSec- und GRE-Verbindungen verwenden möchten, können Sie maximal 5 Gbit/s von IPsec-Durchsatz oder maximal 15 Gbit/s von GRE-Durchsatz bereitstellen. Wenn Sie 2 Gbit/s von IPsec-Durchsatz bereitstellen, Sie müssen also beispielsweise 3 Gbit/s von IPsec-Durchsatz, die Links für die Bereitstellung auf dem Gateway oder 9 Gbit/s von GRE-Durchsatz verlassen.

In mehr mathematischen Begriffen ausgedrückt:

- Gesamtkapazität des Gateways = 25 Gbit/s

- Verfügbare Gesamtkapazität zu IPsec = 5 Gbit/s (fest)

- Verfügbare Gesamtkapazität zu GRE = 15 Gbit/s (fest)

- IPSec-Durchsatzverhältnis für dieses Gateway = 25/5 = 5 Gbit/s

- GRE-Durchsatzrate für dieses Gateway = 25/15 = 5/3 Gbit/s

Wenn beispielsweise ein Kunde 2 Gbit/s von IPsec-Durchsatz zuweisen:

Verfügbare Kapazität auf dem Gateway verbleibende = Gesamtkapazität des-Gateways – Verhältnis der IPsec-Durchsatz * IPSec-Durchsatz (verwendeten Kapazität) zugeordnet,

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25: 5 * 2 = 15 Gbit/s

Verbleibende IPsec-Durchsatz, der auf dem Gateway zugewiesen werden kann 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5-2 = 3 Gbit/s

Verbleibende GRE-Durchsatz, der auf dem Gateway zugewiesen werden können = verbleibende Kapazität des Verhältnisses der Gateway-GRE-Durchsatz 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;15 * 3/5 = 9 Gbit/s

Das Durchsatzverhältnis variiert abhängig von der Gesamtkapazität des Gateways. Dabei ist zu beachten ist, dass Sie die gesamte Kapazität, auf die TCP-Bandbreite für die Gateway-VM verfügbar festlegen sollten. Wenn Sie mehrere virtuelle Computer gehostet wird, auf dem Gateway haben, müssen Sie die Gesamtkapazität des Gateways entsprechend anpassen.

Darüber hinaus: ist die gatewaykapazität kleiner als die Kapazität des insgesamt verfügbaren Tunnel, wird die gesamte verfügbare Tunnel Kapazität auf die gatewaykapazität festgelegt. Z. B. Wenn Sie die gatewaykapazität bis 4 Gbit/s festgelegt, ist die gesamte verfügbare Kapazität für GRE, IPsec und L3-bis 4 Gbit/s, festgelegt das Durchsatzverhältnis für jeden Tunnel 1 Gbit/s zu überlassen.

## <a name="windows-server-2016-behavior"></a>Windows Server 2016-Verhalten

Das Gateway Kapazität Berechnungsalgorithmus für Windows Server 2016 bleibt unverändert. In Windows Server 2016, maximale-IPsec-tunnelbandbreite auf (3/20) begrenzt war\*gatewaykapazität für ein Gateway. Die entsprechenden Verhältnisse für GRE und L3-Tunnel wurden 1/5 "und" 1/2, bzw.

Wenn Sie von Windows Server 2016 auf Windows Server-2019 aktualisieren:

1.  **GRE und L3-Tunnel:** Die Logik der 2019 für Windows Server-Zuordnung wird wirksam, nachdem der Netzwerkcontroller-Knoten zum Windows Server-2019 aktualisiert

2.  **IPSec-Tunnel:** Der Windows Server 2016-gatewaylogik Zuordnung weiterhin funktioniert, bis alle Gateways in den gatewaypool, um Windows Server-2019 aktualisiert. Für alle Gateways in den gatewaypool, müssen Sie den Azure-Gateway-Dienst festlegen, um **automatische**.

>[!NOTE]
>Es ist möglich, die nach dem Upgrade auf Windows Server-2019 ein Gateway Übermaß (wie die Logik für die Zuordnung von Windows Server 2016, Windows Server-2019 geändert wird). In diesem Fall weiterhin die vorhandenen Verbindungen auf dem Gateway vorhanden. Die REST-Ressource für das Gateway löst eine Warnung, dass das Gateway Übermaß ist. In diesem Fall sollten Sie einige Verbindungen zu einer anderen Gateway verschieben.

---