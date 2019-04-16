---
title: Erstellen eines neuen NIC-Teams auf einem Host- oder virtuellen Computer
description: Dieses Thema enthält Informationen zur Konfiguration der NIC-Teamvorgang, damit Sie wissen, dass die Auswahl, die Sie vornehmen müssen, bei der Konfiguration eines neuen NIC-Teams in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4caaa86-5799-4580-8775-03ee213784a3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6a9866d1f4e72b3c77c3233b5e5582d250cfe6a2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-new-nic-team-on-a-host-computer-or-vm"></a>Erstellen eines neuen NIC-Teams auf einem Host- oder virtuellen Computer

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält Informationen zur Konfiguration der NIC-Teamvorgang, damit Sie wissen, dass die Auswahl, die Sie vornehmen müssen, bei der Konfiguration eines neuen NIC-Teams. Dieses Thema enthält die folgenden Abschnitte.  
  
-   [Auswählen einer Teamvorgangsmodus](#bkmk_teaming)  
  
-   [Auswahl einer Modus](#bkmk_lb)  
  
-   [Wählen eine Einstellung Standby-Adapter](#bkmk_standby)  
  
-   [Mithilfe der primären Team Interface-Eigenschaft](#bkmk_primary)  
  
> [!NOTE]  
> Wenn Sie diese Konfigurationselemente bereits vertraut sind, können Sie die folgenden Verfahren, NIC-Teamvorgang konfigurieren.  
>   
> -   [Erstellen eines neuen NIC-Teams auf einem virtuellen Computer](../../technologies/nic-teaming/Create-a-New-NIC-Team-in-a-VM.md)  
> -   [Erstellen eines neuen NIC-Teams](../../technologies/nic-teaming/Create-a-New-NIC-Team.md)  
  
Bei der Erstellung eines neuen NIC-Teams müssen Sie die folgenden Eigenschaften für den NIC-Team konfigurieren.  
  
-   Teamname  
  
-   Mitgliederadapter  
  
-   Teamvorgangsmodus  
  
-   Lastenausgleichsmodus  
  
-   Standby-Adapter  
  
Sie können optional auch Konfigurieren der primären teamschnittstelle und eine virtuelles LAN (VLAN) Anzahl.  
  
Diese Eigenschaften des NIC-Teams werden in der folgenden Abbildungangezeigt, die Beispielwerte für einige Eigenschaften des NIC-Teams enthält.  
  
![Eigenschaften von NIC-Team](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_06_properties.jpg)  
  
## <a name="bkmk_teaming"></a>Auswählen einer Teamvorgangsmodus  
Die Optionen für teamvorgangsmodus sind **Switch unabhängigen**, **statischer Teamvorgang**, und **Link Aggregation Control Protocol (LACP)**. Statischer Teamvorgang und LACP sind Switch abhängig. Aus Leistungsgründen NIC-Teams mit allen drei Teaming-Modi empfiehlt es sich, einen Lastenausgleich Modus der dynamische Verteilerliste zu verwenden.  
  
**Switch unabhängigen**  
  
Mit unabhängigen wechseln Modus, oder den Optionen für die NIC-Teams Mitglieder verbunden sind erkennen das Vorhandensein des NIC-Teams und Bestimmen des Netzwerkdatenverkehrs Teammitgliedern des NIC - verteilen nicht verteilt stattdessen das NIC-Team eingehenden Netzwerkdatenverkehr die NIC-Team Member.  
  
Wenn Sie dynamische Verteilerliste Switch unabhängigen Modus verwenden, wird die Last des Netzwerkdatenverkehrs basierend auf den TCP-Ports Adressen-Hash, entsprechend der Änderung durch den dynamischen Lastenausgleich Algorithmus verteilt. Der Algorithmus für dynamische Lastenausgleich verteilt Abläufe, um das Team Member bandbreitennutzung zu optimieren, sodass einzelne Fluss Übertragungen von einem aktiven Teammitglied zum anderen verschieben können. Der Algorithmus berücksichtigt die kleine Möglichkeit Umverteilen des Datenverkehrs verursachen Out-of-Order Lieferung von Paketen, damit dauert die Schritte, um dieses Risiko zu minimieren.  
  
**Abhängige Switch**  
  
Mit abhängigen wechseln, der Switch, der den NIC-Team Mitglieder verbunden werden bestimmt, wie den eingehenden Netzwerkdatenverkehr zwischen den Mitgliedern der NIC-Team zu verteilen. Der Switch verfügt über vollständige Unabhängigkeit zu bestimmen, wie Sie den Datenverkehr über den NIC-Team-Mitglieder zu verteilen.  
  
> [!IMPORTANT]  
> Switch abhängige Teamvorgang erfordert, dass alle Teammitglieder mit demselben physischen Switch verbunden sind oder ein Multi-Gehäuse, die wechseln eine Switch-ID zwischen mehreren Gehäusen freigibt.  
  
Statische Teaming müssen Sie manuell konfigurieren, den Switch und dem Host, auf welche Links das Team zu identifizieren. Da es sich um eine statisch konfigurierte Lösung handelt, gibt es kein zusätzliches Protokoll bei der Switch und der Host Identifizierung falsch angeschlossener, Kabel oder andere Fehler, die dazu führen können, dass das Team zu einem Fehler beim Ausführen. In diesem Modus wird in der Regel von Switches der Serverklasse unterstützt.  
  
Im Gegensatz zu statischen Teamvorgang identifiziert LACP teamvorgangsmodus dynamisch Links, die zwischen dem Host und dem Switch verbunden sind. Diese dynamischen Verbindung ermöglicht die automatische Erstellung eines Teams und, theoretisch jedoch nur selten in der Praxis, die Erweiterung und Reduzierung eines Teams einfach durch die Übertragung oder den Empfang von LACP Pakete aus der Peer-Entität. Alle Switches der Serverklasse LACP unterstützt und alle erfordert der Netzwerkbetreiber LACP am Port Switches vom Administrator zu aktivieren. Wenn Sie eine teamvorgangsmodus von LACP konfigurieren, agiert NIC-Teaming immer in LACPs aktiven Modus mit einem kurzen Timer.  Keine Option ist derzeit für den Timer oder Ändern des LACP-Modus verfügbar.  
  
Beim Verwenden von abhängigen Switch Modi mit dynamische Verteilerliste wird die Last des Netzwerkdatenverkehrs basierend auf den TransportPorts Adressen-Hash, entsprechend der Änderung durch den dynamischen Lastenausgleich Algorithmus verteilt.  Das dynamische Laden Netzwerklastenausgleich Algorithmus verteilt Abläufe, um die Nutzung der Team Member Bandbreite zu optimieren. Einzelne Fluss Übertragungen können von einem aktiven Teammitglied als Teil des die dynamische Verteilerliste verschieben. Der Algorithmus berücksichtigt die kleine Möglichkeit Umverteilen des Datenverkehrs verursachen Out-of-Order Lieferung von Paketen, damit dauert die Schritte, um dieses Risiko zu minimieren.  
  
Als bestimmt der Switch mit allen abhängigen Switch-Konfigurationen den eingehenden Datenverkehr zwischen den Teammitgliedern zu verteilen.  Der Schalter wird erwartet, dass eine angemessene Arbeit verteilt den Datenverkehr zwischen den Teammitgliedern, ist jedoch in vollständiger Unabhängigkeit, um zu bestimmen, wie dies der Fall ist.  
  
## <a name="bkmk_lb"></a>Auswahl einer Modus  
Die Optionen für den Lastenausgleich Verteilung Modus sind **Adressen-Hash**, **Hyper-V-Port**, und **dynamische**.  
  
**Adressen-Hash**  
  
In diesem Modus des Lastenausgleichs erstellt einen Hash, der basierend auf der Adresskomponenten des Pakets. Es weist dann Pakete mit diesem Hashwert zu einem der verfügbaren Adapter. In der Regel ist dieser Mechanismus allein ausreichen, um einen angemessenen Ausgleich über die verfügbaren Adapter zu erstellen.  
  
Windows PowerShell können Sie Werte für die folgenden hashing Funktionskomponenten angeben.  
  
-   TCP-Ports von Quelle und Ziel und Quelle und Ziel-IP-Adressen. Dies ist die Standardeinstellung, bei der Auswahl **Adressen-Hash** als der Netzwerklastenausgleich-Modus.  
  
-   Quell- und Ziel-IP-Adressen nur.  
  
-   Quell- und Ziel-MAC-Adressen nur.  
  
Der TCP-Ports Hash erstellt die kleinste Verteilung von datenverkehrsströmen, was zu kleineren Datenströmen führt, die unabhängig zwischen Teammitgliedern NIC verschoben werden können. Jedoch nicht Sie den Hash der TCP-Ports verwenden, für den Datenverkehr, der nicht TCP oder UDP-basiert oder, in dem die TCP- und UDP-Ports aus dem Stapel, z.B. mit IPsec-geschützten Datenverkehr. In diesen Fällen der Hash wird automatisch verwendet, die IP-Adressen-Hash, oder klicken, ist der Datenverkehr nicht IP-Datenverkehr, der MAC-Adressen-Hash verwendet wird.  
  
**Hyper-V-Port**  
  
Es ist ein Vorteil bei der Verwendung von Hyper-V-Port im Modus für NIC-Teams, die auf Hyper-V-Hosts konfiguriert sind. Da virtuelle Computer unabhängige MAC-Adressen haben, möglich MAC-Adresse des virtuellen Computers – oder den Port, mit den der virtuellen Computer auf dem virtuellen Hyper-V-Switch verbunden ist – die Grundlage, auf den Netzwerkverkehr zwischen Teammitgliedern NIC teilen.  
  
> [!IMPORTANT]  
> NIC-Teams, die Sie innerhalb von virtuellen Maschinen zu erstellen, kann mit dem Hyper-V-Port Load balancing-Modus konfiguriert werden. Verwenden Sie die Adressen-Hash lastenausgleichsmodus stattdessen.  
  
Da der angrenzende Switch immer eine bestimmte MAC-Adresse auf einem Port zu Gesicht bekommen, verteilt der Switch die /-Ausgang-Last (der Datenverkehr vom Switch zum Host) auf mehrere Links auf Grundlage des Ziel-MAC (VM-MAC)-Adresse. Dies ist besonders nützlich, wenn der Warteschlangen für virtuelle Computer (Vmq) verwendet werden, da eine Warteschlange bestimmte Netzwerkkarte platziert werden kann, in denen die ist auf eingehende Datenverkehr erwartet.  
  
Allerdings verfügt der Host nur wenige virtuelle Computer, dieser Modus präzise genug, um eine ausgewogene Verteilung zu erreichen möglicherweise nicht. In diesem Modus wird auch immer einen einzelnen virtuellen Computer (d.h., der Datenverkehr von einem einzigen Switch-Port) auf die Bandbreite beschränken, die auf einer einzelnen Schnittstelle verfügbar ist. NIC-Teamvorgang verwendet den Hyper-V Virtual Switch-Port als Bezeichner anstatt die Quell-MAC-Adresse, da in einigen Fällen ein virtuellen Computer mit mehr als eine MAC-Adresse an einem Switchport konfiguriert werden kann.  
  
**Dynamische**  
  
Dieser Netzwerklastenausgleich-Modus nutzt die besten Eigenschaften der einzelnen die beiden anderen Modi und kombiniert sie in einem einzigen Modus:  
  
-   Ausgehende geladen werden basierend auf den ein Hash der TCP-Ports und IP-Adressen verteilt.  Dynamische Modus neu verteilt werden auch Lasten in Echtzeit, damit Sie ein bestimmter ausgehender Fluss hin- und Herwechseln zwischen Teammitgliedern verschoben werden kann.  
  
-   Eingehende geladen werden auf die gleiche Weise als Modus für den Hyper-V-Anschluss verteilt.  
  
Laden die ausgehenden in diesem Modus werden dynamisch basierend auf dem Konzept von Flowlets ausgeglichen. Genau wie menschlichen Sprache natürliche Umbrüche an den Enden des Wörter und Sätze verfügt, haben TCP-Flüsse (TCP-Kommunikationsdatenströme) auch vorkommende Pausen. Der Teil einer TCP-Fluss zwischen zwei solche Pausen wird als eine Flowlet bezeichnet.  
  
Bei der dynamischen Modus Algorithmus erkennt, dass eine Grenze Flowlet gefunden wurde, z.B. wenn eine Pause lang genug, den Fluss TCP aufgetreten ist - - gesteigert der Algorithmus den Fluss zu einem anderen Teammitglied automatisch bei Bedarf.  In einigen Fällen kann der Algorithmus auch in regelmäßigen Abständen Flüsse neu zu verteilen, die keine Flowlets enthalten. Aus diesem Grund kann die Affinität zwischen TCP-Fluss und Team Member jederzeit ändern, wie der dynamische Lastenausgleich Algorithmus funktioniert, um die Arbeitslast der Teammitglieder auszugleichen.  
  
Ob das Team mit unabhängigen Switch oder einem Switch abhängige Modus konfiguriert ist, wird empfohlen, dass Sie dynamische Verteilerliste Modus für eine optimale Leistung verwenden.  
  
Es wird eine Ausnahme von dieser Regel das NIC-Team hat nur zwei Teammitglieder Switch unabhängigen Modus konfiguriert ist und Active/Standby-Modus aktiviert ist, mit einer Netzwerkkarte aktiv und der andere für den Standbymodus konfiguriert wurde. Mit dieser Konfiguration NIC-Team ermöglicht die Verteilung von Adressen-Hash etwas bessere Leistung als dynamische Verteilung.  
  
## <a name="bkmk_standby"></a>Wählen eine Einstellung Standby-Adapter  
Die Optionen für den Standbymodus Adapter sind keine (alle Adapter aktiv) oder Ihre Auswahl für einen bestimmten Netzwerkadapter im NIC-Team, das als Standby-Adapter, fungiert, während andere Auswahlzustände Teammitglieder aktiv sind. Wenn Sie einen Netzwerkadapter als Standby-Adapter konfigurieren, keinen Netzwerkdatenverkehr gesendet bzw. vom Adapter verarbeitet werden, es sei denn, und bis zum Zeitpunkt, wenn eine aktive NIC ein Fehler auftritt. Nachdem eine aktive NIC ein Fehler auftritt, die NIC Standbymodus aktiviert wird und Prozesse des Netzwerkverkehrs. Wenn alle Teammitglieder Dienst wiederhergestellt werden, ist der Standbymodus Teammitglied an Standby-Status zurückgegeben.  
  
Wenn Sie eine zwei-NIC-Team und einer Netzwerkkarte als Standby-Adapter konfiguriert werden, verlieren Sie die Bandbreite Aggregation Vorteile, die mit zwei aktive NICs vorhanden sind.  
  
> [!IMPORTANT]  
> Sie müssen sich nicht um festzulegen, die einen Adapter Standbymodus, um Fehlertoleranz zu erzielen. Fehlertoleranz ist immer vorhanden, wenn mindestens zwei Netzwerkadapter in einem NIC-Team vorhanden sind.  
  
## <a name="bkmk_primary"></a>Mithilfe der primären Team Interface-Eigenschaft  
Um das Dialogfeld primären Teamschnittstelle zuzugreifen, müssen Sie den Link klicken, der in der Abbildungunten hervorgehoben ist.  
  
![Primäre Team Interface-Eigenschaft](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_10_primaryteaminterface.jpg)  
  
Nachdem Sie den markierten Link im folgenden auf **neue Teamschnittstelle** das Dialogfeld wird geöffnet.  
  
![Neue Teamschnittstelle (Dialogfeld)](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_newteaminterface.jpg)  
  
Wenn Sie VLANs verwenden, können Sie dieses Dialogfeld, um eine VLAN-Nummer anzugeben.  
  
Ob Sie VLANs verwenden, können Sie einen tNIC Namen für das NIC-Team angeben.  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen eines neuen NIC-Teams auf einem virtuellen Computer](../../technologies/nic-teaming/Create-a-New-NIC-Team-in-a-VM.md)  
[NIC-Teamvorgang](NIC-Teaming.md)  
  


