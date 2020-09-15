---
title: Überlegungen zur Windows Server-Hardware Leistung
description: Überlegungen zur Windows Server-Hardware Leistung.
ms.topic: conceptual
ms.author: qizha
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fe316dd1f21d3f5e151cef60f63c3644ad1af06d
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077632"
---
# <a name="server-hardware-power-considerations"></a>Server Hardware Power Considerations (Überlegungen zum Energiebedarf von Serverhardware)

Es ist wichtig, die zunehmende Bedeutung der Energieeffizienz in Unternehmens-und Rechenzentrums Umgebungen zu erkennen. Hohe Leistung und geringer Energieverbrauch sind häufig widersprüchliche Ziele, aber indem Sie die Serverkomponenten sorgfältig auswählen, können Sie das richtige Gleichgewicht zwischen Ihnen erzielen. In den folgenden Abschnitten werden die Richtlinien für die Energieeigenschaften und die Funktionen von Server Hardwarekomponenten aufgeführt.

## <a name="processor-recommendations"></a>Empfehlungen für den Prozessor

Häufigkeit, Betriebsspannung, Cache Größe und Prozesstechnologie wirken sich auf den Energieverbrauch von Prozessoren aus. Prozessoren haben eine TDP-Bewertung (Thermo Design Point), die einen grundlegenden Hinweis auf den Energieverbrauch im Vergleich zu anderen Modellen liefert.

Entscheiden Sie sich im Allgemeinen für den niedrigsten TDP-Prozessor, der Ihre Leistungsziele erfüllt. Außerdem sind neuere Prozessor Prozessoren in der Regel effizienter, und Sie können mehr Energiezustände für die Windows-Energie Verwaltungs Algorithmen verfügbar machen, was eine bessere Energie Verwaltung auf allen Leistungsstufen ermöglicht. Oder Sie verwenden möglicherweise einige der neuen "kooperativen" Energie Verwaltungstechniken, die Microsoft in Zusammenarbeit mit Hardwareherstellern entwickelt hat.

Weitere Informationen zu kooperativen Energie Verwaltungstechniken finden Sie im Abschnitt "Collaborative Processor Performance Control" in der [Spezifikation "Advanced Configuration and Power Interface](http://www.uefi.org/sites/default/files/resources/ACPI_5_1release.pdf)".

## <a name="memory-recommendations"></a>Speicher Empfehlungen

Speicher Konten für einen zunehmenden Anteil der gesamten Systemleistung. Viele Faktoren wirken sich auf den Energieverbrauch eines Speicher-DIMM aus, z. b. auf Speichertechnologie, Fehlerkorrektur Code (ECC), Busfrequenz, Kapazität, Dichte und Anzahl der Ränge. Daher empfiehlt es sich, erwartete Strom Bewertungen zu vergleichen, bevor Sie große Mengen an Arbeitsspeicher kaufen.

Der Arbeitsspeicher ist jetzt verfügbar, Sie müssen jedoch die Leistungs-und Kosten Kompromisse in Erwägung gezogen. Wenn Ihr Server Paging wird, sollten Sie auch die Stromkosten der pagingdatenträger berücksichtigen.

## <a name="disks-recommendations"></a>Empfehlungen für Datenträger

Ein höheres RPM bedeutet einen erhöhten Energieverbrauch. SSD-Laufwerke sind leistungsfähiger als rotierende Laufwerke. Außerdem erfordern 2,5-Zoll-Laufwerke im Allgemeinen weniger Leistung als 3,5 Zoll-Laufwerke.

## <a name="network-and-storage-adapter-recommendations"></a>Empfehlungen für Netzwerk- und Speicheradapter

Einige Adapter verringern den Energieverbrauch während Leerlaufzeiten. Dies ist ein wichtiger Aspekt bei 10-GB-Netzwerkadaptern und Speicher Verbindungen mit hoher Bandbreite (4-8 GB). Solche Geräte können große Mengen an Energie beanspruchen.

## <a name="power-supply-recommendations"></a>Empfehlungen zur Stromversorgung

Das verbessern der Energieversorgung ist eine hervorragend Möglichkeit, den Energieverbrauch zu reduzieren, ohne die Leistung zu beeinträchtigen Hochleistungs Stromversorgung kann pro Server viele kilostunden pro Jahr einsparen.

## <a name="fan-recommendations"></a>Lüfter-Empfehlungen

Fans, wie Stromversorgungen, sind ein Bereich, in dem Sie den Energieverbrauch reduzieren können, ohne die Systemleistung zu beeinträchtigen. Die Lüfter mit variabler Geschwindigkeit können das RPM verringern, wenn die Systemlast abnimmt und andernfalls unnötige Energieverbrauch entfällt.

## <a name="usb-devices-recommendations"></a>Empfehlungen für USB-Geräte

Windows Server 2016 aktiviert standardmäßig den selektiven Suspend für USB-Geräte. Ein schlecht geschriebener Gerätetreiber kann jedoch weiterhin die System Energieeffizienz um einen beträchtlichen Rand stören. Um potenzielle Probleme zu vermeiden, trennen Sie die USB-Geräte, deaktivieren Sie Sie im BIOS, oder wählen Sie Server aus, für die keine USB-Geräte erforderlich sind.

## <a name="remotely-managed-power-strip-recommendations"></a>Remote verwaltete Strom Band Empfehlungen

Strom Striche sind kein wesentlicher Bestandteil der Server Hardware, Sie können jedoch einen großen Unterschied im Rechenzentrum ausmachen. Messungen zeigen, dass die volumeserver, die angeschlossen sind, aber bereits ausgeschaltet sind, möglicherweise bis zu 30 Watt Energie benötigen.

Um die Stromverschwendung zu vermeiden, können Sie einen Remote verwalteten stromstreifen für jedes Rack von Servern bereitstellen, um die Stromversorgung von bestimmten Servern Programm gesteuert zu trennen.

## <a name="processor-terminology"></a>Prozessor Terminologie

Die in diesem Thema verwendete Prozessor Terminologie reflektiert die Hierarchie der Komponenten, die in der folgenden Abbildung dargestellt sind. Die folgenden Begriffe werden von der größten bis zur kleinsten Granularität von-Komponenten verwendet:

- Prozessor Socket
- NUMA-Knoten
- Core
- Logischer Prozessor

![Prozessor Terminologie](../media/perftune-guide-figure-1.png)

## <a name="additional-references"></a>Weitere Verweise

- [Überlegungen zur Leistung von Serverhardware](index.md)

- [Power and Performance Tuning](power/power-performance-tuning.md) (Leistungs- und Energieoptimierung)

- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](power/processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)

- [Recommended Balanced Power Plan Parameters for Workloads Requiring Quick Response Times](power/recommended-balanced-plan-parameters.md) (Empfohlene Parameter für den ausgewogenen Energiesparplan für Workloads, die kurze Antwortzeiten erfordern)
