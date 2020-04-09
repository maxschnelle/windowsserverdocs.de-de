---
title: Softwarelastenausgleich (SLB) für SDN
description: In diesem Thema erfahren Sie mehr über den Software Lastenausgleich für Software-Defined Networking in Windows Server 2016.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 97abf182-4725-4026-801c-122db96964ed
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 245faa00eed6f8ee49f8d178ab2cde5d01b1e23e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859573"
---
# <a name="software-load-balancing-slb-for-sdn"></a>Software Lastenausgleich \(SLB-\) für Sdn

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über den Software Lastenausgleich für Software-Defined Networking in Windows Server 2016.  

Clouddienstanbieter (Cloud Service Providers, CSPs) und Unternehmen, die Software-Defined Networking (SDN) in Windows Server 2016 bereitstellen, können den Software Lastenausgleich (SLB) verwenden, um den Netzwerk Datenverkehr von Mandanten und Mandanten Kunden gleichmäßig auf die Ressourcen Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.
  
Windows Server SLB bietet die folgenden Funktionen.  
  
-   Lasten Ausgleichs Dienste der Ebene 4 (L4) für "Nord-Süd" und "Ost-West" TCP/UDP-Datenverkehr.  
  
-   Öffentlicher und interner Netzwerk Datenverkehr für den Lastenausgleich.  
  
-   Unterstützt dynamische IP-Adressen (Dips) in virtuellen lokalen Netzwerken (Virtual Local Area Networks, VLANs) und in virtuellen Netzwerken, die Sie mithilfe der Hyper-V-Netzwerkvirtualisierung erstellen.  
  
-   Unterstützung der Integritätsprüfung.  
  
-   Bereit für die cloudskalierung, einschließlich Funktionen für horizontales Skalieren und zentrales hochskalieren für Multiplexer und Host-Agents.  
  
Weitere Informationen finden Sie unter [Software Load Balancing Features](#bkmk_features) in diesem Thema.  
  
> [!NOTE]  
> Die mehr Instanzen Fähigkeit für VLANs wird vom Netzwerk Controller nicht unterstützt. Sie können jedoch VLANs mit SLB für verwaltete Workloads von Dienstanbietern verwenden, z. b. die Rechenzentrumsinfrastruktur und Webserver mit hoher Dichte.  
  
Mithilfe von Windows Server SLB können Sie die Lasten Ausgleichs Funktionen mithilfe von SLB-VMS auf denselben Hyper-V-Computeservern, die Sie für Ihre anderen VM-Workloads verwenden, horizontal hochskalieren. Daher unterstützt SLB das schnelle Erstellen und Löschen von Lasten Ausgleichs Endpunkten, die für den CSP-Betrieb erforderlich sind. Außerdem unterstützt Windows Server SLB zehn Gigabyte pro Cluster, bietet ein einfaches Bereitstellungs Modell und lässt sich problemlos horizontal hoch-und Herunterskalieren.  
  
**Funktionsweise von SLB**  
  
SLB ordnet virtuelle IP-Adressen (VIPs) dynamischen IP-Adressen (Dips) zu, die Teil eines clouddienstsatzes von Ressourcen im Rechenzentrum sind.  
  
VIPs sind einzelne IP-Adressen, die öffentlichen Zugriff auf einen Pool von virtuellen Computern mit Lastenausgleich ermöglichen. VIPs sind z. b. IP-Adressen, die im Internet verfügbar gemacht werden, sodass Mandanten und Mandanten Kunden eine Verbindung mit Mandanten Ressourcen im cloudrechenzentrum herstellen können.  
  
Dips sind die IP-Adressen der Mitglieds-VMS eines Pools mit Lastenausgleich hinter der VIP. Dips werden den Mandanten Ressourcen innerhalb der cloudinfrastruktur zugewiesen.  
  
VIPs befinden sich im SLB Multiplexer (MUX).  Der Mux besteht aus mindestens einem virtuellen Computer (Virtual Machines, VMS).  Der Netzwerk Controller stellt jedem VIP jede beliebige VIP-Adresse zur Verfügung, und jedes MUX verwendet Border Gateway Protocol (BGP), um den Routern im physischen Netzwerk eine/32-Route ankündigen zu können.  BGP ermöglicht den physischen Netzwerk Routern Folgendes:  
  
-   Erfahren Sie, dass eine VIP-Adresse für jedes MUX verfügbar ist, auch wenn sich die muxes in unterschiedlichen Subnetzen in einem Layer 3-Netzwerk befinden.  
  
-   Verteilen Sie die Last für jede VIP über alle verfügbaren muxes mithilfe von ECMP-Routing (equal cost Multipfad).  
  
-   Automatisches Erkennen von MUX-Fehlern oder Entfernen von Datenverkehr an das fehlgeschlagene MUX.  
  
-   Verteilen Sie die Last von der fehlerhaften oder entfernten MUX-Auslastung auf die fehlerfreien muxes.  
  
Wenn öffentlicher Datenverkehr aus dem Internet eingeht, untersucht SLB MUX den Datenverkehr, der die VIP als Ziel enthält, und ordnet den Datenverkehr zu und schreibt ihn so, dass er bei einer einzelnen DIP-Adresse ankommt. Für eingehenden Netzwerk Datenverkehr wird diese Transaktion in einem zweistufigen Prozess durchgeführt, der zwischen den virtuellen MUX-Computern (VMS) und dem Hyper-V-Host, auf dem sich die Ziel-DIP befindet, aufgeteilt wird:  
  
-   Lastenausgleich: der Mux verwendet die VIP, um eine DIP auszuwählen, kapselt das Paket und leitet den Datenverkehr an den Hyper-V-Host weiter, auf dem sich die DIP-Adresse befindet.  
  
-   Netzwerk Adressübersetzung (Network Address Translation, NAT): der Hyper-V-Host entfernt die Kapselung aus dem Paket, übersetzt die VIP in eine DIP-Adresse, ordnet die Ports neu zu und leitet das Paket an die DIP-VM weiter.  
  
Der Mux weiß, wie Sie VIPs den richtigen Dips zuordnen, weil Sie mithilfe des Netzwerk Controllers Richtlinien für den Lastenausgleich definieren. Zu diesen Regeln gehören das Protokoll, der Front-End-Port, der Back-End-Port und der Verteilungs Algorithmus (5, 3 oder 2 Tupel).  
  
Wenn Mandanten-VMS Antworten und ausgehenden Netzwerk Datenverkehr an die Internet-oder Remote Mandanten Standorte zurücksenden, weil die NAT vom Hyper-v-Host ausgeführt wird, umgeht der Datenverkehr das MUX und wechselt direkt vom Hyper-v-Host zum edgerouter. Dieser MUX-Umgehungs Prozess wird als Direct Server Return (DSR) bezeichnet.  
  
Nachdem der anfängliche Netzwerkdaten Verkehrsfluss festgelegt wurde, umgeht der eingehende Netzwerk Datenverkehr den SLB-MUX vollständig.  
  
In der folgenden Abbildung führt ein Client Computer eine DNS-Abfrage für die IP-Adresse einer SharePoint-Unternehmenswebsite aus, in diesem Fall ein fiktives Unternehmen mit dem Namen "". Der folgende Vorgang wird ausgeführt.  
  
-   Der DNS-Server gibt die VIP-107.105.47.60 an den Client zurück.  
  
-   Der Client sendet eine HTTP-Anforderung an die VIP.  
  
-   Das physische Netzwerk verfügt über mehrere Pfade, um die VIP zu erreichen, die sich auf einem beliebigen MUX befindet.  Jeder Router verwendet ECMP, um das nächste Segment des Pfads auszuwählen, bis die Anforderung bei einer MUX eintrifft.  
  
-   Der Mux, der die Anforderung empfängt, überprüft konfigurierte Richtlinien und erkennt, dass zwei Dips, 10.10.10.5 und 10.10.20.5, in einem virtuellen Netzwerk verfügbar sind, um die Anforderung an die VIP zu verarbeiten 107.105.47.60  
  
-   Die MUX wählt die DIP-10.10.10.5 aus und kapselt die Pakete mithilfe von vxlan, damit Sie Sie mithilfe der physischen Netzwerkadresse des Hosts an den Host mit der DIP-Adresse senden können.  
  
-   Der Host empfängt das gekapselte Paket und überprüft es.  Die Kapselung wird entfernt, und das Paket wird neu geschrieben, sodass das Ziel jetzt die DIP-10.10.10.5 anstelle der VIP-Adresse ist und den Datenverkehr an die DIP-VM sendet.  
  
-   Die Anforderung hat nun die SharePoint-Website von "Site" in Server Farm 2 erreicht. Der Server generiert eine Antwort und sendet Sie an den Client, wobei seine eigene IP-Adresse als Quelle verwendet wird.  
  
-   Der Host fängt das ausgehende Paket im virtuellen Switch ab, das speichert, dass der Client, nun das Ziel, die ursprüngliche Anforderung an die VIP gerichtet hat.  Der Host schreibt die Quelle des Pakets in die VIP-Datei, damit die DIP-Adresse für den Client nicht angezeigt wird.  
  
-   Der Host leitet das Paket direkt an das Standard Gateway für das physische Netzwerk weiter, das seine Standard Routing Tabelle verwendet, um das Paket an den Client weiterzuleiten, der die Antwort schließlich empfängt.  
  
![Software Lastenausgleich-Prozess](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**Lastenausgleich für internen Daten Center-Datenverkehr**  
  
Beim Lastenausgleich des internen Netzwerk Datenverkehrs zum Rechenzentrum, z. b. zwischen Mandanten Ressourcen, die auf unterschiedlichen Servern ausgeführt werden und Mitglieder desselben virtuellen Netzwerks sind, führt der virtuelle Hyper-V-Switch, mit dem die virtuellen Computer verbunden sind, NAT aus.  
  
Beim internen Lastenausgleich des Datenverkehrs wird die erste Anforderung an das MUX gesendet und von diesem verarbeitet, das die entsprechende DIP-Abladung auswählt und den Datenverkehr an die DIP leitet. Ab diesem Zeitpunkt umgeht der etablierte Daten Verkehrsfluss das MUX und wechselt direkt von der VM zum virtuellen Computer.  
  
**Integritätstests**  
  
SLB umfasst Integritätstests zum Überprüfen der Integrität der Netzwerkinfrastruktur, einschließlich der folgenden.  
  
-   TCP-Test an Port  
  
-   HTTP-Test an Port und URL  
  
Anders als bei einer herkömmlichen Load Balancer-Appliance, bei der der Test auf dem Gerät basiert und über die Verbindung zu der DIP verläuft, stammt der SLB-Test von dem Host, auf dem sich die DIP-Datei befindet, und wechselt direkt vom SLB-Host-Agent zum DIP und verteilt die Arbeiten Sie auf den Hosts.  
  
## <a name="software-load-balancing-infrastructure"></a><a name="bkmk_infrastructure"></a>Infrastruktur für den Software Lastenausgleich  
Zum Bereitstellen von Windows Server SLB müssen Sie zuerst den Netzwerk Controller in Windows Server 2016 und mindestens eine SLB MUX-VM bereitstellen.  
  
Außerdem müssen Sie Hyper-v-Hosts mit dem SDN-fähigen virtuellen Hyper-v-Switch konfigurieren und sicherstellen, dass der SLB-Host-Agent ausgeführt wird.  Die Router, die die Hosts bedienen, müssen das ECMP-Routing (equal cost Multipfad) und Border Gateway Protocol (BGP) unterstützen. Sie müssen so konfiguriert werden, dass BGP-peeringanforderungen von den SLB-muxes akzeptiert werden.  
  
Im folgenden finden Sie eine Übersicht über die SLB-Infrastruktur.  

![Infrastruktur für den Software Lastenausgleich](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
In den folgenden Abschnitten finden Sie weitere Informationen zu diesen Elementen der SLB-Infrastruktur.  
  
### <a name="scvmm"></a>SCVMM  
Mit System Center 2016 können Sie den Netzwerk Controller unter Windows Server 2016 konfigurieren, einschließlich des SLB-Managers und der System Überwachung. Sie können auch mit System Center SLB-muxs bereitstellen und SLB-Host-Agents auf Computern installieren, auf denen Windows Server 2016 und Hyper-V ausgeführt werden.  
  
Weitere Informationen zu System Center 2016 finden Sie unter [System Center 2016](https://www.microsoft.com/server-cloud/products/system-center-2016/).  
  
> [!NOTE]  
> Wenn Sie System Center 2016 nicht verwenden möchten, können Sie Windows PowerShell oder eine andere Verwaltungs Anwendung verwenden, um Netzwerk Controller und andere SLB-Infrastrukturen zu installieren und zu konfigurieren. Weitere Informationen finden Sie unter Bereitstellen eines [Netzwerk Controllers mithilfe von Windows PowerShell](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="network-controller"></a>Netzwerkcontroller  
Der Netzwerk Controller hostet den SLB-Manager und führt die folgenden Aktionen für SLB aus.  
  
-   Verarbeitet SLB-Befehle, die über die Northbound-API von System Center, Windows PowerShell oder einer anderen Netzwerk Verwaltungs Anwendung kommen.  
  
-   Berechnet die Richtlinie für die Verteilung an Hyper-V-Hosts und SLB-muxes.  
  
-   Stellt den Integritäts Status der SLB-Infrastruktur bereit.  
  
### <a name="slb-mux"></a>SLB-MUX  
Der SLB-MUX verarbeitet den eingehenden Netzwerk Datenverkehr und ordnet VIPs zu Dips zu und leitet den Datenverkehr an die richtige DIP weiter. Jede MUX verwendet BGP auch zum Veröffentlichen von VIP-Routen auf Edge-Routern. BGP Keep Alive benachrichtigt muxes, wenn ein Mux ausfällt. Dadurch können aktive muxes die Last bei einem MUX-Fehler weiterverteilen, was im Grunde einen Lastenausgleich für die Lasten Ausgleichs Module bereitstellt.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Hosts, auf denen Hyper-V ausgeführt wird  
Sie können SLB mit Computern verwenden, auf denen Windows Server 2016 und Hyper-V ausgeführt werden. Die virtuellen Computer auf dem Hyper-v-Host können ein beliebiges Betriebssystem ausführen, das von Hyper-v unterstützt wird.  
  
### <a name="slb-host-agent"></a>SLB-Host-Agent  
Wenn Sie SLB bereitstellen, müssen Sie System Center, Windows PowerShell oder eine andere Verwaltungs Anwendung verwenden, um den SLB-Host-Agent auf jedem Hyper-V-Host Computer bereitzustellen. Sie können den SLB-Host-Agent auf allen Versionen von Windows Server 2016 installieren, die Hyper-V-Unterstützung einschließlich nano Server bereitstellen.  
  
Der SLB-Host-Agent lauscht auf SLB-Richtlinien Updates vom Netzwerk Controller. Außerdem werden von den Host-Agents Regeln für SLB in die Sdn-fähigen virtuellen Hyper-V-Switches integriert, die auf dem lokalen Computer konfiguriert sind.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>SDN-fähiger virtueller Hyper-V-Switch  
Damit ein virtueller Switch mit SLB kompatibel ist, müssen Sie den Hyper-V Virtual Switch Manager oder Windows PowerShell-Befehle verwenden, um den Switch zu erstellen. Anschließend müssen Sie die virtuelle Filter Plattform für den virtuellen Switch aktivieren.  
  
Informationen zum Aktivieren von VFP auf virtuellen Switches finden Sie unter den Windows PowerShell-Befehlen [Get-vmsystemswitchextension](https://technet.microsoft.com/library/hh848603.aspx) und [enable-vmswitchextension](https://technet.microsoft.com/library/hh848541.aspx?f=255&MSPPError=-2147217396).  
  
Der Sdn-aktivierte virtuelle Hyper-V-Switch führt die folgenden Aktionen für SLB aus.  
  
-   Verarbeitet den Datenpfad für SLB.  
  
-   Empfängt eingehenden Netzwerk Datenverkehr von der Mux.  
  
-   Umgeht das MUX für ausgehenden Netzwerk Datenverkehr und sendet es mithilfe von DSR an den Router.  
  
-   Wird auf Nano Server-Instanzen von Hyper-V ausgeführt.  
  
### <a name="bgp-enabled-router"></a>BGP-fähiger Router  
Der BGP-Router führt die folgenden Aktionen für SLB aus.  
  
-   Leitet eingehenden Datenverkehr mithilfe von ECMP an die MUX weiter.  
  
-   Bei ausgehendem Netzwerk Datenverkehr wird von die vom Host bereitgestellte Route verwendet.  
  
-   Lauscht auf Routen Aktualisierungen für VIPs aus SLB MUX.  
  
-   Entfernt SLB-muxes aus der SLB-Rotation, wenn Keep-Alive fehlschlägt.  
  
## <a name="software-load-balancing-features"></a><a name="bkmk_features"></a>Features für den Software Lastenausgleich  
Im folgenden finden Sie einige der Features und Funktionen von SLB.  
  
**Kernfunktionalität**  
  
-   SLB bietet Schicht 4-Lasten Ausgleichs Dienste für den TCP/UDP-Datenverkehr "Nord-Süd" und "Ost-West".  
  
-   Sie können SLB in einem Hyper-V-netzwerkvirtualisierungsbasierten Netzwerk verwenden.  
  
-   Sie können SLB mit einem VLAN-basierten Netzwerk für DIP-VMS verwenden, die mit einem Sdn-fähigen virtuellen Hyper-V-Switch verbunden sind.  
  
-   Eine SLB-Instanz kann mehrere Mandanten verarbeiten.  
  
-   SLB und DIP unterstützen einen skalierbaren Rückgabe Pfad mit geringer Latenz, wie von Direct Server Return (DSR) implementiert.  
  
-   SLB-Funktionen, wenn Sie auch Switch Embedded Teaming (Set) oder Single root Input/Output Virtualization (SR-IOV) verwenden  
  
-   SLB umfasst IPv4-Unterstützung (Internet Protocol Version 4).  
  
-   Für Site-to-Site-Gatewayszenarien bietet SLB NAT-Funktionen, um allen Standort-zu-Standort-Verbindungen die Verwendung einer einzelnen öffentlichen IP-Adresse zu ermöglichen.  
  
-   Sie können SLB einschließlich Host-Agent und MUX unter Windows Server 2016, Vollversion, Core und Nano installieren.  
  
**Skalierung und Leistung**  
  
-   Bereit für die cloudskalierung, einschließlich Funktionen für horizontales Skalieren und zentrales hochskalieren für muxes und Host-Agents.  
  
-   Ein aktives SLB-Manager-Netzwerk Controller Modul kann acht MUX-Instanzen unterstützen.  
  
**Hohe Verfügbarkeit**  
  
-   Sie können SLB auf mehr als zwei Knoten in einer aktiv/aktiv-Konfiguration bereitstellen.  
  
-   Muxes können hinzugefügt und aus dem MUX-Pool entfernt werden, ohne dass sich dies auf den SLB-Dienst auswirkt. Dies behält die SLB-Verfügbarkeit bei   
    einzelne muxes werden gepatcht.  
  
-   Einzelne MUX-Instanzen haben eine Betriebszeit von 99%.  
  
-   System Überwachungsdaten sind für Verwaltungs Entitäten verfügbar.  
  
**Richt**  
  
-   Sie können SLB mit SCVMM bereitstellen und konfigurieren.  
  
-   SLB bietet einen mehr Instanzen fähigen Unified Edge durch nahtlose Integration in Microsoft-Geräte, z. b. das mehr Instanzen fähige RAS-Gateway, die Datacenter Firewall und den Routen Reflektor.  
  

