---
title: Virtueller Hyper-V-Switch
description: Dieses Thema enthält eine Übersicht über virtuelle Hyper-V-Switch unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17962b9bbb90a5ea1b6a4a303c64d72f74be37b5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860921"
---
# <a name="hyper-v-virtual-switch"></a>Virtueller Hyper-V-Switch

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält eine Übersicht über virtuelle Hyper-V-Switch, die Sie mit der Möglichkeit zum Verbinden virtueller Computer bietet \(VMs\) , Netzwerke, die außerhalb der Hyper\-V-Host, einschließlich dem Intranet Ihrer Organisation und das Internet. 

Sie können auch eine Verbinden mit virtuellen Netzwerken auf dem Server mit Hyper\-V beim Bereitstellen von Software Defined Networking \(SDN\).

> [!NOTE]  
> Zusätzlich zu diesem Thema wird die folgende Dokumentation zum virtuellen Hyper-V-Switch verfügbar.  
>   
> - [Verwalten von virtuellen Hyper-V-Switch](Manage-Hyper-V-Virtual-Switch.md) 
> - [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Netzwerkswitchteams in Windows PowerShell](https://technet.microsoft.com/library/jj553812.aspx)
> - [Was ist neu in VMM 2016](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [Einrichten des VMM Netzwerk-fabric](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [Erstellen von Netzwerken mit VMM 2012](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-V: Konfigurieren von VLANs und VLAN-Kennzeichnung](https://social.technet.microsoft.com/wiki/contents/articles/1306.hyper-v-configure-vlans-and-vlan-tagging.aspx)  
> - [Hyper-V: Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie Erweiterungen von Drittanbietern erforderlich ist](https://social.technet.microsoft.com/wiki/contents/articles/13071.hyper-v-the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions.aspx)
>
> Weitere Informationen zu anderen netzwerktechnologien, finden Sie unter [Netzwerkfunktionen in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).
  
Hyper\-V Virtual Switch handelt es sich einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der verfügbar ist auf virtuellen Hyper\-bei der Installation der Hyper V-Manager\-V-Serverrolle.

Virtuelle Hyper-V-Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden von VMs mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen.  
  
> [!NOTE]  
> Der virtuelle Hyper-V-Switch unterstützt nur Ethernet und keine anderen drahtgebundenen lokalen Netzwerk (LAN)-Technologien, wie z. B. Infiniband und Fibre Channel.  
  
Virtuelle Hyper-V-Switch umfasst Funktionen für Mandanten isoliert, datenverkehrsstrukturierung, Schutz vor schädlichen virtuellen Computern und vereinfachte Problembehandlung. 

Mit integrierter Unterstützung für Network Device Interface Specification \(NDIS\) filtern, Treiber und Windows-Filterplattform \(WFP\) -Callout-Treibern, den virtuellen Hyper-V-Switch ermöglicht die unabhängige Hersteller \(ISVs\) erstellen erweiterbaren Plug-Ins, wird aufgerufen, virtuelle Switcherweiterungen, die erweiterte Funktionen von Netzwerkfunktionen und Sicherheit bereitstellen können. Erweiterungen für virtuelle Switches, die Sie dem virtuellen Hyper-V-Switch hinzufügen, werden im Manager für virtuelle Switches des Hyper-V-Managers angezeigt.
  
In der folgenden Abbildung hat ein virtuellen Computer eine virtuelle Netzwerkkarte, die mit der Hyper-V-Switch über einen Switchport verbunden ist.  
  
![Verbindungen für virtuelle Switches](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Hyper-V-Switches Funktionen bieten Ihnen mehr Optionen zur Erzwingung der Trennung von Mandanten, Strukturierung und Kontrolle des Netzwerkdatenverkehrs und Einsatz von Schutzmaßnahmen gegen schädlichen virtuellen Computern.

>[!NOTE]
> In Windows Server 2016 zeigt ein virtuellen Computer mit einer virtuellen Netzwerkkarte genau den maximalen Durchsatz für die virtuelle Netzwerkkarte. Anzeigen die virtuelle NIC-Geschwindigkeit in **Netzwerkverbindungen**mit der rechten Maustaste auf das gewünschte virtuelle NIC-Symbol, und klicken Sie dann auf **Status**. Die virtuelle NIC **Status** Dialogfeld wird geöffnet. In **Verbindung**, den Wert der **Geschwindigkeit** entspricht die Geschwindigkeit der physischen NIC auf dem Server installiert.
  
## <a name="bkmk_apps"></a>Verwendet für Hyper-V-Switch

Es folgen einige Szenarien zu Anwendungsfällen für Hyper-V-Switch.

**Anzeigen von Statistiken**: Ein Entwickler bei einem Cloudhostinganbieter implementiert ein Verwaltungspaket, mit dem der aktuelle Zustand des virtuellen Hyper-V-Switches angezeigt wird. Das Verwaltungspaket kann aktuelle Funktionen, Konfigurationseinstellungen und individuelle Portnetzwerkstatistiken mit WMI für den gesamten Switch abfragen. Der Status des Switches wird dann angezeigt, um Administratoren eine kurze Übersicht über den Switch zu geben.  
  
**Ressourcennachverfolgung**: Eine Hostingfirma vertreibt Hostingdienste, deren Preise sich nach der Ebene der Mitgliedschaft richten. Die verschiedenen Mitgliedschaftsebenen umfassen unterschiedliche Netzwerkleistungsebenen. Der Administrator ordnet die Ressourcen so zu, dass die Netzwerkverfügbarkeit entsprechend den Anforderungen der SLAs gleichmäßig verteilt ist. Der Administrator überwacht programmgesteuert Informationen wie die aktuelle Nutzung der zugewiesenen Bandbreite und die Anzahl der virtuellen Computer (VM) zugewiesen, Warteschlange für virtuelle Computer (VMQ) und IOV-Kanäle. Dasselbe Programm protokolliert außerdem in regelmäßigen Abständen die verwendeten Ressourcen zusätzlich zu den zugewiesenen Ressourcen pro virtuellem Computer, sodass die Ressourceneinträge doppelt erfasst werden.  
  
**Verwalten der Reihenfolge von switcherweiterungen**: Ein Unternehmen hat Erweiterungen auf seinem Hyper-V-Host installiert, um den Datenverkehr überwachen und die Erkennung von Eindringversuchen melden zu können. Während der Wartung werden möglicherweise einige Erweiterungen aktualisiert, was zu Änderungen in der Reihenfolge der Erweiterungen führt. Ein einfaches Skriptprogramm wird ausgeführt, um die Erweiterungen nach einer Aktualisierung wieder zu ordnen.  
  
**Weiterleitungserweiterung verwaltet VLAN-ID**: Ein großes Switchunternehmen erstellt eine Weiterleitungserweiterung, über die alle Richtlinien für das Netzwerk angewendet werden. Ein verwaltetes Element sind IDs für virtuelle lokale Netzwerke (Virtual Local Area Network, VLAN). Der virtuelle Switch übergibt die Kontrolle des VLAN an eine Weiterleitungserweiterung. Installation für die Switch-Unternehmens ruft programmgesteuert eine Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)-Anwendungsprogrammierschnittstelle (API), die die Transparenz aktiviert den Hyper-V-Switch übergeben und keine Aktionen für VLAN-Tags.  
  
## <a name="bkmk_func"></a>Funktionen der Hyper-V-Switches
 
Einige der Prinzipalfeatures, die der Hyper-V-Switch umfasst, sind:  
  
-   **ARP/ND Poisoning (spoofing) Schutz**: Bietet Schutz vor einem schädlichen virtuellen Computer, der per ARP-Spoofing (Address Resolution-Protokoll) versucht, IP-Adressen von anderen virtuellen Computern zu stehlen. Bietet Schutz vor Angriffen, die per Nachbarermittlungs-Spoofing (Neighbor Discovery, ND) für IPv6 gestartet werden können.  
  
-   **DHCP-Wächter Protection**: Bietet Schutz vor einem schädlichen virtuellen Computer, der sich als DHCP-Server (Dynamic Host Configuration-Protokoll) für Man-in-the-middle-Angriffe ausgibt.  
  
-   **Port-ACLs**: Ermöglichen die Filterung von Datenverkehr basierend auf MAC- oder IP-Adressen bzw. Bereichen (Media Access Control/Internet Protocol) und somit die Einrichtung der Isolation virtueller Netzwerke.  
  
-   **Trunkmodus zu einem virtuellen Computer**: Ermöglicht Administratoren die Einrichtung eines bestimmten virtuellen Computers als virtuelles Gerät und die anschließende Weiterleitung von Datenverkehr verschiedener VLANs an den virtuellen Computer.  
  
-   **Überwachung des Netzwerkdatenverkehrs**: Ermöglicht Administratoren die Überprüfung von Datenverkehr, der den Netzwerkswitch durchläuft.  
  
-   **Isoliertes (privates) VLAN**: Ermöglicht Administratoren die Aufteilung von Datenverkehr auf mehrere VLANs, um die Einrichtung isolierter Mandantencommunities zu vereinfachen.  
  
Im Folgenden finden Sie eine Liste der Funktionen, die die Verwendbarkeit des virtuellen Hyper-V-Switches verbessern:  
  
-   **Bandbreitengrenze und burstunterstützung**: Per Bandbreitenmindestwert wird sichergestellt, dass immer eine bestimmte Menge an Bandbreite reserviert ist. Die maximale Bandbreite begrenzt die Bandbreite, die ein virtueller Computer belegen kann.  
  
-   **Explicit Congestion Notification (ECN)-Kennzeichnung Unterstützung**:  -Kennzeichnung, auch bekannt als Data Center (DCTCP), kann der physischen Switches und Betriebssystem, um den Fluss des Datenverkehrs zu regulieren so, dass die Pufferressourcen des Switches nicht überflutet, dies führt zu höheren Durchsatz beim Datenverkehr.  
  
-   **Diagnose**: Die Diagnose ermöglicht die einfache Ablaufverfolgung und Überwachung von Ereignissen und Paketen über den virtuellen Switch.
