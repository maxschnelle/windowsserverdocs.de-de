---
title: Leistungsoptimierung für Windows Server-Container
description: Empfehlungen zur Leistungsoptimierung für Windows Server-Container unter Windows Server 16
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: davso; ericam; yashi
author: akino
ms.date: 10/16/2017
ms.openlocfilehash: a4508e28e54562748422b198f703e23326d15720
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851633"
---
# <a name="performance-tuning-windows-server-containers"></a>Leistungsoptimierung für Windows Server-Container

## <a name="introduction"></a>Einführung
Windows Server 2016 ist die erste Version von Windows, bei der die Containertechnologie bereits in das Betriebssystem integriert ist. In Windows Server 2016 sind zwei Arten von Containern verfügbar: Windows Server-Container und Hyper-V-Container. Jeder Containertyp unterstützt entweder die Server Core- oder Nano Server-SKU von Windows Server 2016. 

Diese Konfigurationen sind mit unterschiedlichen Auswirkungen auf die Leistung verbunden. Unten finden Sie eine Beschreibung, damit Sie entscheiden können, welche Konfiguration für Ihre Szenarien geeignet ist. Außerdem werden die Details der Auswirkungen auf die Leistung sowie die Nachteile der Optionen beschrieben.

### <a name="windows-server-container-and-hyper-v-containers"></a>Windows Server-Container und Hyper-V-Container

Windows Server-Container und Hyper-V-Container weisen viele Portabilitäts- und Konsistenzvorteile auf, aber sie unterscheiden sich in Bezug auf die Isolationsgarantie und die Leistungsmerkmale.

**Windows Server-Container**: Bieten Anwendungsisolation mithilfe einer Technologie zum Isolieren von Prozessen und Namespaces. Ein Windows Server-Container teilt sich einen Kernel mit dem Containerhost und allen Container, die auf dem Host ausgeführt werden.

**Hyper-V-Container**: Erweitern die Isolationsmöglichkeiten von Windows Server-Containern, indem jeder Container auf einem stark optimierten virtuellen Computer ausgeführt wird. Bei dieser Konfiguration wird der Kernel des Containerhosts nicht gemeinsam mit den Hyper-V-Containern verwendet.

Die zusätzliche Isolation durch Hyper-V-Container wird größtenteils durch eine Hypervisor-Isolationsebene zwischen dem Container und dem Containerhost erreicht. Dies wirkt sich auf die Containerdichte aus (im Gegensatz zu Windows Server-Containern), da es zu einer reduzierten Freigabe von Systemdateien und Binärdateien kommen kann. Dies führt allgemein zu einem größeren Speicher- und Arbeitsspeicherbedarf. Außerdem kommt es für einige Netzwerk-, Speicher-E/A- und CPU-Pfade zum erwarteten Mehraufwand.

### <a name="nano-server-and-server-core"></a>Nano Server und Server Core

Windows Server-Container und Hyper-V-Container verfügen über Unterstützung für Server Core und für eine neue Installationsoption, die unter Windows Server 2016 verfügbar ist: [Nano Server](https://technet.microsoft.com/windows-server-docs/compute/nano-server/getting-started-with-nano-server). 

Nano Server ist ein remote verwaltetes Serverbetriebssystem, das für private Clouds und Rechenzentren optimiert ist. Das Betriebssystem ähnelt Windows Server im Modus Server Core, ist aber deutlich kleiner, hat keine Möglichkeit zur lokalen Anmeldung, und unterstützt ausschließlich 64-Bit-Anwendungen, Tools und Agents. Es beansprucht erheblich weniger Speicherplatz und startet schneller.

## <a name="container-start-up-time"></a>Startzeit von Containern
Die Startzeit von Containern ist eine wichtige Metrik in vielen Szenarien, in denen sich durch Container die größten Vorteile ergeben. Daher ist es sehr wichtig zu verstehen, wie die Startzeit von Containern am besten optimiert werden kann. Unten sind einige Kompromisse beschrieben, die beim Optimieren ggf. eingegangen werden müssen, um eine Verbesserung der Startzeit zu erzielen.

### <a name="first-logon"></a>Erste Anmeldung

Microsoft stellt ein Basisimage für Nano Server und Server Core bereit. Das Basisimage für Server Core wurde optimiert, indem der Mehraufwand für die Startzeit beseitigt wurde, der mit der ersten Anmeldung (Windows-Willkommensseite) verbunden ist. Dies ist beim Nano Server-Basisimage nicht der Fall. Dieser Aufwand kann für Images auf Nano Server-Basis aber beseitigt werden, indem für das Containerimage mindestens eine Ebene committet wird. Für nachfolgende Containerstarts über das Image fällt der Aufwand für die erste Anmeldung dann nicht mehr an.
### <a name="scratch-space-location"></a>Ort des sicheren Speicherbereichs

Für Container wird standardmäßig ein temporärer sicherer Speicherbereich auf Systemlaufwerkmedien des Containerhosts verwendet, um Daten während der Lebensdauer des ausgeführten Containers zu speichern. Dieser Bereich wird als Systemlaufwerk des Containers verwendet, und daher wird dieser Pfad für viele Schreib- und Lesevorgänge der Containervorgänge genutzt. Für Hostsysteme, bei denen sich das Systemlaufwerk auf rotierenden magnetischen Medien (HDDs) befindet und gleichzeitig schnellere Speichermedien verfügbar sind (schnellere HDDs oder SSDs), kann der sichere Speicherbereich des Containers auf ein anderes Laufwerk verlagert werden. Dies erreichen Sie, indem Sie den Befehl „dockerd –g“ verwenden. Dieser Befehl ist global und wirkt sich auf alle Container aus, die auf dem System ausgeführt werden.

### <a name="nested-hyper-v-containers"></a>Geschachtelte Hyper-V-Container
Mit Hyper-V für Windows Server 2016 wird Unterstützung für die Hypervisor-Schachtelung eingeführt. Es ist jetzt also möglich, einen virtuellen Computer über einen anderen virtuellen Computer auszuführen. Dies ermöglicht viele nützliche Szenarien, aber es werden auch einige Auswirkungen auf die Leistung verstärkt, die für den Hypervisor bestehen. Der Grund ist, dass oberhalb des physischen Hosts zwei Hypervisor-Ebenen ausgeführt werden.

Für Container ergibt sich hieraus eine Beeinträchtigung, wenn ein Hyper-V-Container auf einem virtuellen Computer ausgeführt wird. Da ein Hyper-V-Container die Isolation über eine Hypervisor-Ebene zwischen sich selbst und dem Containerhost realisiert, hat dies folgende Auswirkung, wenn der Containerhost ein virtueller Computer auf Hyper-V-Basis ist: Es kommt in Bezug auf Containerstartzeit, Speicher-E/A und Durchsatz sowie CPU zu Mehraufwand bei der Leistung.

## <a name="storage"></a>Speicher
### <a name="mounted-data-volumes"></a>Eingebundene Datenvolumes

Bei Containern ist es möglich, dass das Systemlaufwerk des Containerhosts für den sicheren Speicherbereich des Containers verwendet wird. Der sichere Speicherbereich des Containers verfügt aber über eine ähnlich lange Lebensdauer wie der Container. Dies bedeutet, dass der sichere Speicherbereich und alle zugeordneten Daten verloren gehen, wenn der Container angehalten wird.

Es gibt aber viele Szenarien, in denen Daten unabhängig von der Lebensdauer des Containers beibehalten werden sollen. Für diese Fälle wird das Einbinden von Datenvolumes vom Containerhost in den Container unterstützt. Für Windows Server-Container kann der Mehraufwand für den E/A-Pfad, der bei eingebundenen Datenvolumes anfällt, vernachlässigt werden (nahezu native Leistung). Wenn Datenvolumes aber in Hyper-V-Container eingebunden werden, kommt es für diesen Pfad zu E/A-Leistungsbeeinträchtigungen. Außerdem werden diese Beeinträchtigungen noch verstärkt, wenn Hyper-V-Container auf virtuellen Computern ausgeführt werden.

### <a name="scratch-space"></a>Sicherer Speicherbereich

Sowohl für Windows Server-Container als auch für Hyper-V-Container wird für den sicheren Speicherbereich des Containers standardmäßig eine dynamische VHD mit 20 GB bereitgestellt. Bei beiden Containertypen nimmt das Betriebssystem des Containers einen Teil des Platzes ein. Dies gilt für jeden Container, der gestartet wird. Daher ist es wichtig zu wissen, dass sich jeder gestartete Container auf den Speicher auswirkt und je nach Workload bis zu 20 GB auf die Sicherungsspeichermedien schreiben kann. Dies sollte bei der Konfiguration von Speichermedien jeweils bedacht werden.
(Kann die Größe des sicheren Speicherbereichs konfiguriert werden?)

## <a name="networking"></a>Netzwerk
Windows Server-Container und Hyper-V-Container verfügen über unterschiedliche Netzwerkmodi, damit die Anforderungen verschiedener Netzwerkkonfigurationen bestmöglich erfüllt werden können. Für jede dieser Optionen gelten eigene Leistungsmerkmale.

### <a name="windows-network-address-translation-winnat"></a>Windows-Netzwerkadressenübersetzung (WinNAT)

Jeder Container erhält eine IP-Adresse aus einem internen, privaten IP-Präfix (z. B. 172.16.0.0/12). Portweiterleitung/-zuordnung vom Containerhost zu Containerendpunkten wird unterstützt. Docker erstellt standardmäßig ein NAT-Netzwerk, wenn dockerd zum ersten Mal ausgeführt wird.

Von diesen drei Modi ist die NAT-Konfiguration der teuerste Netzwerk-E/A-Pfad, für den aber der geringste Konfigurationsaufwand anfällt. 

Windows Server-Container verwenden eine Host-vNIC für die Verbindung mit dem virtuellen Switch. Hyper-V-Container verwenden eine synthetische VM-NIC (nicht für die Utility-VM verfügbar gemacht) für die Verbindung mit dem virtuellen Switch. Wenn Container mit dem externen Netzwerk kommunizieren, werden die Pakete per WinNAT mit angewendeten Adressübersetzungen weitergeleitet, wodurch es zu Mehraufwand kommt.

### <a name="transparent"></a>Transparent

Jeder Containerendpunkt ist direkt mit dem physischen Netzwerk verbunden. IP-Adressen aus dem physischen Netzwerk können mithilfe eines externen DHCP-Servers statisch oder dynamisch zugewiesen werden.

Der Modus „Transparent“ ist in Bezug auf den Netzwerk-E/A-Pfad der kostengünstigste. Externe Pakete werden direkt über die virtuelle NIC des Containers übergeben, sodass direkter Zugriff auf das externe Netzwerk besteht.

### <a name="l2-bridge"></a>L2-Brücke
Alle Containerendpunkte befinden sich in demselben IP-Subnetz wie der Containerhost. Die IP-Adressen müssen statisch aus dem gleichen Präfix wie der Containerhost zugewiesen werden. Alle Containerendpunkte auf dem Host verfügen aufgrund der Layer-2-Adressübersetzung über dieselbe MAC-Adresse.

Der Modus „L2-Brücke“ ermöglicht eine höhere Leistung als der Modus „WinNAT“, da er direkten Zugriff auf das externe Netzwerk bietet. Die Leistung des Modus „Transparent“ erreicht er aber nicht, da er auch mit der MAC-Adressübersetzung verbunden ist.




