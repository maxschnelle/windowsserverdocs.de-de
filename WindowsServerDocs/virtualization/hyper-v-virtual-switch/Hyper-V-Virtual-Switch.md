---
title: Virtueller Hyper-V-Switch
description: Dieses Thema enthält eine Übersicht über den virtuellen Hyper-V-Switch in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c508005af67e9dd5b0c9a22693aca25eb19e8e48
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366833"
---
# <a name="hyper-v-virtual-switch"></a>Virtueller Hyper-V-Switch

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält eine Übersicht über den virtuellen Hyper-V-Switch, mit dem Sie virtuelle Computer \(vms @ no__t-1 mit Netzwerken verbinden können, die sich außerhalb des Hyper @ no__t-2V-Hosts befinden, einschließlich Intranet und Internet der Organisation. 

Sie können auch eine Verbindung mit virtuellen Netzwerken auf dem Server herstellen, auf dem Hyper @ no__t-0V ausgeführt wird, wenn Sie Software-Defined Networking \(sdn @ no__t-2 bereitstellen.

> [!NOTE]  
> Zusätzlich zu diesem Thema ist die folgende Dokumentation zum virtuellen Hyper-V-Switch verfügbar.  
>   
> - [Verwalten virtueller Hyper-V-Switches](Manage-Hyper-V-Virtual-Switch.md) 
> - [Remotezugriff auf den direkten Speicher (RDMA) und Switch Embedded Teaming (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Cmdlets für Netzwerk Switch-Team in Windows PowerShell](https://technet.microsoft.com/library/jj553812.aspx)
> - [Neues in VMM 2016](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [Einrichten des VMM-netzwerkfabrics](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [Erstellen von Netzwerken mit VMM 2012](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [hyper-V: Konfigurieren von VLANs und VLAN-Kennzeichnung @ no__t-0  
> - [hyper-V: Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn Sie für Erweiterungen von Drittanbietern erforderlich ist @ no__t-0
>
> Weitere Informationen zu anderen Netzwerktechnologien finden Sie unter [Netzwerk in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).
  
Der virtuelle Hyper @ no__t-0V-Switch ist ein softwarebasierter Layer-2-Ethernet-Netzwerk Switch, der im Hyper @ no__t-1V-Manager verfügbar ist, wenn Sie die Server Rolle "Hyper @ no__t-2V" installieren.

Der virtuelle Hyper-V-Switch umfasst Programm gesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen.  
  
> [!NOTE]  
> Der virtuelle Hyper-V-Switch unterstützt nur Ethernet und keine anderen drahtgebundenen lokalen Netzwerk (LAN)-Technologien, wie z. B. Infiniband und Fibre Channel.  
  
Der virtuelle Hyper-V-Switch umfasst Mandanten Isolations Funktionen, Datenverkehrs Strukturierung, Schutz vor böswilligen virtuellen Computern und vereinfachte Problembehandlung. 

Mit der integrierten Unterstützung für die Netzwerkgeräte Schnittstelle \(ndis @ no__t-1-Filtertreiber und Windows-Filter Plattform \(wfp @ no__t-3-Legenden-Treiber ermöglicht der virtuelle Hyper-V-Switch unabhängige Softwarehersteller \(isvs @ no__ t-5 zum Erstellen erweiterbarer Plug-ins, die als Erweiterungen für virtuelle Switches bezeichnet werden, die erweiterte Netzwerk-und Sicherheitsfunktionen bieten können. Erweiterungen für virtuelle Switches, die Sie dem virtuellen Hyper-V-Switch hinzufügen, werden im Manager für virtuelle Switches des Hyper-V-Managers angezeigt.
  
In der folgenden Abbildung verfügt ein virtueller Computer über eine virtuelle NIC, die über einen Switchport mit dem virtuellen Hyper-V-Switch verbunden ist.  
  
![Verbindungen mit virtuellen Switches](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Die Funktionen des virtuellen Hyper-V-Switches bieten Ihnen weitere Optionen zum Erzwingen der Isolation von Mandanten, zum Strukturieren und Steuern von Netzwerk Datenverkehr und zum Anwenden von Schutzmaßnahmen gegen schädliche virtuelle Computer.

>[!NOTE]
> In Windows Server 2016 zeigt ein virtueller Computer mit einer virtuellen NIC genau den maximalen Durchsatz für die virtuelle NIC an. Klicken Sie zum Anzeigen der Geschwindigkeit der virtuellen NIC unter **Netzwerkverbindungen**mit der rechten Maustaste auf das gewünschte virtuelle NIC-Symbol, und klicken Sie dann auf **Status**. Das Dialogfeld **Status** der virtuellen NIC wird geöffnet. In **Verbindung**entspricht der Wert der **Geschwindigkeit** der Geschwindigkeit der physischen NIC, die auf dem Server installiert ist.
  
## <a name="bkmk_apps"></a>Verwendung für virtuellen Hyper-V-Switch

Im folgenden finden Sie einige Anwendungsszenarien für den virtuellen Hyper-V-Switch.

**Anzeigen von Statistiken**: Ein Entwickler bei einem Cloudhostinganbieter implementiert ein Verwaltungspaket, mit dem der aktuelle Zustand des virtuellen Hyper-V-Switches angezeigt wird. Das Verwaltungspaket kann aktuelle Funktionen, Konfigurationseinstellungen und individuelle Portnetzwerkstatistiken mit WMI für den gesamten Switch abfragen. Der Status des Switches wird dann angezeigt, um Administratoren eine kurze Übersicht über den Switch zu geben.  
  
**Ressourcen Nachverfolgung**: Eine Hostingfirma vertreibt Hostingdienste, deren Preise sich nach der Ebene der Mitgliedschaft richten. Die verschiedenen Mitgliedschaftsebenen umfassen unterschiedliche Netzwerkleistungsebenen. Der Administrator ordnet die Ressourcen so zu, dass die Netzwerkverfügbarkeit entsprechend den Anforderungen der SLAs gleichmäßig verteilt ist. Der Administrator verfolgt Informationen wie die aktuelle Nutzung der zugewiesenen Bandbreite und die Anzahl zugewiesener VM-Warteschlangen (Virtual Machine Queue, VMQ) oder IOV-Kanäle Programm gesteuert. Dasselbe Programm protokolliert außerdem in regelmäßigen Abständen die verwendeten Ressourcen zusätzlich zu den zugewiesenen Ressourcen pro virtuellem Computer, sodass die Ressourceneinträge doppelt erfasst werden.  
  
**Verwalten der Reihenfolge von switcherweiterungen**: Ein Unternehmen hat Erweiterungen auf seinem Hyper-V-Host installiert, um den Datenverkehr überwachen und die Erkennung von Eindringversuchen melden zu können. Während der Wartung werden möglicherweise einige Erweiterungen aktualisiert, was zu Änderungen in der Reihenfolge der Erweiterungen führt. Ein einfaches Skriptprogramm wird ausgeführt, um die Erweiterungen nach einer Aktualisierung wieder zu ordnen.  
  
**Weiterleitungs Erweiterung verwaltet VLAN-ID**: Ein großes Switchunternehmen erstellt eine Weiterleitungserweiterung, über die alle Richtlinien für das Netzwerk angewendet werden. Ein verwaltetes Element sind IDs für virtuelle lokale Netzwerke (Virtual Local Area Network, VLAN). Der virtuelle Switch übergibt die Kontrolle des VLAN an eine Weiterleitungserweiterung. Die Installation des switchunternehmens ruft Programm gesteuert eine-API (Windows-Verwaltungsinstrumentation (WMI)-Anwendungsprogrammierschnittstelle (Application Programming Interface, API) auf, die die Transparenz übernimmt und den virtuellen Hyper-V-Switch anteilt, die VLAN-Tags zu übergeben und keine Aktionen auszuführen.  
  
## <a name="bkmk_func"></a>Funktionalität des virtuellen Hyper-V-Switches
 
Einige der Prinzipalfeatures, die der Hyper-V-Switch umfasst, sind:  
  
-   **ARP/ND-Vergiftungen-Schutz (Spoofing)** : Bietet Schutz vor einem schädlichen virtuellen Computer, der per ARP-Spoofing (Address Resolution-Protokoll) versucht, IP-Adressen von anderen virtuellen Computern zu stehlen. Bietet Schutz vor Angriffen, die per Nachbarermittlungs-Spoofing (Neighbor Discovery, ND) für IPv6 gestartet werden können.  
  
-   **Schutz durch DHCP-Wächter**: Bietet Schutz vor einem schädlichen virtuellen Computer, der sich als DHCP-Server (Dynamic Host Configuration-Protokoll) für Man-in-the-middle-Angriffe ausgibt.  
  
-   **Port-ACLs**: Ermöglichen die Filterung von Datenverkehr basierend auf MAC- oder IP-Adressen bzw. Bereichen (Media Access Control/Internet Protocol) und somit die Einrichtung der Isolation virtueller Netzwerke.  
  
-   **Trunk Modus zu einem**virtuellen Computer: Ermöglicht Administratoren die Einrichtung eines bestimmten virtuellen Computers als virtuelles Gerät und die anschließende Weiterleitung von Datenverkehr verschiedener VLANs an den virtuellen Computer.  
  
-   **Überwachung des Netzwerk Datenverkehrs**: Ermöglicht Administratoren die Überprüfung von Datenverkehr, der den Netzwerkswitch durchläuft.  
  
-   **Isoliertes (privates) VLAN**: Ermöglicht Administratoren die Aufteilung von Datenverkehr auf mehrere VLANs, um die Einrichtung isolierter Mandantencommunities zu vereinfachen.  
  
Im Folgenden finden Sie eine Liste der Funktionen, die die Verwendbarkeit des virtuellen Hyper-V-Switches verbessern:  
  
-   **Bandbreitenbeschränkung und Burst Unterstützung**: Per Bandbreitenmindestwert wird sichergestellt, dass immer eine bestimmte Menge an Bandbreite reserviert ist. Die maximale Bandbreite begrenzt die Bandbreite, die ein virtueller Computer belegen kann.  
  
-   **Unterstützung von expliziten Überlastungs Benachrichtigungen (ECN)** :  Mithilfe der ECN-Kennzeichnung (auch als Data centertcp (dctcp) bezeichnet) kann der physische Switch und das Betriebssystem den Fluss des Datenverkehrs so regulieren, dass die Puffer Ressourcen des Switches nicht überflutet werden. Dies führt zu einem höheren Durchsatz beim Datenverkehr.  
  
-   **Diagnose**: Die Diagnose ermöglicht die einfache Ablaufverfolgung und Überwachung von Ereignissen und Paketen über den virtuellen Switch.
