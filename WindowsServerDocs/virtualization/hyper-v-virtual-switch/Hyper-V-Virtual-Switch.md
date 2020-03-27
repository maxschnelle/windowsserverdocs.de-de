---
title: Virtueller Hyper-V-Switch
description: Dieses Thema enthält eine Übersicht über den virtuellen Hyper-V-Switch in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fb2ebf485b5004e457558fc16d8535662c0c5ff2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307980"
---
# <a name="hyper-v-virtual-switch"></a>Virtueller Hyper-V-Switch

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält eine Übersicht über den virtuellen Hyper-V-Switch, der Ihnen die Möglichkeit bietet, virtuelle Computer \(VMS\) mit Netzwerken zu verbinden, die sich außerhalb des Hyper\-V-Hosts befinden, einschließlich Intranet und Internet der Organisation. 

Sie können auch eine Verbindung mit virtuellen Netzwerken auf dem Server herstellen, auf dem Hyper\-V ausgeführt wird, wenn Sie Software-Defined Networking \(Sdn-\)bereitstellen.

> [!NOTE]  
> Zusätzlich zu diesem Thema ist die folgende Dokumentation zum virtuellen Hyper-V-Switch verfügbar.  
>   
> - [Verwalten virtueller Hyper-V-Switches](Manage-Hyper-V-Virtual-Switch.md) 
> - [Remotezugriff auf den direkten Speicher (RDMA) und Switch Embedded Teaming (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Cmdlets für Netzwerk Switch-Team in Windows PowerShell](https://technet.microsoft.com/library/jj553812.aspx)
> - [Neues in VMM 2016](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [Einrichten des VMM-netzwerkfabrics](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [Erstellen von Netzwerken mit VMM 2012](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-V: Konfigurieren von VLANs und VLAN-Tagging](https://social.technet.microsoft.com/wiki/contents/articles/1306.hyper-v-configure-vlans-and-vlan-tagging.aspx)  
> - [Hyper-V: die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn Sie für Erweiterungen von Drittanbietern erforderlich ist.](https://social.technet.microsoft.com/wiki/contents/articles/13071.hyper-v-the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions.aspx)
>
> Weitere Informationen zu anderen Netzwerktechnologien finden Sie unter [Netzwerk in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).
  
Beim virtuellen Hyper\-v-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerk Switch, der im Hyper\-v-Manager verfügbar ist, wenn Sie die Hyper\-v-Server Rolle installieren.

Der virtuelle Hyper-V-Switch umfasst Programm gesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen.  
  
> [!NOTE]  
> Der virtuelle Hyper-V-Switch unterstützt nur Ethernet und keine anderen drahtgebundenen lokalen Netzwerk (LAN)-Technologien, wie z. B. Infiniband und Fibre Channel.  
  
Der virtuelle Hyper-V-Switch umfasst Mandanten Isolations Funktionen, Datenverkehrs Strukturierung, Schutz vor böswilligen virtuellen Computern und vereinfachte Problembehandlung. 

Mit der integrierten Unterstützung für die netzwerkgeräteschnittstellen Spezifikation \(NDIS\) Filtertreiber und Windows-Filter Plattform \(WFP\) Legenden-Treiber ermöglicht der virtuelle Hyper-V-Switch unabhängigen Softwareanbietern \(ISVs\), erweiterbare Plug-ins zu erstellen, die als Erweiterungen für virtuelle Switches bezeichnet werden, die erweiterte Netzwerk-und Sicherheitsfunktionen bieten können. Erweiterungen für virtuelle Switches, die Sie dem virtuellen Hyper-V-Switch hinzufügen, werden im Manager für virtuelle Switches des Hyper-V-Managers angezeigt.
  
In der folgenden Abbildung verfügt ein virtueller Computer über eine virtuelle NIC, die über einen Switchport mit dem virtuellen Hyper-V-Switch verbunden ist.  
  
![Verbindungen mit virtuellen Switches](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Die Funktionen des virtuellen Hyper-V-Switches bieten Ihnen weitere Optionen zum Erzwingen der Isolation von Mandanten, zum Strukturieren und Steuern von Netzwerk Datenverkehr und zum Anwenden von Schutzmaßnahmen gegen schädliche virtuelle Computer.

>[!NOTE]
> In Windows Server 2016 zeigt ein virtueller Computer mit einer virtuellen NIC genau den maximalen Durchsatz für die virtuelle NIC an. Klicken Sie zum Anzeigen der Geschwindigkeit der virtuellen NIC unter **Netzwerkverbindungen**mit der rechten Maustaste auf das gewünschte virtuelle NIC-Symbol, und klicken Sie dann auf **Status**. Das Dialogfeld **Status** der virtuellen NIC wird geöffnet. In **Verbindung**entspricht der Wert der **Geschwindigkeit** der Geschwindigkeit der physischen NIC, die auf dem Server installiert ist.
  
## <a name="uses-for-hyper-v-virtual-switch"></a><a name="bkmk_apps"></a>Verwendung für virtuellen Hyper-V-Switch

Im folgenden finden Sie einige Anwendungsszenarien für den virtuellen Hyper-V-Switch.

**Anzeigen von Statistiken**: ein Entwickler bei einem gehosteten cloudhersteller implementiert ein Verwaltungspaket, in dem der aktuelle Status des virtuellen Hyper-V-Switches angezeigt wird. Das Verwaltungspaket kann aktuelle Funktionen, Konfigurationseinstellungen und individuelle Portnetzwerkstatistiken mit WMI für den gesamten Switch abfragen. Der Status des Switches wird dann angezeigt, um Administratoren eine kurze Übersicht über den Switch zu geben.  
  
**Ressourcen Nachverfolgung**: ein Hostingunternehmen verkauft Hostingdienste, die auf der Ebene der Mitgliedschaft abgerechnet werden. Die verschiedenen Mitgliedschaftsebenen umfassen unterschiedliche Netzwerkleistungsebenen. Der Administrator ordnet die Ressourcen so zu, dass die Netzwerkverfügbarkeit entsprechend den Anforderungen der SLAs gleichmäßig verteilt ist. Der Administrator verfolgt Informationen wie die aktuelle Nutzung der zugewiesenen Bandbreite und die Anzahl zugewiesener VM-Warteschlangen (Virtual Machine Queue, VMQ) oder IOV-Kanäle Programm gesteuert. Dasselbe Programm protokolliert außerdem in regelmäßigen Abständen die verwendeten Ressourcen zusätzlich zu den zugewiesenen Ressourcen pro virtuellem Computer, sodass die Ressourceneinträge doppelt erfasst werden.  
  
**Verwalten der Reihenfolge von switcherweiterungen**: ein Unternehmen hat Erweiterungen auf seinem Hyper-V-Host installiert, um den Datenverkehr zu überwachen und die Angriffs Erkennung zu melden. Während der Wartung werden möglicherweise einige Erweiterungen aktualisiert, was zu Änderungen in der Reihenfolge der Erweiterungen führt. Ein einfaches Skriptprogramm wird ausgeführt, um die Erweiterungen nach einer Aktualisierung wieder zu ordnen.  
  
**Weiterleitungs Erweiterung verwaltet VLAN-ID**: ein Haupt switchunternehmen baut eine Weiterleitungs Erweiterung auf, die alle Richtlinien für das Netzwerk anwendet. Ein verwaltetes Element sind IDs für virtuelle lokale Netzwerke (Virtual Local Area Network, VLAN). Der virtuelle Switch übergibt die Kontrolle des VLAN an eine Weiterleitungserweiterung. Die Installation des switchunternehmens ruft Programm gesteuert eine-API (Windows-Verwaltungsinstrumentation (WMI)-Anwendungsprogrammierschnittstelle (Application Programming Interface, API) auf, die die Transparenz übernimmt und den virtuellen Hyper-V-Switch anteilt, die VLAN-Tags zu übergeben und keine Aktionen auszuführen.  
  
## <a name="hyper-v-virtual-switch-functionality"></a><a name="bkmk_func"></a>Funktionalität des virtuellen Hyper-V-Switches
 
Einige der Prinzipalfeatures, die der Hyper-V-Switch umfasst, sind:  
  
-   **ARP/ND-Vergiftung (Spoofing)** : bietet Schutz vor böswilligen virtuellen Computern, die das Adressauflösungsprotokoll (ARP) Spoofing verwenden, um IP-Adressen von anderen virtuellen Computern zu stehlen. Bietet Schutz vor Angriffen, die per Nachbarermittlungs-Spoofing (Neighbor Discovery, ND) für IPv6 gestartet werden können.  
  
-   **DHCP Guard-Schutz**: schützt vor einem schädlichen virtuellen Computer, der sich als DHCP-Server (Dynamic Host Configuration-Protokoll) für man-in-the-Middle-Angriffe darstellt.  
  
-   **Port-ACLs**: ermöglicht das Filtern von Datenverkehr auf der Grundlage von Medien Access Control (Mac) oder IP-Adressen/-Bereichen (Internet Protocol), sodass Sie die Isolation virtueller Netzwerke einrichten können.  
  
-   **Trunk Modus zu VM**: ermöglicht Administratoren die Einrichtung eines bestimmten virtuellen Computers als virtuelles Gerät und die anschließende Weiterleitung von Datenverkehr von verschiedenen VLANs an den virtuellen Computer.  
  
-   **Überwachung des Netzwerk Datenverkehrs**: ermöglicht Administratoren das Überprüfen von Datenverkehr, der den Netzwerk Switch durchläuft.  
  
-   **Isoliertes (privates) VLAN**: ermöglicht Administratoren das Aufteilen von Datenverkehr auf mehrere VLANs, um die Einrichtung isolierter Mandanten Communities zu vereinfachen.  
  
Im Folgenden finden Sie eine Liste der Funktionen, die die Verwendbarkeit des virtuellen Hyper-V-Switches verbessern:  
  
-   **Bandbreitenbeschränkung und Burst Unterstützung**: die Mindestbandbreite garantiert die reservierte Bandbreite. Die maximale Bandbreite begrenzt die Bandbreite, die ein virtueller Computer belegen kann.  
  
-   **Unterstützung von expliziten Überlastungs Benachrichtigungen (ECN)** : ECN-Kennzeichnung, auch bekannt als Data centertcp (dctcp), ermöglicht dem physischen Switch und dem Betriebssystem, den Daten Verkehrsfluss so zu regulieren, dass die Puffer Ressourcen des Switches nicht überflutet werden. Dies führt zu einem höheren Durchsatz beim Datenverkehr.  
  
-   **Diagnose**: die Diagnose ermöglicht die einfache Ablauf Verfolgung und Überwachung von Ereignissen und Paketen über den virtuellen Switch.
