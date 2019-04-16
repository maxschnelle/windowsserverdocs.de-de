---
title: NIC-Teamvorgang
description: Dieses Thema enthält eine Übersicht über Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abded6f3-5708-4e35-9a9e-890e81924fec
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 142f56153187368effdb802c0c1b50359fffc36a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nic-teaming"></a>NIC-Teamvorgang

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält eine Übersicht über Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang in Windows Server 2016.

> [!NOTE]  
> Zusätzlich zu diesem Thema wird der folgende Inhalt NIC-Teaming verfügbar.  
>   
> - [NIC-Teamvorgang auf virtuellen Maschinen & #40; VMs & #41;](nict-vms.md)
> - [NIC-Teamvorgang und virtuelle lokale Netzwerke & #40; VLANs & #41;](nict-and-vlans.md)
> - [NIC-Teaming-MAC-Adresse und Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md)
> - [Problembehandlung bei der NIC-Teamvorgang](Troubleshooting-NIC-Teaming.md) 
> - [Erstellen eines neuen NIC-Teams auf einem Host- oder virtuellen Computer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)
> - [NIC-Teamvorgang (NetLBFO)-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/jj130849.aspx)
> - TechNet Gallery herunterladen: [führt Windows Server 2016-NIC und Switch Embedded Teaming-Benutzer](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)
  
## <a name="bkmk_over"></a>NIC-Teamvorgang: Übersicht  
NIC-Teaming ermöglicht Ihnen, zwischen einem und 32 physische Ethernet-Netzwerkadapter in einen oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei einem Fehler des Netzwerkadapters.  
  
NIC-Team Element Netzwerkadapter müssen in dem gleichen physischen Hostcomputer in einem Team platziert werden installiert sein.  
  
> [!NOTE]  
> Ein NIC-Teams, die nur einen Netzwerkadapter enthält bereitstellen keine Lastenausgleich und Failover; jedoch mit einem einzelnen Netzwerkadapter können Sie NIC-Teamvorgang für die Trennung des Netzwerkverkehrs, wenn Sie auch virtuelle lokale Netzwerke (VLANs) verwenden.  
  
Wenn Sie Netzwerkkarten in einem NIC-Team konfigurieren, sind sie in der NIC teaming Lösung allgemeingültigen Kern, klicken Sie dann einen oder mehrere virtuelle Adapter (auch als Team NICs [tNICs] oder Team Schnittstellen) für das Betriebssystem zeigt verbunden. Windows Server 2016 unterstützt bis zu 32 Team Schnittstellen pro Team. Es gibt eine Vielzahl von Algorithmen, die ausgehenden Datenverkehr (Load) zwischen NICs zu verteilen.  
  
Die folgende Abbildung zeigt ein NIC-Team mit mehreren tNICs.  
  
![NIC-Team mit mehreren tNICs](../../media/NIC-Teaming/nict_overview.jpg)  
  
Darüber hinaus können Sie Ihre einem Team verwendete NIC mit dem gleichen Switch oder mit verschiedenen Switches herstellen. Wenn Sie Netzwerkkarten mit verschiedenen Switches zu verbinden, müssen beide Switches im selben Subnetz sein.  
  
## <a name="bkmk_avail"></a>NIC-Teaming-Verfügbarkeit  
NIC-Teamvorgang ist in allen Versionen von Windows Server 2016 verfügbar. Darüber hinaus können Sie Windows PowerShell-Befehle, Remotedesktop und Remote Server Administration Tools, um NIC-Teamvorgang von Computern zu verwalten, die ein Clientbetriebssystem ausgeführt werden, auf denen die Tools unterstützt werden.  
  
## <a name="bkmk_nics"></a>Unterstützte und nicht unterstützte NICs für den NIC-Teamvorgang  
Sie können alle Ethernet-NIC, die den Windows-Hardware-Qualifikation und -Logo-Test (WHQL-Tests) in einem NIC-Team in Windows Server 2016 bestanden hat.  
  
Die folgenden NICs können in einem NIC-Team platziert werden.  
  
-   Hyper-V virtuelle Netzwerkadapter, die Hyper-V Virtual Switch-Ports in der Hostpartition nicht als Netzwerkkarten verfügbar sind.  
  
    > [!IMPORTANT]  
    > Virtuelle Hyper-V-NICs, die in der Hostpartition (vNICs) verfügbar gemacht werden, müssen nicht in einem Team platziert werden. Teamvorgang vNICs innerhalb der Host-Partition wird in eine Konfiguration oder eine Kombination nicht unterstützt. Versuche, eine Team könnte einen vollständigen Verlust der Kommunikation, wenn Netzwerkfehler auftreten.  
  
-   Der Kerneldebugger-Netzwerkadapter (KDNIC).  
  
-   Netzwerkkarten, die für den Netzwerkstart verwendet werden.  
  
-   Netzwerkkarten, die andere Ethernet, z. B. WWAN, WLAN-/ WLAN, Bluetooth und Infiniband, einschließlich Internetprotokoll über NICs Infiniband (IPoIB) verwenden.  
  
## <a name="bkmk_compat"></a>NIC-Teaming-Kompatibilität  
NIC-Teamvorgang ist kompatibel mit allen netzwerktechnologien in Windows Server 2016 mit den folgenden Ausnahmen.  
  
-   **Single-Root-e/a-Virtualisierung (SR-IOV)**. Bei SR-IOV werden Daten direkt an die Netzwerkschnittstellenkarte übermittelt, ohne Umweg über den Netzwerkstapel (in der Host-Betriebssystem, bei der Virtualisierung). Aus diesem Grund ist es nicht möglich, dass das NIC-Team zu untersuchen oder die Daten an einen anderen Pfad im Team umleiten.  
  
-   **Systemeigene Host Quality of Service (QoS)**. Wenn QoS-Richtlinien für festgelegt sind ist ein systemeigenes oder Host-System und diese Richtlinien aufrufen Mindestbandbreite Einschränkungen, der Gesamtdurchsatz für ein NIC-Team kleiner als ohne die Bandbreitenrichtlinien vorhanden sein kann.  
  
-   **TCP-Chimney**. TCP-Chimney ist mit NIC-Teamvorgänge, weil der TCP-Chimney den gesamten Netzwerkstapel direkt an die NIC lagert nicht unterstützt  
  
-   **802.1 x-Authentifizierung**. Die 802.1X-Authentifizierung sollte nicht mit NIC-Teamvorgang verwendet werden. Einige Optionen lassen sich nicht auf die Konfiguration der 802. 1 X-Authentifizierung und NIC-Teamvorgang auf den gleichen Port aus.  
  
Weitere Informationen zum NIC-Teaming mithilfe von virtuellen Computern (VMs), die auf einem Hyper-V-Host ausgeführt werden, finden Sie unter [NIC-Teamvorgang in virtuellen Maschinen & #40; VMs & #41; ](../../technologies/nic-teaming/../../technologies/nic-teaming/NIC-Teaming-in-Virtual-Machines--VMs-.md).  
  
## <a name="bkmk_vmq"></a>NIC-Teaming und Warteschlangen für virtuelle Computer (Vmq)  
VMQ und NIC-Teamvorgang funktionieren gut zusammen; VMQ muss aktiviert sein, wenn Hyper-V aktiviert ist. Je nach Konfiguration Switch-Modus und der Verteilungsalgorithmus laden präsentiert NIC-teaming entweder VMQ-Funktionen mit dem Hyper-V-Switch, die die Anzahl der Warteschlangen für die kleinste Anzahl von Warteschlangen, die von jedem Adapter im Team (Min-Warteschlangen-Modus) unterstützt werden oder die Gesamtanzahl der verfügbaren Warteschlangen auf allen Teammitgliedern (Summe der Warteschlangen Modus) angezeigt.  
  
Insbesondere ist das Team im Switch unabhängigen teaming-Modus und die Verteilung auf Hyper-V-Port oder dynamische Modus festgelegt ist, wird die Anzahl der Warteschlangen gemeldet ist die Summe aller Warteschlangen, die von den Teammitgliedern (Summe der Warteschlangen Modus); Andernfalls ist die Anzahl der Warteschlangen gemeldet, die kleinste Anzahl von Warteschlangen, die von jedem Mitglied des Teams (Min-Warteschlangen-Modus) unterstützt.  
  
Dies hat folgende Gründe:  
  
-   Bei der Switch unabhängigen Team im Hyper-V-Port oder dynamische Modus wird die eingehende Datenverkehr für einen Hyper-V-Switch-Port (VM) immer auf dem gleichen Teammitglied ankommen. Der Host kann Vorhersagen/Kontrolle die Member den Datenverkehr für eine bestimmte virtuelle Maschine erhalten, damit NIC-Teaming sorgfältigere über welche VMQ-Warteschlange auf einem bestimmten Teammitglied zugewiesen werden können. NIC-Teaming, arbeiten mit der Hyper-V-Switch, der VMQ für eine virtuelle Maschine auf genau ein Teammitglied fest und wissen, dass die Warteschlange eingehender Datenverkehr auftritt.  
  
-   Wenn das Team in alle abhängigen Switch-Modus (statischer Teamvorgang oder Teamvorgang LACP), ist die Option, die das Team verbunden ist steuert die Verteilung des eingehenden Datenverkehr. Der Host-NIC-Teaming-Software kann nicht vorherzusagen, welche Team Member den eingehenden Datenverkehr für eine virtuelle Maschine erhalten und möglicherweise, dass der Switch den Datenverkehr für eine virtuelle Maschine auf allen Teammitgliedern verteilt. Als Ergebnis der NIC-Teaming-Software funktioniert mit dem Hyper-V-Switch eine Warteschlange für den virtuellen Computer auf jedem Mitglied des Sicherheitsteams Programme, nicht nur ein Teammitglied.  
  
-   Wenn das Team im switchunabhängige Modus befindet und eine Adresse Load-Verteilung Hashalgorithmus verwendet, wird der eingehende Datenverkehr immer eine Netzwerkkarte (primäre Teammitglieds) – alle Daten auf nur einem Teammitglied stammen. Da andere Teammitglieder mit eingehenden Datenverkehr, denen sie mit programmiert abrufen zu tun sind nicht in die Warteschlange gleich als dem primären Mitglied, damit andere Ausfall der primäre Mitglied Teammitglied kann verwendet werden, um den eingehenden Datenverkehr übernehmen und die Warteschlangen bereits vorhanden sind.  
  
Die meisten NICs haben Warteschlangen auf, die für (erhalten Side Scaling, RSS) oder VMQ, aber nicht beide gleichzeitig verwendet werden können. Einige VMQ-Einstellungen werden Einstellungen für RSS-Warteschlangen angezeigt, aber es sind wirklich Einstellungen auf die generischen Warteschlangen auf, die sowohl RSS-als auch VMQ verwenden, je nachdem, welches Feature aktuell verwendet wird. Jede Netzwerkkarte verfügt, die Eigenschaften für erweiterte Werte für * RssBaseProcNumber und \*MaxRssProcessors. Im folgenden werden einige VMQ-Einstellungen, die Systemleistung verbessert.  
  
-   Im Idealfall sollten jede Netzwerkkarte haben die * RssBaseProcNumber legen Sie auf eine gerade Zahl größer als oder gleich zwei (2). Dies ist, da es sich bei den ersten physischen Prozessor Core 0 (logische Prozessoren 0 und 1), in der Regel wird der Großteil System verarbeitet, die Netzwerk-Verarbeitung von diesem physischen Prozessor gelenkten werden sollte. (Einige Computerarchitektur verfügen nicht über zwei logische Prozessoren pro physischem Prozessor damit für solche Computer die base-Prozessor größer als oder gleich 1 sein soll. Wenn Sie im Zweifelsfall Annahme, dass der Host eine 2 logischen Prozessor pro physischen Prozessor-Architektur verwendet.)  
  
-   In der Summe der Warteschlangen Modus ist das Team sollte die Teammitglieder Prozessoren, das Ausmaß praktisch, übereinander sein. In einem 4-Core-Host (8 logische Prozessoren) mit einem Team 2 10 Gbps Netzwerkkarten festlegen Sie z. B. den ersten Basis 2-Prozessor und 4 Kerne nutzen. die zweite würde verwenden grundlegende Prozessor 6 und 2 Kerne festgelegt werden.  
  
-   Im Prozessor wird von den Mitgliedern des Teams verwendet müssen identisch sein, wenn das Team im Min-Warteschlangen-Modus befindet.  
  
## <a name="bkmk_hnv"></a>NIC-Teaming und Hyper-V-Netzwerkvirtualisierung (HNV)  
NIC-Teamvorgang ist vollständig kompatibel mit Hyper-V-Netzwerkvirtualisierung (HNV).  Das Hyper-v-Verwaltungssystem Informationen zum NIC-Teaming Treiber, der Verteilung die Last auf eine Weise, die für den Hyper-v-Datenverkehr optimiert ist NIC-Teaming ermöglicht.  
  
## <a name="bkmk_live"></a>NIC-Teaming und Live-Migration  
NIC-Teamvorgang in virtuelle Maschinen hat keine Auswirkungen auf Livemigration. Die gleichen Regeln vorhanden sind für die Live-Migration, ob der NIC-Teamvorgang auf dem virtuellen Computer konfiguriert ist oder nicht.  
  
## <a name="see-also"></a>Siehe auch  
[NIC-Teamvorgang auf virtuellen Maschinen & #40; VMs & #41;](../../technologies/nic-teaming/../../technologies/nic-teaming/NIC-Teaming-in-Virtual-Machines--VMs-.md)  
  


