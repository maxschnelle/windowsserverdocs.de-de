---
title: Nic-Team Vorgangs Einstellungen
description: In diesem Thema erhalten Sie einen Überblick über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-nict
ms.topic: article
ms.assetid: a4caaa86-5799-4580-8775-03ee213784a3
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 133e44c83032976f08819529508b3990b6e78596
ms.sourcegitcommit: fdc3ce1992f4dd6ea1771479d525126abbbcfa72
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256680"
---
# <a name="nic-teaming-settings"></a>Nic-Team Vorgangs Einstellungen
In diesem Thema erhalten Sie einen Überblick über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.


  
![Nic-Team Eigenschaften](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_06_properties.jpg)  

## <a name="teaming-modes"></a>Teaming-Modi 
Die Optionen für den Team Vorgangs Modus sind **Switch Independent** und **Switch Dependent**. Der Switch-abhängige Modus umfasst den **statischen** Team Vorgang und das **Link Aggregation Control Protocol (LACP)**. 

>[!TIP]
>Für eine optimale NIC-Team Leistung empfiehlt es sich, einen Lasten Ausgleichs Modus für die dynamische Verteilung zu verwenden.  
  
### <a name="switch-independent"></a>Switch-unabhängig
  
[!INCLUDE [switch-independent-shortdesc-include](../../includes/switch-independent-shortdesc-include.md)] 
  
Wenn Sie den Schalter unabhängigen Modus mit dynamischer Verteilung verwenden, wird die Auslastung des Netzwerk Datenverkehrs basierend auf dem TCP-Ports-Adress Hash entsprechend der Änderung durch den dynamischen Lasten Ausgleichs Algorithmus verteilt. Der dynamische Lasten Ausgleichs Algorithmus verteilt Flows neu, um die Bandbreitenauslastung der Teammitglieder zu optimieren, sodass einzelne Fluss Übertragungen von einem aktiven Teammitglied zu einem anderen verschoben werden können. Der Algorithmus berücksichtigt die kleine Möglichkeit, dass das erneute Verteilen von Datenverkehr zu einer fehl Ordnung der Bereitstellung von Paketen führen kann. Daher müssen Sie Maßnahmen ergreifen, um diese Möglichkeit zu minimieren.  
  
### <a name="switch-dependent"></a>Wechsel abhängige  

[!INCLUDE [switch-dependent-shortdesc-include](../../includes/switch-dependent-shortdesc-include.md)]  
  
> [!IMPORTANT]  
> Switch Dependent Team Vorgang erfordert, dass alle Teammitglieder mit dem gleichen physischen Switch oder einem Multichassis-Switch verbunden sind, der eine Switch-ID für das mehrere Chassis freigibt.


- **Statischer Teaming.** Beim statischen Team Vorgang müssen Sie sowohl den Switch als auch den Host manuell konfigurieren, um zu bestimmen, welche Links das Team bilden. Da es sich hierbei um eine statisch konfigurierte Lösung handelt, gibt es kein zusätzliches Protokoll, das es dem Switch und dem Host unterstützt, nicht ordnungsgemäß konfigurierte Kabel oder andere Fehler zu identifizieren, die zu einem Fehler des Teams führen könnten. Dieser Modus wird im Allgemeinen von Switches der Serverklasse unterstützt.

- **Link Aggregation Control Protocol (LACP).** Im Gegensatz zum statischen Team Vorgang identifiziert der LACP-Team Vorgangs Modus dynamisch Verknüpfungen, die zwischen dem Host und dem Switch verbunden sind. Diese dynamische Verbindung ermöglicht die automatische Erstellung eines Teams und, in der Praxis, die Erweiterung und Reduzierung eines Teams einfach durch die Übertragung oder den Empfang von LACP-Paketen aus der Peer Entität. Alle Server Klassen Switches unterstützen LACP, und alle erfordern, dass der Netzwerk Operator LACP auf dem Switchport administrativ aktiviert. Wenn Sie einen Teaming-Modus von LACP konfigurieren, wird der NIC-Team Vorgang immer im aktiven Modus von LACP mit einem kurzen Timer ausgeführt.  Derzeit ist keine Option verfügbar, um den Timer zu ändern oder den LACP-Modus zu ändern.


Wenn Sie Wechsel abhängige Modi mit dynamischer Verteilung verwenden, wird die Auslastung des Netzwerk Datenverkehrs basierend auf dem transportports-Adress Hash entsprechend der Änderung durch den dynamischen Lasten Ausgleichs Algorithmus verteilt.  Der dynamische Lasten Ausgleichs Algorithmus verteilt Flows neu, um die Bandbreitenauslastung der Teammitglieder zu optimieren. Einzelne Fluss Übertragungen können als Teil der dynamischen Verteilung von einem aktiven Teammitglied zu einem anderen verschoben werden. Der Algorithmus berücksichtigt die kleine Möglichkeit, dass das erneute Verteilen von Datenverkehr zu einer fehl Ordnung der Bereitstellung von Paketen führen kann. Daher müssen Sie Maßnahmen ergreifen, um diese Möglichkeit zu minimieren.  
  
Wie bei allen switchabhängigen Konfigurationen bestimmt der Switch, wie der eingehende Datenverkehr zwischen den Teammitgliedern verteilt wird.  Es wird davon ausgegangen, dass der Switch einen angemessenen Auftrag für die Verteilung des Datenverkehrs auf die Teammitglieder durchführt  


## <a name="load-balancing-modes"></a>Lasten ausgleichsmodi  
Die Optionen für den Lasten Ausgleichs-Verteilungsmodus sind **Adress Hash**, **Hyper-V-Port**und **dynamisch**.  
  
### <a name="address-hash"></a>Adress Hash
  
[!INCLUDE [address-hash-shortdesc-include](../../includes/address-hash-shortdesc-include.md)]
  
Verwenden Sie Windows PowerShell, um Werte für die folgenden hashingfunktionskomponenten anzugeben.  
  
-   Quell-und Ziel-TCP-Ports und Quell-und Ziel-IP-Adressen. Dies ist die Standardeinstellung, wenn Sie **Address Hash** als Lasten Ausgleichs Modus auswählen.  
  
-   Nur Quell-und Ziel-IP-Adressen.  
  
-   Nur Quell-und Ziel-MAC-Adressen.  
  
Der TCP-Ports-Hash erstellt die präziseste Verteilung von Daten Verkehrsströmen, was zu kleineren Datenströmen führt, die unabhängig zwischen den NIC-Teammitgliedern verschoben werden können. Sie können jedoch den TCP-Ports-Hash nicht für Datenverkehr verwenden, der nicht auf TCP oder UDP basiert, oder wo die TCP-und UDP-Ports aus dem Stapel ausgeblendet werden, z. b. mit IPsec-geschütztem Datenverkehr. In diesen Fällen verwendet der Hash automatisch den IP-Adress Hash, oder wenn der Datenverkehr kein IP-Datenverkehr ist, wird der MAC-Adress Hash verwendet.  
  
### <a name="hyper-v-port"></a>Hyper-V-Port
  
[!INCLUDE [hyper-v-port-shortdesc-include](../../includes/hyper-v-port-shortdesc-include.md)]  
  
Da der angrenzende Switch immer eine bestimmte MAC-Adresse an einem Port sieht, verteilt der Switch die Eingangs Last (den Datenverkehr vom Switch an den Host) auf der Grundlage der Mac-Adresse (Mac-Adresse) auf mehrere Links. Dies ist besonders nützlich, wenn virtuelle Computer Warteschlangen (vmqs) verwendet werden, da eine Warteschlange auf der jeweiligen NIC platziert werden kann, an der der Datenverkehr erwartet wird.  
  
Wenn der Host jedoch nur über wenige VMS verfügt, ist dieser Modus möglicherweise nicht genau genug, um eine ausgewogene Verteilung zu erzielen. In diesem Modus wird außerdem immer eine einzelne VM (d. h. der Datenverkehr von einem einzelnen Switchport) auf die Bandbreite beschränkt, die auf einer einzelnen Schnittstelle verfügbar ist. Der NIC-Team Vorgang verwendet den virtuellen Hyper-V-Switchport als Bezeichner anstelle der Quell-MAC-Adresse, da ein virtueller Computer in manchen Fällen mit mehr als einer Mac-Adresse für einen Switchport konfiguriert werden kann.  
  
### <a name="dynamic"></a>Dynamisch
  
[!INCLUDE [dynamic-shortdesc-include](../../includes/dynamic-shortdesc-include.md)]
  
Die ausgehenden Lasten in diesem Modus werden basierend auf dem Konzept der flowlets dynamisch ausgeglichen. Ebenso wie bei der menschlichen Sprache an den Enden von Wörtern und Sätzen natürliche Unterbrechungen auftreten, sind TCP-Flows (TCP-Kommunikationsstreams) natürlich auch Unterbrechungen aufgetreten. Der Teil eines TCP-Flows zwischen zwei Unterbrechungen wird als flowlet bezeichnet.  
  
Wenn der Algorithmus für den dynamischen Modus erkennt, dass eine flowlet-Grenze gefunden wurde (z. b. wenn im TCP-Fluss eine Unterbrechung der Länge aufgetreten ist), gleicht der Algorithmus den Flow ggf. automatisch an ein anderes Teammitglied aus.  In einigen Fällen kann der Algorithmus auch regelmäßig einen Ausgleich für Flows durchführen, die keine flowlets enthalten. Aus diesem Grund kann sich die Affinität zwischen TCP-Fluss und Teammitglied jederzeit ändern, da der dynamische Ausgleichs Algorithmus funktioniert, um die Arbeitsauslastung der Teammitglieder auszugleichen.  
  
Unabhängig davon, ob das Team mit einem Wechsel unabhängigen oder einem der Switch-abhängigen Modi konfiguriert ist, wird empfohlen, den dynamischen Verteilungsmodus für eine optimale Leistung zu verwenden.  
  
Es gibt eine Ausnahme von dieser Regel, wenn das NIC-Team nur über zwei Team Mitglieder verfügt, im Switch Independent-Modus konfiguriert ist und den aktiv/Standby-Modus aktiviert hat, wobei eine NIC aktiv und die andere für den Standby-Modus konfiguriert ist. Mit dieser NIC-Team Konfiguration bietet die Adress Hash Verteilung eine etwas bessere Leistung als die dynamische Verteilung.  


## <a name="standby-adapter-setting"></a>Standby-Adapter Einstellung  
Die Optionen für den standbyadapter sind **None (alle Adapter aktiv)** oder Ihre Auswahl eines bestimmten Netzwerkadapters im NIC-Team, das als standbyadapter fungiert. Wenn Sie eine NIC als standbyadapter konfigurieren, sind alle anderen nicht ausgewählten Teammitglieder aktiv, und es wird kein Netzwerk Datenverkehr an den Adapter gesendet oder vom Adapter verarbeitet, bis eine aktive NIC ausfällt. Nachdem eine aktive NIC ausfällt, wird die Standby-NIC aktiv und verarbeitet den Netzwerk Datenverkehr. Wenn alle Teammitglieder in den Dienst wieder hergestellt werden, kehrt der Standby-Teammitglied in den Standbystatus zurück.  

Wenn Sie über ein zwei-NIC-Team verfügen und eine NIC als standbyadapter konfigurieren möchten, verlieren Sie die Vorteile der Bandbreiten Aggregation, die mit zwei aktiven NICs vorhanden sind.  Sie müssen keinen Standby-Adapter festlegen, um Fehlertoleranz zu erzielen. die Fehlertoleranz ist immer vorhanden, wenn mindestens zwei Netzwerkadapter in einem NIC-Team vorhanden sind.
 
  
## <a name="primary-team-interface-property"></a>Eigenschaft der primären Team Schnittstelle  
Um auf das Dialogfeld primäre Team Schnittstelle zuzugreifen, müssen Sie auf den Link klicken, der in der Abbildung unten hervorgehoben ist.  
  
![Eigenschaft der primären Team Schnittstelle](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_10_primaryteaminterface.jpg)  
  
Nachdem Sie auf den markierten Link klicken, wird das folgende Dialogfeld " **neue Team Schnittstelle** " geöffnet.  
  
![Dialogfeld "Neue Teamschnittstelle"](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_newteaminterface.jpg)  
  
Wenn Sie VLANs verwenden, können Sie in diesem Dialogfeld eine VLAN-Nummer angeben.  
  
Unabhängig davon, ob Sie VLANs verwenden, können Sie einen NIC-Namen für das NIC-Team angeben.  
  


---
