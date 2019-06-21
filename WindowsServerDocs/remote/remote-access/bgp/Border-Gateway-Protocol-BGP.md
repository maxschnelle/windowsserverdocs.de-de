---
title: Border Gateway Protocol (BGP)
description: Sie können in diesem Thema verwenden, um ein Verständnis des Border Gateway Protocol (BGP) in Windows Server 2016, einschließlich Bereitstellungstopologien für die BGP-Unterstützung und BGP-Features und Funktionen zu erhalten.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78cc2ce3-a48e-45db-b402-e480b493fab1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 655a7b02468db4246b85b495289806a3f9735a95
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282004"
---
# <a name="border-gateway-protocol-bgp"></a>Border Gateway Protocol (BGP)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erhalten Sie Informationen zum Verständnis des Border Gateway Protocol (BGP), einschließlich Bereitstellungstopologien mit BGP-Unterstützung und BGP-Features sowie -Funktionen.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema wird die folgende Dokumentation zum BGP verfügbar.  
>   
> -   [BGP-Befehlsreferenz für Windows PowerShell](../../remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [BGP unterstützt Bereitstellungstopologien](#bkmk_top)  
  
-   [BGP-Funktionen](#bkmk_features)  
  
Wenn auf einem Windows Server 2016 RAS-Dienst konfiguriert \(RAS\) Gateway im mehrinstanzenmodus, Border Gateway Protocol (BGP) bietet Ihnen die Möglichkeit zum Verwalten des Routings von Netzwerkdatenverkehr zwischen Ihrem Mandanten-VM-Netzwerken und Remotestandorten. Sie können auch BGP verwenden, für die einzelnen Mandanten RAS-Gateway-Bereitstellungen, und beim Bereitstellen von Remotezugriff als ein lokales Netzwerk \(LAN\) Router.  
  
BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind.  
  
Um BGP-routing zu verwenden, müssen Sie installieren die **RAS-Dienst \(RAS\)**  bzw. die **Routing** Rollendienst der Remotezugriffs-Serverrolle auf einem Computer oder virtuellen Computer \(VM\) -hängt von der Art des Systems, die Sie verwenden, und zwar unabhängig davon, ob Sie eine mehrinstanzenfähige Bereitstellung haben:  
  
-   Bei einer mehrinstanzenfähigen Bereitstellung empfiehlt es sich, dass Sie das RAS-Gateway auf einer oder mehreren VMs installieren. Verwenden mehrerer VMs bietet hohe Verfügbarkeit. Das RAS-Gateway ist in der Lage, mehrere Verbindungen von mehreren Mandanten verarbeiten und besteht aus einem Hyper-V-Host und einem virtuellen Computer, der das Gateway tatsächlich konfiguriert ist. Dieses Gateway mit Standort-zu-Standort-VPN-Verbindungen konfiguriert ist, als mehrinstanzenfähiger BGP-Router zu Exchange-Mandanten und Cloud-Dienstanbieter \(CSP\) Subnetzrouten.  
  
-   Für einen einzelnen Mandanten Edge-Gateway-Bereitstellung oder die Bereitstellung einer LAN-Router können Sie das RAS-Gateway auf einem physischen Computer oder einem virtuellen Computer installieren.  
  
> [!IMPORTANT]  
> Bei der Installation eines RAS-Gateways müssen Sie angeben, ob BGP für jeden Mandanten, mithilfe aktiviert ist der **Enable-RemoteAccessRoutingDomain** Windows PowerShell-Befehl mit der **Typ** Parameterwert  **Alle**. Um den Remotezugriff als LAN aktiviertem BGP-Router ohne mandantenfähigen Funktionen zu installieren, können Sie den Befehl **Install-RemoteAccess--- VpnType RoutingOnly**.  
>   
> Der folgende Beispielcode veranschaulicht, wie zum Installieren von RAS im mehrinstanzenmodus mit allen RAS-Funktionen (Punkt-zu-Standort-VPN-Standort-zu-Standort-VPN und BGP routing) für zwei Mandanten, Contoso und Fabrikam aktiviert.  
  
```  
$Contoso_RoutingDomain = "ContosoTenant"  
$Fabrikam_RoutingDomain = "FabrikamTenant"  
  
Install-RemoteAccess -MultiTenancy  
  
Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru  
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru  
```  
  
## <a name="bkmk_top"></a>BGP unterstützt Bereitstellungstopologien  
Im Folgenden sind die unterstützten Bereitstellungstopologien aufgeführt, bei denen Unternehmensstandorte mit einem Cloud Service Provider (CSP)-Datencenter verbunden sind.  
  
In allen Szenarien ist das CSP-Gateway ein Windows Server 2016-RAS-Gateway am Rand. Der RAS-Gateway, mehrere Verbindungen von mehreren Mandanten verarbeiten kann, besteht aus einem Hyper-V-Host und einem virtuellen Computer, der das Gateway tatsächlich konfiguriert ist. Dieses Edgegateway wird als mehrinstanzenfähiger BGP-Router für den Austausch von Unternehmens- und CSP-Subnetzrouten mit Standort-zu-Standort-VPN-Verbindungen konfiguriert.  
  
Mandanten stellen eine Verbindung mit ihren Ressourcen im CSP-Datencenter mithilfe einer Standort-zu-Standort-(S2S)-VPN-Verbindung her. Darüber hinaus wird das BGP-Routingprotokoll für dynamischen Routinginformationsaustausch zwischen den Unternehmens- und den CSP-Gateways bereitgestellt.  
  
Die folgenden Bereitstellungstopologien werden unterstützt.  
  
-   [RAS-VPN-Standort-zu-Standort-Gateway mit BGP am Unternehmensstandort](#bkmk_top1)  
  
-   [Drittanbietergateway mit BGP am Unternehmensstandort](#bkmk_top2)  
  
-   [Mehrere Unternehmensstandorte mit drittanbietergateways](#bkmk_top3)  
  
-   [Separate Endpunkte für BGP und VPN](#bkmk_top4)  
  
Die folgenden Abschnitte enthalten weitere Informationen über die einzelnen unterstützten BGP-Topologien.  
  
### <a name="bkmk_top1"></a>RAS-VPN-Standort-zu-Standort-Gateway mit BGP am Unternehmensstandort  
Diese Topologie stellt einen mit einem CSP verbundene Unternehmensstandort dar. Die unternehmensroutingtopologie enthält einen internen Router, Windows Server 2016-RAS-Gateway-Konfiguration für VPN-Standort-zu-Standort-Verbindungen mit den CSP, und ein edgefirewallgerät. Das RAS-Gateway beendet die S2S-VPN und BGP-Verbindungen.  
  
![RAS-VPN-Standort-zu-Standort-Gateway](../../media/Border-Gateway-Protocol-BGP/bgp_01.jpg)  
  
Beide Standorte sind mittels externem Border Gateway Protocol (eBGP) verbunden, das Informationen zwischen BGP-fähigen Routern in separaten autonomen Systemen (AS) übertragen kann. Dazu müssen sowohl das Unternehmen als auch der CSP unterschiedliche autonome Systemnummern (ASN) besitzen. Dies ist ein Parameter, der integraler Bestandteil des BGP-Protokolls ist.  
  
In diesem Szenario funktioniert BGP auf folgende Weise.  
  
-   Das Edgegerät des Unternehmensstandorts erlernt mithilfe von BGP die virtualisierten Subnetzrouten (10.2.1.0/24), die in der Cloud gehostet werden. Dieses Gerät kündigt auch die lokalen Subnetzrouten (10.1.1.0/24), die mehrinstanzenfähige CSP-RAS-Gateway.  
  
-   Der Edgerouter des Kunden lernt lokale interne Routen über einen der folgenden Mechanismen:  
  
    -   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Beispiel 10.1.1.0/24). In der Zwischenzeit lernt der interne Router externe Routen (z. B. 10.2.1.0/24) vom Edgegerät, und der interne Router muss diese Routen an andere lokale Router über ein internes Gatewayprotokoll (IGP), wie z. B. OSPF (Open Shortest Path First) oder Routing Information-Protokoll (RIP), verteilen.  
  
    -   Das Edgegerät kann mit statischen Routen oder Schnittstellen zur Auswahl von Routen für die Ankündigung mithilfe von BGP konfiguriert werden. Das Edgegerät verteilt die externen Routen mit einem IGP auch an andere lokale Router.  
  
### <a name="bkmk_top2"></a>Drittanbietergateway mit BGP am Unternehmensstandort  
Diese Topologie stellt einen Unternehmensstandort dar, der mit einem Edgerouter eines Drittanbieters eine Verbindung mit einem CSP herstellt. Der Edgerouter dient auch als Standort-zu-Standort-VPN-Gateway.  
  
![Drittanbietergateway mit BGP an der Unternehmensstandortedge](../../media/Border-Gateway-Protocol-BGP/bgp_02.jpg)  
  
Der Unternehmensedgerouter lernt lokale interne Routen mit einem der folgenden Mechanismen:  
  
-   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Fall 10.1.1.0/24)  
  
-   Das Edgegerät implementiert ein internes Gatewayprotokoll (IGP) und ist direkt am internen Routing beteiligt.  
  
### <a name="bkmk_top3"></a>Mehrere Unternehmensstandorte mit CSP cloud-Datencenter  
Diese Topologie stellt mehrere Unternehmensstandorte dar, die mit einem Edgerouter eines Drittanbieters eine Verbindung mit einem CSP herstellen. Die Edgegeräte der Drittanbieter dienen als Standort-zu-Standort-VPN-Gateways und BGP-Router.  
  
![Mehrere Unternehmensstandorte mit CSP cloud-Datencenter](../../media/Border-Gateway-Protocol-BGP/bgp_03.jpg)  
  
Die Edgerouter des Kunden lernen lokale interne Routen mit einem der folgenden Mechanismen:  
  
-   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Fall 10.1.1.0/24)  
  
-   Das Edgegerät implementiert ein internes Gatewayprotokoll (IGP) und ist direkt am internen Routing beteiligt.  
  
Jeder Unternehmensstandort lernt die Routen vom anderen Standort über die direkte eBGP-Verbindung.  
  
Jeder Unternehmensstandort lernt die gehosteten Netzwerkrouten direkt und über den anderen Unternehmensstandort, wählt jedoch die optimale Route auf Grundlage der Kosten der Route aus.  
  
Wenn der BGP-Router am Unternehmensstandort 1 mit dem Enterprise-Website 2 BGP-Router verbinden kann, da die Verbindung fehlgeschlagen ist, der Standort 1 BGP-Router beginnt dynamisch die Routen mit Enterprise-Website-2-Netzwerk zu lernen, aus der BGP-Router des CSP und der Datenverkehr wird nahtlos umgeleitet von Standort 1 zu Standort 2 über den Windows Server-BGP-Router an den CSP.  
  
### <a name="bkmk_top4"></a>Separate Endpunkte für BGP und VPN  
Diese Topologie stellt ein Unternehmen dar, das zwei verschiedene Router als BGP- und Standort-zu-Standort-VPN-Endpunkte verwendet. Standort-zu-Standort-VPN wird auf dem Windows Server 2016 RAS-Gateway beendet, während BGP auf einem internen Router beendet wird. Auf der CSP-Seite der Verbindungen beendet der CSP sowohl VPN-als auch BGP-Verbindungen mit dem RAS-Gateway. Bei dieser Konfiguration muss die interne Drittanbieter-Routerhardware die Umverteilung von IGP-Routen an BGP sowie von BGP-Routen an IGP unterstützen.  
  
![Separate Endpunkte für BGP und VPN](../../media/Border-Gateway-Protocol-BGP/bgp_04.jpg)  
  
Der interne Router lernt Unternehmensrouten mit einem der folgenden Mechanismen:  
  
-   BGP  
  
-   Ein internes Gatewayprotokoll (IGP), wie z. B. OSPF oder RIP.  
  
-   Statische Routenkonfiguration  
  
Wenn am Unternehmensstandort ein IGP verwendet wird, muss der interne Router IGP-Routen an BGP und BGP-Routen an IGP-Routen umverteilen, um die Subnetzverbindung zwischen den virtuellen CSP-Netzwerken und den lokalen Unternehmenssubnetzen aufrechtzuerhalten.  
  
Mit dieser Bereitstellung hat das Unternehmen RAS-Gateway eine Standort-zu-Standort-VPN-Verbindung mit dem CSP-RAS-Gateway, das Enterprise-RAS-Gateway die Routen zum CSP-Gateway bereitstellt. Der interne Unternehmensrouter lernt dann diese Route zum CSP-Gateway unter Verwendung von iBGP mit dem Enterprise-RAS-Gateway. Aus diesem Grund kann der interne Unternehmensrouter dann eine peeringsitzung mit dem CSP-RAS-Gateway-BGP-Router herstellen.  
  
Ab diesem Punkt Tauschen der interne Unternehmensrouter und das CSP-RAS-Gateway Routinginformationen aus. Und der Enterprise-RAS-BGP-Router lernt CSP-Routen und unternehmensrouten, um Pakete zwischen den Netzwerken physisch weiterleiten.  
  
## <a name="bkmk_features"></a>BGP-Funktionen  
Im folgenden werden die Funktionen von der RAS-Gateway-BGP-Router.  
  
**BGP-Routing als ein Rollendienst der Remotezugriff**. Sie können jetzt installieren die **Routing** Rollendienst der Remotezugriffs-Serverrolle ohne Installation der **Remote Access Service (RAS)** Rollendienst, wenn Sie Remotezugriff als BGP-LAN-Router verwenden möchten.  Dies reduziert den Speicherbedarf der BGP-Router und installiert nur die erforderlichen Komponenten für das dynamische BGP-routing. Der Routingdienst für die Rolle eignet sich Wenn nur eine BGP-Router-VM erforderlich ist, und die Verwendung von DirectAccess oder VPN nicht erforderlich. Darüber hinaus bietet mithilfe von Remotezugriff als LAN mit BGP-Router mit den dynamischen routing-Vorteilen von BGP in Ihrem internen Netzwerk.  
  
**BGP-Statistiken (Nachrichtenindikatoren, Routingindikatoren)** . Der BGP-Router unterstützt, falls erforderlich, die Anzeige von Nachrichten- und Routingstatistiken mit dem Windows PowerShell-Befehl **Get-BgpStatistics** .  
  
**Equal Cost Multi Path Routing (ECMP)-Unterstützung**. Der BGP-Router unterstützt ECMP und kann über mehr als eine Route mit gleichen Kosten in BGP-Routingtabelle und -stapel verfügen. Die BGP-Routerauswahl der Route für die Übertragung von Datenpaketen ist bei aktiviertem ECMP zufällig.  
  
**HoldTime-Konfiguration**. Der BGP-Router unterstützt die Konfiguration des HoldTimer-Werts entsprechend den Erfordernissen des Netzwerks. Dieser Zeitgeber kann dynamisch geändert werden, um Interoperabilität mit Geräten von Drittanbietern oder ein bestimmtes maximales Sitzungstimeout der BGP-Peeringsitzung zu gewährleisten.  
  
**Interne BGP- und externe BGP-Unterstützung**. Der BGP-Router unterstützt iBGP- und eBGP-Peering. Um eines der beiden Protokolle zu konfigurieren, müssen Sie sicherstellen, dass die entsprechenden ASNs den lokalen und Remote-BGP-Routern zugewiesen sind. Alle vier BGP-Bereitstellungstopologien umfassen die Verwendung von eBGP-Peering, und die vierte Topologie verwendet zudem iBGP-Peering.  
  
**Interoperabilität mit Drittanbieterlösungen**. Der BGP-Router basiert auf der neuesten BGP-Spezifikation in der Version 4 und wurde für die Interoperabilität mit den meisten wichtigen Drittanbieter-BGP-Routinggeräten getestet. Weitere Informationen finden Sie unter RFC 4271 (Request for Comments), [A Border Gateway Protocol 4 (BGP-4)](https://tools.ietf.org/html/rfc4271).  
  
**Unterstützung von IPv4- und IPv6-Transportpeering**. Der BGP-Router unterstützt IPv4- und IPv6-Peering. Sie müssen jedoch den BGP-Bezeichner als IPv4-Adresse des BGP-Routers konfigurieren. Für alle BGP-Routerbereitstellungstopologien kann einer der beiden Peeringtypen (IPV4/IPv6) verwendet werden.  
  
**IPv4- und IPv6-Unicastrouten-Lern- und Ankündigungsfunktionen (Multiprotokoll-NRLI [Network Layer Reachability Information])** . Unabhängig von der verwendeten Transportart kann der BGP-Router IPv4- und IPv6-Routen austauschen, wenn die entsprechende Funktion beim Einrichten der Sitzung durch andere BGP-Router angekündigt wird. Zum Konfigurieren von IPv6-Routing, muss der Parameter IPv6Routing aktiviert sein, und eine lokale, globale IPv6-Adresse muss auf Routerebene konfiguriert sein.  
  
**Peering im gemischten Modus und im passiven Modus**. Sie können konfigurieren, BGP-peeringsitzungen entweder im gemischten Modus -, in dem der BGP-Router als Initiator und Responder - fungiert oder im passiven Modus, in dem der BGP-Router kein peering initiiert, jedoch auf eingehende Anforderungen reagiert. Der gemischte Modus ist die Standardeinstellung und wird für BGP-Peering empfohlen. Dies gilt, wenn Sie den passiven Modus nicht zum Debuggen und zur Diagnose verwenden möchten. Für alle BGP-Routerbereitstellungstopologien ist Peering im gemischten Modus erforderlich, um automatische Neustarts bei Fehlerereignissen zu aktivieren.  
  
**Routenattribut-Umschreibefunktion**. Sie können die folgenden Attribute von den BGP-Routereingangs und -Ausgangsroutenankündigungen mithilfe der BGP-Routingrichtlinien Next-Hop, MED, Local-Pref und Community hinzufügen, ändern oder entfernen.  
  
**Routenfilterung**. Der BGP-Router unterstützt Filterung von Eingangs und -Ausgangsroutenankündigungen basierend auf mehreren Routenattributen wie Präfix, ASN-Bereich, Community und Next-Hop.  
  
**Route-Reflector (RR) und RR-Client**. Der BGP-Router kann als eine Route-Reflector und einem RR-Client fungieren. Dies ist nützlich in komplexe Topologien, in denen RR im Netzwerk vereinfachen kann, indem Sie RR-Cluster bilden.  
  
**Route-Refresh-Unterstützung**. Der BGP-Router unterstützt Route-Refresh und kündigt dies standardmäßig beim Peering an. Es kann einen neuen Satz von routenaktualisierungen, wenn Sie von einem Peer per Route-Refresh-Nachricht senden sowie senden eine Route-Refresh, die Routing-Tabelle in den Ereignissen wie Änderungen an den Routing-Richtlinien für einen Peer zu aktualisieren. Dadurch wird das Szenario der ändern oder aktualisieren die BGP-Routing-Richtlinien in Windows Server 2016, ohne dass Sie das peering neu starten müssen.  
  
**Unterstützung für die Konfiguration von statischen Routen**. Sie können statische Routen oder Schnittstellen auf dem BGP-Router mit dem Windows PowerShell-Befehl **Add-BgpCustomRoute** konfigurieren. Die statischen Routen, die Sie konfigurieren, können die Präfixe oder Schnittstellennamen sein, von denen die Routen ausgewählt werden müssen. Allerdings werden nur die Routen mit auflösbaren Next-Hops in die BGP-Routingtabellen einbezogen und den Peers angekündigt.  
  
**Transitroutingunterstützung**. Der BGP-Router unterstützt transitrouting für iBGP-zu-iBGP-Verbindungen und iBGP-zu-eBGP-Verbindungen sowie eBGP-zu-eBGP-Verbindungen.  
  
**Weiterleiten der Flap-Dämpfung**. Route Flap-Dämpfung zum BGP-Routing in Windows Server 2016 bietet Unterstützung für die Flap-Dämpfung Route. Z. B. wenn eine Route ständig angekündigt wird, und zurückgezogen, die Routingtabelle instabil, sodass Sie können konfigurieren, die BGP-Router, weisen Sie eine Kauf Gewichtung auf die Route für flapping – überwachen und entsprechend zu unterdrücken oder aufheben – es nach Bedarf zu unterdrücken. Dadurch wird eine stabile Routingtabelle verwalten und weniger Verarbeitung durch den BGP-Router.  
  
**Weiterleiten von Aggregation**. Route zu aggregieren, um das BGP-Router bietet Ihnen die Möglichkeit, Aggregatrouten zu konfigurieren und die präziseren routenankündigungen mit zusammengefasste oder aggregierte Routen Peers zu ersetzen. Dies führt zu einer geringeren Anzahl von Route-Advertisement-Meldungen, die über das Netzwerk übertragen.  
  
> [!NOTE]  
> In System Center heißt das RAS-Gateway, Windows Server-Gateway.  
  

  

