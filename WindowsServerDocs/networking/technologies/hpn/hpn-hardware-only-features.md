---
title: Hochleistungs Netzwerke
description: Dieses Thema bietet einen Überblick über die Auslagerungs-und Optimierungstechnologien in Windows Server 2016 und enthält Links zu weiteren Anleitungen zu diesen Technologien.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 3a561096da49efc4c217c0736d888674b2acf202
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871948"
---
## <a name="hardware-only-ho-features-and-technologies"></a>Hardware Only (HO)-Features und -Technologien

Diese Hardwarebeschleunigung verbessern die Netzwerkleistung in Verbindung mit der Software, sind aber nicht eng Teil eines Software Features. Beispiele hierfür sind Interrupt-Moderation, Fluss Steuerung und Empfangs seitige IPv4-Prüfsummen Abladung.

>[!TIP]
>Die Funktionen sh und Ho sind verfügbar, wenn Sie von der installierten NIC unterstützt werden. Die Funktionsbeschreibungen unten beschreiben, wie Sie festzustellen, ob Ihre NIC das Feature unterstützt.

### <a name="address-checksum-offload"></a>Address Checksum Offload

Address Prüfsumme Abladungen sind eine NIC-Funktion, die die Berechnung von Adress Prüfsummen (IP, TCP, UDP) für Sende-und Empfangs Vorgänge auf die NIC-Hardware ablädt.

Beim Empfangs Pfad berechnet die Prüfsumme-Abladung die Prüfsummen in den IP-, TCP-und UDP-Headern (nach Bedarf) und gibt dem Betriebssystem an, ob die Prüfsummen bestanden, fehlgeschlagen oder nicht überprüft wurden. Wenn die NIC bestätigt, dass die Prüfsummen gültig sind, akzeptiert das Betriebssystem das Paket unangefochten. Wenn die NIC bestätigt, dass die Prüfsummen ungültig sind oder nicht aktiviert sind, berechnet der IP-/TCP/UDP-Stapel die Prüfsummen intern intern. Wenn die berechnete Prüfsumme fehlschlägt, wird das Paket verworfen.

Beim sendepfad berechnet die Abladung der Prüfsumme die Prüfsummen und fügt Sie nach Bedarf in den IP-, TCP-oder UDP-Header ein.

Durch das Deaktivieren von Prüfsumme-Abladungen auf dem sendepfad werden die Prüfsummenberechnung und die Einfügung von Paketen, die an den Mini Port-Treiber gesendet werden, mithilfe des Features "große Sende Abladung" (LSO) deaktiviert.  Der Benutzer muss auch LSO deaktivieren, um alle Auslagerungs Berechnungen der Prüfsumme zu deaktivieren.

_**Adresschecksum-Offloads verwalten**_

In den erweiterten Eigenschaften gibt es mehrere unterschiedliche Eigenschaften:

-   IPv4-Prüfsumme Abladung

-   TCP-Prüfsumme Offload (IPv4)

-   TCP-Prüfsumme-Auslagerung (IPv6)

-   UDP-Prüfsumme Offload (IPv4)

-   UDP-Prüfsumme Offload (IPv6)

Standardmäßig sind diese immer aktiviert. Es wird empfohlen, alle diese Offloads immer zu aktivieren.

Die Abladungen der Prüfsumme können mithilfe der Cmdlets "Enable-netadapterchecksujeffload" und "deaktivieren-netadapterchecksumuffload" verwaltet werden. Beispielsweise aktiviert das folgende Cmdlet die Berechnungen von TCP (IPv4) und UDP (IPv4)-Prüfsummen:

```PowerShell
Enable-NetAdapterChecksumOffload –Name * -TcpIPv4 -UdpIPv4
```

_**Tipps zur Verwendung von adresschecksum-Offloads**_

Adresschecksum-Offloads sollten unabhängig von der Arbeitsauslastung oder dem Umstand immer aktiviert werden. Bei allen Auslagerungs Technologien können Sie die Netzwerkleistung immer verbessern. Das Abladen von Prüfsummen ist auch erforderlich, damit andere Zustands lose Abladungen funktionieren, z. & # 160; & # 160; & # 160; & # 160; & # 160; & amp; a. Empfangs seitige Skalierung

### <a name="interrupt-moderation-im"></a>Unterbrechungs Moderation (im)

In werden mehrere empfangene Pakete vor dem Unterbrechen des Betriebssystems gepuffert. Wenn eine NIC ein Paket empfängt, wird ein Timer gestartet. Wenn der Puffer voll ist oder der Timer abläuft, je nachdem, welcher Wert zuerst eintritt, unterbricht die NIC das Betriebssystem. 

Viele NICs unterstützen mehr als nur ein-/ausschalten für Interrupt-Moderation. Die meisten NICs unterstützen die Konzepte von "niedrig", "Mittel" und "hoch" für im. Die verschiedenen Raten stellen kürzere oder längere Zeitgeber und geeignete Puffergrößen Anpassungen dar, um die Latenz zu verringern (Moderation mit niedriger Interruptzeit) oder Interrupts zu reduzieren (hohe interruptmoderation).

Zwischen der Reduzierung von Interrupts und einer übermäßig verzögerten Paket Bereitstellung besteht ein ausgewogenes Gleichgewicht. Im Allgemeinen ist die Paketverarbeitung effizienter, wenn die interruptmoderation aktiviert ist. Anwendungen mit hoher Leistung oder niedriger Latenz müssen möglicherweise die Auswirkung der Deaktivierung oder Reduzierung der Unterbrechungs Moderation auswerten.

### <a name="jumbo-frames"></a>Großrahmen

Bei groß Frames handelt es sich um ein NIC-und Netzwerk Feature, das es einer Anwendung ermöglicht, Frames zu senden, die wesentlich größer sind als die standardmäßigen 1500 Bytes In der Regel beträgt der Grenzwert für groß Rahmen ungefähr 9000 Byte, kann jedoch kleiner sein.

Es gab keine Änderungen an der groß Frame Unterstützung in Windows Server 2012 R2.

In Windows Server 2016 gibt es eine neue Auslagerung: MTU_for_HNV. Diese neue Auslagerung funktioniert mit den groß Rahmen Einstellungen, um sicherzustellen, dass der gekapselte Datenverkehr keine Segmentierung zwischen dem Host und dem angrenzenden Switch erfordert. Diese neue Funktion des SDN-Stapels gibt an, dass die NIC automatisch berechnet, was die MTU ankündigen soll und welche die MTU bei der Übertragung verwendet werden soll. Diese Werte für die MTU sind unterschiedlich, wenn eine HNV-Auslagerung verwendet wird. (In der featurekompatibilitäts-Tabelle hat Tabelle 1, MTU_for_HNV die gleichen Interaktionen wie die HNVv2 Abladungen, da Sie direkt mit den HNVv2-Abladungen verknüpft ist.)

### <a name="large-send-offload-lso"></a>Große Sendeabladung (Large Send Offload, LSO)

LSO ermöglicht einer Anwendung, einen großen Datenblock an die NIC zu übergeben, und die NIC teilt die Daten in Pakete auf, die in die maximale Übertragungseinheit (Maximum Transfer Unit, MTU) des Netzwerks passen.

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

Das Zusammenstellen von Empfangs Segmenten (auch als große Empfangs Abladung bezeichnet) ist eine NIC-Funktion, die Pakete annimmt, die Teil desselben Streams sind, der zwischen Netzwerk Interrupts eingeht, und Sie in ein einzelnes Paket zusammenfasst, bevor Sie an das Betriebssystem übertragen werden. RSC ist auf NICs, die an den virtuellen Hyper-V-Switch gebunden sind, nicht verfügbar. Weitere Informationen finden Sie unter [Receive Segment Coalescing (RSC)](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch).