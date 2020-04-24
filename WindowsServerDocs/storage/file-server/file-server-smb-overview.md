---
title: Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server
description: Eine Übersicht über die Verwendung des SMB 3-Protokolls für Dateifreigaben und Fileserving mit Windows Server.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: aafcfcd4d0f2f14836c5b7dee2bdbccbf99fa887
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "78169620"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird das SMB 3-Feature in Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 beschrieben. Die Beschreibung umfasst praktische Anwendungsmöglichkeiten des Features, die wichtigsten neuen oder aktualisierten Funktionen in dieser Version im Vergleich zu früheren Versionen und die Hardwareanforderungen. SMB ist auch ein Fabricprotokoll, das von [SDDC-Lösungen (Software-Defined Data Center)](../../sddc.md) Lösungen wie Direkte Speicherplätze, Speicherreplikat und anderen verwendet wird. Die SMB-Version 3.0 wurde mit Windows Server 2012 eingeführt und in nachfolgenden Versionen inkrementell verbessert.

## <a name="feature-description"></a>Featurebeschreibung

Das Server Message Block-Protokoll (SMB-Protokoll) dient der Freigabe von Netzwerkdateien und ermöglicht es Anwendungen auf einem Computer, Dateien zu lesen und in Dateien zu schreiben sowie Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. SMB kann zudem mit jedem beliebigen Serverprogramm kommunizieren, das für den Empfang einer SMB-Clientanforderung eingerichtet ist. SMB ist ein Fabricprotokoll, das von SDDC-Computingtechnologien (Software-Defined Data Center) wie Direkte Speicherplätze oder Speicherreplikat verwendet wird. Weitere Informationen finden Sie unter [Windows Server-SDDC (Software-Defined Data Center)](../../sddc.md).

## <a name="practical-applications"></a>Praktische Anwendung

In diesem Abschnitt werden ein paar praktische Anwendungen des neuen SMB 3.0-Protokolls vorgestellt.

* **Dateispeicher zur Virtualisierung (Hyper-V™ über SMB)** . Hyper-V kann Dateien virtueller Computer über das SMB 3.0-Protokoll in Dateifreigaben speichern. Zu diesen Dateien gehören Konfigurationsdateien, VHD-Dateien (Virtual Hard Disk, virtuelle Festplatte) und Momentaufnahmen. Dies kann sowohl für eigenständige Dateiserver als auch Clusterdateiserver, die Hyper-V zusammen mit Dateifreigabespeicher für den Cluster verwenden, genutzt werden.
* **Microsoft SQL Server über SMB**. SQL Server kann Benutzerdatenbankdateien auf SMB-Dateifreigaben speichern. Aktuell wird dies von SQL Server 2008 R2 für eigenständige SQL-Server unterstützt. Zukünftige Versionen von SQL Server werden auch die Unterstützung von gruppierten SQL-Servern und Systemdateibanken beinhalten.
* **Herkömmlicher Speicher für Endbenutzerdaten**. Das SMB 3.0-Protokoll bietet Verbesserungen für Information-Worker-Arbeitsauslastungen (oder Clientarbeitsauslastungen). Zu diesen Verbesserungen zählt die Reduzierung der Anwendungslatenz für Benutzer in Filialen, wenn diese Benutzer über ein WAN (Wide Area Network, WAN) auf Daten zugreifen, und der Schutz von Daten vor Lauschangriffen.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In den folgenden Abschnitten werden die Funktionen beschrieben, die in SMB 3 und nachfolgenden Updates hinzugefügt wurden.

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>In Windows Server 2019 und Windows 10, Version 1809 hinzugefügte Funktionen

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Möglichkeit zum Ausführen eines Schreibzugriffs auf einen Datenträger für Dateifreigaben, die nicht fortlaufend verfügbar sind | „Neu“, | Um zusätzliche Sicherheit zu gewährleisten, dass der Schreibvorgang in eine Dateifreigabe den gesamten Software- und Hardwarestapel bis zum physischen Datenträger durchläuft, bevor der Schreibvorgang als abgeschlossen zurückgegeben wird, kannst du das Durchschreiben auf die Dateifreigabe entweder mit dem Befehl `NET USE /WRITETHROUGH` oder mit dem PowerShell-Cmdlet `New-SMBMapping -UseWriteThrough` aktivieren. Es gibt eine gewisse Leistungssteigerung bei der Verwendung von Durchschreiben. Weitere Erläuterungen finden Sie im Blogbeitrag [Steuern des Durchschreibverhaltens in SMB](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677). |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>In Windows Server, Version 1709 und Windows 10, Version 1709 hinzugefügte Funktionen

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Gastzugriff auf Dateifreigaben ist deaktiviert. | „Neu“, | Der SMB-Client lässt die folgenden Aktionen nicht mehr zu: Gastkontozugriff auf einen Remoteserver, Fallback auf das Gastkonto, nachdem ungültige Anmeldeinformationen bereitgestellt wurden. Weitere Informationen finden Sie unter [Gastzugriff in SMB2 in Windows standardmäßig deaktiviert](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser). | 
| Globale SMB-Zuordnung | „Neu“, | Ordnet eine SMB-Remotefreigabe einem Laufwerkbuchstaben zu, der für alle Benutzer auf dem lokalen Host (einschließlich Container) zugänglich ist. Dies ist erforderlich, damit Container-E/A auf dem Datenvolume den Remotebereitstellungspunkt durchlaufen kann. Denken Sie daran, dass alle Benutzer auf dem Containerhost auf die Remotefreigabe zugreifen können, wenn globale Zuordnung in SMB für Container verwendet wird. Jede auf dem Containerhost ausgeführte Anwendung besitzt außerdem Zugriff auf die zugeordnete Remotefreigabe. Weitere Informationen finden Sie unter [Container Storage Support with Cluster Shared Volumes (CSV), Storage Spaces Direct, SMB Global Mapping](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140). |
| SMB-Dialektsteuerung | „Neu“, | Sie können jetzt Registrierungswerte festlegen, um die minimale SMB-Version (Dialekt) und die maximale verwendete SMB-Version zu steuern. Weitere Informationen finden Sie unter [Steuern von SMB-Dialekten](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024). |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>In SMB 3.11 mit Windows Server 2016 und Windows 10, Version 1607 hinzugefügte Funktionen

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| SMB-Verschlüsselung     |   Aktualisiert      | Die SMB 3.1.1-Verschlüsselung mit AES-GCM (Advanced Encryption Standard-Galois/Counter Mode) ist schneller als SMB-Signaturen oder eine frühere SMB-Verschlüsselung mit AES-CCM.   |
| Verzeichniszwischenspeicherung | „Neu“, | SMB 3.1.1 umfasst Verbesserungen bei der Verzeichniszwischenspeicherung. Windows-Clients können nun erheblich größere Verzeichnisse zwischenspeichern (ungefähr 500.000 Einträge). Windows-Clients versuchen, Verzeichnisabfragen mit 1-MB-Puffern durchzuführen, um Roundtrips zu reduzieren und die Leistung zu steigern. |
| Integrität der Vorauthentifizierung | „Neu“, |  In SMB 3.1.1 bietet die Vorauthentifizierungsintegrität verbesserten Schutz vor einem Man-in-the-Middle-Angreifer, der die Verbindungseinrichtung und die Authentifizierungsnachrichten von SMB manipuliert. Weitere Informationen finden Sie unter [SMB 3.1.1-Vorauthentifizierungsintegrität in Windows 10](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10). |
| SMB-Verschlüsselungsverbesserungen | „Neu“, | SMB 3.1.1 bietet einen Mechanismus zum Aushandeln des Kryptografiealgorithmus pro Verbindung mit Optionen für AES-128-CCM und AES-128-GCM. AES-128-GCM ist die Standardeinstellung für neue Windows-Versionen, während ältere Versionen weiterhin AES-128-CCM verwenden. |
| Unterstützung für paralleles Clusterupgrade | „Neu“, | Ermöglicht [parallele Clusterupgrades](../../failover-clustering/cluster-operating-system-rolling-upgrade.md), indem SMB bei der Aktualisierung verschiedene maximale Versionen von SMB für Cluster zu unterstützen scheint. Weitere Informationen zum Zulassen der Kommunikation zwischen SMB und verschiedenen Versionen (Dialekten) des Protokolls finden Sie im Blogbeitrag [Steuern von SMB-Dialekten](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024). |
| Unterstützung von SMB Direct-Clients in Windows 10 | „Neu“, | Windows 10 Enterprise, Windows 10 Education und Windows 10 Pro for Workstations enthalten jetzt Unterstützung für SMB Direct-Clients. |
| Native Unterstützung für FileNormalizedNameInformation-API-Aufrufe | „Neu“, | Fügt native Unterstützung für das Abfragen des normalisierten Namens einer Datei hinzu. Weitere Informationen finden Sie unter [FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6). |

Weitere Einzelheiten finden Sie im Blogbeitrag [Neuerungen in SMB 3.1.1 in Windows Server 2016 Technical Preview 2](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2).

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>In SMB 3.02 mit Windows Server 2012 R2 und Windows 8.1 hinzugefügte Funktionen

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Automatischer Neuausgleich der Clients für Dateiserver mit horizontaler Skalierung     |   „Neu“,      | Verbessert die Skalierbarkeit und Verwaltbarkeit für Dateiserver mit horizontaler Skalierung. SMB-Clientverbindungen werden nach Dateifreigabe (und nicht nach Server) nachverfolgt. Clients werden dann an den Clusterknoten mit dem besten Zugriff auf das von der Dateifreigabe verwendete Volume umgeleitet. Dadurch wird die Effizienz gesteigert, da der Umleitungsdatenverkehr zwischen Dateiserverknoten verringert wird. Clients werden nach der Anfangsverbindung und bei einer Neukonfiguration des Clusterspeichers umgeleitet.    |
| Leistung über WAN   | Aktualisiert  | Windows 8.1 und Windows 10 bieten verbesserte Unterstützung für CopyFile-SRV_COPYCHUNK über SMB, wenn Sie den Datei-Explorer für Remotekopien von einem Speicherort auf einem Remotecomputer in eine andere Kopie auf demselben Server verwenden. Sie kopieren nur eine kleine Menge von Metadaten über das Netzwerk (1/2KiB pro 16MiB Dateidaten werden übertragen). Dies führt zu einer deutlichen Leistungsverbesserung. Dies ist eine Unterscheidung auf Betriebssystemebene und Datei-Explorer-Ebene für SMB. |
| SMB Direct     |   Aktualisiert      | Verbessert die Leistung für kleine E/A-Arbeitsauslastungen, indem die Effizienz beim Hosten von Arbeitsauslastungen mit kleinen E/As (z. B. eine Datenbank für die Onlinetransaktionsverarbeitung (Online Transaction Processing, OLTP) auf einem virtuellen Computer) gesteigert wird. Diese Verbesserungen sind bei der Verwendung von Netzwerkschnittstellen mit höherer Geschwindigkeit wie Ethernet mit 40 GBit/s und InfiniBand mit 56 GBit/s offensichtlich.  |
| SMB-Bandbreiteneinschränkungen | „Neu“, | Sie können nun [Set-SmbBandwidthLimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit) verwenden, um Bandbreiteneinschränkungen in drei Kategorien festzulegen: VirtualMachine (Hyper-V über SMB-Datenverkehr), LiveMigration (Hyper-V-LiveMigration-Datenverkehr über SMB) oder Standard (alle anderen Typen von SMB-Datenverkehr).

Weitere Informationen zu neuen und geänderten SMB-Funktionen in Windows Server 2012 R2 finden Sie unter [Neuerungen in SMB in Windows Server](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>).

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>In SMB 3.0 mit Windows Server 2012 und Windows 8 hinzugefügte Funktionen

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| SMB Transparent Failover     |   „Neu“,    | Ermöglicht es Administratoren, Hardware- oder Softwarewartungen von Knoten in einem Clusterdateiserver durchzuführen, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern. Wenn ein Hardware- oder Softwarefehler in einem Clusterknoten auftritt, stellen die SMB-Clients zudem die Verbindung zu einem anderen Clusterknoten transparent her, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern.        |
| SMB Scale Out     |   „Neu“,      | Unterstützung für mehrere SMB-Instanzen auf einem Dateiserver mit horizontaler Skalierung. Durch die Verwendung freigegebener Clustervolumes der Version 2 (Cluster Shared Volumes, CSV) können Administratoren Dateifreigaben erstellen, die gleichzeitigen Zugriff auf Datendateien bieten, mit direkter E/A und über alle Knoten in einem Dateiservercluster. Dadurch wird die Ausnutzung der Netzwerkbandbreite verbessert und ein besserer Lastausgleich auf den Dateiserverclients erreicht sowie die Leistung für Serveranwendungen optimiert.  |
| SMB Multichannel     |   „Neu“,      |  Ermöglicht die Aggregation von Netzwerkbandbreite und Netzwerkfehlertoleranz, wenn mehrere Pfade zwischen dem SMB-Client und dem -Server verfügbar sind. Auf diese Weise können Serveranwendungen die verfügbare Netzwerkbandbreite voll ausnutzen und sind unempfindlich für Netzwerkausfälle.<br><br>SMB Multichannel in SMB 3 trägt zu einer deutlichen Leistungssteigerung im Vergleich zu früheren Versionen von SMB bei. |
| SMB Direct     |   „Neu“,      | Unterstützt die Verwendung von Netzwerkadaptern mit RDMA-Fähigkeit und kann bei maximaler Geschwindigkeit mit sehr niedriger Latenz arbeiten, und das bei sehr geringer CPU-Nutzung. Für Arbeitsauslastungen wie Hyper-V oder Microsoft SQL Server bedeutet dies, dass ein Remotedateiserver einem lokalen Speicher gleichkommt.<br><br>SMB Direct in SMB 3 trägt zu einer deutlichen Leistungssteigerung im Vergleich zu früheren Versionen von SMB bei.  |
| Leistungsindikatoren für Serveranwendungen     |   „Neu“,      |  Die neuen SMB-Leistungsindikatoren liefern ausführliche, nach Freigabe unterteilte Daten zum Durchsatz, zur Latenz und zu E/A pro Sekunde (IOPS) und ermöglichen es Administratoren, die Leistung von SMB-Dateifreigaben zu analysieren, in denen ihre Daten gespeichert sind. Diese Indikatoren sind speziell für Serveranwendungen wie Hyper-V und SQL Server konzipiert, die Dateien in Remotedateifreigaben speichern.      |
| Leistungsoptimierungen    |  Aktualisiert   | Sowohl der SMB-Client als auch der -Server sind für kleine zufällige Lese-/Schreibvorgänge optimiert worden, die bei Serveranwendungen wie SQL Server OLTP häufig vorkommen. Außerdem ist das Feature Maximum Transmission Unit (MTU) standardmäßig für große Pakete aktiviert, wodurch die Leistung bei großen sequenziellen Übertragungen, wie SQL Server Data Warehouse, Datenbanksicherung und -wiederherstellung oder dem Bereitstellen und Kopieren virtueller Festplatten, deutlich verbessert wird. |
| SMB-spezifische Windows PowerShell-Cmdlets     |   „Neu“,      |  Mit Windows PowerShell-Cmdlets für SMB kann ein Administrator Dateifreigaben auf dem Dateiserver End-to-End von der Befehlszeile aus verwalten.   |
| SMB-Verschlüsselung     |   „Neu“,      | Sorgt für End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor Lauschangriffen in nicht vertrauenswürdigen Netzwerken. Erfordert keine weiteren Bereitstellungskosten und keine Internet Protocol-Sicherheit (IPsec), spezielle Hardware oder WAN-Beschleuniger. Sie kann auf Freigabebasis oder für den gesamten Dateiserver konfiguriert und für eine Vielzahl von Szenarios aktiviert werden, bei denen Daten über nicht vertrauenswürdige Netzwerke übertragen werden. |
| SMB Directory Leasing     |  „Neu“, | Verbessert die Antwortzeiten von Anwendungen in Filialen. Durch die Verwendung von Verzeichnisleases werden Roundtrips vom Client zum Server reduziert, da Metadaten von einem Verzeichniscache mit längerer Lebensdauer abgerufen werden. Die Cachekohärenz bleibt erhalten, da Clients benachrichtigt werden, wenn sich Verzeichnisinformationen auf dem Server ändern. Verzeichnisleases funktionieren mit Szenarien für Basisordner (Lesen/Schreiben ohne Freigabe) und Veröffentlichung (schreibgeschützt mit Freigabe).    |
| Leistung über WAN   | „Neu“,   | Opportunistische Verzeichnissperren (Oplocks) und Oplockleases wurden in SMB 3.0 eingeführt. Bei typischen geschäftlichen bzw. Clientworkloads führen Oplocks/Leases dazu, dass Netzwerkroundtrips um ungefähr 15 % verringert werden.<br><br>In SMB 3 wurde die Windows-Implementierung von SMB optimiert, um das Zwischenspeicherungsverhalten auf dem Client zu verbessern, sowie die Möglichkeit zu bieten, höhere Durchsätze zu übermitteln.<br><br>SMB 3-Featuresverbesserungen an der CopyFile()-API sowie an zugeordneten Tools wie Robocopy, um erheblich mehr Daten über das Netzwerk zu übermitteln. |
| Sichere Dialektaushandlung | „Neu“, | Schützt vor Man-in-the-Middle-Versuchen, eine Herabstufung der Dialektaushandlung durchzuführen. Die Idee ist, zu verhindern, dass ein Lauscher den ursprünglich ausgehandelten Dialekt und die Fähigkeiten zwischen dem Client und dem Server herabstuft. Weitere Informationen finden Sie unter [Sichere SMB3-Dialektaushandlung](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation). Beachten Sie, dass dies durch das Feature [SMB 3.1.1-Vorauthentifizierungsitegrität in Windows 10](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10) in SMB 3.1.1 ersetzt wurde. |


## <a name="hardware-requirements"></a>Hardwareanforderungen

Für SMB Transparent Failover gelten die folgenden Anforderungen:

* Ein Failovercluster, auf dem Windows Server 2012 oder Windows Server 2016 mit mindestens zwei konfigurierten Knoten ausgeführt wird. Der Cluster muss die Clustervalidierungstests bestehen, die im Validierungs-Assistenten enthalten sind.
* Dateifreigaben müssen mit der Eigenschaft %%amp;quot;Fortlaufende Verfügbarkeit%%amp;quot; (Continuous Availability, CA) erstellt werden, die standardmäßig aktiviert ist.
* Dateifreigaben müssen unter CSV-Volumepfaden erstellt werden, um SMB Scale-Out zu nutzen.
* Auf Clientcomputern muss Windows® 8 oder Windows Server 2012 ausgeführt werden. Beide enthalten den aktualisierten SMB-Client, der fortlaufende Verfügbarkeit unterstützt.

> [!NOTE]
> Clients der unteren Ebenen können eine Verbindung mit Dateifreigaben herstellen, für die die CA-Eigenschaft festgelegt ist. Jedoch wird das transparente Failover für diese Clients nicht unterstützt.

Für SMB Multichannel gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Weitere Informationen zu empfohlenen Netzwerkkonfigurationen finden Sie im Abschnitt %%amp;quot;Siehe auch%%amp;quot; am Ende dieses Übersichtsthemas.

Für SMB Direct gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Netzwerkadapter mit RDMA-Fähigkeit sind erforderlich. Aktuell sind diese Adapter in drei unterschiedlichen Typen erhältlich: iWARP, Infiniband und RoCE (RDMA over Converged Ethernet).

## <a name="more-information"></a>Weitere Informationen

Die folgende Liste enthält weitere im Web verfügbare Ressourcen zu SMB und verwandten Technologien in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

* [Speicher](../storage.md)
* [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)
* [Optimieren der Leistung von Dateiservern mit SMB Direct](smb-direct.md)
* [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [Bereitstellen von SMB Multichannel](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [Bereitstellen schneller und effizienter Dateiserver für Serveranwendungen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: Leitfaden zur Problembehandlung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
