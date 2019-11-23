---
title: Gateway-Bandbreite-Zuordnung
description: ''
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: fc59fc9d7dc22b9c5567bae314b4312d76fcff19
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406126"
---
# <a name="gateway-bandwidth-allocation"></a>Gateway-Bandbreite-Zuordnung

>Gilt für: Windows Server

In Windows Server 2016 waren die einzelnen Tunnel Bandbreite für IPSec, GRE und L3 ein Verhältnis zur Gesamtkapazität des Gateways. Aus diesem Grund würden Kunden die gatewaykapazität basierend auf der TCP-Standard Bandbreite bereitstellen, die dies von der Gateway-VM erwartet.

Außerdem war die maximale IPSec-Tunnel Bandbreite auf dem Gateway auf (3/20)\*gatewaykapazität beschränkt, die vom Kunden bereitgestellt wurde. Wenn Sie also beispielsweise die gatewaykapazität auf 100 Mbit/s festlegen, beträgt die IPSec-Tunnel Kapazität 150 Mbit/s. Die entsprechenden Verhältnisse für GRE-und L3-Tunnel sind 1/5 bzw. 1/2.

Obwohl dies für den Großteil der bereit Stellungen funktionierte, war das Modell mit festem Verhältnis für Umgebungen mit hohem Durchsatz nicht geeignet. Auch wenn die Datenübertragungsraten hoch waren (z. b. höher als 40 Gbit/s), ist der maximale Durchsatz von Sdn-gatewaytunneln aufgrund interner Faktoren begrenzt.

In Windows Server 2019 wird für einen Tunneltyp der maximale Durchsatz korrigiert:

-   IPSec = 5 Gbit/s

-   GRE = 15 Gbit/s

-   L3 = 5 Gbit/s

Dies gilt auch, wenn der Gatewayhost/virtuelle Computer NICs mit viel höherem Durchsatz unterstützt, wird der maximale verfügbare Tunnel Durchsatz korrigiert. Ein weiteres Problem, das dies übernimmt, ist die willkürliche über Bereitstellung von Gateways, die bei der Bereitstellung einer sehr hohen Anzahl an gatewaykapazität erfolgt.

## <a name="gateway-capacity-calculation"></a>Berechnung der gatewaykapazität

Im Idealfall legen Sie die gatewaydurchsatz-Kapazität auf den Durchsatz fest, der für die Gateway-VM verfügbar ist. Wenn Sie z. b. über eine einzelne Gateway-VM verfügen und der zugrunde liegende Host-NIC-Durchsatz 25 Gbit/s beträgt, kann auch der gatewaydurchsatz auf 25 Gbit/s festgelegt werden.

Wenn Sie ein Gateway nur für IPSec-Verbindungen verwenden, beträgt die maximal verfügbare Kapazität 5 Gbit/s. Wenn Sie z. b. IPSec-Verbindungen auf dem Gateway bereitstellen, können Sie nur eine Aggregat Bandbreite (eingehend und ausgehend) als 5 Gbit/s bereitstellen.

Wenn Sie das Gateway sowohl für IPSec-als auch für GRE-Verbindungen verwenden, können Sie maximal 5 Gbit/s für den IPSec-Durchsatz oder maximal 15 Gbit/s des GRE-Durchsatzes Wenn Sie also beispielsweise 2 Gbit/s des IPSec-Durchsatzes bereitstellen, verfügen Sie über 3 Gbit/s für den IPSec-Durchsatz, der auf dem Gateway oder 9 Gbit/s für den GRE-Durchsatz verbleiben.

Um dies in mathematischen Begriffen zu platzieren:

- Gesamtkapazität des Gateways = 25 Gbit/s

- Verfügbare IPSec-Kapazität insgesamt = 5 Gbit/s (korrigiert)

- Verfügbare GRE-Kapazität insgesamt = 15 Gbit/s (korrigiert)

- IPSec-Durchsatz Verhältnis für dieses Gateway = 25/5 = 5 Gbit/s

- GRE-Durchsatz Verhältnis für dieses Gateway = 25/15 = 5/3 Gbit/s

Wenn Sie einem Kunden beispielsweise 2 Gbit/s IPSec-Durchsatz zuweisen:

Verbleibende verfügbare Kapazität auf dem Gateway = Gesamtkapazität des Gateways – IPSec-Durchsatz Verhältnis * zugeordneter IPSec-Durchsatz (verwendete Kapazität)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25 – 5 * 2 = 15 Gbit/s

Verbleibender IPSec-Durchsatz, den Sie auf dem Gateway zuordnen können 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5-2 = 3 Gbit/s

Verbleibender GRE-Durchsatz, den Sie dem Gateway zuweisen können = verbleibende Kapazität des Gateways/GRE-Durchsatz Verhältnisses 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;15 * 3/5 = 9 Gbit/s

Das Durchsatz Verhältnis variiert abhängig von der Gesamtkapazität des Gateways. Beachten Sie, dass Sie die Gesamtkapazität auf die TCP-Bandbreite festlegen müssen, die für die Gateway-VM verfügbar ist. Wenn Sie über mehrere virtuelle Computer verfügen, die auf dem Gateway gehostet werden, müssen Sie die Gesamtkapazität des Gateways entsprechend anpassen.

Wenn die gatewaykapazität geringer ist als die gesamte verfügbare Tunnel Kapazität, wird die gesamte verfügbare Tunnel Kapazität auf die gatewaykapazität festgelegt. Wenn Sie die gatewaykapazität beispielsweise auf 4 Gbit/s festlegen, wird die verfügbare Gesamtkapazität für IPSec, L3 und GRE auf 4 Gbit/s festgelegt, sodass das Durchsatz Verhältnis für jeden Tunnel auf 1 Gbit/s festgelegt wird.

## <a name="windows-server-2016-behavior"></a>Windows Server 2016-Verhalten

Der Algorithmus für die Kapazitäts Berechnung des Gateways für Windows Server 2016 bleibt unverändert. In Windows Server 2016 war die maximale IPSec-Tunnel Bandbreite auf (3/20)\*Gateway-Kapazität auf einem Gateway beschränkt. Die entsprechenden Verhältnisse für GRE-und L3-Tunnel waren 1/5 bzw. 1/2.

Wenn Sie ein Upgrade von Windows Server 2016 auf Windows Server 2019 durchführen:

1.  **GRE-und L3-Tunnel:** Die Windows Server 2019-Zuordnungs Logik tritt in Kraft, sobald die Netzwerk Controller Knoten auf Windows Server 2019 aktualisiert werden.

2.  **IPSec-Tunnel:** Die Windows Server 2016-gatewayzuordnungs-Logik funktioniert weiterhin, bis alle Gateways im gatewaypool auf Windows Server 2019 aktualisiert werden. Für alle Gateways im gatewaypool müssen Sie den Azure-Gatewaydienst auf " **automatisch**" festlegen.

>[!NOTE]
>Es ist möglich, dass ein Gateway nach dem Upgrade auf Windows Server 2019 überbelegt wird (da die Zuordnungs Logik von Windows Server 2016 zu Windows Server 2019 geändert wird). In diesem Fall sind die vorhandenen Verbindungen auf dem Gateway weiterhin vorhanden. Die Rest-Ressource für das Gateway löst eine Warnung aus, dass das Gateway über-bereitgestellt wird. In diesem Fall sollten Sie einige Verbindungen zu einem anderen Gateway verschieben.

---