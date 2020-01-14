---
title: Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server
description: Eine Übersicht über die Verwendung des SMB 3-Protokolls für Dateifreigaben und Dateifreigaben mit Windows Server.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 416145a8c4ec20eaf46cf4b5ac88a0cdf38bdf33
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919886"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Übersicht über die Dateifreigabe mithilfe des SMB 3-Protokolls in Windows Server

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird das SMB 3-Feature in Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 beschrieben – praktische Verwendungsmöglichkeiten für das Feature, die wichtigste neue oder aktualisierte Funktionalität in dieser Version im Vergleich zu früheren Versionen und die Hardwareanforderungen. SMB ist auch ein Fabric-Protokoll, das von [Software-Defined Data Center (SDDC)](../../sddc.md) -Lösungen wie direkte Speicherplätze, Speicher Replikat und anderen verwendet wird. SMB-Version 3,0 wurde mit Windows Server 2012 eingeführt und wurde in nachfolgenden Versionen inkrementell verbessert.

## <a name="feature-description"></a>Featurebeschreibung

Das Server Message Block-Protokoll (SMB-Protokoll) dient der Freigabe von Netzwerkdateien und ermöglicht es Anwendungen auf einem Computer, Dateien zu lesen und in Dateien zu schreiben sowie Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. SMB kann auch mit jedem Serverprogramm kommunizieren, das für den Empfang einer SMB-Client Anforderung eingerichtet ist. SMB ist ein Fabric-Protokoll, das von Software-Defined Data Center (SDDC) Computing-Technologien wie direkte Speicherplätze und Speicher Replikat verwendet wird. Weitere Informationen finden Sie unter [Windows Server Software-Defined Datacenter](../../sddc.md).

## <a name="practical-applications"></a>Praktische Anwendungen

In diesem Abschnitt werden ein paar praktische Anwendungen des neuen SMB 3.0-Protokolls vorgestellt.

* **Dateispeicher zur Virtualisierung (Hyper-V™ über SMB)** . Hyper-V kann Dateien virtueller Computer über das SMB 3.0-Protokoll in Dateifreigaben speichern. Zu diesen Dateien gehören Konfigurationsdateien, VHD-Dateien (Virtual Hard Disk, virtuelle Festplatte) und Momentaufnahmen. Dies kann sowohl für eigenständige Dateiserver als auch Clusterdateiserver, die Hyper-V zusammen mit Dateifreigabespeicher für den Cluster verwenden, genutzt werden.
* **Microsoft SQL Server über SMB**. SQL Server kann Benutzerdatenbankdateien auf SMB-Dateifreigaben speichern. Aktuell wird dies von SQL Server 2008 R2 für eigenständige SQL-Server unterstützt. Zukünftige Versionen von SQL Server werden auch die Unterstützung von gruppierten SQL-Servern und Systemdateibanken beinhalten.
* **Herkömmlicher Speicher für Endbenutzerdaten**. Das SMB 3.0-Protokoll bietet Verbesserungen für Information-Worker-Arbeitsauslastungen (oder Clientarbeitsauslastungen). Zu diesen Verbesserungen zählt die Reduzierung der Anwendungslatenz für Benutzer in Filialen, wenn diese Benutzer über ein WAN (Wide Area Network, WAN) auf Daten zugreifen, und der Schutz von Daten vor Lauschangriffen.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In den folgenden Abschnitten werden die Funktionen beschrieben, die in SMB 3 und nachfolgenden Updates hinzugefügt wurden.

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>In Windows Server 2019 und Windows 10, Version 1809, hinzugefügte Features

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Möglichkeit zum Ausführen eines Schreibzugriffs auf einen Datenträger auf Dateifreigaben, die nicht fortlaufend verfügbar sind | „Neu“, | Zum Bereitstellen einer zusätzlichen Sicherheit, die von Schreibvorgängen in eine Dateifreigabe über den Software-und Hardware Stapel bis zum physischen Datenträger geführt wird, bevor der Schreibvorgang als abgeschlossen zurückgegeben wird, können Sie den Schreibzugriff für die Dateifreigabe aktivieren, indem Sie entweder den `NET USE /WRITETHROUGH` Befehl Ore das `New-SMBMapping -UseWriteThrough` PowerShell-Cmdlet verwenden. Es gibt eine gewisse Leistungssteigerung bei der Verwendung von Write-Through. Weitere Erläuterungen finden Sie im Blogbeitrag [Steuern von Schreibverhalten in SMB](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677) . |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>In Windows Server, Version 1709 und Windows 10, Version 1709, hinzugefügte Features

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Der Gast Zugriff auf Dateifreigaben ist deaktiviert. | „Neu“, | Der SMB-Client lässt die folgenden Aktionen nicht mehr zu: Gast Konto Zugriff auf einen Remote Server. Fallback auf das Gastkonto, nachdem ungültige Anmelde Informationen bereitgestellt wurden. Weitere Informationen finden Sie unter [Gast Zugriff in SMB2 standardmäßig deaktiviert in Windows](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser). | 
| Globale SMB-Zuordnung | „Neu“, | Ordnet eine SMB-Remote Freigabe einem Laufwerk Buchstaben zu, der für alle Benutzer auf dem lokalen Host, einschließlich Container, zugänglich ist. Dies ist erforderlich, damit die Container-e/a auf dem Daten Volume den Remote-Einstellungspunkt durchlaufen kann. Beachten Sie, dass bei Verwendung der globalen SMB-Zuordnung für Container alle Benutzer auf dem Container Host auf die Remote Freigabe zugreifen können. Jede Anwendung, die auf dem Container Host ausgeführt wird, hat auch Zugriff auf die zugeordnete Remote Freigabe. Weitere Informationen finden Sie [unter Unterstützung des Container Speichers mit freigegebenen Clustervolumes (CSV), direkte Speicherplätze, globale SMB-Zuordnung](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140). |
| SMB-Dialekt Steuerelement | „Neu“, | Sie können jetzt Registrierungs Werte festlegen, um die minimale SMB-Version (Dialekt) und die maximale verwendete SMB-Version zu steuern. Weitere Informationen finden Sie unter [Steuern von SMB-Dialekten](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024). |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>In SMB 3,11 hinzugefügte Features mit Windows Server 2016 und Windows 10, Version 1607

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| SMB-Verschlüsselung     |   Aktualisiert      | Die SMB-Verschlüsselung mit dem Advanced Encryption Standard-Galois/Counter Mode (AES-GCM) ist schneller als SMB-Signaturen oder eine frühere SMB-Verschlüsselung mit AES-CCM.   |
| Verzeichnis Zwischenspeicherung | „Neu“, | SMB 3.1.1 umfasst Verbesserungen bei der Verzeichnis Zwischenspeicherung. Windows-Clients können nun erheblich größere Verzeichnisse Zwischenspeichern, ungefähr 500.000 Einträge. Windows-Clients versuchen, Verzeichnis Abfragen mit 1 MB Puffer durchführen, um Roundtrips zu reduzieren und die Leistung zu steigern. |
| Integrität der Vorauthentifizierung | „Neu“, |  In SMB 3.1.1 bietet die vorauthentifizierungs Integrität einen verbesserten Schutz vor einem man-in-the-Middle-Angreifer, der die Verbindungs Einrichtung und die Authentifizierungs Nachrichten von SMB manipuliert. Weitere Informationen finden Sie unter [SMB 3.1.1-Integrität vor der Authentifizierung in Windows 10](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10). |
| SMB-Verschlüsselungs Verbesserungen | „Neu“, | SMB 3.1.1 bietet einen Mechanismus zum Aushandeln des Kryptografiealgorithmus pro Verbindung mit den Optionen AES-128-ccm und AES-128-GCM. AES-128-GCM ist die Standardeinstellung für neue Windows-Versionen, während ältere Versionen weiterhin AES-128-ccm verwenden werden. |
| Unterstützung für paralleles Cluster Upgrade | „Neu“, | Ermöglicht das parallele [Cluster Upgrade](../../failover-clustering/cluster-operating-system-rolling-upgrade.md) , indem SMB bei der Aktualisierung verschiedene Versionen von SMB für Cluster unterstützt. Weitere Informationen zum Zulassen der Kommunikation zwischen SMB und verschiedenen Versionen (Dialekte) des Protokolls finden Sie im Blogbeitrag [Steuern von SMB-Dialekten](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024). |
| Unterstützung von SMB Direct Client in Windows 10 | „Neu“, | Windows 10 Enterprise, Windows 10 Education und Windows 10 pro für Arbeitsstationen enthalten jetzt Unterstützung für SMB Direct Client. |
| Native Unterstützung für FileNormalizedNameInformation-API-Aufrufe | „Neu“, | Fügt systemeigene Unterstützung für das Abfragen des normalisierten Namens einer Datei hinzu. Weitere Informationen finden Sie unter [FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6). |

Weitere Informationen finden Sie im Blogbeitrag [Neues in SMB 3.1.1 in Windows Server 2016 Technical Preview 2](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2).

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>In SMB 3,02 mit Windows Server 2012 R2 und Windows 8.1 hinzugefügte Features

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| Automatischer Neuausgleich der Clients für Dateiserver mit horizontaler Skalierung     |   „Neu“,      | Verbessert die Skalierbarkeit und Verwaltbarkeit von Dateiservern mit horizontaler Skalierung. SMB-Clientverbindungen werden nach Dateifreigabe (und nicht nach Server) nachverfolgt. Clients werden dann an den Clusterknoten mit dem besten Zugriff auf das von der Dateifreigabe verwendete Volume umgeleitet. Dadurch wird die Effizienz gesteigert, da der Umleitungsdatenverkehr zwischen Dateiserverknoten verringert wird. Clients werden nach der Anfangsverbindung und bei einer Neukonfiguration des Clusterspeichers umgeleitet.    |
| Leistung über WAN   | Aktualisiert  | Windows 8.1 und Windows 10 bieten verbesserte CopyFile-SRV_COPYCHUNK über SMB-Unterstützung, wenn Sie den Datei-Explorer für Remote Kopien von einem Speicherort auf einem Remote Computer in eine andere Kopie auf demselben Server verwenden. Sie kopieren nur eine kleine Menge von Metadaten über das Netzwerk (1/2kib pro 16mib von Datei Daten werden übertragen). Dies führt zu einer deutlichen Leistungsverbesserung. Dies ist eine Unterscheidung auf Betriebssystemebene und Datei-Explorer-Ebene für SMB. |
| SMB Direct     |   Aktualisiert      | Verbessert die Leistung für kleine E/A-Arbeitsauslastungen, indem die Effizienz beim Hosten von Arbeitsauslastungen mit kleinen E/As (z. B. eine Datenbank für die Onlinetransaktionsverarbeitung (Online Transaction Processing, OLTP) auf einem virtuellen Computer) gesteigert wird. Diese Verbesserungen sind offensichtlich, wenn Netzwerkschnittstellen mit höherer Geschwindigkeit verwendet werden, wie z. b. 40 Gbit/s-Ethernet und 56 Gbit  |
| SMB-Bandbreiten Limits | „Neu“, | Sie können jetzt [Set-smbbandwidthlimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit) verwenden, um Bandbreiten Limits in drei Kategorien festzulegen: virtualmachine (Hyper-v über SMB-Datenverkehr), Live Migration (Hyper-v-Livemigration-Datenverkehr über SMB) oder Standard (alle anderen Typen von SMB-Datenverkehr).

Weitere Informationen zu neuen und geänderten Funktionen von SMB in Windows Server 2012 R2 finden Sie unter [Neues in SMB unter Windows Server](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>).

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>In SMB 3,0 mit Windows Server 2012 und Windows 8 hinzugefügte Features

| Feature/Funktionalität  | Neu oder aktualisiert  | Zusammenfassung  |
| --------- | --------- | --------- |
| SMB Transparent Failover     |   „Neu“,    | Ermöglicht es Administratoren, Hardware- oder Softwarewartungen von Knoten in einem Clusterdateiserver durchzuführen, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern. Wenn ein Hardware- oder Softwarefehler in einem Clusterknoten auftritt, stellen die SMB-Clients zudem die Verbindung zu einem anderen Clusterknoten transparent her, ohne Serveranwendungen zu unterbrechen, die Daten in diesen Dateifreigaben speichern.        |
| SMB Scale Out     |   „Neu“,      | Unterstützung für mehrere SMB-Instanzen auf einem Dateiserver mit horizontaler Skalierung. Durch die Verwendung freigegebener Clustervolumes der Version 2 (Cluster Shared Volumes, CSV) können Administratoren Dateifreigaben erstellen, die gleichzeitigen Zugriff auf Datendateien bieten, mit direkter E/A und über alle Knoten in einem Dateiservercluster. Dadurch wird die Ausnutzung der Netzwerkbandbreite verbessert und ein besserer Lastausgleich auf den Dateiserverclients erreicht sowie die Leistung für Serveranwendungen optimiert.  |
| SMB Multichannel     |   „Neu“,      |  Ermöglicht die Aggregation von Netzwerkbandbreite und Netzwerkfehler Toleranz, wenn mehrere Pfade zwischen dem SMB-Client und-Server verfügbar sind. Auf diese Weise können Serveranwendungen die verfügbare Netzwerkbandbreite voll ausnutzen und sind unempfindlich für Netzwerkausfälle.<br><br>SMB Multichannel in SMB 3 trägt zu einer deutlichen Leistungssteigerung im Vergleich zu früheren Versionen von SMB bei. |
| SMB Direct     |   „Neu“,      | Unterstützt die Verwendung von Netzwerkadaptern mit RDMA-Fähigkeit und kann bei maximaler Geschwindigkeit mit sehr niedriger Latenz arbeiten, und das bei sehr geringer CPU-Nutzung. Für Arbeitsauslastungen wie Hyper-V oder Microsoft SQL Server bedeutet dies, dass ein Remotedateiserver einem lokalen Speicher gleichkommt.<br><br>SMB Direct in SMB 3 trägt zu einer erheblichen Leistungssteigerung im Vergleich zu früheren Versionen von SMB bei.  |
| Leistungsindikatoren für Serveranwendungen     |   „Neu“,      |  Die neuen SMB-Leistungsindikatoren liefern detaillierte, pro Freigabe bereitgestellte Informationen über Durchsatz, Latenz und e/a pro Sekunde (IOPS), sodass Administratoren die Leistung von SMB-Dateifreigaben analysieren können, in denen Ihre Daten gespeichert sind. Diese Indikatoren sind speziell für Serveranwendungen wie Hyper-V und SQL Server konzipiert, die Dateien in Remotedateifreigaben speichern.      |
| Leistungsoptimierungen    |  Aktualisiert   | Sowohl der SMB-Client als auch der Server sind für kleine zufällige Lese-/Schreib-e/As optimiert, was bei Server Anwendungen wie SQL Server OLTP üblich ist. Außerdem ist das Feature Maximum Transmission Unit (MTU) standardmäßig für große Pakete aktiviert, wodurch die Leistung bei großen sequenziellen Übertragungen, wie SQL Server Data Warehouse, Datenbanksicherung und -wiederherstellung oder dem Bereitstellen und Kopieren virtueller Festplatten, deutlich verbessert wird. |
| SMB-spezifische Windows PowerShell-Cmdlets     |   „Neu“,      |  Mit Windows PowerShell-Cmdlets für SMB kann ein Administrator Dateifreigaben auf dem Dateiserver End-to-End von der Befehlszeile aus verwalten.   |
| SMB-Verschlüsselung     |   „Neu“,      | Sorgt für End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor Lauschangriffen in nicht vertrauenswürdigen Netzwerken. Erfordert keine weiteren Bereitstellungskosten und keine Internet Protocol-Sicherheit (IPsec), spezielle Hardware oder WAN-Beschleuniger. Sie kann auf Freigabebasis oder für den gesamten Dateiserver konfiguriert und für eine Vielzahl von Szenarios aktiviert werden, bei denen Daten über nicht vertrauenswürdige Netzwerke übertragen werden. |
| SMB Directory Leasing     |  „Neu“, | Verbessert die Antwortzeiten von Anwendungen in Filialen. Durch die Verwendung von Verzeichnisleases werden Roundtrips vom Client zum Server reduziert, da Metadaten von einem Verzeichniscache mit längerer Lebensdauer abgerufen werden. Die Cachekohärenz bleibt erhalten, da Clients benachrichtigt werden, wenn sich Verzeichnisinformationen auf dem Server ändern. Verzeichnis Leases arbeiten mit Szenarien für HomeFolder (Lese-/Schreibzugriff ohne Freigabe) und Veröffentlichung (schreibgeschützt mit Freigabe).    |
| Leistung über WAN   | „Neu“,   | Verzeichnis opportunistische Sperren (oplocks) und Oplock-Leases wurden in SMB 3,0 eingeführt. Bei typischen Office-/clientworkloads werden oplocks/Leases angezeigt, um die Netzwerkroundtrips um ungefähr 15% zu verringern.<br><br>In SMB 3 wurde die Windows-Implementierung von SMB optimiert, um das zwischen Speicherungs Verhalten auf dem Client zu verbessern, sowie die Möglichkeit, höhere Durchsatz Vorgänge durchzusetzen.<br><br>SMB 3-Features Verbesserungen an der CopyFile ()-API sowie an zugeordneten Tools wie Robocopy, um erheblich mehr Daten über das Netzwerk zu übermitteln. |
| Sichere Dialekt Aushandlung | „Neu“, | Schützt vor man-in-the-Middle-versuchen, eine Herabstufung der Dialekt Aushandlung durchführen zu können. Der Gedanke besteht darin, zu verhindern, dass ein eavesdropperwert den anfänglich ausgehandelten Dialekt und die Funktionen zwischen Client und Server herabstuft. Weitere Informationen finden Sie unter [SMB3 Secure Dialekt Aushandlung](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation). Beachten Sie, dass dies durch die [SMB 3.1.1-Funktion zur Vorauthentifizierung von Vorauthentifizierung in Windows 10](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10) in SMB 3.1.1 ersetzt wurde. |


## <a name="hardware-requirements"></a>Hardwareanforderungen

Für SMB Transparent Failover gelten die folgenden Anforderungen:

* Ein Failovercluster unter Windows Server 2012 oder Windows Server 2016 mit mindestens zwei konfigurierten Knoten. Der Cluster muss die Clustervalidierungstests bestehen, die im Validierungs-Assistenten enthalten sind.
* Dateifreigaben müssen mit der Eigenschaft %%amp;quot;Fortlaufende Verfügbarkeit%%amp;quot; (Continuous Availability, CA) erstellt werden, die standardmäßig aktiviert ist.
* Dateifreigaben müssen unter CSV-Volumepfaden erstellt werden, um SMB Scale-Out zu nutzen.
* Auf Client Computern muss Windows® 8 oder Windows Server 2012 ausgeführt werden, die beide den aktualisierten SMB-Client enthalten, der fortlaufende Verfügbarkeit unterstützt.

> [!NOTE]
> Downlevelclients können eine Verbindung mit Dateifreigaben herstellen, die die ca-Eigenschaft aufweisen, das transparente Failover wird für diese Clients jedoch nicht unterstützt.

Für SMB Multichannel gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Weitere Informationen zu empfohlenen Netzwerkkonfigurationen finden Sie im Abschnitt %%amp;quot;Siehe auch%%amp;quot; am Ende dieses Übersichtsthemas.

Für SMB Direct gelten die folgenden Anforderungen:

* Mindestens zwei Computer, auf denen Windows Server 2012 ausgeführt wird, sind erforderlich. Es müssen keine zusätzlichen Features installiert werden. Die Technologie ist standardmäßig aktiviert.
* Netzwerkadapter mit RDMA-Fähigkeit sind erforderlich. Aktuell sind diese Adapter in drei unterschiedlichen Typen erhältlich: iWARP, Infiniband und RoCE (RDMA over Converged Ethernet).

## <a name="more-information"></a>Weitere Informationen

In der folgenden Liste finden Sie weitere Ressourcen im Web zu SMB und verwandten Technologien in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

* [Speicher](../storage.md)
* [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)
* [Verbessern der Leistung eines Dateiservers mit SMB Direct](smb-direct.md)
* [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [Bereitstellen von SMB Multichannel](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [Bereitstellen schneller und effizienter Dateiserver für Server Anwendungen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: Handbuch zur Problembehandlung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
