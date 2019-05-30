---
ms.assetid: 0f2a7f7b-aca8-4e5d-ad67-4258e88bc52f
title: Neuerungen beim Speicher in Windows Server
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dongill
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 05/29/2019
ms.openlocfilehash: 5469d663f64fdb453e03863f409b675473d3f6aa
ms.sourcegitcommit: 8eea7aadbe94f5d4635c4ffedc6a831558733cc0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308569"
---
# <a name="whats-new-in-storage-in-windows-server"></a>Neuerungen beim Speicher in Windows Server

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

In diesem Thema wird erläutert, die neue und geänderte Funktionen im Speicher in Windows Server 2019, Windows Server 2016 und Windows Server Halbjährlicher Kanal frei.

## <a name="whats-new-in-storage-in-windows-server-2019-and-windows-server-version-1903"></a>Neuerungen beim Speicher in Windows Server-2019 und Windows Server, Version 1903

Diese Version von Windows Server bietet die folgenden Änderungen und Technologien.

### <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>Storage-Migration-Dienst migriert jetzt lokale Konten, -Cluster und Linux-Servern

Storage-Migration-Dienst erleichtert es, für die Migration der Server auf eine neuere Version von Windows Server. Es bietet ein grafisches Tool, die inventarisiert, die Daten auf Servern und dann die Daten und die Konfiguration auf neueren Servern übertragen – alles ohne Anwendungen oder Benutzer Änderungen vornehmen müssen.

Wenn diese Version von Windows Server verwenden, um Migrationen zu orchestrieren, haben wir die folgenden Funktionen hinzugefügt:

- Migrieren Sie lokale Benutzer und Gruppen mit dem neuen server
- Migrieren des Speichers von Failoverclustern
- Migrieren des Speichers von einem Linux-Server, der Samba verwendet
- Synchronisieren Sie leichter migrierte Dateifreigaben in Azure mithilfe von Azure File Sync
- Migrieren Sie zu neuen wie z. B. Azure-Netzwerken

Weitere Informationen zu Storage Migration Service, finden Sie unter [Übersicht über die Speicherung Datenbankmigrationsdienst](storage-migration-service/overview.md).

### <a name="system-insights-disk-anomaly-detection"></a>System Insights Datenträger Erkennung von Anomalien

[System Insights](../manage/system-insights/overview.md) ist ein predictive Analytics-Feature, das lokal analysiert Daten von Windows Server System und bietet einen Einblick in die Funktionsweise des Servers. Es enthält eine Reihe von integrierten Funktionen, aber wir haben die Möglichkeit, installieren zusätzliche Funktionen, die über Windows Admin Center, hinzugefügt, der Erkennung von Anomalien ab.

Erkennung von Anomalien ist eine neue Funktion, die hebt hervor, wenn Datenträger gerätefähigkeiten *anders* als üblich. Zwar verschiedene nicht unbedingt kann eine schlechte Sache, sehen diese anomalen Momente hilfreich sein, beim Behandeln von Problemen auf Ihren Systemen.

Diese Funktion steht auch für Server mit Windows Server-2019.

### <a name="windows-admin-center-enhancements"></a>Verbesserungen von Windows Admin Center

Eine neue Version von Windows Admin Center ist, Hinzufügen von neuen Funktionen zu Windows Server. Weitere Informationen zu den neuesten Features finden Sie unter [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md).

## <a name="whats-new-in-storage-in-windows-server-2019-and-windows-server-version-1809"></a>Neuerungen beim Speicher in Windows Server-2019 und Windows Server, Version 1809

Diese Version von Windows Server bietet die folgenden Änderungen und Technologien.

### <a name="manage-storage-with-windows-admin-center"></a>Verwalten von Speicher mit Windows Admin Center

[Windows Admin Center](../manage/windows-admin-center/overview.md) ist eine neue lokal bereitgestellte, browserbasierte-app für die Verwaltung von Servern, Clustern, hyperkonvergenten Infrastruktur mit "direkte Speicherplätze" und Windows 10-PCs. Es ist ohne zusätzliche Kosten über Windows und für die Produktion bereit ist.

Fairerweise sollte erwähnt werden, ist Windows Admin Center ein separater Download, der auf Windows Server-2019 und anderen Versionen von Windows, ausgeführt wird, aber ist neu, und wir wollten nicht verpassen Sie...

### <a name="storage-migration-service"></a>Speichermigrationsdienst

Der Speichermigrationsdienst ist eine neue Technologie, mit der Server leichter auf eine neuere Version von Windows Server migriert werden können. Es bietet ein grafisches Tool, das Daten auf Servern inventarisiert, Daten und Konfiguration auf neuere Server überträgt und dann optional die Identitäten der alten Server auf die neuen Server überträgt, sodass Apps und Benutzer nichts ändern müssen. Weitere Informationen finden Sie unter [Speichermigrationsdienst)](storage-migration-service/overview.md).

### <a id="storage-spaces-direct"></a>"Direkte Speicherplätze" (nur WindowsServer 2019)

Es gibt eine Reihe von Verbesserungen an "direkte Speicherplätze" in Windows Server-2019 ("direkte Speicherplätze" ist nicht in Windows Server enthalten, Halbjährlicher Kanal):

- **Deduplizierung und Komprimierung für ReFS-volumes**

    Store bis zu zehnmal mehr Daten auf dem gleichen Volume mit Deduplizierung und Komprimierung für das ReFS-Dateisystem. (sie hat [nur einem Klick](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be) mit Windows Admin Center aktivieren.) Variabler Größe Blockspeicher mit optionalen Komprimierung maximiert einsparungen abgerechnet, während die mit mehreren Threads Nachbearbeitung Architektur Auswirkungen auf die Leistung minimal bleibt. Volumes unterstützt bis zu 64 TB und werden die erste 4 TB der einzelnen Dateien dedupliziert.

- **Systemeigene Unterstützung für den persistenten Speicher**

    Erhalten Sie beispiellose Leistung mit der systemeigenen Storage Spaces Direct-Unterstützung für persistente Speichermodule, einschließlich Intel® Optane™ DC PM und NVDIMM-N. Verwenden Sie den permanenten Speicher als Cache, um den aktiven Arbeitssatz zu beschleunigen, oder als Kapazität, um eine konsistente niedrige Latenz in der Größenordnung von Mikrosekunden zu gewährleisten. Verwalten Sie persistenten Speicher wie jedes andere Laufwerk in PowerShell oder Windows Admin Center.

- **Geschachtelte Flexibilität in Bezug auf zwei Knoten hyperkonvergenten Infrastruktur am Rand**

    Bewältigen Sie zwei Hardwarefehler auf einmal mit einer völlig neuen Software-Resilience-Option, die von RAID 5+1 inspiriert wurde. Mit verschachtelter Ausfallsicherheit kann ein Storage Spaces Direct-Cluster mit zwei Knoten kontinuierlich verfügbaren Speicher für Anwendungen und virtuelle Maschinen bereitstellen, selbst wenn ein Serverknoten ausfällt und ein Laufwerk auf dem anderen Serverknoten ausfällt.

- **Zwei-Server-Clustern mithilfe eines USB-Speicherstick als Zeuge**

    Verwenden Sie eine kostengünstige USB-Laufwerk mit dem Router verbunden, die als Zeuge in Clustern mit zwei-Server fungiert. Wenn ein Server ausfällt, und klicken Sie dann wieder der USB-Laufwerk-Cluster weiß, welcher Server die neuesten Daten verfügt. Weitere Informationen finden Sie in der [Storage auf der Microsoft-Blog](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/).

- **Windows Admin Center**

    Verwalten und überwachen Sie Storage Spaces Direct mit dem neuen [Dashboard](../manage/windows-admin-center/use/manage-hyper-converged.md), das speziell für Windows entwickelt wurde, und erleben Sie Windows Admin Center. Erstellen, öffnen, erweitern oder löschen Sie Volumes mit nur wenigen Klicks. Überwachen Sie die Leistung wie IOPS und IO-Latenz vom gesamten Cluster bis hinunter zur einzelnen SSD oder HDD. Ohne zusätzliche Kosten für Windows Server 2016 und Windows Server 2019 verfügbar.

- **Leistungsverlauf**

    Erhalten Sie einen mühelosen Einblick in die Ressourcennutzung und -leistung mit [integriertem Verlauf](storage-spaces/performance-history.md). Über 50 wichtige Leistungsindikatoren, die Rechen-, Speicher-, Netzwerk- und Speicherfunktionen umfassen, werden automatisch für bis zu einem Jahr im Cluster gesammelt und gespeichert. Das Beste ist, dass es nichts zu installieren, zu konfigurieren oder zu starten gibt - es funktioniert einfach. Visualisieren Sie in Windows Admin Center oder führen Sie Abfragen oder Verarbeitungen in PowerShell durch

- **Skalieren Sie bis zu 4 PB pro Cluster**

    Erzielen Sie eine Multi-Petabyte-Skalierung - ideal für Medien-, Backup- und Archivierungsfälle. In Windows Server 2019 unterstützt Storage Spaces Direct bis zu 4 Petabyte (PB) = 4.000 Terabyte Rohkapazität pro Speicherpool. Die zugehörigen Kapazitätsrichtlinien werden ebenfalls erhöht: Sie können beispielsweise doppelt so viele Volumes (64 statt 32) erstellen, jeweils doppelt so groß wie zuvor (64 TB statt 32 TB). Zusammenfügen von mehreren Clustern zusammen in einem [Clustern](storage-spaces/cluster-sets.md) für noch höhere Skalierung innerhalb einer Speicherkonto-Namespace. Weitere Informationen finden Sie in der [Storage auf der Microsoft-Blog](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/).

- **Mirror-beschleunigte Parität ist 2 X schneller**

    Mit einer Spiegel-beschleunigten Parität können Sie Storage Spaces Direct-Volumes erstellen, die teilweise Spiegel- und Teileparität sind, wie das Mischen von RAID-1 und RAID-5/6, um das Beste aus beiden zu erhalten. (sie hat [einfacher als Sie denken](https://www.youtube.com/watch?v=R72QHudqWpE) in Windows Admin Center.) In Windows Server-2019 wird die Leistung der Spiegel beschleunigte Parität relativ zum Windows Server 2016 Dank Optimierungen mehr als verdoppelt.

- **Steuern der Wartezeit ausreißererkennung**

    Identifizieren Sie Laufwerke mit abnormaler Latenzzeit mit proaktiver Überwachung und integrierter Ausreißererkennung, die von dem langjährigen und erfolgreichen Ansatz von Microsoft Azure inspiriert wurden. Egal, ob es sich um eine durchschnittliche Latenz oder um eine etwas subtilere 99.-Perzentil-Latenz handelt, langsame Laufwerke werden automatisch in PowerShell und Windows Admin Center mit dem Status "Abnormale Latenz" gekennzeichnet.

- **Trennen Sie manuell die Zuordnung von Volumes, um die Fehlertoleranz zu erhöhen.**

    Dadurch können Administratoren die Zuordnung von Volumes in direkte Speicherplätze manuell zu trennen. Dies erzwingt damit deutlich Fehlertoleranz unter bestimmten Bedingungen erhöhen kann jedoch einige zusätzliche Überlegungen zur und Komplexität. Weitere Informationen finden Sie unter [trennen Sie die Zuordnung von Volumes](storage-spaces/delimit-volume-allocation.md).

### <a name="storage-replica2019"></a>Funktion "Speicherreplikat"

Es gibt eine Reihe von Verbesserungen an [Funktion "Speicherreplikat"](storage-replica/storage-replica-overview.md) in dieser Version:

#### <a name="storage-replica-in-windows-server-standard-edition"></a>Funktion "Speicherreplikat" in WindowsServer Standard Edition

Sie können die Funktion "Speicherreplikat" jetzt mit Windows Server Standard Edition, zusätzlich zur Datacenter Edition verwenden. Funktion "Speicherreplikat" auf Windows Server Standard Edition gelten die folgenden Einschränkungen:

- Das Speicherreplikat repliziert ein einzelnes Volume, anstatt eine unbegrenzte Anzahl von Volumes.
- Volumes können eine Größe von bis zu 2 TB, anstatt eine unbegrenzte Größe aufweisen.

#### <a name="storage-replica-log-performance-improvements"></a>Verbesserungen der Protokollierungsleistung für Speicherreplikate

Wir auch Verbesserungen vorgenommen, wie das Protokoll der Funktion "Speicherreplikat" nachverfolgt, Replikation, Verbessern der Replikationsdurchsatz und Latenz, vor allem auf All-Flash-Speicher als auch für "direkte Speicherplätze"-Cluster, die untereinander replizieren.

Um die höhere Leistung zu erhalten, müssen alle Mitglieder der Replikationsgruppe 2019 für Windows Server ausführen.

#### <a name="test-failover"></a>Testen des Failovers

Sie können jetzt vorübergehend eine Momentaufnahme von den replizierten Speicher auf einem Zielserver zu Testzwecken bereitstellen oder Sichern Zwecke. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](https://aka.ms/srfaq).

#### <a name="windows-admin-center-support"></a>Support für Windows Admin Center

Unterstützung für die grafische Verwaltung der Replikation ist jetzt verfügbar in Windows Admin Center über das Server-Manager-Tool. Dies umfasst die Replikation von Server-zu-Server, Cluster-zu-Cluster als auch Stretched Cluster-Replikation.

#### <a name="miscellaneous-improvements"></a>Verschiedene Verbesserungen

Funktion "Speicherreplikat" enthält außerdem die folgenden Verbesserungen:

-   Ändert, die asynchrone Stretched Cluster-Verhalten, damit ein automatisches Failover auftreten, jetzt
-   Mehrere Fehlerkorrekturen

### <a name="smb"></a>SMB

- **Widerruf SMB1 und Gast**: Windows Server wird die SMB1-Client und Server nicht mehr standardmäßig installiert. Darüber hinaus ist die Möglichkeit deaktiviert, sich als Gast in SMB2 und höher standardmäßig zu authentifizieren. Weitere Informationen finden Sie unter [SMBv1 wird nicht standardmäßig in Windows 10, Version 1709 und Windows Server, Version 1709, installiert](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server). 

- **SMB2/SMB3-Sicherheit und Kompatibilität**: Zusätzliche Optionen für die Sicherheit und Anwendungskompatibilität wurden hinzugefügt, einschließlich der Möglichkeit zum Deaktivieren von Oplocks in SMB2 für ältere Anwendungen als auch erfordern, Signierung oder Verschlüsselung für pro-Verbindung von einem Client. Weitere Informationen finden Sie in der SMBShare PowerShell-Modul-Hilfe.

### <a name="data-deduplication"></a>Datendeduplizierung

- **Jetzt für die Datendeduplizierung unterstützt ReFS**: Nicht mehr zur Auswahl stehen die Vorteile eines modernen Dateisystems mit ReFS und die Datendeduplizierung: Sie können nun die Datendeduplizierung aktivieren, wenn Sie Verweise aktivieren können. Erhöhen Sie die Speichereffizienz von schätzungsweise mehr als 95 % mit ReFS.
- **Datenport-API für die optimierte Eingang/Ausgang auf deduplizierten Volumes**: Entwickler können jetzt das Wissen nutzen die Datendeduplizierung verfügt über das Speichern von Daten effizient zum Verschieben von Daten zwischen Volumes, Servern und effizient-Cluster.

### <a name="file-server-resource-manager"></a>Ressourcen-Manager für Dateiserver

Windows Server-2019 bietet die Möglichkeit, die verhindern, dass des File Server Resource Manager-Diensts erstellen ein Änderungsjournal (auch bekannt als eine USN-Journal) für alle Volumes, beim Starten des Diensts. Dies kann Speicherplatz auf jedem Datenträger sparen, deaktiviert allerdings in Echtzeit die Dateiklassifizierung. Weitere Informationen finden Sie unter [Übersicht über den Ressourcen-Manager für Dateiserver](fsrm/fsrm-overview.md).

## <a name="whats-new-in-storage-in-windows-server-version-1803"></a>Neuerungen beim Speicher in Windows Server, Version 1803

### <a name="file-server-resource-manager"></a>Ressourcen-Manager für Dateiserver

Windows Server enthält Version 1803 die Möglichkeit, um zu verhindern, dass den File Server Resource Manager-Dienst erstellen ein Änderungsjournal (auch bekannt als eine USN-Journal) für alle Volumes, beim Starten des Diensts. Dies kann Speicherplatz auf jedem Datenträger sparen, deaktiviert allerdings in Echtzeit die Dateiklassifizierung. Weitere Informationen finden Sie unter [Übersicht über den Ressourcen-Manager für Dateiserver](fsrm/fsrm-overview.md).

## <a name="whats-new-in-storage-in-windows-server-version-1709"></a>Neuerungen beim Speicher in Windows Server, Version 1709

Windows Server-Version 1709 ist die erste Version von Windows Server im halbjährlichen Kanal. Den halbjährlichen Kanal ist ein Software Assurance-Vorteil und wird in der Produktion 18 Monaten, sechs Monate über eine neue Version vollständig unterstützt.

Weitere Informationen finden Sie unter [Übersicht: Windows Server, Semi-Annual Channel](../get-started/semi-annual-channel-overview.md).

### <a name="storage-replica"></a>Speicherreplikat

Der Schutz für die notfallwiederherstellung von der Funktion "Speicherreplikat" hinzugefügt wurde erweitert, gehören:

- **Testen des Failovers**: die Option zum Bereitstellen des Ziel-Speichers ist jetzt mit der Funktion zum Testen des Failovers möglich. Sie können einen Snapshot des replizierten Speichers auf Zielknoten vorübergehend zu Test- und Sicherungszwecken bereitstellen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](https://aka.ms/srfaq).
- **Unterstützung für Windows Admin Center**: Unterstützung für die grafische Verwaltung der Replikation ist jetzt verfügbar in Windows Admin Center über das Server-Manager-Tool. Dies umfasst die Replikation von Server-zu-Server, Cluster-zu-Cluster als auch Stretched Cluster-Replikation.

Funktion "Speicherreplikat" enthält außerdem die folgenden Verbesserungen:

-   Ändert, die asynchrone Stretched Cluster-Verhalten, damit ein automatisches Failover auftreten, jetzt
-   Mehrere Fehlerkorrekturen

### <a name="smb"></a>SMB

- **Widerruf SMB1 und Gast**: Windows Server, Version 1709 nicht mehr SMB1-Client und Server wird standardmäßig installiert. Darüber hinaus ist die Möglichkeit deaktiviert, sich als Gast in SMB2 und höher standardmäßig zu authentifizieren. Weitere Informationen finden Sie unter [SMBv1 wird nicht standardmäßig in Windows 10, Version 1709 und Windows Server, Version 1709, installiert](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server). 

- **SMB2/SMB3-Sicherheit und Kompatibilität**: Zusätzliche Optionen für die Sicherheit und Anwendungskompatibilität wurden hinzugefügt, einschließlich der Möglichkeit zum Deaktivieren von Oplocks in SMB2 für ältere Anwendungen als auch erfordern, Signierung oder Verschlüsselung für pro-Verbindung von einem Client. Weitere Informationen finden Sie in der SMBShare PowerShell-Modul-Hilfe.

### <a name="data-deduplication"></a>Datendeduplizierung

- **Jetzt für die Datendeduplizierung unterstützt ReFS**: Nicht mehr zur Auswahl stehen die Vorteile eines modernen Dateisystems mit ReFS und die Datendeduplizierung: Sie können nun die Datendeduplizierung aktivieren, wenn Sie Verweise aktivieren können. Erhöhen Sie die Speichereffizienz von schätzungsweise mehr als 95 % mit ReFS.
- **Datenport-API für die optimierte Eingang/Ausgang auf deduplizierten Volumes**: Entwickler können jetzt das Wissen nutzen die Datendeduplizierung verfügt über das Speichern von Daten effizient zum Verschieben von Daten zwischen Volumes, Servern und effizient-Cluster.

## <a name="whats-new-in-storage-in-windows-server-2016"></a>Neuerungen beim Speicher in Windows Server 2016

### <a name="s2d"></a>"Direkte Speicherplätze"  
Mit direkten Speicherplätzen kann hoch verfügbarer und skalierbarer Speicher unter Verwendung von Servern mit lokalem Speicher erstellt werden. Mit diesem Feature wird die Bereitstellung und die Verwaltung von softwaredefinierten Speichersystemen vereinfacht und auch der Weg zur Nutzung neuer Datenträgerklassen wie z. B. SATA-SSD und NVMe geebnet, was vorher bei gruppierten Speicherplätzen mit freigegebenen Datenträgern nicht möglich war.  

**Welchen Nutzen bietet diese Änderung?**  
Mit direkten Speicherplätzen können Dienstanbieter und Unternehmen Server nach Industriestandard mit lokalem Speicher einsetzen, um hoch verfügbare und skalierbare softwaredefinierte Speichersysteme zu erstellen. Die Verwendung von Servern mit lokalem Speicher führt zu weniger Komplexität, höherer Skalierbarkeit und der Möglichkeit, Speichergeräte zu nutzen, die zuvor nicht verwendet werden konnten (z. B. SATA-SSDs zum Senken der Kosten von Flash-Speicher oder NVMe-SSDs für eine höhere Leistung).  

Bei Verwendung von direkten Speicherplätzen wird kein gemeinsames SAS-Fabric benötigt, sodass die Bereitstellung und die Konfiguration vereinfacht werden. Stattdessen wird das Netzwerk als Speicherfabric genutzt. Dabei kommen SMB3 und SMB Direct (RDMA) zum Einsatz, um Speicher mit hoher Geschwindigkeit, geringer Latenz und hoher CPU-Effizienz bereitzustellen. Für eine horizontale Hochskalierung fügen Sie ganz einfach weitere Server hinzu, um die Speicherkapazität und die E/A-Leistung zu steigern.  
Weitere Informationen finden Sie unter [Direkte Speicherplätze in Windows Server 2016](storage-spaces/storage-spaces-direct-overview.md).  

**Worin bestehen die Unterschiede?**  
Dies ist eine neue Funktion in Windows Server 2016.  

### <a name="storage-replica"></a>Funktion "Speicherreplikat"

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

### <a name="storage-qos"></a>Quality of Service für Speicher  
Sie können Quality of Service (QoS) für Speicher jetzt nutzen, um die End-to-End-Speicherleistung zu überwachen und Verwaltungsrichtlinien unter Verwendung von Hyper-V- und CSV-Clustern in Windows Server 2016 zu erstellen.  

**Welchen Nutzen bietet diese Änderung?**  
Sie können nun Speicher-QoS-Richtlinien auf einem CSV-Cluster erstellen und diese einem oder mehreren virtuellen Datenträgern auf virtuellen Hyper-V-Computern zuweisen. Bei Änderungen des Workloads und der Speicherlast wird die Speicherleistung automatisch neu angepasst, um die Richtlinien einzuhalten.  

* In jeder Richtlinie kann ein Reservewert (Minimum) und/oder ein Grenzwert (Maximum) festgelegt werden, der auf eine Sammlung von Datenflüssen angewendet wird (z. B. auf eine virtuelle Festplatte, auf einen einzelnen virtuellen Computer oder eine Gruppe virtueller Computer, auf einen Dienst oder auf einen Mandanten).  
* Über Windows PowerShell oder WMI können die folgenden Aufgaben ausgeführt werden:  
    * Erstellen von Richtlinien auf einem CSV-Cluster
    * Auflisten von Richtlinien auf einem CSV-Cluster
    * Zuweisen einer Richtlinie zu einer virtuellen Festplatte eines virtuellen Hyper-V-Computers 
    * Überwachen der Leistung der einzelnen Flüsse und Status innerhalb der Richtlinie  
* Wenn mehrere virtuelle Festplatten dieselbe Richtlinie verwenden, wird die Leistung gleichmäßig verteilt, um die Mindest- und Höchstwerte der Richtlinien einzuhalten. Daher kann eine Richtlinie zum Verwalten einer virtuellen Festplatte, eines virtuellen Computers, mehrerer virtueller Computer, die einen Dienst umfassen, oder aller virtuellen Computer, die zu einem Mandanten gehören, genutzt werden.  

**Worin bestehen die Unterschiede?**  
Dies ist eine neue Funktion in Windows Server 2016. Das Verwalten von Mindestreserven, das Überwachung von Flüssen aller virtuellen Festplatten im Cluster über einen einzigen Befehl und die zentralisierte, richtlinienbasierte Verwaltung waren in früheren Versionen von Windows Server nicht möglich.  

Weitere Informationen finden Sie unter [Storage Quality of Service](storage-qos/storage-qos-overview.md) (Speicher-QoS).

### <a name="dedup"></a>Die Datendeduplizierung  
| Funktionalität | Neu oder aktualisiert | Beschreibung |
|---------------|----------------|-------------|
| [Unterstützung für große Volumes](data-deduplication/whats-new.md#large-volume-support) | Aktualisiert | Vor Windows Server 2016 musste die Größe der Volumes speziell für die erwartete Änderung konfiguriert werden, wobei Volumes mit über 10 TB keine geeigneten Kandidaten für die Deduplizierung waren. In Windows Server 2016 unterstützt die Datendeduplizierung Volumegrößen von **bis zu 64 TB**. |
| [Unterstützung für große Dateien](data-deduplication/whats-new.md#large-file-support) | Aktualisiert | Vor Windows Server 2016 waren Dateien mit einer Größe von knapp 1 TB keine geeigneten Kandidaten für die Deduplizierung. In Windows Server 2016 werden Dateien mit einer Größe von **bis zu 1 TB** vollständig unterstützt. |
| [Unterstützung für Nano Server](data-deduplication/whats-new.md#nano-server-support) | Neu | Die Datendeduplizierung ist in der neuen Nano Server-Bereitstellungsoption für Windows Server 2016 verfügbar und wird von dieser Option vollständig unterstützt. |
| [Vereinfachte Unterstützung von Sicherungen](data-deduplication/whats-new.md#simple-backup-support) | Neu | In Windows Server 2012 R2 mussten eine Reihe manueller Konfigurationsschritte ausgeführt werden, um virtualisierte Sicherungsanwendungen wie Microsoft [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx) zu unterstützten. In Windows Server 2016 wurde ein neuer Standardverwendungstyp „Sicherung“ hinzugefügt, um eine nahtlose Bereitstellung der Datendeduplizierung für virtualisierte Sicherungsanwendungen zu ermöglichen. |
| [Unterstützung für parallele Upgrades des Clusterbetriebssystems](data-deduplication/whats-new.md#cluster-upgrade-support) | Neu | Die Datendeduplizierung bietet vollständige Unterstützung für das neue Feature für [parallele Upgrades des Clusterbetriebssystems](..//failover-clustering/cluster-operating-system-rolling-upgrade.md) von Windows Server 2016. |

### <a name="smb-hardening-improvements"></a>Verbesserungen für SYSVOL- und NETLOGON-Verbindungen zu Härten von SMB  
In Windows 10 und Windows Server 2016 ist für Clientverbindungen mit den SYSVOL- und NETLOGON-Standardfreigaben von Active Directory Domain Services jetzt die SMB-Signierung und gegenseitige Authentifizierung (z. B. Kerberos) erforderlich.   

**Welchen Nutzen bietet diese Änderung?**  
Durch diese Änderung wird die Wahrscheinlichkeit von Man-in-the-Middle-Angriffen verringert.   

**Worin bestehen die Unterschiede?**  
Wenn die SMB-Signierung und die gegenseitige Authentifizierung nicht verfügbar sind, kann ein Computer mit Windows 10 oder Windows Server 2016 keine domänenbasierten Gruppenrichtlinien und Skripts verarbeiten.  

> [!NOTE]  
> Die Registrierungswerte für diese Einstellungen sind standardmäßig nicht verfügbar, die Härtungsregeln gelten jedoch trotzdem, bis sie von Gruppenrichtlinien oder anderen Registrierungswerten außer Kraft gesetzt werden.  

Weitere Informationen zu diesen Verbesserungen – auch bezeichnet als UNC-Härtung Microsoft Knowledge Base-Artikel finden Sie unter [3000483](https://support.microsoft.com/kb/3000483) und [MS15-011 & MS15-014: Härten von Gruppenrichtlinien](https://blogs.technet.microsoft.com/srd/2015/02/10/ms15-011-ms15-014-hardening-group-policy).  

### <a name="work-folders"></a>Arbeitsordner
Verbesserte änderungsbenachrichtigung, wenn die Arbeitsordner-Server, Windows Server 2016 sowie die Arbeitsordner-Clients ausgeführt wird ist Windows 10.

**Welchen Nutzen bietet diese Änderung?**<br>
Werden unter Windows Server 2012 R2 Dateiänderungen auf die Arbeitsordner-Server synchronisiert, werden die Clients nicht über die Änderung benachrichtigt, und es dauert bis zu 10 Minuten, bis die Aktualisierungen verfügbar sind.  Verwendung von Windows Server 2016 benachrichtigt der Arbeitsordner-Server sofort Windows 10-Clients, und die dateiänderungen werden sofort synchronisiert.

**Worin bestehen die Unterschiede?**<br>
Dies ist eine neue Funktion in Windows Server 2016. Dies erfordert einen Arbeitsordner-Server mit Windows Server 2016 und einen Client mit Windows 10.

Wenn Sie einen älteren Client verwenden oder wenn auf dem Arbeitsordnerserver Windows Server 2012 R2 ausgeführt wird, sucht der Client weiterhin alle zehn Minuten nach Änderungen.

### <a name="refs"></a>ReFS 
Die nächste Iteration von ReFS unterstützt umfangreiche Speicherbereitstellungen mit unterschiedlichen Workloads und bietet Zuverlässigkeit, Resilienz und Skalierbarkeit für Ihre Daten.     

**Welchen Nutzen bietet diese Änderung?**<br>
ReFS sorgt für folgende Verbesserungen:

* ReFS implementiert neue Funktionen für Speicherebenen, die eine höhere Leistung und Speicherkapazität ermöglichen. Diese neuen Funktionen ermöglichen Folgendes:
    * Mehrere Resilienztypen für den gleichen virtuellen Datenträger (beispielsweise mit Spiegelung auf der Leistungsebene und Parität auf der Kapazitätsebene).
    * Schnellere Reaktion auf driftende Workingsets.  
* Die Einführung von Block Cloning hat eine erhebliche Verbesserung der Leistung von VM-Vorgängen zur Folge, was sich beispielsweise bei der Zusammenführung von VHDX-Prüfpunkten bemerkbar macht.
* Das neue ReFS-Überprüfungsprogramm ermöglicht die Behandlung von Speicherverlusten und schützt Daten vor kritischen Beschädigungen. 

**Worin bestehen die Unterschiede?**<br>
Diese Funktionen sind neu in Windows Server 2016. 

## <a name="see-also"></a>Siehe auch  
* [Neuerungen in Windows Server 2016](../get-started/what-s-new-in-windows-server-2016.md)  
