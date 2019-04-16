---
title: Softwarelastenausgleich (SLB) für SDN
description: In diesem Thema können Sie um über die Software des Lastenausgleichs für Software Defined Networking in Windows Server2016 erfahren.
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
ms.openlocfilehash: 5e08afddde9c7be8d955a0cfdaf44f0fc31b8155
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="software-load-balancing-slb-for-sdn"></a>Softwarelastenausgleich \(SLB\) für SDN

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie um über die Software des Lastenausgleichs für Software Defined Networking in Windows Server2016 erfahren.  

Clouddienstanbieter (CSPs) und Unternehmen, die Software Defined Networking (SDN) in Windows Server2016 bereitstellen können Software Load Balancing (SLB) verwenden, um Mandanten und Netzwerkdatenverkehr zwischen Ressourcen im virtuellen Netzwerk gleichmäßig zu verteilen. Die Windows Server-SLB ermöglicht mehrere Server zum Hosten derselben Workload hohe Verfügbarkeit und Skalierbarkeit.
  
Windows Server-SLB umfasst die folgenden Funktionen.  
  
-   Layer-4 (L4) Load balancing Dienste für 'Nord-Süd' und "Ost-West" TCP/UDP-Datenverkehr.  
  
-   Öffentliche und interne Netzwerklastenausgleich von Datenverkehr.  
  
-   Unterstützt die dynamische IP-Adressen (DIP) auf virtuelle lokale Netzwerke (VLANs) und in virtuellen Netzwerken, die Sie mithilfe von Hyper-V-Netzwerkvirtualisierung erstellt.  
  
-   Integrität der Test-Unterstützung.  
  
-   Bereit für die Cloud-Skalierung, einschließlich mit horizontaler Skalierung-Funktion und Skalieren der Funktion für Multiplexers und Host-Agents.  
  
Weitere Informationen finden Sie unter [Features der Software Load Balancing](#bkmk_features) in diesem Thema.  
  
> [!NOTE]  
> Mehrinstanzenfähigkeit für VLANs von Netzwerkcontroller nicht unterstützt, jedoch VLANs mit SLB für Service-Anbieter verwendet werden kann verwaltet Arbeitsauslastungen, z.B. die Datacenter-Infrastruktur und high-Density-Webserver.  
  
Verwenden Windows Server-SLB, können Sie skalieren Ihrer Lastenausgleichsfunktionen mit SLB VMs auf den gleichen Hyper-V-Compute-Servern, die Sie für Ihre anderen VM-Arbeitslasten verwenden. Aus diesem Grund unterstützt SLB das schnelle Erstellen und Löschen von NLB-Endpunkte, die für CSP-Vorgänge erforderlich ist. Windows Server-SLB darüber hinaus Zehntausende von Gigabyte pro Cluster unterstützt, bietet ein einfaches Modell für die Bereitstellungsprozess und ist einfach, Skalierung und in.  
  
**Funktionsweise von SLB**  
  
SLB funktioniert, indem Sie dynamische IP-Adressen (DIP), die Teil einer Cloud-Dienst-Satz von Ressourcen im Datencenter sind virtuelle IP-Adressen (VIPs) zuordnen.  
  
VIPs werden einzelne IP-Adressen, die öffentlichen Zugriff auf einen Pool von laden VMs mit Lastenausgleich bereitstellen. VIPs sind z.B. IP-Adressen, die im Internet verfügbar gemacht werden, damit Mandanten und Mandanten Kunden Mandanten Ressourcen in der Cloud-Datencenter zugreifen können.  
  
DIPs werden die IP-Adressen des Mitglieds VMs eines Netzwerklastenausgleich-Pools hinter der VIP-Adresse. DIPs werden in der Cloud-Infrastruktur für die Mandanten-Ressourcen zugewiesen.  
  
VIPs befinden sich in der SLB zur Vereinheitlichung (MUX).  Der MUX besteht aus einem oder mehreren virtuellen Computern (VMs).  Netzwerkcontroller bietet verwendet den Border Gateway Protocol (BGP) jedes Multiplexing mit einzelnen VIP und jede MUX wiederum jeder VIP Routern im physischen Netzwerk als eine /32 ankündigen Route.  BGP kann der physische Netzwerkrouter an:  
  
-   Hier erfahren Sie, dass eine VIP-Adresse jedes MUX verfügbar ist, auch wenn die MUXes in unterschiedlichen Subnetzen in einem Layer 3-Netzwerk befinden.  
  
-   Verteilen Sie die Last für jede VIP auf alle verfügbaren MUXes mit gleichen Kosten Multi-Path (ECMP)-Routing.  
  
-   Automatisch erkennen Sie einer MUX-Ausfall oder entfernen, und beenden Sie senden von Datenverkehr an den fehlgeschlagenen MUX zu.  
  
-   Verteilen Sie die Last der fehlerhafte oder entfernte MUX auf den fehlerfreien MUXes.  
  
Öffentliche Datenverkehr aus dem Internet empfangen werden, überprüft der MUX SLB den Datenverkehr, der enthält der VIP-Adresse als Ziel, Karten und schreibt den Datenverkehr, damit es auf eine einzelne DIP übermittelt werden. Für eingehenden Netzwerkdatenverkehr wird diese Transaktion in zwei Schrittenausgeführt, die zwischen den MUX virtuellen Computern (VMs) und dem Hyper-V-Host, in denen das Ziel DIP befindet, aufgeteilt ist:  
  
-   Lastenausgleich - Multiplexing verwendet, die VIP, wählen Sie ein DIP kapselt das Paket und leitet den Datenverkehr an dem Hyper-V-Host, wo sich die DIP befindet.  
  
-   Network Address Translation (NAT) - Hyper-V-Hosts, übersetzt die VIP-Adresse in einem DIP, ordnet die Ports und leitet das Paket an die DIP-VM Kapselung aus dem Paket entfernt.  
  
Der MUX weiß, wie die richtige DIP aufgrund von Lastenausgleichsrichtlinien, die Sie definieren mit Netzwerkcontroller VIPs zuordnen. Diese Regeln enthalten, Protokoll, Front-End-Port, Back-End-Port und Verteilungsalgorithmus (5, 3 oder 2-Tupel).  
  
Wenn Mandanten virtuelle Maschinen zu reagieren und Senden ausgehender Datenverkehr an das Internet oder Remote-Mandanten-Speicherorte Netzwerk da die NAT, durch den Hyper-V-Host, den Datenverkehr ausgeführt wird der MUX umgeht und direkt Grenzrouter von Hyper-V-Hosts. Diese MUX Umgehung wird direkt Server zurückgegeben (DSR) bezeichnet.  
  
Und nach dem Einrichten der anfänglichen des Netzwerkdatenverkehrs umgeht der eingehenden Netzwerkdatenverkehr der MUX SLB vollständig.  
  
In der folgenden Abbildungführt ein Clientcomputer eine DNS-Abfrage für die IP-Adresse Unternehmen SharePoint-Website – in diesem Fall ein fiktives Unternehmen, die mit dem Namen Contoso. Der folgende Prozess erfolgt.  
  
-   Der DNS-Server zurück die VIP 107.105.47.60 an den Client.  
  
-   Der Client sendet eine HTTP-Anforderung an die VIP-Adresse.  
  
-   Das physische Netzwerk verfügt über mehrere Pfade für die VIP-Adresse befindet sich auf alle MUX zu erreichen.  Jeder Router entlang der Route verwendet ECMP, um das nächste Segment des Pfads auszuwählen, bis die Anforderung einer MUX erreicht.  
  
-   Der MUX, die die Anforderung empfängt überprüft Richtlinien konfiguriert, und erkennt, dass es zwei DIP verfügbar sind, 10.10.10.5 und 10.10.20.5, in einem virtuellen Netzwerk gibt, die Anforderung an die VIP 107.105.47.60 behandeln  
  
-   Der MUX DIP 10.10.10.5 auswählt und kapselt die Pakete mit VXLAN, damit sie es an den Host mit den Hosts DIP mit physischen Netzwerk-Adresse senden kann.  
  
-   Der Host erhält das gekapselte Paket und untersucht das Programm.  Er entfernt die Kapselung und schreibt das Paket neu, damit das Ziel jetzt DIP 10.10.10.5 anstelle der VIP ist und den Datenverkehr zur DIP-VM sendet.  
  
-   Die Anforderung hat nun die Contoso-SharePoint-Website in Server-Farm 2 erreicht. Der Server eine Antwort generiert und sendet es an den Client mit seiner eigenen IP-Adresse der Quelle.  
  
-   Der Host hört ausgehenden Paket im virtuellen Switch, der speichert, die den-Client jetzt das Ziel, die ursprüngliche Anforderung an der VIP vorgenommen.  Der Host ändert die Quelle des Pakets, das die VIP-Adresse sein, die an den Client die DIP-Adresse nicht angezeigt wird.  
  
-   Der Host Datenpaket das direkt an das Standardgateway für das physische Netzwerk, das die Standard-Routingtabelle verwendet wird, um das Paket an den Client weiterzuleiten, die letztendlich die Antwort erhält.  
  
![Lastenausgleich Prozess](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**Lastenausgleich interne Datacenter für Datenverkehr**  
  
Beim Laden Netzwerklastenausgleich Netzwerkdatenverkehr für das Datencenter und intern zu, wie z.B. zwischen Mandanten-Ressourcen, die auf verschiedenen Servern ausgeführt werden und sind Mitglieder der gleichen virtuellen Netzwerk, dem virtuellen Hyper-V-Switch mit dem die virtuellen Computer verbunden sind NAT ausführt  
  
Mit internen Datenverkehr des Lastenausgleichs ist die erste Anforderung gesendet und von den MUX, wählt die entsprechenden DIP und leitet den Datenverkehr an die DIP verarbeitet. Ab diesem Punkt der etablierten Datenverkehrsfluss den MUX umgeht und navigiert direkt von VM zu VM.  
  
**Integrität der Prüfpunkte**  
  
SLB enthält Integrität Tests zum Überprüfen der Integritäts der Netzwerkinfrastruktur, einschließlich der folgenden.  
  
-   Test der TCP-Port  
  
-   HTTP-Test zum Anschluss und die URL  
  
Im Gegensatz zu einer herkömmlichen laden Lastenausgleichsmodul Appliance, in dem der Prüfpunkt auf dem Gerät stammt und über das Netzwerk übertragen wird, in der DIP, stammt Prüfpunkts SLB auf dem Host, in denen DIP befindet, und ruft direkt vom Agent-Host SLB DIP, die Arbeit weiter auf die Hosts verteilt.  
  
## <a name="bkmk_infrastructure"></a>Software Load Balancing-Infrastruktur  
Zum Bereitstellen von Windows Server-SLB müssen Sie zuerst die Netzwerk-Controller in Windows Server2016 und einen oder mehrere SLB MUX-VMs bereitstellen.  
  
Darüber hinaus müssen Sie die Hyper-V-Hosts mit dem SDN-fähigen virtuellen Hyper-V-Switch konfigurieren und stellen Sie sicher, dass der SLB Host-Agent ausgeführt wird.  Die Router, die die Hosts dienen müssen gleich Kosten Multipfad (ECMP) Routing und Border Gateway Protocol (BGP) unterstützen und müssen zum Annehmen von BGP-Peers Anforderungen aus den SLB MUXes konfiguriert werden.  
  
Es folgt eine Übersicht über die SLB-Infrastruktur.  

![Software-Netzwerklastenausgleich-Infrastruktur](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
Die folgenden Abschnitte enthalten weitere Informationen zu diesen Elementen der SLB-Infrastruktur.  
  
### <a name="scvmm"></a>SCVMM  
Mit System Center 2016 können Sie Netzwerkcontroller unter Windows Server2016, einschließlich der SLB-Manager und Systemmonitor konfigurieren. Sie können auch System Center SLB MUXs bereitstellen und SLB-Host-Agents auf Computern installieren, auf denen Windows Server2016 und Hyper-V ausgeführt werden.  
  
Weitere Informationen zu System Center 2016, finden Sie unter [System Center 2016](https://www.microsoft.com/en-us/server-cloud/products/system-center-2016/).  
  
> [!NOTE]  
> Wenn Sie nicht System Center 2016 verwenden möchten, können Sie Windows PowerShell oder eine andere Anwendung zum Installieren und Konfigurieren von Netzwerk-Controller und andere SLB-Infrastruktur. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="network-controller"></a>Netzwerkcontroller  
Netzwerkcontroller hostet die SLB-Manager und führt die folgenden Aktionen für SLB.  
  
-   Prozesse SLB-Befehle, die über die Northbound-API von System Center, Windows PowerShell oder einem anderen Netzwerk-Management-Anwendung stammen.  
  
-   Berechnet die Richtlinie für die Verteilung an Hyper-V-Hosts und SLB MUXes.  
  
-   Enthält den Status der SLB-Infrastruktur.  
  
### <a name="slb-mux"></a>SLB MUX  
Der MUX SLB eingehenden Netzwerkdatenverkehr verarbeitet VIPs DIP zugeordnet, und leitet den Datenverkehr in der richtigen DIP. Jede MUX verwendet außerdem BGP VIP-Routen in Edge-Router zu veröffentlichen. BGP-Keepalive benachrichtigt MUXes beim Ausfall einer MUX active MUXes zum Verteilen der Last beim Ausfall eines MUX - Bereitstellung im Wesentlichen für den Netzwerklastenausgleich für den Lastenausgleich ermöglicht.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Hosts, auf denen Hyper-V ausgeführt wird  
Sie können SLB mit Computern, auf denen Windows Server2016 und Hyper-V ausgeführt werden. Die virtuellen Maschinen auf dem Hyper-V-Host können jedes beliebige Betriebssystem auszuführen, die von Hyper-V unterstützt wird.  
  
### <a name="slb-host-agent"></a>SLB Host-Agent  
Wenn Sie SLB bereitstellen, müssen Sie System Center, Windows PowerShell oder eine andere Anwendung des SLB Host-Agent auf jedem Hyper-V-Host-PC verwenden. Sie können der SLB Host-Agent für alle Versionen von Windows Server2016 installieren, die Hyper-V-Unterstützung, einschließlich Nano Server bereitstellen.  
  
Der Agent SLB überwacht SLB richtlinienupdates aus dem Netzwerkcontroller. Darüber hinaus Programme der hostagent Regeln für SLB, in den SDN-fähige Hyper-V virtuellen Switches, die auf dem lokalen Computer konfiguriert sind.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>SDN-fähigen virtuellen Hyper-V-Switch  
Verwenden Hyper-V Virtual Switch-Manager oder Windows PowerShell-Befehle, um den Switch zu erstellen, und Sie müssen Virtual Filtering Platform (VFP) für den virtuellen Switch aktivieren, für ein virtueller Switch mit SLB, kompatibel.  
  
Informationen zum Aktivieren der VFP für virtuelle Switches finden Sie in Windows PowerShell-Befehle [Get-VMSystemSwitchExtension](https://technet.microsoft.com/en-us/library/hh848603.aspx) und [Enable-VMSwitchExtension](https://technet.microsoft.com/en-us/library/hh848541.aspx?f=255&MSPPError=-2147217396).  
  
Der SDN-fähigen virtuellen Hyper-V-Switch führt die folgenden Aktionen für SLB.  
  
-   Verarbeitet den Datenpfad für SLB.  
  
-   Empfängt eingehenden Netzwerkdatenverkehr von den MUX.  
  
-   Der MUX für ausgehenden Netzwerkverkehr an den Router mithilfe der DSR gesendet wird, umgeht.  
  
-   Auf Nano Server-Instanzen von Hyper-V ausgeführt wird.  
  
### <a name="bgp-enabled-router"></a>BGP-fähigen Router  
Der BGP-Router führt die folgenden Aktionen für SLB.  
  
-   Leitet eingehende Datenverkehr zu den MUX ECMP verwenden.  
  
-   Für ausgehenden Netzwerkverkehr verwendet die Route, die vom Host bereitgestellt wird.  
  
-   Routeupdates überwacht für VIPs aus SLB MUX.  
  
-   SLB MUXes entfernt aus der Drehung SLB, wenn Keep Alive ein Fehler auftritt.  
  
## <a name="bkmk_features"></a>Features der Software Load Balancing  
Es folgen einige der Features und Funktionen des SLB.  
  
**Kernfunktionen**  
  
-   SLB bietet Layer-4-Lastenausgleich Dienste für 'Nord-Süd' und "Ost-West" TCP/UDP-Datenverkehr  
  
-   Sie können auf einem Hyper-V-Netzwerkvirtualisierung-basierten Netzwerk SLB verwenden.  
  
-   Sie können SLB mit einem VLAN-basierten Netzwerk für die DIP-VMs mit einem SDN aktiviert Hyper-V Virtual Switch verbunden.  
  
-   Ein SLB Instanz kann mehrere Mandanten behandeln.  
  
-   SLB und DIP unterstützen einen skalierbaren und mit geringer Wartezeit kehren Pfad durch direkte Server zurückgegeben (DSR) implementiert.  
  
-   SLB-Funktionen, wenn Sie auch Switch Embedded Teaming (SET) oder Single Root Input/Output Virtualization (SR-IOV) verwenden  
  
-   SLB enthält Internet Protocol Version 4 (IPv4) unterstützen  
  
-   Für die Standort-zu-Standort-Gateway-Szenarios bietet SLB NAT-Funktionalität, um alle Standort-zu-Standort-Verbindungen mit eine einzelne öffentliche IP-Adresse verwenden aktivieren  
  
-   Sie können SLB, einschließlich der Server-Agent und den MUX, unter Windows Server2016 Core und Nano-Installation installieren.  
  
**Skalierung und Leistung**  
  
-   Bereit für die Cloud-Skalierung, einschließlich mit horizontaler Skalierung-Funktion und Skalieren der Funktion für MUXes und Host-Agents.  
  
-   Eine aktive Netzwerkcontroller SLB-Manager-Modul kann 8 MUX-Instanzen unterstützen.  
  
**Hohe Verfügbarkeit**  
  
-   Sie können SLB auf mehr als 2 Knoten in einer Aktiv/Aktiv-Konfiguration bereitstellen.  
  
-   MUXes hinzugefügt, und aus dem Pool MUX ohne Auswirkungen auf den Dienst SLB entfernt werden können. Dies gewährleistet die SLB Verfügbarkeit bei   
    Einzelne MUXes sind gepatcht werden.  
  
-   Einzelne MUX-Instanzen haben eine Betriebszeit von 99%  
  
-   Überwachungsdaten ist für die Verwaltung Entitäten verfügbar  
  
**Ausrichtung**  
  
-   Sie können bereitstellen und Konfigurieren von SLB mit SCVMM  
  
-   SLB bietet eine einheitliche mehrinstanzenfähigen Edge durch nahtlose Integration mit Microsoft-Einheiten, wie der RAS-Mehrinstanzenfähiges Gateway, Datacenter Firewall und Route-Reflector.  
  

