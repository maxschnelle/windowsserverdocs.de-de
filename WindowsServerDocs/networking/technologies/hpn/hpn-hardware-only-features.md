---
title: Hochleistungs-Netzwerk
description: Dieses Thema bietet einen Überblick über die Auslagerung und Optimierung von Technologien in Windows Server 2016, und enthält Links zu weiteren Anleitungen zu diesen Technologien.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 09e18a41452baa0add8e055ceb22d2f5c2ad886e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815831"
---
## <a name="hardware-only-ho-features-and-technologies"></a>Hardware Only (HO)-Features und -Technologien

Diese Hardware beschleunigungen Verbesserung der netzwerkleistung in Verbindung mit der Software sind jedoch nicht Repositoryschicht eng Bestandteil jeder Softwarefunktion. Beispiele: Interruptüberprüfung, flusssteuerung und Receive-Side-IPv4-Prüfsummenoffload.

>[!TIP]
>SH und HO-Features sind verfügbar, wenn die installierte NIC unterstützt. Die folgenden Beschreibungen von Features werden beschrieben, wie mitteilen, ob die NIC die Funktion unterstützt.

### <a name="address-checksum-offload"></a>Adresse-Prüfsumme

Adresse Prüfsumme abladungen sind ein NIC-Feature, das die Berechnung der Adresse Prüfsummen (IP, TCP, UDP) auf die NIC-Hardware verlagert für senden und empfangen.

Auf dem empfängerpfad der-Prüfsumme berechnet die Prüfsummen in die IP-, TCP und UDP-Header (nach Bedarf), und überprüfen, ob für das Betriebssystem die Prüfsummen übergeben, ist fehlgeschlagen oder nicht aktiviert. Wenn die NIC bestätigt, dass die Prüfsummen gültig ist, wird das Betriebssystem, das Paket fungierenden akzeptiert werden. Wenn die NIC, dass die Prüfsummen ungültig oder nicht aktiviert sind bestätigt, wird von der IP-/ TCP/UDP-Stapel erneut intern die Prüfsummen berechnet. Wenn die berechnete Prüfsumme ein Fehler auftritt, ruft das Paket verworfen.

Auf dem sendepfad der-Prüfsumme berechnet und fügt die Prüfsummen in den IP-, TCP oder UDP-Header entsprechend.

Deaktivieren Prüfsummen abladungen auf dem sendepfad wird nicht prüfsummenberechnung und die Einfügung für Pakete an den Miniporttreiber, die mit der großen senden Offload (LSO)-Funktion gesendet werden deaktiviert.  Um alle prüfsummenberechnungen Auslagerung deaktivieren, muss der Benutzer auch LSO deaktivieren.

_**Die Prüfsumme Abladungen Adresse verwalten**_

Es gibt mehrere unterschiedliche Eigenschaften, in den erweiterten Eigenschaften:

-   IPv4--Prüfsumme

-   TCP--Prüfsumme (IPv4)

-   TCP--Prüfsumme (IPv6)

-   UDP--Prüfsumme (IPv4)

-   UDP--Prüfsumme (IPv6)

Standardmäßig sind diese alle immer aktiviert. Es wird empfohlen, alle diese abladevorgänge immer zu aktivieren.

Verlagert die Prüfsumme kann mit den Cmdlets Enable-NetAdapterChecksumOffload "und" Disable-NetAdapterChecksumOffload verwaltet werden. Das folgende Cmdlet ermöglicht z. B. TCP (IPv4) und die Berechnung von Prüfsummen aufgewendet UDP (IPv4):

```PowerShell
Enable-NetAdapterChecksumOffload –Name * -TcpIPv4 -UdpIPv4
```

_**Tipps zur Verwendung der Adresse Prüfsumme Auslagerungen**_

Adresse Prüfsumme lagert sollte immer unabhängig davon, welche arbeitsauslastung oder Fall aktiviert werden. Dies die meisten Basic aller offload-Technologien verbessern immer die Leistung Ihres Netzwerks. CHECKSUM-Abladung sind ebenso Voraussetzung für andere statuslose auslagerungen einschließlich funktioniert Empfang zusammengeführter Segmente (RSC), empfangsseitige Skalierung (RSS) und large Send offload (LSO).

### <a name="interrupt-moderation-im"></a>Interruptüberprüfung (IM)

Instant-Messaging puffert mehrere empfangene Pakete vor dem Unterbrechen des Betriebssystems. Wenn eine NIC ein Paket empfängt, wird ein Timer gestartet. Wenn der Puffer voll ist oder der Zeitgeber abläuft, die zuerst eintretende unterbricht die Netzwerkkarte des Betriebssystems. 

NIC-Anzahl, die mehr als nur ein-/ausschalten für Interruptüberprüfung unterstützt wird. Die meisten Netzwerkkarten unterstützen die Konzepte der eine geringe, mittlere und hohes Maß an, für Instant-Messaging. Der unterschiedlichen Preise stellen kürzeres oder längeres Timer entsprechende Größe Anpassungen und Verringerung der Latenz (niedrige interruptüberprüfung), oder reduzieren die Interrupts (hohe interruptüberprüfung) dar.

Es ist ein Lastenausgleich auf zwischen Interrupts zu reduzieren und übermäßig verzögert zustellungsreihenfolge von Paketen erzielt werden. Im Allgemeinen ist die paketverarbeitung effizienter Interruptüberprüfung aktiviert. Hohe Leistung oder Wartezeit-Anwendungen müssen möglicherweise die Auswirkungen des deaktivieren, oder Verringern der Interruptüberprüfung bewertet.

### <a name="jumbo-frames"></a>Großrahmen

Großrahmen ist eine NIC und Netzwerk-Funktion, die ermöglicht einer Anwendung, Frames senden, die viel größer als die standardmäßigen 1500 Bytes sind. In der Regel der Grenzwert zu Großrahmen etwa 9000 Byte jedoch kleiner sein kann.

Es wurden keine Änderungen an Jumbo Frame-Support in Windows Server 2012 R2.

In Windows Server 2016 ist eine neue Auslagerung: MTU_for_HNV. Diese neue Auslagerung arbeitet mit Jumbo Frame-Einstellungen, um sicherzustellen, dass die gekapselten Datenverkehr keine Segmentierung zwischen dem Host und der angrenzende Switch erforderlich. Diese neue Funktion von SDN-Stapel verfügt über die NIC, auf welche MTU angekündigt werden soll und welche maximale Übertragungseinheit für die Verwendung bei der Übertragung automatisch zu berechnen. Diese Werte für die maximale Übertragungseinheit unterscheiden sich, wenn alle hnv-Auslagerung verwendet wird. (In der Tabelle Feature Compatibility in Tabelle 1, MTU_for_HNV die gleichen Interaktionen müssten wie lagert die HNVv2 abladungen haben, da er direkt mit der HNVv2 verknüpft ist.)

### <a name="large-send-offload-lso"></a>Große Sendeabladung (Large Send Offload, LSO)

LSO kann es sich um eine Anwendung einem großen Datenblock auf die NIC und die NIC unterbricht die Daten an Pakete übergeben, die in der Einheit MTU (Maximum Transfer) des Netzwerks zu entsprechen.

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

Receive Segment Coalescing, auch bekannt als große erhalten Auslagerung, wird eine NIC-Funktion, die Pakete verwendet, die den gleichen Stream gehören, die zwischen Netzwerkinterrupts eingeht und fügt sie in einem einzelnen Paket vor dem Bereitstellen des Betriebssystems zusammen. RSC ist nicht verfügbar, auf NICs, die mit dem virtuellen Hyper-V-Switch gebunden sind. Weitere Informationen finden Sie unter [erhalten Segment Coalescing (RSC)](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch).