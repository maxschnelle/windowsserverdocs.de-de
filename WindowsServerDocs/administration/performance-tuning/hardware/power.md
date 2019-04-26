---
title: Überlegungen zur Power von Server-Hardware
description: Überlegungen zur Power von Server-Hardware
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5261c856a0a29f9f58526e4f9580a16bbed5be56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874301"
---
# <a name="server-hardware-power-considerations"></a>Überlegungen zur Power von Server-Hardware

Es ist wichtig, die zunehmende Bedeutung der Energieeffizienz in der Enterprise und Data Center-Umgebung zu erkennen. Hohe Leistung und Nutzung von energiesparendes sind häufig in Konflikt stehende Ziele, aber wenn Sie die Serverkomponenten sorgfältig auswählen, erreichen Sie das richtige Gleichgewicht zwischen ihnen. In den folgenden Abschnitten werden Richtlinien für die Power-Merkmalen und Funktionen von Server-Hardware-Komponenten aufgelistet.

## <a name="processor-recommendations"></a>Prozessor-Empfehlungen

Häufigkeit, Betrieb, Spannung, Cachegröße und Prozess-Technologie wirken sich auf den Energieverbrauch der Prozessoren. Prozessoren verfügen über einen temperaturüberwachung Entwurf (TDP) Bewertung zu verweisen, die einen grundlegenden Überblick über die Energieverbrauch relativ zu anderen Modellen zu erhalten.

Deaktivieren Sie in der Regel für den niedrigsten TDP-Prozessor, der Ihre Leistungsziele erfüllt. Darüber hinaus neuere prozessorgenerationen sind in der Regel mehr Energie, die effizient und sie möglicherweise verfügbar machen mehrere Energiezustände für die Windows Power Management-Algorithmen, wodurch eine bessere energieverwaltung auf allen Ebenen der Leistung. Oder sie können einige der neuen "kooperativen? Power Management-Techniken, die Microsoft in Zusammenarbeit mit Hardwareherstellern entwickelt wurde.

Weitere Informationen zur kooperativen Power Management-Techniken, finden Sie im Abschnitt mit dem Namen Zusammenarbeit Prozessor Leistung-Steuerelement in der [Advanced Configuration and Power Interface Specification](http://www.uefi.org/sites/default/files/resources/ACPI_5_1release.pdf).


## <a name="memory-recommendations"></a>Speicherempfehlungen
Arbeitsspeicher-Konten für den eine zunehmende Anteil der gesamten Systemenergiezustand. Viele Faktoren beeinflussen den Energieverbrauch von Speicher-DIMM, z. B. in-Memory-Technologie, Fehlerkorrektur-Code (ECC), Häufigkeit der Bus, Kapazität, Dichte und Anzahl der Ränge. Aus diesem Grund empfiehlt es sich um erwarteten Power Bewertungen zu vergleichen, vor dem Kauf großer Mengen an Arbeitsspeicher.

Mit geringem Arbeitsspeicher ist jetzt verfügbar, aber Sie müssen die Kompromisse Leistung und Kosten berücksichtigen. Wenn Ihr Server paging sein wird, müssen Sie auch die Stromkosten der Datenträger auslagern abwägen.


## <a name="disks-recommendations"></a>Datenträger-Empfehlungen
Höhere u/Min bedeutet mehr Energie verbraucht. SSD-Laufwerke sind mehr Energie verbrauchen effizienter als rotierenden Festplatten. Außerdem erfordern 2,5-Zoll-Laufwerke in der Regel weniger Energie als 3,5-Zoll-Laufwerke.

## <a name="network-and-storage-adapter-recommendations"></a>Netzwerk- und Empfehlungen für Speicher-Adapter
Einige Adapter verringern Stromverbrauch während Leerlaufzeiten. Dies ist ein wichtiger Aspekt für 10-Gb-Netzwerkadapter und hoher Bandbreite (4 und 8 Gb) Speicher Links. Solche Geräte können die Menge an Energie nutzen.


## <a name="power-supply-recommendations"></a>Empfehlungen für Power-Netzteils
Verbesserung der Energieeffizienz-Angebot ist eine hervorragende Möglichkeit, den Energieverbrauch zu senken, ohne Leistung zu beeinträchtigen. High-Efficiency Netzteile können viele die Anzeige pro Jahr pro Server speichern.


## <a name="fan-recommendations"></a>Lüfter Empfehlungen
Lüfter, z. B. Netzteile, sind ein Bereich, in dem Sie Energieverbrauch reduzieren können, ohne Beeinträchtigung der Systemleistung. Lüfter Variable-Geschwindigkeit können u/min als System-abnimmt, entfernen andernfalls unnötigen Energieverbrauch reduziert werden.


## <a name="usb-devices-recommendations"></a>USB-Geräte-Empfehlungen
Windows Server 2016 ermöglicht das selektive anhalten standardmäßig für USB-Geräte. Allerdings kann ein schlecht geschriebener Gerätetreiber weiterhin Energieeffizienz durch eine beachtliche Rand unterbrechen. Um potenzielle Probleme zu vermeiden, trennen Sie USB-Geräte, deaktivieren sie das BIOS oder wählen Sie Server, die keine USB-Geräte erfordern.


## <a name="remotely-managed-power-strip-recommendations"></a>Remote verwalteten Strip Empfehlungen
Steckdosenleisten sind nicht Bestandteil von Serverhardware können, aber sie einen großen Unterschied im Rechenzentrum. Messungen zeigen, dass Volume-Server, die angeschlossen sind, aber haben wurde Administrationsfeatures ausgeschaltet, noch bis zu 30 Watt erfordern können.

Um zu vermeiden, Strom zu verschwenden, können Sie einen Remote verwalteten Steckerleiste für jedes Rack mit Servern programmgesteuert Power von bestimmten Servern getrennt bereitstellen.

## <a name="processor-terminology"></a>Prozessor-Terminologie
Prozessor-Terminologie in diesem Thema gibt die Hierarchie der Komponenten verfügbar sind, in der folgenden Abbildung. Begriffe, die vom größten zum kleinsten Granularität der Komponenten sind folgende:

-   Prozessorsocket
-   NUMA-Knoten
-   Core
-   Logischer Prozessor

![Prozessor-Terminologie](../media/perftune-guide-figure-1.png)

## <a name="see-also"></a>Siehe auch
- [Überlegungen zur Leistung von Server-Hardware](index.md)
- [Leistung und Leistungsoptimierung](power/power-performance-tuning.md)
- [Processor Power Management-Optimierung](power/processor-power-management-tuning.md)
- [Ausgeglichene Parametern empfohlen](power/recommended-balanced-plan-parameters.md)
