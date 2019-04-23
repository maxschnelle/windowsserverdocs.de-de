---
title: NIC-Teamvorgang-Einstellungen
description: In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.
manager: dougkim
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
ms.date: 09/13/2018
ms.openlocfilehash: 57957e88ff4c398be23355534d5cc0ad7f920bb1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877931"
---
# <a name="nic-teaming-settings"></a>NIC-Teamvorgang-Einstellungen
In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.


  
![NIC-Team-Eigenschaften](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_06_properties.jpg)  

## <a name="teaming-modes"></a>Teaming-Modi 
Die Optionen für den teammodus sind **Switchunabhängig** und **abhängige Schalter**. Die abhängige Schalter-Modus schließt **statischer Teamvorgang** und **Link Aggregation Control Protocol (LACP)**. 

>[!TIP]
>Für eine optimale Leistung für NIC-Team empfehlen wir die Verwendung einer lastenausgleichsmodus dynamische Verteilung.  
  
### <a name="switch-independent"></a>Switch-unabhängig
  
[!INCLUDE [switch-independent-shortdesc-include](../../includes/switch-independent-shortdesc-include.md)] 
  
Wenn Sie Schalter Independent-Modus mit dynamische Verteilung verwenden, wird die Last des Netzwerkdatenverkehrs verteilt basierend auf der TCP-Ports adresshash, wie von der dynamische Lastenausgleichsalgorithmus nicht geändert. Der dynamische Lastenausgleichsalgorithmus verteilt Flows Team Member bandbreitennutzung zu optimieren, damit einzelne Flow Übertragungen von einem aktiven Team Teammitglied auf einen anderen verschoben werden können. Der Algorithmus berücksichtigt die geringe Möglichkeit, dass das Verteilen von Datenverkehr verursachen Out-of-Order-Übermittlung von Paketen, daher dauert die Schritte aus, um diese Gefahr zu minimieren.  
  
### <a name="switch-dependent"></a>Switch-abhängige  

[!INCLUDE [switch-dependent-shortdesc-include](../../includes/switch-dependent-shortdesc-include.md)]  
  
> [!IMPORTANT]  
> Switch-abhängige Teamvorgang wird benötigt, dass alle Teammitglieder mit demselben physischen Switch verbunden sind, oder ein Multi-Chassis, die wechseln gemeinsam eine Switch-ID in der mehrere Gehäuse.


- **Statischer Teamvorgang.** Statischer Teamvorgang erfordert, dass Sie manuell konfigurieren, sowohl den Switch als auch der Host identifizieren, welche Links das Team bilden. Da es sich um eine statisch konfigurierte Lösung handelt, gibt es kein zusätzliches Protokoll bei den Switch und der Host Identifizierung falsch angeschlossen, Kabel oder anderer Fehler, die das Team zu einem Fehler beim Ausführen verursachen können. Dieser Modus wird im Allgemeinen von Switches der Serverklasse unterstützt.

- **Link Aggregation Control Protocol (LACP).** Im Gegensatz zu statischer Teamvorgang identifiziert LACP-teamvorgangsmodus dynamisch Links, die zwischen dem Host und dem Switch verbunden sind. Diese dynamische Verbindung ermöglicht die automatische Erstellung eines Teams und, theoretisch jedoch selten in der Praxis, Erweiterung und Reduzierung eines Teams einfach durch die Übertragung oder des Empfangs von LACP-Paketen, von der peerentität. Alle Switches der Serverklasse unterstützt LACP, und alle der Netzwerk-Operator, um LACP am Port Switches aktivieren durch den Administrator erfordern. Wenn Sie eine teammodus von LACP konfigurieren, arbeitet der NIC-Teamvorgang immer im aktiven Modus des LACP mit einem kurzen Timer.  Keine Option ist derzeit verfügbar ist, den Timer oder Ändern des LACP-Modus.


Wenn Sie abhängige Schalter Modi mit dynamische Verteilung verwenden, wird die Last des Netzwerkdatenverkehrs verteilt basierend auf den TransportPorts adresshash, wie von der dynamische Lastenausgleichsalgorithmus nicht geändert.  Der dynamische Lastenausgleichsalgorithmus verteilt Datenströme, um die Optimierung der bandbreitenauslastung für Team-Element. Einzelne Flow Übertragungen können von einem aktiven Teammitglied zu einem anderen als Teil der dynamische Verteilung verschieben. Der Algorithmus berücksichtigt die geringe Möglichkeit, dass das Verteilen von Datenverkehr verursachen Out-of-Order-Übermittlung von Paketen, daher dauert die Schritte aus, um diese Gefahr zu minimieren.  
  
Wie Sie der Switch mit allen abhängigen Switch-Konfigurationen wie verteilen Sie eingehenden Datenverkehr zwischen den Teammitgliedern bestimmt.  Der Schalter wird erwartet, eine sinnvolle Arbeit den Datenverkehr auf die Mitglieder des Teams verteilt, aber über vollständige Unabhängigkeit, um zu bestimmen, wie dies der Fall ist.  


## <a name="load-balancing-modes"></a>Laden von Lastenausgleich-Modi  
Die Optionen des Lastenausgleichs-Verteilungsmodus **Adresshash**, **Hyper-V-Port**, und **dynamische**.  
  
### <a name="address-hash"></a>Adresshash
  
[!INCLUDE [address-hash-shortdesc-include](../../includes/address-hash-shortdesc-include.md)]
  
Verwenden Sie Windows PowerShell, um Werte für die folgenden Funktionskomponenten für hashing anzugeben.  
  
-   Quelle und Ziel-TCP-Ports und die Quelle und Ziel-IP-Adressen. Dies ist die Standardeinstellung, bei der Auswahl **Adresshash** als Lastenausgleich-Modus.  
  
-   Quell- und Zielserver müssen Sie nur IP-Adressen.  
  
-   Quelle und Ziel-MAC-Adressen nur.  
  
Der Hash der TCP-Ports erstellt die detaillierteste Verteilung von datenverkehrsströmen, was zu kleineren Datenströmen, die unabhängig zwischen Teammitgliedern des NIC verschoben werden können. Allerdings können keine den Hash der TCP-Ports für den Datenverkehr, die nicht TCP oder UDP-basiert sein, oder, in dem die TCP- und UDP-Ports aus dem Stapel, z. B. mit IPsec-geschützten Datenverkehr. In diesen Fällen der-Hash verwendet automatisch den Hash des IP-Adresse, oder klicken, ist der Datenverkehr nicht IP-Datenverkehr, der Hash der MAC-Adresse verwendet wird.  
  
### <a name="hyper-v-port"></a>Hyper-V-Port
  
[!INCLUDE [hyper-v-port-shortdesc-include](../../includes/hyper-v-port-shortdesc-include.md)]  
  
Da der benachbarte Switch immer eine bestimmte MAC-Adresse auf einem Port erkennt, verteilt der Switch die eingehende Last (der Datenverkehr vom Switch zum Host) für mehrere Verknüpfungen, die basierend auf dem Ziel (VM-MAC)-MAC-Adresse an. Dies ist besonders nützlich, wenn Warteschlangen für virtuelle Computer (Vmq) verwendet werden, weil eine Warteschlange für die bestimmten Netzwerkschnittstellenkarte platziert werden kann, in denen der Datenverkehr erwartet wird, auf das eintreffen.  
  
Allerdings verfügt der Host nur wenige virtuelle Computer, in diesem Modus präzise genug, um eine ausgewogene Verteilung zu erreichen möglicherweise nicht. In diesem Modus wird immer einen einzelnen virtuellen Computer (d. h. der Datenverkehr von einem einzigen Switch-Port) auf die Bandbreite beschränkt, die auf einer einzelnen Schnittstelle verfügbar ist. NIC-Teamvorgang verwendet die Hyper-V Virtual Switch-Port als Bezeichner anstelle der Quell-MAC-Adresse, da in einigen Fällen ein virtuellen Computer mit mehr als eine MAC-Adresse an einem Switchport konfiguriert werden kann.  
  
### <a name="dynamic"></a>Dynamic
  
[!INCLUDE [dynamic-shortdesc-include](../../includes/dynamic-shortdesc-include.md)]
  
Die ausgehende lädt in diesem Modus werden dynamisch basierend auf dem Konzept von Flowlets ausgeglichen. Genau wie der menschliche Stimme natürliche datenbrüche an den Enden der Wörter und Sätze verfügt, müssen TCP-Flüsse (TCP-kommunikationsstreams) auch vorkommende unterbrochen. Der Teil einer TCP-Datenflusses zwischen zwei solchen Unterbrechungen wird als eine Flowlet bezeichnet.  
  
Wenn der dynamischen Modus-Algorithmus erkennt, dass eine Grenze Flowlet gefunden wurde, z. B. wenn eine Unterbrechung einer ausreichenden Länge, in den TCP-Fluss aufgetreten ist - - lastausgleichsvorgang der Algorithmus automatisch den Fluss auf ein anderes Teammitglied, bei Bedarf.  In einigen Fällen kann der Algorithmus in regelmäßigen Abständen Flows ausgleichen, die keine Flowlets enthalten. Aus diesem Grund kann die Affinität zwischen TCP-Flow-Teammitglied zu einem beliebigen Zeitpunkt ändern, wie der dynamische Lastenausgleich Algorithmus funktioniert, um die arbeitsauslastung Mitglied des Teams verteilen.  
  
Ob das Team mit Switchunabhängig oder einer der Modi, abhängige Schalter konfiguriert ist, empfiehlt es sich, dass Sie dynamische Verteilungsmodus für eine optimale Leistung verwenden.  
  
Es gibt eine Ausnahme von dieser Regel auf, wenn das NIC-Team nur zwei Teammitglieder hat, im Switch-Independent-Modus konfiguriert ist, und verfügt über aktiv/Standby-Modus aktiviert ist, mit einer NIC, die aktiv und der andere für den Standbymodus konfiguriert. Bei dieser Konfiguration NIC-Team bietet Adresse hashverteilung etwas bessere Leistung als die dynamische Verteilung.  


## <a name="standby-adapter-setting"></a>Standby-Adapter-Einstellung  
Die Optionen für die Standby-Adapter sind **keine (alle Adapter aktiv)** oder Ihre Auswahl für einen bestimmten Netzwerkadapter im NIC-Team, die als Standby-Adapter dient. Wenn Sie eine NIC als Standby-Adapter konfigurieren, alle nicht ausgewählten Teammitglieder sind aktiv, und kein Netzwerkdatenverkehr gesendet bzw. vom Adapter verarbeitet werden, bis eine aktive NIC fehlschlägt. Wenn eine aktive NIC fehlgeschlagen ist, die Standby-NIC aktiviert wird und der Netzwerkdatenverkehr für Prozesse. Wenn alle Teammitglieder Dienst wiederhergestellt zu erhalten, wird das standby-Team-Element zu standby-Status zurückgegeben.  

Wenn Sie ein zwei-NIC-Team und eine NIC als Standby-Adapter konfiguriert werden, verlieren Sie die Bandbreite Aggregation Vorteile, die mit zwei aktiven NICs vorhanden sind.  Sie müssen sich nicht zum Festlegen eines Standby-Adapters für die Fehlertoleranz zu erzielen. Fehlertoleranz ist immer vorhanden, wenn mindestens zwei Netzwerkadapter vorhanden, in einem NIC-Team sind.
 
  
## <a name="primary-team-interface-property"></a>Eigenschaft der primären Team-Schnittstelle  
Um das Dialogfeld für die primären Teamschnittstelle zuzugreifen, müssen Sie den Link klicken, der in der folgenden Abbildung hervorgehoben wird.  
  
![Eigenschaft des primären Team-Schnittstelle](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_10_primaryteaminterface.jpg)  
  
Nachdem Sie den hervorgehobenen Link im folgenden auf **neue Teamschnittstelle** Dialogfeld wird geöffnet.  
  
![Dialogfeld "Neue Teamschnittstelle"](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_newteaminterface.jpg)  
  
Wenn Sie VLANs verwenden, können Sie das Dialogfeld zu öffnen, eine VLAN-Nummer an.  
  
Unabhängig davon, ob Sie VLANs verwenden, können Sie einen tNIC-Namen für das NIC-Team angeben.  
  


---