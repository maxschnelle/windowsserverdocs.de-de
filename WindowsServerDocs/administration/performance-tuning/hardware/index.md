---
title: Überlegungen zur Leistung von Serverhardware
description: Überlegungen zur Leistung von Serverhardware für Windows Server 2016
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: phstee
author: phstee
ms.date: 01/08/2018
ms.openlocfilehash: f9c7f0e589980f7d985f165e318667ebe2e5d5c5
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866749"
---
# <a name="server-hardware-performance-considerations"></a>Überlegungen zur Leistung von Serverhardware

Der folgende Abschnitt enthält wichtige Aspekte, die Sie bei der Wahl Ihrer Serverhardware berücksichtigen sollten. Diese Richtlinien helfen Ihnen dabei, Leistungsengpässe zu beseitigen, die ansonsten unter Umständen die Leistung des Servers beeinträchtigen.

## <a name="processor-recommendations"></a>Empfehlungen für den Prozessor

Verwenden Sie für Server 64-Bit-Prozessoren. 64-Bit-Prozessoren verfügen über einen deutlich größeren Adressraum und werden für Windows Server 2016 vorausgesetzt. Es steht keine 32-Bit-Edition des Betriebssystems zur Verfügung, 32-Bit-Anwendungen können jedoch unter dem 64-Bit-Betriebssystem Windows Server 2016 ausgeführt werden.

Zur Erhöhung der Rechenleistung eines Servers können Sie einen Prozessor mit höher getakteten Kernen verwenden oder die Anzahl von Prozessorkernen erhöhen. Sollte die CPU die beschränkende Ressource des Systems sein, bietet ein Kern mit doppelter Frequenz in der Regel eine höhere Leistungsverbesserung als zwei Kerne mit einfacher Frequenz.

Bei Verwendung mehrerer Kerne ist keine perfekte lineare Skalierung zu erwarten, und bei aktiviertem Hyperthreading kann der Skalierungsfaktor ggf. sogar noch niedriger sein, da Hyperthreading auf der gemeinsamen Nutzung von Ressourcen des gleichen physischen Kerns basiert.


>[!Important]
> Stimmen Sie den Arbeitsspeicher und das E/A-Subsystem auf die CPU-Leistung ab (und umgekehrt).

Vergleichen Sie keine CPU-Frequenzen unterschiedlicher Hersteller und Prozessorgenerationen miteinander: Ein solcher Vergleich kann sich als irreführender Geschwindigkeitsindikator erweisen.

Achten Sie für Hyper-V darauf, dass der Prozessor die Adressübersetzung der zweiten Ebene (Second Level Address Translation, SLAT) unterstützt. Sie wird von Intel als EPT (Extended Page Tables) und von AMD als NPT (Nested Page Tables) implementiert. Ob dieses Feature vorhanden ist, können Sie auf Ihrem Server mithilfe von „SystemInfo.exe“ überprüfen.

## <a name="cache-recommendations"></a>Empfehlungen für den Cache

Verwenden Sie große L2- oder L3-Prozessorcaches. Bei neueren Architekturen wie Haswell oder Skylake steht ein einheitlicher Last Level Cache (LLC) oder ein L4-Cache zur Verfügung. Die größeren Caches bieten im Allgemeinen eine bessere Leistung und spielen häufig eine wichtigere Rolle als die reine CPU-Frequenz.

## <a name="memory-ram-and-paging-storage-recommendations"></a>Empfehlungen für Arbeitsspeicher (RAM) und Auslagerungsspeicher

>[!Note] 
> Einige Systeme besitzen unter einer neuen Installation von Windows Server 2016 möglicherweise eine geringere Speicherleistung als unter Windows Server 2012 R2. Bei der Entwicklung von Windows Server 2016 wurde eine Reihe von Änderungen zur Verbesserung der Sicherheit und Zuverlässigkeit der Plattform vorgenommen. Einige Änderungen – etwa die standardmäßige Aktivierung von Windows Defender – führen zu längeren E/A-Pfaden, wodurch sich ggf. die E/A-Leistung bei bestimmten Workloads und Mustern verschlechtert. Microsoft rät davon ab, Windows Defender zu deaktivieren, da es sich dabei um eine wichtige Schutzebene für Ihre Systeme handelt. 

Erhöhen Sie den Arbeitsspeicher, um Ihren Arbeitsspeicherbedarf zu decken.
Sollte Ihr Computer akut mehr Arbeitsspeicher benötigen, nutzt Windows Speicherplatz auf der Festplatte, um den Arbeitsspeicher des Systems durch sogenanntes Auslagern zu ergänzen. Zu viel Auslagerung beeinträchtigt die Leistung des gesamten Systems.
Berücksichtigen Sie zur Optimierung der Auslagerung die folgenden Richtlinien für die Platzierung der Auslagerungsdatei:
- Isolieren Sie die Auslagerungsdatei auf einer eigenen Speichervorrichtung, oder stellen Sie zumindest sicher, dass sie nicht die gleichen Speichervorrichtungen verwendet wie andere Dateien, auf die häufig zugegriffen wird. Platzieren Sie also beispielsweise die Auslagerungsdatei und die Betriebssystemdateien jeweils auf separaten physischen Laufwerken.

- Platzieren Sie die Auslagerungsdatei auf einem Laufwerk ohne Fehlertoleranz. Im Falle eines Datenträgerfehlers kommt es wahrscheinlich zu einem Systemabsturz. Falls Sie die Auslagerungsdatei auf einem fehlertoleranten Laufwerk platzieren, bedenken Sie, dass Daten bei einem fehlertoleranten System häufig langsamer geschrieben werden, da die Daten an mehrere Orte geschrieben werden.

- Verwenden Sie mehrere Datenträger oder ein Datenträgerarray, wenn Sie zusätzliche Datenträgerbandbreite für die Auslagerung benötigen. Platzieren Sie nicht mehrere Auslagerungsdateien in verschiedenen Partitionen des gleichen physischen Laufwerks.

## <a name="peripheral-bus-recommendations"></a>Empfehlungen für den Peripheriebus
Unter Windows Server 2016 sollte für die primären Speicher- und Netzwerkschnittstellen PCI Express (PCIe) verwendet werden. Daher werden Server mit PCIe-Bus empfohlen. Verwenden Sie für Ethernetadapter mit 10 GB und mehr mindestens PCIe x8-Slots, um durch den Bus bedingte Geschwindigkeitseinbußen zu vermeiden.

## <a name="disk-recommendations"></a>Empfehlungen für Datenträger
Verwenden Sie Datenträger mit höherer Drehzahl, um wahlfreie Anforderung zu beschleunigen (um durchschnittlich etwa 2 ms zwischen Laufwerken mit 7.200 U/Min und 15.000 U/Min) und die Bandbreite für sequenzielle Anforderungen zu erhöhen. Bei Datenträgern mit hoher Drehzahl müssen allerdings Faktoren wie Kosten, Energiebedarf und andere Aspekte berücksichtigt werden.

Für Unternehmen konzipierte 2,5-Zoll-Datenträger können pro Sekunde eine deutlich höhere Anzahl wahlfreier Anforderungen bewältigen als entsprechende 3,5-Zoll-Laufwerke.

Speichern Sie Daten, auf die häufig zugegriffen wird (insbesondere solche, auf die sequenziell zugegriffen wird) am Anfang des Datenträgers, da es sich hierbei grob um den äußersten (und somit schnellsten) Bereich handelt.

Die Zusammenfassung kleiner Laufwerke zu einigen wenigen Laufwerken mit hoher Kapazität kann sich insgesamt negativ auf die Speicherleistung auswirken. Die geringere Anzahl von Spindeln führt dazu, dass weniger Anforderungen parallel verarbeitet werden können, was unter Umständen einen geringeren Durchsatz und längere Antwortzeiten zur Folge hat (abhängig von der Workloadintensität).

Der Einsatz von SSDs und Flashdatenträgern mit hoher Geschwindigkeit ist hilfreich bei Datenträgern mit hoher E/A-Rate oder wartezeitempfindlicher E/A, von denen hauptsächlich gelesen wird. SSDs oder Flashdatenträger eignen sich gut als Startdatenträger, da sie die Startzeit erheblich verbessern können.

NVMe-SSDs bieten eine überragende Leistung mit höherer Befehlswarteschlangentiefe, effizienterer Interruptverarbeitung und höherer Effizienz für 4-KB-Befehle. Dies ist insbesondere in Szenarien mit intensiver simultaner E/A hilfreich.


## <a name="network-and-storage-adapter-recommendations"></a>Empfehlungen für Netzwerk- und Speicheradapter

Der folgende Abschnitt enthält die empfohlenen Merkmale für Netzwerk- und Speicheradapter für Hochleistungsserver. Mit diesen Einstellungen können Sie verhindern, dass Ihre Netzwerk- oder Speicherhardware bei hoher Auslastung zu einem Engpass wird.

### <a name="certified-adapter-usage"></a>Verwendung zertifizierter Adapter
Verwenden Sie einen Adapter, der die Tests der Windows-Hardwarezertifizierung bestanden hat.

### <a name="64-bit-capability"></a>64-Bit-Fähigkeit
64-Bit-fähige Adapter können direkte Speicherzugriffsvorgänge (Direct Memory Access, DMA) für große physische Speicherorte (größer als 4 GB) ausführen. Sollte der Treiber keine DMA-Vorgänge mit einer Größe von mehr als 4 GB unterstützen, wird die E/A vom System unter Verwendung eines physischen Adressraums mit weniger als 4 GB doppelt gepuffert.

### <a name="copper-and-fiber-adapters"></a>Kupfer- und Glasfaseradapter
Kupferadapter bieten in der Regel die gleiche Leistung wie ihre Glasfaser-Pendants, und bei einigen Fibre Channel-Adaptern sind sowohl Kupfer als auch Glasfaser verfügbar. Manche Umgebungen eignen sich besser für Kupferadapter, während andere Umgebungen besser für Glasfaseradapter geeignet sind.

### <a name="dual--or-quad-port-adapters"></a>Adapter mit zwei oder vier Ports
Adapter mit mehreren Ports sind hilfreich bei Servern mit einer begrenzten Anzahl von PCI-Slots.

Einige Adapter verfügen über zwei oder vier SCSI-Busse auf einer einzelnen Adapterkarte, um SCSI-Beschränkungen hinsichtlich der Anzahl von Datenträgern zu behandeln, die mit einem SCSI-Bus verbunden werden können. Bei Fibre Channel-Adaptern kann in der Regel eine unbegrenzte Anzahl von Datenträgern mit dem Adapter verbunden werden (es sei denn, sie befinden sich hinter einer SCSI-Schnittstelle).

Bei SAS-Adaptern (Serial Attached SCSI) und SATA-Adaptern (Serial ATA) ist die Verbindungsanzahl ebenfalls eingeschränkt. Das liegt an der seriellen Art der Protokolle. Sie können jedoch Switches verwenden, um weitere Datenträger zu anzuschließen.

Dieses Feature ist bei Netzwerkadaptern für Lastenausgleichs- oder Failoverszenarien vorhanden. Durch die Verwendung von zwei Netzwerkadaptern mit jeweils einem einzelnen Port lässt sich bei der gleichen Workload in der Regel eine bessere Leistung erzielen als mit einem einzelnen Netzwerkadapter mit zwei Ports.

Die Beschränkung des PCI-Busses kann bei Adaptern mit mehreren Ports ein bedeutender limitierender Faktor für die Leistung sein. Aus diesem Grund empfiehlt es sich, sie in einem hochleistungsfähigen PCIe-Slot mit ausreichender Bandbreite zu platzieren.

### <a name="interrupt-moderation"></a>Interruptüberprüfung
Einige Adapter können moderieren, wie häufig sie die Hostprozessoren unterbrechen, um eine Aktivität oder deren Abschluss anzugeben. Die Interruptüberprüfung hat häufig eine Verringerung der CPU-Auslastung auf dem Host zur Folge. Sie muss jedoch auf intelligente Weise erfolgen, da sich sonst unter Umständen die Wartezeit erhöht.

### <a name="receive-side-scaling-rss-support"></a>Unterstützung der empfangsseitigen Skalierung (Receive Side Scaling, RSS)
RSS ermöglicht die Skalierung der Paketempfangsverarbeitung auf der Grundlage der Anzahl verfügbarer Computerprozessoren. Dies ist insbesondere bei einem Ethernet mit einer Geschwindigkeit von 10 GB oder mehr von Bedeutung.

### <a name="offload-capability-and-other-advanced-features-such-as-message-signaled-interrupt-msi-x"></a>Auslagerungsfunktion und andere erweiterte Features wie etwa MSI-X (Message Signaled Interrupt)
Auslagerungsfähige Adapter tragen zur Verringerung der CPU-Auslastung und somit zur Verbesserung der Leistung bei.

### <a name="dynamic-interrupt-and-deferred-procedure-call-dpc-redirection"></a>Dynamische Umleitung von Interrupts und DPCs (Deferred Procedure Calls)
Unter Windows Server 2016 können PCIe-Speicheradapter Interrupts und DPCs dank NUMA-E/A dynamisch umleiten. Darüber hinaus trägt das Feature bei Multiprozessorsystemen zur Verbesserung von Workloadpartitionierung, Cachetrefferraten und der Interconnect-Nutzung der Onboardhardware bei E/A-intensiven Workloads bei.

## <a name="see-also"></a>Weitere Informationen
- [Server Hardware Power Considerations](power.md) (Überlegungen zum Energiebedarf von Serverhardware)
- [Power and Performance Tuning](power/power-performance-tuning.md) (Leistungs- und Energieoptimierung)
- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](power/processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)
- [Recommended Balanced Power Plan Parameters for Workloads Requiring Quick Response Times](power/recommended-balanced-plan-parameters.md) (Empfohlene Parameter für den ausgewogenen Energiesparplan für Workloads, die kurze Antwortzeiten erfordern)
