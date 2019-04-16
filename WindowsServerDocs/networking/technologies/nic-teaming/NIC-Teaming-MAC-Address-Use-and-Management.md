---
title: NIC-Teaming-MAC-Adresse und Verwaltung
description: Dieses Thema enthält Informationen wie NIC-Teamvorgang verwendet, das die MAC-Adresse (MAC) in Windows Server 2016 steuern.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26d105e0-afc3-44b5-bb5e-0c884a4c5d62
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ab624665c964b100e6b1ed633120299b55e37df
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nic-teaming-mac-address-use-and-management"></a>NIC-Teaming-MAC-Adresse und Verwaltung

>Gilt für: Windows Server 2016

Wenn Sie ein NIC-Team mit unabhängigen Switch-Modus und Adressen-Hash oder dynamische Verteilung konfigurieren, steuern das Team verwendet die MAC-MAC-Adresse des primären Mitglieds NIC-Team für ausgehenden Datenverkehr. Die primäre NIC-Team angehört, einen Netzwerkadapter, die vom Betriebssystem aus dem ersten Satz von Teammitglieder ausgewählt.  
  
Die primären Teammitglied ist das erste Teammitglied zum Binden an das Team, nach der Erstellung oder nach dem Neustart der Host-PC. Da die primären Teammitglied auf nicht deterministische Weise bei jedem Start ändern kann, NIC aktivieren/deaktivieren Aktion oder andere Neukonfiguration Aktivitäten, die primären Teammitglied ändern und die MAC-Adresse des Teams abweichen kann.  
  
In den meisten Fällen ist dies Probleme verursachen, aber es gibt einige Fälle, in denen Probleme auftreten können.  
  
Wenn das primäre Teammitglied vom Team entfernt und klicken Sie dann in Betrieb möglicherweise ein Konflikt der MAC-Adresse. Um dieses Problem zu beheben, deaktivieren Sie und aktivieren Sie dann die teamschnittstelle. Der Prozess der deaktivieren und aktivieren die teamschnittstelle bewirkt, dass die Schnittstelle für Wählen Sie eine neue MAC-Adresse aus der verbleibenden Teammitglieder, sodass die MAC-Adressenkonflikts nicht.  
  
Sie können die MAC-Adresse des NIC-Teams auf eine bestimmte MAC-Adresse festlegen, indem in der primären teamschnittstelle Einstellung wie können beim Konfigurieren der MAC-Adresse des alle physischen NIC  
  
## <a name="mac-address-use-on-transmitted-packets"></a>Verwenden Sie die MAC-Adresse auf übertragene Pakete  
Wenn Sie ein NIC-Team in unabhängigen Modus wechseln und Adressen-Hash oder dynamische Verteilung konfigurieren, die Pakete aus einer einzigen Quelle (z. B. einen einzelnen virtuellen Computer) wird gleichzeitig verteilt über mehrere Teammitglieder. Um zu verhindern, dass die Switches erste verwechselt und MAC schlagenden Alarme zu verhindern, ist die Quell-MAC-Adresse mit einer anderen MAC-Adresse auf den auf Teammitglieder als primären Teammitglieds übertragener Frames ersetzt. Aus diesem Grund jedes Teammitglied verwendet eine andere MAC-Adresse und MAC-Adressenkonflikte werden verhindert, und es sei denn, bis ein Fehler auftritt.  
  
Wenn ein Fehler auf die primäre NIC erkannt wird, beginnt die NIC-Teaming-Software mithilfe des primären Teammitglieds MAC-Adresse auf dem Mitglied des Sicherheitsteams, das ausgewählt wird, und dient als temporäre primären Teammitglieds (d. h., die eine, die mit dem Switch als primären Teammitglieds jetzt angezeigt werden).  Diese Änderung gilt nur für Datenverkehr, die sollte gesendet werden auf dem primären Teammitglied mit MAC-Adresse des primären Teammitglieds als Quelle MAC-Adresse. Andere Datenverkehr wird weiterhin mit den Quell-MAC-Adresse gesendet werden, die vor dem Auftreten des Fehlers verwendet.  
  
Es folgen Listen, die beschreiben, NIC-Teaming-MAC-Adresse Ersatz-Verhalten abhängig, wie das Team konfiguriert ist:  
  
1.  **Im Switch unabhängigen Modus Adressen-Hash-Verteilung**  
  
    -   Alle ARP- und NS-Pakete werden auf dem primären Teammitglied gesendet.  
  
    -   Der gesamte Datenverkehr für NICs als primären Teammitglieds werden gesendet, mit der MAC-Quelladresse angepasst die NIC auf dem sie gesendet werden  
  
    -   Der gesamte Datenverkehr auf dem primären Teammitglied wird mit der ursprünglichen Quelle MAC-Adresse gesendet (der das Team Quell-MAC-Adresse sein)  
  
2.  **Im Switch unabhängigen Modus mit Hyper-V-Port-Verteilung**  
  
    -   Jeder VmSwitch-Port wird zu einem Teammitglied affinitized.  
  
    -   Jedes Paket wird auf dem Teammitglied gesendet, der der Port affinitized ist  
  
    -   Kein Quell-MAC-Austausch erfolgt.  
  
3.  **Im Switch unabhängigen Modus mit dynamische Verteilerliste**  
  
    -   Jeder VmSwitch-Port wird zu einem Teammitglied affinitized.  
  
    -   Alle ARP/NS-Pakete werden auf dem Teammitglied gesendet, die der Port affinitized ist  
  
    -   Pakete, die auf dem Team-Member, der die affinitized Teammitglied gesendet haben kein Quell-MAC-Adresse Ersatz "Fertig"  
  
    -   Über ein Teammitglied als affinitized Teammitglieds gesendete Pakete müssen Quelle MAC-Adresse Ersatz "Fertig"  
  
4.  **Im Switch abhängige Modus (alle Verteilungen)**  
  
    -   Kein Quell-MAC-Adresse Ersatz wird ausgeführt.  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen eines neuen NIC-Teams auf einem Host- oder virtuellen Computer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)  
[NIC-Teamvorgang](NIC-Teaming.md)  
  


