---
title: NIC-Teaming-MAC-Adresse verwenden und Verwaltung
description: Beim Konfigurieren eines NIC-Teams mit unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung steuern das Team verwendet, die die MAC-Adresse (MAC) des primären Mitglieds-NIC-Team für ausgehenden Datenverkehr. Dem primären NIC-Team-Mitglied ist, einen Netzwerkadapter, die vom Betriebssystem aus den anfänglichen Satz von Team-Mitglieder ausgewählt wird.
manager: dougkim
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
ms.openlocfilehash: 074a55d2f0a5423af5892ed73dc8a2b8dbda9d5b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824251"
---
# <a name="nic-teaming-mac-address-use-and-management"></a>NIC-Teaming-MAC-Adresse verwenden und Verwaltung

>Gilt für: Windows Server 2016

Beim Konfigurieren eines NIC-Teams mit unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung steuern das Team verwendet, die die MAC-Adresse (MAC) des primären Mitglieds-NIC-Team für ausgehenden Datenverkehr. Dem primären NIC-Team-Mitglied ist, einen Netzwerkadapter, die vom Betriebssystem aus den anfänglichen Satz von Team-Mitglieder ausgewählt wird.  Es ist das erste Teammitglied an das Team zu binden, nach der Erstellung oder nachdem der Hostcomputer neu gestartet wurde. Da das primäre Teammitglied in eine nicht deterministische Weise bei jedem Startvorgang ändern kann, NIC aktivieren/deaktivieren-Aktion oder andere Neukonfiguration-Aktivitäten, die primären Teammitglied ändern und die MAC-Adresse des Teams variieren kann.  
  
In den meisten Fällen nicht dies Probleme verursachen, aber es gibt einige Fälle, in dem Probleme auftreten können.  
  
Wenn das primäre Teammitglied vom Team entfernt und klicken Sie dann in Betrieb möglicherweise ein MAC-Adressenkonflikts vorhanden sein. Um diesen Konflikt zu beheben, deaktivieren Sie, und klicken Sie dann aktivieren Sie die teamschnittstelle. Der Prozess der deaktivieren und aktivieren die teamschnittstelle bewirkt, dass die Schnittstelle für die restlichen Mitglieder des Teams, sodass nicht die MAC-Adressenkonflikts wählen Sie eine neue MAC-Adresse.  
  
Sie können die MAC-Adresse des NIC-Teams auf eine bestimmte MAC-Adresse festlegen, indem in der primären teamschnittstelle festlegen wie können beim Konfigurieren der MAC-Adresse physischen Netzwerkkarte.  
  
## <a name="mac-address-use-on-transmitted-packets"></a>Verwenden Sie die MAC-Adresse auf gesendeten Pakete  
Wenn Sie ein NIC-Team im unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung konfigurieren, die Pakete aus einer einzelnen Quelle (z. B. einen einzelnen virtuellen Computer) gleichzeitig verteilt mehreren Teammitgliedern. Um zu verhindern, dass die Switches verwechselt abrufen und MAC Alarme Fluktuation zu verhindern, wird die Quell-MAC-Adresse mit einer anderen MAC-Adresse für die Teammitglieder als das primäre Teammitglied übertragenen Frames ersetzt. Aus diesem Grund jedes Teammitglied verwendet eine andere MAC-Adresse und MAC-Adresskonflikte werden verhindert, es sei denn, und bis der Fehler auftritt.  
  
Wenn ein Fehler auf die primäre NIC erkannt wird, beginnt die NIC-Teamvorgang-Software mit MAC-Adresse des primären Teammitglieds auf das Teammitglied aus, das ausgewählt wird, dient als temporäre primären Teammitglieds (d. h., das Element, die jetzt mit dem Switch als dem primären Team mich angezeigt werden l).  Diese Änderung gilt nur für Datenverkehr, der ging gesendet werden auf dem primären Team-Mitglied mit MAC-Adresse des primären Teammitglieds als die Quell-MAC-Adresse verwendet werden. Anderer Datenverkehr wird weiterhin mit den Quell-MAC-Adresse gesendet werden, die sie vor dem Ausfall verwendet haben, würden.  
  
Folgendes sind Listen, die beschreiben das Verhalten der NIC-Teamvorgang-MAC-Adresse ersetzen, basierend auf wie das Team konfiguriert ist:  
  
1.  **Im Modus für Switchunabhängig mit hashverteilung Adresse**  
  
    -   Alle ARP- und NS-Pakete werden auf dem primären Team-Mitglied gesendet.  
  
    -   Der gesamte Datenverkehr, die auf NICs als das primäre Teammitglied werden gesendet, mit der MAC-Quelladresse, die geändert wird, entsprechend die NIC auf dem sie gesendet werden  
  
    -   Der gesamte Datenverkehr auf dem primären Team-Element wird mit der ursprünglichen Quelle MAC-Adresse gesendet (die des Teams Quell-MAC-Adresse sein kann).  
  
2.  **Im Switch unabhängigen Modus mit Hyper-V-Port-Verteilung**  
  
    -   Jede VmSwitch-Port ist an ein anderes Teammitglied zugeordnet.  
  
    -   Jedes Paket wird auf dem Teammitglied gesendet, der der Port zugeordnet ist  
  
    -   Es erfolgt kein Quell-MAC-Ersatz  
  
3.  **Im Modus für Switchunabhängig mit dynamische Verteilung**  
  
    -   Jede VmSwitch-Port ist an ein anderes Teammitglied zugeordnet.  
  
    -   Alle ARP/NS-Pakete werden auf dem Teammitglied gesendet, die der Port zugeordnet ist  
  
    -   Pakete, die auf dem Teammitglied, das das kategorisierter Teammitglied gesendet haben kein Quell-MAC-Adresse ersetzen durchgeführt  
  
    -   Pakete, die auf ein anderes Teammitglied kategorisierter Teammitglieds gesendet werden Quelle MAC-Adresse ersetzen durchgeführt haben.  
  
4.  **Im abhängigen Switch-Modus (alle Verteilungen)**  
  
    -   Keine Quelle Ersatz der MAC-Adresse wird ausgeführt.  
  
## <a name="related-topics"></a>Verwandte Themen
- [NIC-Teamvorgang](NIC-Teaming.md): In diesem Thema stellen wir Ihnen in Windows Server 2016 einen Überblick über die Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang. NIC-Teamvorgang ermöglicht Ihnen, zwischen 1 und 32 gruppieren, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  

- [Einstellungen für die NIC-Teamvorgang](nic-teaming-settings.md): In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.
  
- [Erstellen eines neuen NIC-Teams auf einem Host oder virtuellen Computer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md): In diesem Thema erstellen Sie einen neuen NIC-Teams auf einem Hostcomputer oder in einer Hyper-V-Computer (VM) unter Windows Server 2016.

- [Problembehandlung bei der NIC-Teamvorgang](Troubleshooting-NIC-Teaming.md): In diesem Thema werden Möglichkeiten zum Beheben von NIC-Teamvorgang, z. B. Hardware, Wertpapiere der physische Switch und das Deaktivieren oder aktivieren Netzwerkadapter, die mithilfe von Windows PowerShell beschrieben. 
  


