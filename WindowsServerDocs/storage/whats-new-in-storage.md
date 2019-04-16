---
ms.assetid: 0f2a7f7b-aca8-4e5d-ad67-4258e88bc52f
title: Neuerungen beim Speicher in Windows Server
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dongill
ms.technology: storage
ms.topic: article
author: kumudd
ms.date: 09/15/2016
ms.openlocfilehash: 9aab6246f7ddc86629834bf20a7d21cc4ce2ec8f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="whats-new-in-storage-in-windows-server-2016"></a>Neuerungen beim Speicher in Windows Server 2016

>Gilt für: Windows Server2016

In diesem Thema wird die neue und geänderte Speicherfunktionalität in Windows Server2016 erläutert.

## <a name="s2d"></a>Speicherplätze DAS  
Mit direkten Speicherplätzen kann hoch verfügbarer und skalierbarer Speicher unter Verwendung von Servern mit lokalem Speicher erstellt werden. Mit diesem Feature wird die Bereitstellung und die Verwaltung von softwaredefinierten Speichersystemen vereinfacht und auch der Weg zur Nutzung neuer Datenträgerklassen wie z.B. SATA-SSD und NVMe geebnet, was vorher bei gruppierten Speicherplätzen mit freigegebenen Datenträgern nicht möglich war.  

**Welchen Nutzen bietet diese Änderung?**  
Mit direkten Speicherplätzen können Dienstanbieter und Unternehmen Server nach Industriestandard mit lokalem Speicher einsetzen, um hoch verfügbare und skalierbare softwaredefinierte Speichersysteme zu erstellen. Die Verwendung von Servern mit lokalem Speicher führt zu weniger Komplexität, höherer Skalierbarkeit und der Möglichkeit, Speichergeräte zu nutzen, die zuvor nicht verwendet werden konnten (z.B. SATA-SSDs zum Senken der Kosten von Flash-Speicher oder NVMe-SSDs für eine höhere Leistung).  

Bei Verwendung von direkten Speicherplätzen wird kein gemeinsames SAS-Fabric benötigt, sodass die Bereitstellung und die Konfiguration vereinfacht werden. Stattdessen wird das Netzwerk als Speicherfabric genutzt. Dabei kommen SMB3 und SMB Direct (RDMA) zum Einsatz, um Speicher mit hoher Geschwindigkeit, geringer Latenz und hoher CPU-Effizienz bereitzustellen. Für eine horizontale Hochskalierung fügen Sie ganz einfach weitere Server hinzu, um die Speicherkapazität und die E/A-Leistung zu steigern.  
Weitere Informationen finden Sie unter [Direkte Speicherplätze in Windows Server 2016](storage-spaces/storage-spaces-direct-overview.md).  

**Worin bestehen die Unterschiede?**  
Dies ist eine neue Funktion in Windows Server 2016.  

## <a name="storage-replica"></a>Speicherreplikat  
Speicherreplikat ermöglicht eine speicheragnostische, synchrone Replikation auf Blockebene zwischen Servern oder Clustern für die Notfallwiederherstellung sowie das Strecken eines Failoverclusters zwischen Standorten. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt. Die asynchrone Replikation ermöglicht die Standorterweiterung über regionale Bereiche hinaus mit der Möglichkeit von Datenverlusten.  

**Welchen Nutzen bietet diese Änderung?**  
Mithilfe der Speicherreplikation können Sie folgende Ziele erreichen:  

* Bereitstellen einer Notfallwiederherstellungslösung von einem einzigen Anbieter für geplante und ungeplante Ausfälle unternehmenskritischer Workloads.
* Verwenden des SMB3-Transportprotokolls mit bewährter Zuverlässigkeit, Skalierbarkeit und Leistung.
* Strecken von Windows-Failoverclustern über regionale Bereiche hinweg.
* Einsatz von Microsoft-Software für die gesamte Speicher- und Clusterumgebung. Dazu zählen Hyper-V, Speicherreplikate, Speicherplätze, Cluster, Dateiserver mit horizontaler Skalierung, SMB3, Deduplizierung und ReFS/NTFS.
* Aufgrund der folgenden Merkmale können Sie die Kosten und die Komplexität senken: 
    * Hardwareagnostisches System, das keine spezifische Speicherkonfiguration wie DAS oder SAN benötigt.
    * Möglichkeit, allgemeine Speicher- und Netzwerktechnologien zu nutzen.
    * Problemlose grafische Verwaltung für einzelne Knoten und Cluster über den Failovercluster-Manager.
    * Umfangreiche Skriptoptionen über Windows PowerShell. 
* Weniger Downtime sowie höhere Zuverlässigkeit und Produktivität dank Windows.  
* Unterstützbarkeit, Leistungsmetriken und Diagnosefunktionen.  

Weitere Informationen finden Sie unter [Speicherreplikate in Windows Server 2016](storage-replica/storage-replica-overview.md).  

**Worin bestehen die Unterschiede?**  
Dies ist eine neue Funktion in Windows Server 2016.  

## <a name="storage-qos"></a>Quality of Service für Speicher  
Sie können Quality of Service (QoS) für Speicher jetzt nutzen, um die End-to-End-Speicherleistung zu überwachen und Verwaltungsrichtlinien unter Verwendung von Hyper-V- und CSV-Clustern in Windows Server 2016 zu erstellen.  

**Welchen Nutzen bietet diese Änderung?**  
Sie können nun Speicher-QoS-Richtlinien auf einem CSV-Cluster erstellen und diese einem oder mehreren virtuellen Datenträgern auf virtuellen Hyper-V-Computern zuweisen. Bei Änderungen des Workloads und der Speicherlast wird die Speicherleistung automatisch neu angepasst, um die Richtlinien einzuhalten.  

* In jeder Richtlinie kann ein Reservewert (Minimum) und/oder ein Grenzwert (Maximum) festgelegt werden, der auf eine Sammlung von Datenflüssen angewendet wird (z.B. auf eine virtuelle Festplatte, auf einen einzelnen virtuellen Computer oder eine Gruppe virtueller Computer, auf einen Dienst oder auf einen Mandanten).  
* Über Windows PowerShell oder WMI können die folgenden Aufgaben ausgeführt werden:  
    * Erstellen von Richtlinien auf einem CSV-Cluster
    * Auflisten von Richtlinien auf einem CSV-Cluster
    * Zuweisen einer Richtlinie zu einer virtuellen Festplatte eines virtuellen Hyper-V-Computers 
    * Überwachen der Leistung der einzelnen Flüsse und Status innerhalb der Richtlinie  
* Wenn mehrere virtuelle Festplatten dieselbe Richtlinie verwenden, wird die Leistung gleichmäßig verteilt, um die Mindest- und Höchstwerte der Richtlinien einzuhalten. Daher kann eine Richtlinie zum Verwalten einer virtuellen Festplatte, eines virtuellen Computers, mehrerer virtueller Computer, die einen Dienst umfassen, oder aller virtuellen Computer, die zu einem Mandanten gehören, genutzt werden.  

**Worin bestehen die Unterschiede?**  
Dies ist eine neue Funktion in Windows Server 2016. Das Verwalten von Mindestreserven, das Überwachung von Flüssen aller virtuellen Festplatten im Cluster über einen einzigen Befehl und die zentralisierte, richtlinienbasierte Verwaltung waren in früheren Versionen von Windows Server nicht möglich.  

Weitere Informationen finden Sie unter [Storage Quality of Service](storage-qos/storage-qos-overview.md) (Speicher-QoS).

## <a name="dedup"></a>Datendeduplizierung  
| Funktion | Neu oder aktualisiert | Beschreibung |
|---------------|----------------|-------------|
| [Unterstützung für große Volumes](data-deduplication/whats-new.md#large-volume-support) | Aktualisiert | Vor Windows Server 2016 musste die Größe der Volumes speziell für die erwartete Änderung konfiguriert werden, wobei Volumes mit über 10TB keine geeigneten Kandidaten für die Deduplizierung waren. In Windows Server 2016 unterstützt die Datendeduplizierung Volumegrößen von **bis zu 64TB**. |
| [Unterstützung für große Dateien](data-deduplication/whats-new.md#large-file-support) | Aktualisiert | Vor Windows Server2016 waren Dateien mit einer Größe von knapp 1TB keine geeigneten Kandidaten für die Deduplizierung. In Windows Server 2016 werden Dateien mit einer Größe von **bis zu 1TB** vollständig unterstützt. |
| [Unterstützung für Nano Server](data-deduplication/whats-new.md#nano-server-support) | „Neu“, | Die Datendeduplizierung ist in der neuen Nano Server-Bereitstellungsoption für Windows Server2016 verfügbar und wird von dieser Option vollständig unterstützt. |
| [Vereinfachte Unterstützung von Sicherungen](data-deduplication/whats-new.md#simple-backup-support) | „Neu“, | In Windows Server 2012 R2 mussten eine Reihe manueller Konfigurationsschritte ausgeführt werden, um virtualisierte Sicherungsanwendungen wie Microsoft [Data Protection Manager](https://technet.microsoft.com/en-us/library/hh758173.aspx) zu unterstützten. In Windows Server 2016 wurde ein neuer Standardverwendungstyp „Sicherung“ hinzugefügt, um eine nahtlose Bereitstellung der Datendeduplizierung für virtualisierte Sicherungsanwendungen zu ermöglichen. |
| [Unterstützung für parallele Upgrades des Clusterbetriebssystems](data-deduplication/whats-new.md#cluster-upgrade-support) | „Neu“, | Die Datendeduplizierung bietet vollständige Unterstützung für das neue Feature für [parallele Upgrades des Clusterbetriebssystems](..//failover-clustering/cluster-operating-system-rolling-upgrade.md) von Windows Server 2016. |

## <a name="smb-hardening-improvements"></a>Verbesserungen beim Härten von SMB für SYSVOL- und NETLOGON-Verbindungen  
In Windows 10 und Windows Server 2016 ist für Clientverbindungen mit den SYSVOL- und NETLOGON-Standardfreigaben von Active Directory Domain Services jetzt die SMB-Signierung und gegenseitige Authentifizierung (z.B. Kerberos) erforderlich.   

**Welchen Nutzen bietet diese Änderung?**  
Durch diese Änderung wird die Wahrscheinlichkeit von Man-in-the-Middle-Angriffen verringert.   

**Worin bestehen die Unterschiede?**  
Wenn die SMB-Signierung und die gegenseitige Authentifizierung nicht verfügbar sind, kann ein Computer mit Windows 10 oder Windows Server2016 keine domänenbasierten Gruppenrichtlinien und Skripts verarbeiten.  

> [!NOTE]  
> Die Registrierungswerte für diese Einstellungen sind standardmäßig nicht verfügbar, die Härtungsregeln gelten jedoch trotzdem, bis sie von Gruppenrichtlinien oder anderen Registrierungswerten außer Kraft gesetzt werden.  

Weitere Informationen zu diesen Verbesserungen (auch als UNC-Härtung bezeichnet) finden Sie im Microsoft Knowledge Base-Artikel [3000483](http://support.microsoft.com/kb/3000483) und unter [MS15-011 & MS15-014: Hardening Group Policy](http://blogs.technet.microsoft.com/srd/2015/02/10/ms15-011-ms15-014-hardening-group-policy) (MS15-011 & MS15-014: Härten von Gruppenrichtlinien).  

## <a name="work-folders"></a>Arbeitsordner
Verbesserte Änderungsbenachrichtigung, wenn auf dem Arbeitsordner-Server Windows Server 2016 und auf dem Arbeitsordner-Clients Windows 10 ausgeführt wird.

**Welchen Nutzen bietet diese Änderung?**<br>
Werden unter Windows Server 2012 R2 Dateiänderungen auf die Arbeitsordner-Server synchronisiert, werden die Clients nicht über die Änderung benachrichtigt, und es dauert bis zu 10 Minuten, bis die Aktualisierungen verfügbar sind.  Bei Verwendung von Windows Server 2016 benachrichtigt der Arbeitsordner-Server die Windows 10-Clients sofort, und die Dateiänderungen werden sofort synchronisiert.

**Worin bestehen die Unterschiede?**<br>
Dies ist eine neue Funktion in Windows Server 2016. Dies erfordert einen Arbeitsordnerserver mit Windows Server 2016 und einen Client mit Windows 10.

Wenn Sie einen älteren Client verwenden oder wenn auf dem Arbeitsordnerserver Windows Server2012R2 ausgeführt wird, sucht der Client weiterhin alle zehn Minuten nach Änderungen.

## <a name="refs"></a>ReFS 
Die nächste Iteration von ReFS unterstützt umfangreiche Speicherbereitstellungen mit unterschiedlichen Workloads und bietet Zuverlässigkeit, Resilienz und Skalierbarkeit für Ihre Daten.     

**Welchen Nutzen bietet diese Änderung?**<br>
ReFS sorgt für folgende Verbesserungen:

* ReFS implementiert neue Funktionen für Speicherebenen, die eine höhere Leistung und Speicherkapazität ermöglichen. Diese neuen Funktionen ermöglichen Folgendes:
    * Mehrere Resilienztypen für den gleichen virtuellen Datenträger (beispielsweise mit Spiegelung auf der Leistungsebene und Parität auf der Kapazitätsebene).
    * Schnellere Reaktion auf driftende Workingsets. 
    * Unterstützung von SMR-Medien (Shingled Magnetic Recording). 
* Die Einführung von Block Cloning hat eine erhebliche Verbesserung der Leistung von VM-Vorgängen zur Folge, was sich beispielsweise bei der Zusammenführung von VHDX-Prüfpunkten bemerkbar macht.
* Das neue ReFS-Überprüfungsprogramm ermöglicht die Behandlung von Speicherverlusten und schützt Daten vor kritischen Beschädigungen. 

**Worin bestehen die Unterschiede?**<br>
Diese Funktionen sind neu in Windows Server2016. 

## <a name="see-also"></a>Weitere Informationen  
* [Neuerungen in Windows Server2016](../get-started/what-s-new-in-windows-server-2016.md)  
