---
title: NIC-Teaming-MAC-Adresse verwenden und Verwaltung
description: Wenn Sie ein NIC-Team mit dem Switch-unabhängigen Modus und entweder Address Hash oder Dynamic Load Distribution konfigurieren, verwendet das Team die Media Access Control (Mac)-Adresse des primären NIC-Teammitglieds für ausgehenden Datenverkehr. Das primäre NIC-Team Mitglied ist ein Netzwerkadapter, der vom Betriebssystem aus der anfänglichen Gruppe von Team Mitgliedern ausgewählt wird.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26d105e0-afc3-44b5-bb5e-0c884a4c5d62
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3ff03dae44600ff79ed22d298ee338c570e61e36
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405491"
---
# <a name="nic-teaming-mac-address-use-and-management"></a>NIC-Teaming-MAC-Adresse verwenden und Verwaltung

>Gilt für: Windows Server 2016

Wenn Sie ein NIC-Team mit dem Switch-unabhängigen Modus und entweder Address Hash oder Dynamic Load Distribution konfigurieren, verwendet das Team die Media Access Control (Mac)-Adresse des primären NIC-Teammitglieds für ausgehenden Datenverkehr. Das primäre NIC-Team Mitglied ist ein Netzwerkadapter, der vom Betriebssystem aus der anfänglichen Gruppe von Team Mitgliedern ausgewählt wird.  Es ist das erste Teammitglied, das nach der Erstellung oder nach dem Neustart des Host Computers an das Team gebunden werden soll. Da sich das primäre Teammitglied bei jedem Start auf nicht deterministische Weise ändern kann, wenn die NIC-Aktion deaktiviert/aktiviert oder andere Neukonfigurations Aktivitäten ausgeführt werden, kann sich das primäre Teammitglied ändern, und die Mac-Adresse des Teams kann variieren.  
  
In den meisten Fällen verursacht dies keine Probleme, aber es gibt einige Fälle, in denen Probleme auftreten können.  
  
Wenn das primäre Teammitglied aus dem Team entfernt und dann in den Betrieb versetzt wird, liegt möglicherweise ein Mac-Adress Konflikt vor. Deaktivieren Sie die Team Schnittstelle, und aktivieren Sie Sie dann, um diesen Konflikt zu beheben. Der Prozess der Deaktivierung und anschließenden Aktivierung der Team Schnittstelle bewirkt, dass die Schnittstelle eine neue Mac-Adresse aus den verbleibenden Teammitgliedern auswählt und somit den Mac-Adress Konflikt beseitigt.  
  
Sie können die Mac-Adresse des NIC-Teams auf eine bestimmte MAC-Adresse festlegen, indem Sie Sie in der primären Team Schnittstelle festlegen, so wie Sie dies auch beim Konfigurieren der Mac-Adresse einer beliebigen physischen NIC tun können.  
  
## <a name="mac-address-use-on-transmitted-packets"></a>Mac-Adress Verwendung für übertragene Pakete  
Wenn Sie ein NIC-Team im Wechsel unabhängigen Modus konfigurieren und entweder die Hash-oder dynamische Lastenverteilung durchsetzen, werden die Pakete aus einer einzelnen Quelle (z. b. eine einzelne VM) gleichzeitig auf mehrere Team Mitglieder verteilt. Um zu verhindern, dass die Switches verwirrt werden, und um Mac-Fluktuation-Alarme zu verhindern, wird die MAC-Quelladresse durch eine andere Mac-Adresse in den Frames ersetzt, die auf andere Teammitglieder als das primäre Teammitglied übertragen werden. Aus diesem Grund verwendet jedes Teammitglied eine andere Mac-Adresse, und Mac-Adresskonflikte werden verhindert, wenn ein Fehler auftritt.  
  
Wenn ein Fehler auf der primären NIC erkannt wird, startet die NIC-Team Vorgangs Software die Mac-Adresse des primären Teammitglieds auf dem Teammitglied, das als temporäres primäres Teammitglied fungieren soll (d. h. das Konto, das nun als primäres Teammitglied angezeigt wird. mber).  Diese Änderung gilt nur für Datenverkehr, der an das primäre Teammitglied mit der Mac-Adresse des primären Teammitglieds als Quell-MAC-Adresse gesendet wird. Der andere Datenverkehr wird weiterhin mit der Quell-MAC-Adresse gesendet, die vor dem Auftreten des Fehlers verwendet wurde.  
  
Im folgenden finden Sie Listen, die das Austausch Verhalten des NIC-Team Vorgangs für Mac-Adressen basierend auf der Konfiguration des Teams beschreiben:  
  
1.  **Im Wechsel unabhängigen Modus mit Adress Hash Verteilung**  
  
    -   Alle ARP-und NS-Pakete werden an das primäre Teammitglied gesendet.  
  
    -   Der gesamte Datenverkehr, der auf Netzwerkkarten außer dem primären Teammitglied gesendet wird, wird mit der geänderten Quell-MAC-Adresse gesendet, die der NIC entspricht, an der Sie gesendet werden.  
  
    -   Der gesamte an das primäre Teammitglied gesendete Datenverkehr wird mit der ursprünglichen MAC-Quelladresse gesendet (bei der es sich um die Mac-Adresse des Teams handeln kann).  
  
2.  **Im Wechsel unabhängigen Modus mit der Hyper-V-Port Verteilung**  
  
    -   Jeder VMSwitch-Port ist einem Teammitglied zugeordnet.  
  
    -   Jedes Paket wird an das Teammitglied gesendet, dem der Port zugeordnet ist.  
  
    -   Keine Quell-Mac-Ersetzung durchgeführt  
  
3.  **Im Wechsel unabhängigen Modus mit dynamischer Verteilung**  
  
    -   Jeder VMSwitch-Port ist einem Teammitglied zugeordnet.  
  
    -   Alle ARP/NS-Pakete werden an das Teammitglied gesendet, dem der Port zugeordnet ist.  
  
    -   Für Pakete, die für das Teammitglied gesendet werden, dem das affininitisierte Teammitglied angehört, ist keine Quell-MAC-Adressen Ersetzung abgeschlossen  
  
    -   Für Pakete, die für ein anderes Teammitglied als das affininitisierte Teammitglied gesendet werden, wird die Mac-Adresse der Quelle abgeschlossen.  
  
4.  **Im Switch-abhängigen Modus (alle Verteilungen)**  
  
    -   Es wird keine Quell-MAC-Adressen Ersetzung durchgeführt.  
  
## <a name="related-topics"></a>Verwandte Themen
- [NIC](NIC-Teaming.md)-Team Vorgang: In diesem Thema erhalten Sie einen Überblick über den NIC-Team Vorgang (Network Interface Card) in Windows Server 2016. Mit dem NIC-Team Vorgang können Sie zwischen einem und 32 physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  

- [Einstellungen für NIC](nic-teaming-settings.md)-Team Vorgänge: In diesem Thema erhalten Sie einen Überblick über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.
  
- [Erstellen eines neuen NIC-Teams auf einem Host Computer oder einer VM](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md): In diesem Thema erstellen Sie ein neues NIC-Team auf einem Host Computer oder auf einem virtuellen Hyper-V-Computer (VM), auf dem Windows Server 2016 ausgeführt wird.

- [Problem](Troubleshooting-NIC-Teaming.md)Behandlung beim NIC-Team Vorgang: In diesem Thema wird erläutert, wie Sie Probleme mit dem NIC-Team Vorgang beheben, wie z. b. Hardware, physische switchwertgeräte und das Deaktivieren oder Aktivieren von Netzwerkadaptern mithilfe von Windows PowerShell. 
  


