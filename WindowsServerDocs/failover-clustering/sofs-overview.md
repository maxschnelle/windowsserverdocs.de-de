---
title: Horizontale Skalierung Dateiserver für Übersicht über Daten
description: Übersicht über das Feature horizontal skalierten Dateiserver für Windows Server 201 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04e25e9c69062611d9d14c220614f148ac5de770
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082190"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>Horizontale Skalierung Dateiserver für Übersicht über Daten

>Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

Horizontale Skalierung Dateiserver ist ein Feature, das horizontal skalierten Dateifreigaben, die für den Datei-basierten Anwendung Serverspeicher ständig verfügbar sind, bereitgestellt werden sollen. Horizontale Skalierung Dateifreigaben bietet die Möglichkeit, den gleichen Ordner aus mehreren Knoten desselben Clusters freizugeben. Dieses Szenario liegt der Schwerpunkt zum Planen und Bereitstellen von horizontal skalierten Dateiserver.

Sie können bereitstellen und konfigurieren einen gruppierten Dateiserver mithilfe einer der folgenden Methoden:

- **Horizontale Skalierung Dateiserver für Anwendungsdaten** Dieses gruppierte Datei-Server-Feature in Windows Server 2012 eingeführt wurde, und ermöglicht das Speichern von Server-Anwendungsdaten wie Hyper-V VM-Dateien in Dateifreigaben, und erhalten eine ähnliche Ebene der Zuverlässigkeit, Verfügbarkeit, Verwaltbarkeit und hoch Leistung, die Sie von einem Storage Area Network erwarten. Alle Dateifreigaben, die gleichzeitig auf allen Knoten online sind. Dateifreigaben, die diese Art von gruppierten Dateiserver zugeordnet werden horizontal skalierten Dateifreigaben bezeichnet. Dies wird gelegentlich als aktiv / aktiv bezeichnet. Dies ist der empfohlene Server Dateityp, wenn entweder Hyper-V über SMB über Server Message Block (SMB) oder Microsoft SQL Server bereitstellen.
- **Dateiserver für die allgemeine Verwendung** Dies ist die Aufrechterhaltung der die gruppierten Dateiserver, der seit der Einführung der Failover-Clusterunterstützung in Windows Server unterstützt wurde hat. Diese Art von gruppierten Dateiserver, und daher aller Freigaben die gruppierten Dateiserver zugeordnet ist jeweils auf einem Knoten online. Dies wird gelegentlich als Aktiv/Passiv- oder Dual-aktive bezeichnet. Dateifreigaben, die diese Art von gruppierten Dateiserver zugeordnet werden als gruppierte Dateifreigaben bezeichnet. Dies ist der empfohlene Dateityp Server beim Bereitstellen von Informationen Worker-Szenarien.

## <a name="scenario-description"></a>Beschreibung des Szenarios

Mit horizontal skalierten Dateifreigaben können Sie den gleichen Ordner aus mehreren Knoten eines Clusters freigeben. Beispielsweise bei einem Server-Cluster mit vier-Knoten-Datei, die Skalierung Server Message Block (SMB) verwendet wird, kann ein Computer mit Windows Server 2012 R2 oder Windows Server 2012 Dateifreigaben aus vier Knoten zugreifen. Dies geschieht durch die Nutzung von neue Windows Server Failover Clustering Features und Funktionen von Dateiprotokoll Server Windows SMB 3.0. Datei Serveradministratoren können bieten horizontal skalierten Dateifreigaben und ständig verfügbar Dateidienste für Server-Clientanwendungen und schnell wider, da es einfach weitere Server online auf der heutigen reagieren. All dies kann in einer produktionsumgebung durchgeführt werden, und es ist für die Server-Anwendung vollständig transparent.

Wichtigsten Vorteile von horizontal skalierten Dateiserver in umfassen:

- **Aktiv / aktiv-Dateifreigaben**. Alle Knoten im Cluster können akzeptieren und SMB-Clientanforderungen bedienen. Zusammenarbeiten, machen Sie die Datei, die gleichzeitig genutzt werden Inhalte, die über alle Knoten im Cluster zugegriffen werden, um transparentes Failover auf alternative Clusterknoten während geplante und ungeplante Ausfälle Service bereitstellen SMB 3.0-Cluster und clients Unterbrechung.
- **Erhöhte Bandbreite**. Die maximale freigeben Bandbreite wird die gesamte Bandbreite aller Datei-Server-Cluster-Knoten. Im Gegensatz zu früheren Versionen von Windows Server wird die gesamte Bandbreite nicht mehr auf die Bandbreite von einem einzelnen Clusterknoten eingeschränkt; Vielmehr definiert die Möglichkeit der Sicherung Speichersystem Nebenbedingungen jedoch. Sie können die gesamte Bandbreite durch Hinzufügen von Knoten erhöhen.
- **CHKDSK ohne Ausfallzeiten**. CHKDSK in Windows Server 2012 wird erheblich verbessert, um die Zeit erheblich zu verkürzen, die einem Dateisystem zur Reparatur offline ist. Gruppierte freigegebene Volumes (CSVs) dauern einen Schritt weiter durch den Wegfall der offline Phase. Eine CSV-Datei System (CSVFS) können CHKDSK ohne Beeinträchtigung des Applikationen mit im Dateisystem geöffnet werden.
- **Clustered Shared Volume Cache**. CSVs in Windows Server 2012 führt die Unterstützung für Lese-Cache, der deutlich die Leistung in bestimmten Szenarien wie in Virtual Desktop Infrastructure (VDI) verbessern kann.
- **Einfachere Verwaltung**. Mit horizontal skalierten Dateiserver die Horizontal skalierte Dateiserver erstellen, und fügen Sie die erforderlichen CSVs und Dateifreigaben. Es ist nicht mehr erforderlich, erstellen mehrere gruppierten Dateiserver, jeweils mit separaten Clusterdatenträger, und klicken Sie dann entwickeln Platzierungsrichtlinien um Aktivitäten auf jedem Clusterknoten sicherzustellen.
- **Automatische einen Ausgleich der horizontal skalierten Dateiserver-Clients**. In Windows Server 2012 R2 verbessert die automatische Lastausgleich Skalierbarkeit und verwaltbarkeit für dezentrales Skalieren Dateiserver. SMB-Clientverbindungen pro Dateifreigabe nachverfolgt werden (statt pro Server), und Clients werden mit dem besten Zugriff auf die Lautstärke von der Dateifreigabe verwendet klicken Sie dann auf den Clusterknoten umgeleitet. Dadurch wird die Effizienz durch Reduzierung des Datenverkehrs zwischen Dateiserverknoten Umleitung verbessert. Clients werden umgeleitet nach eine erste Verbindung und beim Cluster-Speicher neu konfiguriert wird.

## <a name="in-this-scenario"></a>In diesem Szenario

In den folgenden Themen sind verfügbar, die Sie bei der Bereitstellung eines Dateiservers Skalierung unterstützen:

- [Plan für die horizontale Skalierung Dateiserver](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [Schritt 1: Planen der Speicherung horizontal skalierten Dateiserver](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [Schritt 2: Planen Sie für Netzwerke in Dateiserver Skalierung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [Bereitstellen von horizontal skalierten Dateiserver](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [Schritt 1: Installieren von erforderlichen Komponenten für die horizontale Skalierung Dateiserver](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [Schritt 2: Konfigurieren der horizontal skalierten Dateiserver](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [Schritt 3: Konfigurieren von Hyper-V, um die Skalierung Dateiserver verwenden](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [Schritt 4: Konfigurieren von Microsoft SQL Server für die horizontale Skalierung Dateiserver verwenden](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>Horizontale Skalierung Dateiserver verwenden

Sie sollten nicht horizontal skalierten Dateiserver verwenden, wenn Ihre Arbeitslast eine hohe Anzahl von Metadaten-Vorgänge, wie das Öffnen von Dateien, generiert Schließen von Dateien, Erstellen neuer Dateien oder vorhandene Dateien umbenennen. Für eine typische Information Worker würde viele Vorgänge Metadaten generieren. Sie sollten eines Dateiservers Skalierung verwenden, wenn Sie die Skalierbarkeit und Einfachheit, die es bietet interessiert sind und wenn Sie nur Technologies benötigen, die mit horizontal skalierten Dateiserver unterstützt werden.

Die folgende Tabelle enthält die Funktionen in SMB 3.0, das allgemeine Windows-Dateisystem, Datei Server Daten Management Technologien und allgemeine Arbeitslasten. Sie können sehen, ob die Technologie mit horizontal skalierten Dateiserver unterstützt wird oder wenn es sich um eine herkömmliche gruppierten Dateiserver (auch bekannt als eines Dateiservers für die allgemeine Verwendung) erfordert.

<table>
<thead>
<tr class="header">
<th>Technologiebereich</th>
<th>Feature</th>
<th>Allgemeine Datei-Server-Cluster</th>
<th>Skalierten Sie horizontal Dateiserver</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SMB</td>
<td>SMB ständige Verfügbarkeit</td>
<td>Ja</td>
<td>Ja</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB Multichannel</td>
<td>Ja</td>
<td>Ja</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB Direct</td>
<td>Ja</td>
<td>Ja</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB-Verschlüsselung</td>
<td>Ja</td>
<td>Ja</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>Transparentes failover</td>
<td>Ja (wenn es sich um eine ständige Verfügbarkeit aktiviert ist)</td>
<td>Ja</td>
</tr>
<tr class="even">
<td>Dateisystem</td>
<td>NTFS</td>
<td>Ja</td>
<td>NA</td>
</tr>
<tr class="odd">
<td>Dateisystem</td>
<td>Resilient File System (<a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">ReFS</a>)</td>
<td>Empfohlene mit Speicher Direct Räume</td>
<td>Empfohlene mit Speicher Direct Räume</td>
</tr>
<tr class="even">
<td>Dateisystem</td>
<td>Freigegebene Volume-Dateisystem (CSV)</td>
<td>NA</td>
<td>Ja</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>BranchCache</td>
<td>Ja.</td>
<td>Nein</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>Datendeduplizierung (WindowsServer 2012)</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>Datendeduplizierung (Windows Server 2012 R2)</td>
<td>Ja</td>
<td>Ja (nur VDI)</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>DFS-Namespace (DFSN) Stamm Serverstamm</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>DFS-Namespace (DFSN) Ordner Zielserver</td>
<td>Ja</td>
<td>Ja</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>DFS-Replikation (DFSR)</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>Datei Ressourcen-Manager (Bildschirme und Kontingente)</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>Datei Klassifizierung Infrastruktur</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>Dynamische Access Control (anspruchsbasierte Access CAP)</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>Ordnerumleitung</td>
<td>Ja</td>
<td>Nicht empfohlen *</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>Offline-Dateien (das clientseitige Zwischenspeichern)</td>
<td>Ja</td>
<td>Nicht empfohlen *</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>Servergespeicherte Benutzerprofile</td>
<td>Ja</td>
<td>Nicht empfohlen *</td>
</tr>
<tr class="odd">
<td>Dateiverwaltung</td>
<td>Basisverzeichnisse</td>
<td>Ja</td>
<td>Nicht empfohlen *</td>
</tr>
<tr class="even">
<td>Dateiverwaltung</td>
<td>Arbeitsordner</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="odd">
<td>NFS</td>
<td>NFS-Server</td>
<td>Ja</td>
<td>Nein</td>
</tr>
<tr class="even">
<td>Anwendungen</td>
<td>Hyper-V</td>
<td>Nicht empfohlen</td>
<td>Ja</td>
</tr>
<tr class="odd">
<td>Anwendungen</td>
<td>Microsoft SQL Server</td>
<td>Nicht empfohlen</td>
<td>Ja</td>
</tr>
</tbody>
</table>

\ * Ordnerumleitung, Offline-Dateien, servergespeicherte Benutzerprofile oder Home-Verzeichnisse generieren eine große Anzahl der Schreibvorgänge, die unmittelbar (ohne Pufferung) auf den Datenträger geschrieben werden müssen bei der Verwendung von ständig verfügbaren Dateifreigaben Leistung im Vergleich zu reduzieren Dateifreigaben für allgemeine Zwecke. Kontinuierlich sind auch verfügbar Dateifreigaben mit Ressourcen-Manager für Dateiserver und PCs unter Windows XP nicht kompatibel. Darüber hinaus kann Offline-Dateien nicht den Übergang in den Offlinemodus 3 bis 6 Minuten, nachdem ein Benutzer Zugriff auf eine Freigabe verliert der Benutzer frustrierend sein kann, die noch nicht immer Offlinemodus Offline-Dateien verwenden.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Horizontale Skalierung Dateiserver eignen sich für den Serverspeicher-Anwendung. Einige Beispiele für serveranwendungen, die ihre Daten auf einer horizontal skalierten Dateifreigabe gespeichert werden können, sind unten aufgeführt:

- Der Webserver (Internet Information Services, IIS) kann Konfigurationen und Daten für Websites in einer horizontal skalierten Dateifreigabe speichern. Weitere Informationen finden Sie unter [Freigegebene Konfiguration](http://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264).
- Hyper-V kann Konfigurations- und live virtuellen Festplatten auf einer horizontal skalierten Dateifreigabe gespeichert. Weitere Informationen finden Sie unter [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>).
- SQL Server können live Datenbankdateien auf einer horizontal skalierten Dateifreigabe gespeichert. Weitere Informationen finden Sie unter [Installieren von SQL Server mit SMB-Datei als eine Speicheroption freigeben](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option).
- Virtual Machine Manager (VMM) können eine Bibliothek freigeben (die Vorlagen für virtuelle Computer und die zugehörigen Dateien enthält) in einer horizontal skalierten Dateifreigabe gespeichert. Der Bibliotheksserver selbst darf jedoch keines Dateiservers horizontal skalierten sein – es muss auf einem eigenständigen Server oder einem Failovercluster, der die horizontale Skalierung Datei Cluster-Serverrolle nicht verwendet werden.

Wenn Sie eine horizontale Skalierung Dateifreigabe als Bibliotheksfreigabe verwenden, können Sie nur die Technologien, die mit horizontal skalierten Dateiserver kompatibel sind. DFS-Replikation können Sie beispielsweise eine Bibliotheksfreigabe auf einer horizontal skalierten Dateifreigabe gehostet repliziert werden. Es ist außerdem wichtig, dass der horizontale Skalierung Dateiserver der neuesten Softwareupdates installiert haben.

Um eine horizontale Skalierung Dateifreigabe als eine Bibliotheksfreigabe verwenden, zuerst Hinzufügen eines Bibliotheksservers (wahrscheinlich ein virtueller Computer) mit einer lokalen Freigabe oder keine Freigaben überhaupt. Wenn Sie eine Bibliotheksfreigabe hinzufügen, wählen Sie dann eine Dateifreigabe, die auf einem Dateiserver horizontal skalierten gehostet wird. Diese Freigabe sollte VMM verwaltet und ausschließlich für die Verwendung durch den Bibliotheksserver erstellten sein. Stellen Sie außerdem sicher, dass Sie die neuesten Updates auf dem Dateiserver horizontal skalierten installieren. Weitere Informationen zum Hinzufügen von VMM Bibliotheksserver und Bibliotheksfreigaben finden Sie unter [Hinzufügen von Benutzerprofilen in die VMM-Bibliothek](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801). Eine Liste der derzeit Hotfixes für die Datei- und Storage Services finden Sie unter [Microsoft Knowledge Base-Artikel 2899011](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie).

>[!NOTE]
>Einige Benutzer, wie Information-Worker haben Arbeitslasten, die eine größere Auswirkung auf die Leistung haben. Beispielsweise Vorgänge wie öffnen und Schließen von Dateien, und Erstellen neuer Dateien und vorhandene Dateien umbenennen, wenn durch mehrere Benutzer durchgeführt wirkt sich auf die Leistung haben. Wenn mit ständige Verfügbarkeit eine Dateifreigabe aktiviert ist, Datenintegrität Softwareentwicklern, aber es wirkt sich auch auf die allgemeine Leistung. Ständige Verfügbarkeit erfordert, dass Daten auf den Datenträger auf Integrität bei Ausfall von einem Clusterknoten auf einem Dateiserver Skalierung über schreibt. Aus diesem Grund kann ein Benutzer, der mehrere große Dateien auf einem Dateiserver kopiert erheblich langsamer in ständig verfügbar Dateifreigabe erwarten.

## <a name="features-included-in-this-scenario"></a>In diesem Szenario enthaltenen Features

In der folgenden Tabelle sind die Funktionen, die Teil dieses Szenarios sind und beschreibt, wie unterstützen.

<table>
<thead>
<tr class="header">
<th>Feature</th>
<th>Wie in diesem Szenario unterstützt</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">Failoverclusterunterstützung</a></td>
<td>Failovercluster die folgenden Features in Windows Server 2012 zur Unterstützung von horizontal skalierten Dateiserver hinzugefügt: Netzwerkname verteilt, der horizontal skalierten Dateiserver Ressourcentyp, Cluster Shared Volumes (CSV) 2 und die hohe Verfügbarkeit für dezentrales Skalieren Datei Server-Rolle. Weitere Informationen zu diesen Features finden Sie unter <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">What's New in der Failover-Clusterunterstützung in Windows Server 2012 [umgeleitet]</a>.</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">Server Message Block</a></td>
<td>SMB 3.0 hinzugefügt, die folgenden Features in Windows Server 2012 zur Unterstützung von horizontal skalierten Dateiserver: SMB transparentes Failover, SMB Multichannel und direkte SMB.<br />
<br />
Weitere Informationen über neue und geänderte Funktionalität für SMB in Windows Server 2012 R2 finden Sie unter <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">What's New in SMB in Windows Server</a>.</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>Weitere Informationen

- [Software definiert Storage Design Considerations Guide](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [Steigern der Server, Speicherung und Verfügbarkeit des Netzwerks](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [Bereitstellen von schnell und effizient Dateiserver für Serveranwendungen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [Zum Skalieren oder nicht für die horizontale Skalierung, skalieren, ist die Frage](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx) (Blogbeitrag)
- [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)