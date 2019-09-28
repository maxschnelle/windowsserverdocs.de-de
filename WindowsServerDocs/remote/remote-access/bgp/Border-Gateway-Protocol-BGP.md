---
title: Border Gateway Protocol (BGP)
description: Sie können dieses Thema verwenden, um ein Verständnis der Border Gateway Protocol (BGP) in Windows Server 2016 zu erhalten, einschließlich BGP-unterstützter Bereitstellungstopologien und BGP-Features und-Funktionen.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78cc2ce3-a48e-45db-b402-e480b493fab1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ae6fddce1564e44ad72a5630c6abb16cdb6735d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388981"
---
# <a name="border-gateway-protocol-bgp"></a>Border Gateway Protocol (BGP)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie Informationen zum Verständnis des Border Gateway Protocol (BGP), einschließlich Bereitstellungstopologien mit BGP-Unterstützung und BGP-Features sowie -Funktionen.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema ist die folgende BGP-Dokumentation verfügbar.  
>   
> -   [BGP-Befehlsreferenz für Windows PowerShell](../../remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [BGP-Unterstützte Bereitstellungstopologien](#bkmk_top)  
  
-   [BGP-Funktionen](#bkmk_features)  
  
Wenn Sie auf einem Windows Server 2016-RAS-Dienst \(ras @ no__t-1 Gateway im mehr Instanzen Modus konfiguriert werden, bietet Border Gateway Protocol (BGP) die Möglichkeit, das Routing von Netzwerk Datenverkehr zwischen den VM-Netzwerken Ihrer Mandanten und deren Remote- Websites. Sie können BGP auch für RAS-Gateway-bereit Stellungen mit einem Mandanten und bei der Bereitstellung des Remote Zugriffs als lokales Netzwerk \(lan @ no__t-1-Router verwenden.  
  
BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind.  
  
Um das BGP-Routing verwenden zu können, müssen Sie den RAS **-Dienst \(ras @ no__t-2** und/oder den **Routing** Rollen Dienst der RAS-Server Rolle auf einem Computer oder virtuellen Computer installieren \(vm @ no__t-5-der von Ihnen verwendete Systemtyp hängt von ab. unabhängig davon, ob Sie über eine mehr Instanzen fähige Bereitstellung verfügen:  
  
-   Bei einer mehr Instanzen fähigen Bereitstellung wird empfohlen, das RAS-Gateway auf einem oder mehreren virtuellen Computern zu installieren. Die Verwendung mehrerer virtueller Computer bietet hohe Verfügbarkeit. Das RAS-Gateway kann mehrere Verbindungen von mehreren Mandanten verarbeiten und besteht aus einem Hyper-V-Host und einem virtuellen Computer, der tatsächlich als Gateway konfiguriert ist. Dieses Gateway ist mit Standort-zu-Standort-VPN-Verbindungen als mehr Instanzen fähiger BGP-Router für Exchange-Mandanten und clouddienstanbieter \(csp @ no__t-1-Subnetzrouten konfiguriert.  
  
-   Für eine Bereitstellung eines Edge-Gateways mit einem einzelnen Mandanten oder eine LAN-routerbereitstellung können Sie das RAS-Gateway entweder auf einem physischen Computer oder auf einem virtuellen Computer installieren.  
  
> [!IMPORTANT]  
> Bei der Installation eines RAS-Gateways müssen Sie angeben, ob BGP für jeden Mandanten aktiviert ist, indem Sie den Windows PowerShell **-Befehl enable-remoteaccessroutingdomain** mit dem **Typparameter** Wert **all**verwenden. Wenn Sie den Remote Zugriff als BGP-fähigen LAN-Router ohne mehr Instanzen fähige Funktionen installieren möchten, können Sie den Befehl **install-remoteaccess-vpntype routingonly**verwenden.  
>   
> Der folgende Beispielcode veranschaulicht, wie Sie RAS im mehr Instanzen Modus mit allen RAS-Funktionen (Punkt-zu-Standort-VPN, Site-to-Site-VPN und BGP-Routing) installieren können, die für zwei Mandanten aktiviert sind: "mso" und "Fabrikam".  
  
```  
$Contoso_RoutingDomain = "ContosoTenant"  
$Fabrikam_RoutingDomain = "FabrikamTenant"  
  
Install-RemoteAccess -MultiTenancy  
  
Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru  
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru  
```  
  
## <a name="bkmk_top"></a>BGP-Unterstützte Bereitstellungstopologien  
Im Folgenden sind die unterstützten Bereitstellungstopologien aufgeführt, bei denen Unternehmensstandorte mit einem Cloud Service Provider (CSP)-Datencenter verbunden sind.  
  
In allen Szenarien ist das CSP-Gateway ein Windows Server 2016-RAS-Gateway am Rand. Das RAS-Gateway, das mehrere Verbindungen von mehreren Mandanten verarbeiten kann, besteht aus einem Hyper-V-Host und einem virtuellen Computer, der tatsächlich als Gateway konfiguriert ist. Dieses Edgegateway wird als mehrinstanzenfähiger BGP-Router für den Austausch von Unternehmens- und CSP-Subnetzrouten mit Standort-zu-Standort-VPN-Verbindungen konfiguriert.  
  
Mandanten stellen eine Verbindung mit ihren Ressourcen im CSP-Datencenter mithilfe einer Standort-zu-Standort-(S2S)-VPN-Verbindung her. Darüber hinaus wird das BGP-Routingprotokoll für dynamischen Routinginformationsaustausch zwischen den Unternehmens- und den CSP-Gateways bereitgestellt.  
  
Die folgenden Bereitstellungstopologien werden unterstützt.  
  
-   [RAS-VPN-Standort-zu-Standort-Gateway mit BGP am Unternehmens Standort Edge](#bkmk_top1)  
  
-   [Drittanbieter Gateway mit BGP am Unternehmens Standort Edge](#bkmk_top2)  
  
-   [Mehrere Unternehmensstandorte mit Drittanbieter Gateways](#bkmk_top3)  
  
-   [Separate Beendigungs Punkte für BGP und VPN](#bkmk_top4)  
  
Die folgenden Abschnitte enthalten weitere Informationen über die einzelnen unterstützten BGP-Topologien.  
  
### <a name="bkmk_top1"></a>RAS-VPN-Standort-zu-Standort-Gateway mit BGP am Unternehmens Standort Edge  
Diese Topologie stellt einen mit einem CSP verbundene Unternehmensstandort dar. Die Unternehmens Routing Topologie enthält einen internen Router, ein Windows Server 2016-RAS-Gateway, das für VPN-Standort-zu-Standort-Verbindungen mit dem CSP konfiguriert ist, und ein edgefirewallgerät. Das RAS-Gateway beendet die S2S-VPN-und BGP-Verbindungen.  
  
![RAS-VPN-Standort-zu-Standort-Gateway](../../media/Border-Gateway-Protocol-BGP/bgp_01.jpg)  
  
Beide Standorte sind mittels externem Border Gateway Protocol (eBGP) verbunden, das Informationen zwischen BGP-fähigen Routern in separaten autonomen Systemen (AS) übertragen kann. Dazu müssen sowohl das Unternehmen als auch der CSP unterschiedliche autonome Systemnummern (ASN) besitzen. Dies ist ein Parameter, der integraler Bestandteil des BGP-Protokolls ist.  
  
In diesem Szenario funktioniert BGP auf folgende Weise.  
  
-   Das Edgegerät des Unternehmensstandorts erlernt mithilfe von BGP die virtualisierten Subnetzrouten (10.2.1.0/24), die in der Cloud gehostet werden. Dieses Gerät kündigt auch die lokalen Subnetzrouten (10.1.1.0/24) für das mehr Instanzen fähige CSP-RAS-Gateway an.  
  
-   Der Edgerouter des Kunden lernt lokale interne Routen über einen der folgenden Mechanismen:  
  
    -   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Beispiel 10.1.1.0/24). In der Zwischenzeit lernt der interne Router externe Routen (z. B. 10.2.1.0/24) vom Edgegerät, und der interne Router muss diese Routen an andere lokale Router über ein internes Gatewayprotokoll (IGP), wie z. B. OSPF (Open Shortest Path First) oder Routing Information-Protokoll (RIP), verteilen.  
  
    -   Das Edgegerät kann mit statischen Routen oder Schnittstellen zur Auswahl von Routen für die Ankündigung mithilfe von BGP konfiguriert werden. Das Edgegerät verteilt die externen Routen mit einem IGP auch an andere lokale Router.  
  
### <a name="bkmk_top2"></a>Drittanbieter Gateway mit BGP am Unternehmens Standort Edge  
Diese Topologie stellt einen Unternehmensstandort dar, der mit einem Edgerouter eines Drittanbieters eine Verbindung mit einem CSP herstellt. Der Edgerouter dient auch als Standort-zu-Standort-VPN-Gateway.  
  
![Drittanbietergateway mit BGP an der Unternehmensstandortedge](../../media/Border-Gateway-Protocol-BGP/bgp_02.jpg)  
  
Der Unternehmensedgerouter lernt lokale interne Routen mit einem der folgenden Mechanismen:  
  
-   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Fall 10.1.1.0/24)  
  
-   Das Edgegerät implementiert ein internes Gatewayprotokoll (IGP) und ist direkt am internen Routing beteiligt.  
  
### <a name="bkmk_top3"></a>Mehrere Unternehmensstandorte mit Verbindung zum CSP-clouddatencenter  
Diese Topologie stellt mehrere Unternehmensstandorte dar, die mit einem Edgerouter eines Drittanbieters eine Verbindung mit einem CSP herstellen. Die Edgegeräte der Drittanbieter dienen als Standort-zu-Standort-VPN-Gateways und BGP-Router.  
  
![Mehrere Unternehmensstandorte mit Verbindung zum CSP-clouddatencenter](../../media/Border-Gateway-Protocol-BGP/bgp_03.jpg)  
  
Die Edgerouter des Kunden lernen lokale interne Routen mit einem der folgenden Mechanismen:  
  
-   Das Edgegerät führt BGP mit einem internen Router aus und lernt interne Routen (in diesem Fall 10.1.1.0/24)  
  
-   Das Edgegerät implementiert ein internes Gatewayprotokoll (IGP) und ist direkt am internen Routing beteiligt.  
  
Jeder Unternehmensstandort lernt die Routen vom anderen Standort über die direkte eBGP-Verbindung.  
  
Jeder Unternehmensstandort lernt die gehosteten Netzwerkrouten direkt und über den anderen Unternehmensstandort, wählt jedoch die optimale Route auf Grundlage der Kosten der Route aus.  
  
Wenn der BGP-Router an Enterprise Site 1 keine Verbindung mit dem BGP-Router des Enterprise-Standorts 2 herstellen kann, weil die Konnektivität fehlgeschlagen ist, beginnt der BGP-Router von Standort 1 dynamisch, die Routen an das Netzwerk des Unternehmens Standorts 2 vom CSP-BGP-Router zu erlernen. die Umleitung von Standort 1 an Standort 2 über den Windows Server BGP-Router beim CSP.  
  
### <a name="bkmk_top4"></a>Separate Beendigungs Punkte für BGP und VPN  
Diese Topologie stellt ein Unternehmen dar, das zwei verschiedene Router als BGP- und Standort-zu-Standort-VPN-Endpunkte verwendet. Die Site-to-Site-VPN-Verbindung wird auf dem Windows Server 2016-RAS-Gateway beendet, während BGP auf einem internen Router beendet wird. Auf der CSP-Seite der Verbindungen beendet der CSP sowohl VPN-als auch BGP-Verbindungen mit dem RAS-Gateway. Bei dieser Konfiguration muss die interne Drittanbieter-Routerhardware die Umverteilung von IGP-Routen an BGP sowie von BGP-Routen an IGP unterstützen.  
  
![Separate Endpunkte für BGP und VPN](../../media/Border-Gateway-Protocol-BGP/bgp_04.jpg)  
  
Der interne Router lernt Unternehmensrouten mit einem der folgenden Mechanismen:  
  
-   BGP  
  
-   Ein internes Gatewayprotokoll (IGP), wie z. B. OSPF oder RIP.  
  
-   Statische Routenkonfiguration  
  
Wenn am Unternehmensstandort ein IGP verwendet wird, muss der interne Router IGP-Routen an BGP und BGP-Routen an IGP-Routen umverteilen, um die Subnetzverbindung zwischen den virtuellen CSP-Netzwerken und den lokalen Unternehmenssubnetzen aufrechtzuerhalten.  
  
Bei dieser Bereitstellung verfügt das Enterprise RAS-Gateway über eine Standort-zu-Standort-VPN-Verbindung mit dem CSP-RAS-Gateway, das dem Enterprise RAS-Gateway die Routen zum CSP-Gateway bereitstellt. Der interne Unternehmens Router lernt dann diese Route zum CSP-Gateway, indem IBGP mit dem Enterprise RAS-Gateway verwendet wird. Aus diesem Grund kann der interne Unternehmens Router dann eine peeringsitzung mit dem BGP-Router für das CSP-Gateway erstellen.  
  
Ab diesem Zeitpunkt tauschen der interne Unternehmens Router und das CSP-RAS-Gateway Routing Informationen aus. Und der Enterprise RAS-BGP-Router lernt die CSP-Routen und Unternehmens Routen, um Pakete physisch zwischen den Netzwerken weiterzuleiten.  
  
## <a name="bkmk_features"></a>BGP-Funktionen  
Im folgenden finden Sie die Features des RAS-Gateway-BGP-Routers.  
  
**BGP-Routing als Rollen Dienst des Remote Zugriffs**. Sie können jetzt den **Routing** Rollen Dienst der Remote Zugriffs-Server Rolle installieren, ohne den RAS-Rollen Dienst **(Remote Access Service** ) zu installieren, wenn Sie den Remote Zugriff als BGP-LAN-Router verwenden möchten.  Dadurch wird der Speicherbedarf des BGP-Routers reduziert, und nur die für das dynamische BGP-Routing erforderlichen Komponenten werden installiert. Der Routing Rollen Dienst ist nützlich, wenn nur eine BGP-Router-VM erforderlich ist und Sie DirectAccess oder VPN nicht verwenden müssen. Außerdem bietet die Verwendung des Remote Zugriffs als LAN-Router mit BGP die dynamischen Routing Vorteile von BGP in Ihrem internen Netzwerk.  
  
**BGP-Statistiken (Nachrichtenindikatoren, Routingindikatoren)** . Der BGP-Router unterstützt, falls erforderlich, die Anzeige von Nachrichten- und Routingstatistiken mit dem Windows PowerShell-Befehl **Get-BgpStatistics** .  
  
**Equal Cost Multi Path Routing (ECMP)-Unterstützung**. Der BGP-Router unterstützt ECMP und kann über mehr als eine Route mit gleichen Kosten in BGP-Routingtabelle und -stapel verfügen. Die BGP-Routerauswahl der Route für die Übertragung von Datenpaketen ist bei aktiviertem ECMP zufällig.  
  
**HoldTime-Konfiguration**. Der BGP-Router unterstützt die Konfiguration des HoldTimer-Werts entsprechend den Erfordernissen des Netzwerks. Dieser Zeitgeber kann dynamisch geändert werden, um Interoperabilität mit Geräten von Drittanbietern oder ein bestimmtes maximales Sitzungstimeout der BGP-Peeringsitzung zu gewährleisten.  
  
**Interne BGP- und externe BGP-Unterstützung**. Der BGP-Router unterstützt iBGP- und eBGP-Peering. Um eines der beiden Protokolle zu konfigurieren, müssen Sie sicherstellen, dass die entsprechenden ASNs den lokalen und Remote-BGP-Routern zugewiesen sind. Alle vier BGP-Bereitstellungstopologien umfassen die Verwendung von eBGP-Peering, und die vierte Topologie verwendet zudem iBGP-Peering.  
  
**Interoperabilität mit Drittanbieterlösungen**. Der BGP-Router basiert auf der neuesten BGP-Spezifikation in der Version 4 und wurde für die Interoperabilität mit den meisten wichtigen Drittanbieter-BGP-Routinggeräten getestet. Weitere Informationen finden Sie unter RFC 4271 (Request for Comments), [A Border Gateway Protocol 4 (BGP-4)](https://tools.ietf.org/html/rfc4271).  
  
**Unterstützung von IPv4- und IPv6-Transportpeering**. Der BGP-Router unterstützt IPv4- und IPv6-Peering. Sie müssen jedoch den BGP-Bezeichner als IPv4-Adresse des BGP-Routers konfigurieren. Für alle BGP-Routerbereitstellungstopologien kann einer der beiden Peeringtypen (IPV4/IPv6) verwendet werden.  
  
**IPv4- und IPv6-Unicastrouten-Lern- und Ankündigungsfunktionen (Multiprotokoll-NRLI [Network Layer Reachability Information])** . Unabhängig von der verwendeten Transportart kann der BGP-Router IPv4- und IPv6-Routen austauschen, wenn die entsprechende Funktion beim Einrichten der Sitzung durch andere BGP-Router angekündigt wird. Zum Konfigurieren von IPv6-Routing, muss der Parameter IPv6Routing aktiviert sein, und eine lokale, globale IPv6-Adresse muss auf Routerebene konfiguriert sein.  
  
**Peering im gemischten Modus und im passiven Modus**. Sie können BGP-peeringsitzungen im gemischten Modus konfigurieren. Dabei fungiert der BGP-Router sowohl als Initiator-als auch als Beantworter-oder Passiv-Modus, wobei der BGP-Router kein Peering initiiert, aber auf eingehende Anforderungen antwortet. Der gemischte Modus ist die Standardeinstellung und wird für BGP-Peering empfohlen. Dies gilt, wenn Sie den passiven Modus nicht zum Debuggen und zur Diagnose verwenden möchten. Für alle BGP-Routerbereitstellungstopologien ist Peering im gemischten Modus erforderlich, um automatische Neustarts bei Fehlerereignissen zu aktivieren.  
  
**Routenattribut-Umschreibefunktion**. Sie können die folgenden Attribute von den BGP-Routereingangs und -Ausgangsroutenankündigungen mithilfe der BGP-Routingrichtlinien Next-Hop, MED, Local-Pref und Community hinzufügen, ändern oder entfernen.  
  
**Routenfilterung**. Der BGP-Router unterstützt Filterung von Eingangs und -Ausgangsroutenankündigungen basierend auf mehreren Routenattributen wie Präfix, ASN-Bereich, Community und Next-Hop.  
  
**Routen Reflektor (RR) und RR-Client**. Der BGP-Router kann als Routen Reflektor und RR-Client fungieren. Dies ist bei komplexen Topologien nützlich, bei denen RR das Netzwerk durch die Bildung von RR-Clustern vereinfachen kann.  
  
**Route-Refresh-Unterstützung**. Der BGP-Router unterstützt Route-Refresh und kündigt dies standardmäßig beim Peering an. Es ist in der Lage, einen neuen Satz von Routen Aktualisierungen zu senden, wenn er von einem Peer per Route-Refresh-Nachricht angefordert wird, und eine Route-Aktualisierung zu senden, um die Routing Tabelle in Ereignissen wie Routing Richtlinien Änderungen für einen Peer zu aktualisieren. Dies ermöglicht das ändern oder Aktualisieren der BGP-Routing Richtlinien in Windows Server 2016, ohne dass das Peering neu gestartet werden muss.  
  
**Unterstützung für die Konfiguration von statischen Routen**. Sie können statische Routen oder Schnittstellen auf dem BGP-Router mit dem Windows PowerShell-Befehl **Add-BgpCustomRoute** konfigurieren. Die statischen Routen, die Sie konfigurieren, können die Präfixe oder Schnittstellennamen sein, von denen die Routen ausgewählt werden müssen. Allerdings werden nur die Routen mit auflösbaren Next-Hops in die BGP-Routingtabellen einbezogen und den Peers angekündigt.  
  
**Transitroutingunterstützung**. Der BGP-Router unterstützt Transit Routing für IBGP-zu-IBGP-Verbindungen, IBGP-zu-EBGP-Verbindungen sowie EBGP-zu-EBGP-Verbindungen.  
  
Die Weiterleitungs **Klappen Dämpfung**. Die Weiterleitung von Klappen für das BGP-Routing in Windows Server 2016 bietet Unterstützung für die Weiterleitungen von Routen dämpfen. Wenn z. b. eine Route ständig angekündigt und zurückgezogen wird, sodass die Routing Tabelle instabil wird, können Sie den BGP-Router so konfigurieren, dass er der Route eine Dämpfungs Gewichtung zuweist und ihn nach Bedarf zu unterdrücken oder zu unterdrücken. Dies hilft bei der Verwaltung einer stabilen Routing Tabelle und der geringeren Verarbeitung durch den BGP-Router.  
  
**Routen Aggregation**. Durch die Weiterleitung von Aggregationen an den BGP-Router haben Sie die Möglichkeit, Aggregat Routen zu konfigurieren und die präziseteren Routen Ankündigungen durch Zusammenfassungs-oder Aggregat Routen an Peers zu ersetzen. Dies führt zu einer geringeren Anzahl von Routen Ankündigungs Meldungen, die im Netzwerk übertragen werden.  
  
> [!NOTE]  
> In System Center wird das RAS-Gateway als Windows Server-Gateway bezeichnet.  
  

  

