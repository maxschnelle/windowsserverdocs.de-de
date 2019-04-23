---
title: Softwarelastenausgleich (SLB) für SDN
description: Sie können in diesem Thema verwenden, um weitere Informationen zur Software-Lastenausgleich für die Software Defined Networking unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97abf182-4725-4026-801c-122db96964ed
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 26fb4aa21e80618c4c63bd9edbf8731bf886db62
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853761"
---
# <a name="software-load-balancing-slb-for-sdn"></a>Softwarelastenausgleich \(SLB\) für SDN

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um weitere Informationen zur Software-Lastenausgleich für die Software Defined Networking unter Windows Server 2016.  

Clouddienstanbieter (CSPs) und Unternehmen, das Bereitstellen von Software-Defined Networking (SDN) in Windows Server 2016 können (Software Load Balancing, SLB) Sie um Mandanten und Kunden mandantennetzwerk-Datenverkehr auf virtuelle Netzwerkressourcen gleichmäßig zu verteilen. Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.
  
Windows Server-Softwarelastenausgleichs umfasst die folgenden Funktionen.  
  
-   Layer-4 (L4) werden die Lastenausgleichsdienste für "Nord-Süd" und "Ost-West" TCP/UDP-Datenverkehr.  
  
-   Öffentliche und interne Netzwerk-Datenverkehr über den Lastenausgleich.  
  
-   Unterstützt die dynamische IP-Adressen (DIPs) auf virtuelle lokale Netzwerke (VLANs) und in virtuellen Netzwerken, die Sie erstellen mithilfe von Hyper-V-Netzwerkvirtualisierung.  
  
-   Health Probe-Unterstützung.  
  
-   Bereit für cloudebene, einschließlich von horizontaler-Funktion, ein, und Funktionen für Multiplexers und Host-Agents zentral hochskalieren.  
  
Weitere Informationen finden Sie unter [Software Load Balancing Features](#bkmk_features) in diesem Thema.  
  
> [!NOTE]  
> Mehrinstanzenfähigkeit für VLANs wird vom Netzwerkcontroller nicht unterstützt, aber Sie VLANs mit SLB für Dienstanbieter verwenden können verwaltet arbeitsauslastungen, z. B. die Datacenter-Infrastruktur und den Webserver mit hoher Dichte.  
  
Verwendung von Windows Server-Softwarelastenausgleichs können Sie horizontal hochskalieren Ihrer Lastenausgleichsfunktionen, die mit der SLB-VMs auf den gleichen Hyper-V-Compute-Servern, die Sie für Ihre VM-Workloads verwenden. Aus diesem Grund unterstützt SLB das schnelle Erstellen und Löschen der Endpunkte für den Lastenausgleich, die für CSP-Vorgänge erforderlich ist. Windows Server-Softwarelastenausgleichs darüber hinaus unterstützt Dutzende von Gigabyte pro Cluster, bietet ein einfaches Modell für die Bereitstellung und ist einfach, horizontale hoch- und Herunterskalieren.  
  
**Funktionsweise von SLB**  
  
SLB funktioniert, indem Sie dynamische IP-Adressen (DIPs), die Teil einer Cloud-Dienst-Satz von Ressourcen im Rechenzentrum sind virtuelle IP-Adressen (VIPs) zuordnen.  
  
VIPs werden einzelne IP-Adressen, die öffentlichen Zugriff auf einen Pool von Load VMs mit Lastenausgleich bereitstellen. VIPs sind z. B. IP-Adressen, die im Internet verfügbar gemacht werden, damit Mandanten und mandantenkunden auf mandantenressourcen in der Cloud-Datencenter verbinden können.  
  
DIPs sind die IP-Adressen der VMs von einem Load balancer-Pool hinter der VIP-Member. DIPs werden in der Cloudinfrastruktur auf die mandantenressourcen zugewiesen.  
  
VIPs befinden sich in der SLB Multiplexer (MUX-Instanz).  Die Mux-Instanz besteht aus einem oder mehreren virtuellen Computern (VMs).  Bietet Netzwerkcontroller die Möglichkeit jedes MUX-Instanz mit jeder VIP-Adresse, und jede MUX wiederum verwendet Border Gateway Protocol (BGP) jede VIP an Router auf dem physischen Netzwerk als/32 ankündigen Route.  BGP ermöglicht die physische Netzwerkrouter auf:  
  
-   Erfahren Sie, dass eine VIP-Adresse jedes MUX-Instanz verfügbar ist, auch wenn die/Mux in unterschiedlichen Subnetzen in einem Layer 3-Netzwerk befinden.  
  
-   Verteilen Sie die Last für jede VIP, auf alle verfügbaren MUX gleich Cost Multi Path (ECMP) routing verwenden.  
  
-   Automatisch erkennen Sie MUX-Instanz ausfällt oder entfernt, und beenden Sie senden von Datenverkehr an die fehlerhafte MUX-Instanz zu.  
  
-   Verteilen Sie die Last für die fehlerhafte oder entfernte MUX-Instanz, auf die fehlerfrei MUX.  
  
Wenn öffentlichen Datenverkehr über das Internet eingeht, untersucht der SLB MUX den Datenverkehr, der enthält der VIP-Adresse als Ziel, und ordnet und schreibt den Datenverkehr neu, sodass er einen einzelnen DIP-Adresse erreichen wird. Für den eingehenden Netzwerkdatenverkehr wird diese Transaktion in einem zweistufigen Prozess ausgeführt, die zwischen den virtuellen MUX-Maschinen (VMs) und den Hyper-V-Host auf dem sich das Ziel DIP-Adresse befindet unterteilt ist:  
  
-   Lastenausgleich – die Mux-Instanz verwendet, wählen Sie eine DIP-Adresse, die VIP-Adresse des Pakets kapselt und leitet den Datenverkehr an dem Hyper-V-Host, auf dem sich die DIP-Adresse befindet.  
  
-   Netzwerkadressübersetzung (NAT) - Hyper-V-Hosts Kapselung aus dem Paket entfernt, die VIP-Adresse, eine DIP-Adresse übersetzt, die Ports zugeordnet und leitet das Paket an die DIP-VM.  
  
Die Mux-Instanz weiß, wie der richtige DIPs aufgrund von Richtlinien, die Sie definieren, indem Sie mithilfe von Netzwerkcontroller für den Lastenausgleich virtuellen IP-Adressen zugeordnet. Diese Regeln umfassen das Protokoll, Port der Front-End, Back-End-Port und Verteilungsalgorithmus (5, 3 oder 2-Tupel).  
  
Wenn Mandanten auf die virtuellen Computer zu reagieren und Senden ausgehender Datenverkehr an das Internet oder remote-Mandanten-Speicherorte, Netzwerk da durch den Hyper-V-Host, den Datenverkehr vom NAT-Gerät ausgeführt wird, umgeht die Mux-Instanz und werden direkt an den edgerouter auf dem Hyper-V-Host. Diese MUX Umgehung wird Direct Server Return (DSR) bezeichnet.  
  
Nachdem die anfängliche des Netzwerkdatenverkehrs hergestellt wurde, der eingehenden Netzwerkdatenverkehr umgangen wird der SLB MUX vollständig.  
  
In der folgenden Abbildung führt ein Clientcomputer eine DNS-Abfrage für die IP-Adresse von einem Unternehmen SharePoint-Website – in diesem Fall ein fiktives Unternehmen namens Contoso. Der folgende Prozess durchgeführt wird.  
  
-   Der DNS-Server zurückgegeben die VIP 107.105.47.60 an den Client.  
  
-   Der Client sendet eine HTTP-Anforderung an die VIP-Adresse an.  
  
-   Das physische Netzwerk verfügt über mehrere Pfade zur Verfügung, um die VIP-Adresse befindet sich auf alle MUX-Instanz zu erreichen.  Alle Router auf dem Weg verwendet ECMP, das jeweils nächste Segment des Pfads auszuwählen, bis die Anforderung an eine MUX ankommt.  
  
-   Die Mux-Instanz, die die Anforderung erhält konfigurierte Richtlinien überprüft und feststellt, dass es zwei Abfälle verfügbar ist, 10.10.10.5 und 10.10.20.5, in einem virtuellen Netzwerk zur Verarbeitung der Anforderung an die VIP 107.105.47.60 gibt  
  
-   Die Mux-Instanz die DIP-Adresse 10.10.10.5 auswählt und kapselt die Pakete, VXLAN verwenden, damit sie es an den Host, der die DIP-Adresse mit den Hosts enthält physikalische Netzwerkadresse senden kann.  
  
-   Der Host des gekapselten Pakets empfängt und überprüft.  Es entfernt die Kapselung und ändert das Paket aus, damit das Ziel jetzt die DIP-Adresse 10.10.10.5 anstelle der VIP-Adresse ist und den Datenverkehr zu virtuellen Computer die DIP-Adresse sendet.  
  
-   Die Anforderung hat die Contoso-SharePoint-Website im Server-Farm 2 erreicht. Der Server eine Antwort generiert und sendet sie an den Client mit eigener IP-Adresse der Quelle.  
  
-   Der Host fängt dem ausgehende Paket auf dem virtuellen Switch, der speichert, die den Client nun das Ziel, die ursprüngliche Anforderung an der VIP vorgenommen.  Der Host ändert die Quelle des Pakets ist die VIP-Adresse, die an den Client die DIP-Adresse nicht angezeigt wird.  
  
-   Der Host leitet das Paket direkt an das Standardgateway für das physische Netzwerk, das die standardmäßige Routingtabelle verwendet wird, um das Paket an den Client weiterzuleiten, die schließlich die Antwort empfängt.  
  
![Prozess für den Lastenausgleich-Software](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**Lastenausgleich interne Datacenter für Datenverkehr**  
  
Wenn laden Netzwerkverkehr zum Lastenausgleich für das Datencenter und intern, wie z. B. zwischen mandantenressourcen, die auf verschiedenen Servern ausgeführt werden und sind Mitglieder der gleichen virtuellen Netzwerk, den virtuellen Hyper-V-Switch mit dem die virtuellen Computer verbunden sind NAT ausführt  
  
Mit Lastenausgleich von internem Datenverkehr wird die erste Anforderung gesendet und verarbeitet die Mux-Instanz, die wählt der entsprechenden DIP-Adresse und leitet den Datenverkehr weiter, um die DIP-Adresse. Ab diesem Punkt der festgelegten Datenverkehr umgeht die Mux-Instanz und gelangt direkt von der VM zu VM.  
  
**Integritätstests**  
  
SLB enthält Integritätstests zum Überprüfen der Integritäts der Netzwerkinfrastruktur, einschließlich der folgenden.  
  
-   TCP-Test an port  
  
-   HTTP-Test, um Port- und URL  
  
Im Gegensatz zu einer herkömmlichen lastenausgleichsappliance, in dem der Test auf dem Gerät stammt und über das Netzwerk an die DIP-Adresse gesendet, der SLB-Test stammt, auf dem Host, in denen die DIP-Adresse befindet und gelangt direkt von der SLB-Host-Agent an die DIP, die weitere Verteilung, der Arbeiten Sie auf den Hosts.  
  
## <a name="bkmk_infrastructure"></a>Software Load Balancing-Infrastruktur  
Zum Bereitstellen von Windows Server-Softwarelastenausgleichs müssen Sie zunächst den Netzwerkcontroller in Windows Server 2016 und mindestens eine SLB/MUX-VM bereitstellen.  
  
Darüber hinaus müssen Sie Hyper-V-Hosts mit dem SDN-fähigen virtuellen Hyper-V-Switch konfigurieren und stellen Sie sicher, dass der SLB-Host-Agent ausgeführt wird.  Die Router, die die Hosts dienen müssen unterstützen die gleichen Kosten Multipfad (ECMP) routing und Border Gateway Protocol (BGP) und müssen so konfiguriert werden, dass die BGP-peering-Anforderungen von der SLB/MUX akzeptiert.  
  
Es folgt eine Übersicht über die SLB-Infrastruktur.  

![Software-Lastenausgleich-Infrastruktur](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
Die folgenden Abschnitte enthalten weitere Informationen zu diesen Elementen der SLB-Infrastruktur.  
  
### <a name="scvmm"></a>SCVMM  
Mit System Center 2016 können Sie den Netzwerkcontroller unter Windows Server 2016, einschließlich der SLB-Manager und die Systemüberwachung konfigurieren. Sie können auch System Center verwenden, zum Bereitstellen des SLB MUXs und SLB-Host-Agents auf Computern installieren, auf denen Windows Server 2016 und Hyper-V ausgeführt werden.  
  
Weitere Informationen zu System Center 2016 finden Sie unter [System Center 2016](https://www.microsoft.com/server-cloud/products/system-center-2016/).  
  
> [!NOTE]  
> Wenn Sie nicht, System Center 2016 zu verwenden möchten, können Sie Windows PowerShell oder eine andere verwaltungsanwendung installieren und konfigurieren den Netzwerkcontroller und anderen SLB-Infrastruktur. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="network-controller"></a>Netzwerkcontroller  
Netzwerkcontroller hostet die SLB-Manager und führt die folgenden Aktionen für SLB.  
  
-   Verarbeitet die SLB-Befehle, die über die Northbound-API von System Center, Windows PowerShell oder eine andere verwaltungsanwendung für Netzwerk stammen.  
  
-   Berechnet die Richtlinie für die Verteilung an Hyper-V-Hosts und SLB/MUX.  
  
-   Stellt den Integritätsstatus der SLB-Infrastruktur bereit.  
  
### <a name="slb-mux"></a>SLB MUX  
Der SLB MUX verarbeitet die eingehenden Netzwerkdatenverkehr virtuellen IP-Adressen, DIPs zugeordnet, und leitet den Datenverkehr an der richtige DIP. Jede MUX verwendet auch BGP zum Veröffentlichen von VIP-Routen in Edge-Routern. BGP Keep-Alive benachrichtigt MUX, wenn es sich bei einem MUX-Instanz ein Fehler auftritt, wodurch active verteilen die Last bei einem MUX-Fehler - die wesentlichen Lastenausgleich für den Load balancer-MUX.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Hosts, auf denen Hyper-V ausgeführt wird  
Sie können SLB mit Computern, auf denen Windows Server 2016 und Hyper-V ausgeführt werden. Die virtuellen Computer, auf dem Hyper-V-Host können einem beliebigen Betriebssystem ausführen, die von Hyper-V unterstützt wird.  
  
### <a name="slb-host-agent"></a>SLB-Host-Agent  
Wenn Sie die SLB bereitstellen, müssen Sie System Center, Windows PowerShell oder eine andere verwaltungsanwendung verwenden, der SLB-Host-Agent auf jedem Hyper-V-Host-Computer bereitstellen. Sie können den SLB-Host-Agent auf allen Versionen von Windows Server 2016 installieren, die Hyper-V-Unterstützung, einschließlich Nano Server bereitstellen.  
  
Der SLB-Host-Agent Lauscht auf SLB-richtlinienaktualisierungen vom Netzwerkcontroller. Darüber hinaus programmiert der Host-Agent Regeln für SLB, in der SDN-fähige Hyper-V virtuelle Switches, die auf dem lokalen Computer konfiguriert sind.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>SDN aktiviert Hyper-V-Switches  
Verwenden Hyper-V Virtual Switch-Manager oder Windows PowerShell-Befehle, um den Switch zu erstellen, und dann müssen Sie Virtual Filtering Platform (VFP) aktivieren, für den virtuellen Switch, für ein virtueller Switch mit SLB, kompatibel sein.  
  
Informationen zum Aktivieren der VFP für virtuelle Switches finden Sie in der Windows PowerShell-Befehle [Get-VMSystemSwitchExtension](https://technet.microsoft.com/library/hh848603.aspx) und [Enable-VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx?f=255&MSPPError=-2147217396).  
  
SDN aktiviert den virtuellen Hyper-V-Switch führt die folgenden Aktionen für SLB.  
  
-   Verarbeitet den Datenpfad für SLB an.  
  
-   Empfängt Netzwerkdatenverkehr von der MUX-Instanz an.  
  
-   Umgeht die Mux-Instanz für den ausgehenden Netzwerkdatenverkehr an den Router mit DSR senden.  
  
-   Klicken Sie auf Nano Server-Instanzen von Hyper-V ausgeführt wird.  
  
### <a name="bgp-enabled-router"></a>BGP-fähige Router  
Der BGP-Router führt die folgenden Aktionen für SLB.  
  
-   Routen Sie eingehenden Datenverkehr, für die Verwendung von ECMP MUX-Instanz.  
  
-   Für den ausgehenden Netzwerkdatenverkehr verwendet die Route, die vom Host bereitgestellt wird.  
  
-   Routeupdates überwacht für die virtuellen IP-Adressen von SLB MUX.  
  
-   SLB/MUX entfernt aus der Rotation SLB, wenn Keep-Alive ein Fehler auftritt.  
  
## <a name="bkmk_features"></a>Software Load Balancing-Funktionen  
Es folgen einige der Features und Funktionen der SLB.  
  
**Kernfunktionen**  
  
-   SLB ermöglicht Layer-4-Lastenausgleich für "Nord-Süd" und "Ost-West" TCP/UDP-Datenverkehr  
  
-   Sie können in einem Hyper-V-Netzwerkvirtualisierung basierenden Netzwerk SLB verwenden.  
  
-   Sie können SLB mit einem Netzwerk mit VLAN-basierte für DIP-VMs, die mit einem SDN aktiviert Hyper-V-Switch verbunden sind.  
  
-   Eine SLB-Dienstinstanz kann die Verarbeitung mehrerer Mandanten  
  
-   SLB und DIP-Adresse unterstützt einen skalierbaren und mit geringer Latenz Rückgabepfad, gemäß der Implementierung von Direct Server Return (DSR)  
  
-   SLB-funktioniert, wenn Sie auch Switch Embedded Teaming (SET) oder Single Root Input/Output Virtualization (SR-IOV) verwenden  
  
-   SLB enthält Internet Protocol, Version 4 (IPv4) unterstützt  
  
-   Für die Standort-zu-Standort-Gateway-Szenarios bietet der SLB NAT-Funktionalität, sodass alle Standort-zu-Standort-Verbindungen mit eine einzelne öffentliche IP-Adresse verwenden  
  
-   Sie können die SLB, einschließlich der Host-Agent und die Mux-Instanz, auf Windows Server 2016 Core und Nano-Installation installieren.  
  
**Skalierung und Leistung**  
  
-   Bereit für cloudebene, einschließlich von horizontaler-Funktion, ein, und Funktionen für MUX und Host-Agents zentral hochskalieren.  
  
-   Eine aktive Netzwerkcontroller SLB-Manager-Modul kann 8/MUX-Instanzen unterstützen.  
  
**Hohe Verfügbarkeit**  
  
-   Sie können auf mehr als 2 Knoten in einer Aktiv/Aktiv-Konfiguration SLB bereitstellen.  
  
-   MUX können hinzugefügt und entfernt aus dem Pool MUX-Instanz ohne Auswirkungen auf die SLB-Diensts. Hierdurch bleibt die SLB-Verfügbarkeit bei   
    einzelne MUX werden gepatcht wird.  
  
-   Einzelne MUX-Instanzen haben eine Betriebszeit von 99 %  
  
-   Daten für die Systemüberwachung ist für Management-Entitäten verfügbar  
  
**Alignment**  
  
-   Sie können auch bereitstellen und Konfigurieren von SLB mit SCVMM  
  
-   SLB stellt einen mehrinstanzenfähigen einheitlichen Edge bereit, durch die nahtlose Integration mit Microsoft-Geräten wie z. B. die RAS-Mehrinstanzenfähiges Gateway, Datacenter Firewall und Route-Reflector.  
  

