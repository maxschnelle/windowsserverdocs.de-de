---
title: Network File System (Übersicht)
description: Erläutert, was Network File System ist.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b0d339df588c784f8fe46f7dd0e6ce2975d0c48
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034655"
---
# <a name="network-file-system-overview"></a>Network File System (Übersicht)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, die NFS-Rollendienst und Features, die mit der Datei- und Speicherdienste-Serverrolle in Windows Server enthalten. Network File System (NFS) stellt eine dateifreigabelösung für Unternehmen, die heterogene Umgebungen verfügen, die sowohl für Windows als auch für nicht-Windows-Computer enthalten.

## <a name="feature-description"></a>Featurebeschreibung

Verwenden das NFS-Protokoll, können Sie Dateien zwischen PCs unter Windows und andere nicht-Windows-Betriebssysteme, wie z. B. Linux- oder UNIX übertragen.

NFS unter Windows Server enthält die Server für NFS- und Client für NFS. Ein Computer unter Windows Server können Server für NFS fungieren als Dateiserver NFS für andere nicht-Windows-Clientcomputer. Client für NFS ermöglicht es einen Windows-basierten Computer unter Windows Server, auf Dateien zugreifen, die auf einem nicht - Windows-NFS-Server gespeichert.

## <a name="windows-and-windows-server-versions"></a>Windows und Windows Server-Versionen

Windows unterstützt mehrere Versionen der NFS-Client und Server, je nach Version des Betriebssystems und Ihrer Familie. 

| Betriebssysteme | NFS-Server-Versionen |NFS-Clientversionen|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | Nicht zutreffend | NFSv2, NFSv3 |
| Windows Server 2008, Windows Server 2008 R2 | NFSv2, NFSv3 | NFSv2, NFSv3 |
| Windows Server 2012, Windows Server 2012 R2, WindowsServer 2016, WindowsServer 2019 | NFSv2, NFSv3, NFSv4.1  | NFSv2, NFSv3 |

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Hier sind einige Möglichkeiten der Verwendung von NFS:

- Verwenden Sie einen Windows NFS-Dateiserver, um Multiprotokoll-Zugriff auf die gleiche Dateifreigabe über sowohl von SMB- und NFS-Protokolle von plattformübergreifenden Clients zu ermöglichen.
- Bereitstellen eines Windows NFS-Datei-Servers in einer Umgebung vorwiegend nicht-Windows-Betriebssystem, um nicht-Windows-Client Computern der Zugriff auf die NFS-Dateifreigaben bereitzustellen.
- Migrieren Sie Anwendungen auf einem Betriebssystem zu einem anderen durch Speicherung der Daten in Dateifreigaben, die sowohl von SMB- und NFS-Protokollen über ein.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

Neue und geänderte Funktionen in Network File System enthält Unterstützung für die NFS-Version 4.1 und verbesserte Bereitstellung und verwaltbarkeit. Informationen über die neuen oder geänderten in Windows Server 2012-Funktionen finden Sie in der folgende Tabelle:

|Feature/Funktionalität|Neu oder aktualisiert|Beschreibung|
|---|---|---|
|[NFS-Version 4.1](#nfs-version-41)|Neu|Erhöhte Sicherheit, Leistung und Interoperabilität im Vergleich zu NFS V3.|
|[NFS-Infrastruktur](#nfs-infrastructure)|Aktualisiert|Bereitstellung und verwaltbarkeit verbessert und erhöht die Sicherheit.|
|[Fortlaufende Verfügbarkeit von NFS V3](#nfs-version-3-continuous-availability)|Aktualisiert|Verbessert die fortlaufende Verfügbarkeit für Clients für NFS-Version 3.|
|[Verbesserungen bei der Bereitstellung und verwaltbarkeit](#deployment-and-manageability-improvements)|Aktualisiert|Können Sie ganz einfach bereitstellen und Verwalten von NFS mit neuen Windows PowerShell-Cmdlets und ein neuer WMI-Anbieter.|

## <a name="nfs-version-41"></a>NFS-Version 4.1

NFS-Version 4.1 implementiert alle erforderlichen Aspekte, zusätzlich einige optionale Aspekte, zu der [RFC 5661](https://tools.ietf.org/html/rfc5661):

- **Pseudo-Dateisystem**, ein Dateisystem, die getrennt von physischen und logischen-Namespace und ist kompatibel mit NFS V3 und NFS-Version 2. Für exportierte Dateisystem des Pseudo-Dateisystems gehört, wird ein Alias bereitgestellt.
- **Zusammengesetzte RPCs** relevante Vorgängen kombinieren, und reduzieren Sie die "chattiness".
- **Sitzungen und der angegebenen Sitzung Trunking** ermöglicht nur eine semantische und kontinuierliche Verfügbarkeit und eine bessere Leistung, die gleichzeitig von mehreren Netzwerken zwischen 4.1 von NFS-Clients und der NFS-Server.

## <a name="nfs-infrastructure"></a>NFS-Infrastruktur

Verbesserungen für die gesamte Infrastruktur für NFS unter Windows Server 2012 werden unten genauer beschrieben:

- Die **(Remoteprozeduraufruf) / externe Daten Datendarstellung (XDR)** Transportinfrastruktur, die von der WinSock-Netzwerkprotokoll für beide Server für NFS und Client für NFS verfügbar ist. Dieser Transport Device Interface (TDI) ersetzt, bietet eine bessere Unterstützung und bietet eine bessere Skalierbarkeit und Empfangen von empfangsseitige Skalierung (RSS).
- Die **RPC-Port multiplexer** Feature ist firewallfreundlich (weniger Ports verwalten) und vereinfacht die Bereitstellung von NFS.
- **Automatisch optimierte Caches und Threadpools** sind Resource Management-Funktionen der neuen RPC/XDR-Infrastruktur, die dynamische Optimierung automatisch Caches und Threadpools basierend auf der Workload. Dadurch wird das Rätselraten beim vollständig entfernt, beim Optimieren von Parametern, die eine optimale Leistung bereitstellen, sobald NFS bereitgestellt wird.
- **Neue Kerberos-Implementierung und Authentifizierung Datenschutzoptionen** durch das Hinzufügen von Unterstützung der Kerberos-Datenschutz (Krb5p) zusammen mit den vorhandenen krb5 und krb5i Authentifizierungsoptionen zur Verfügung.
- **Identity-Zuordnung Windows PowerShell-Modul** Cmdlets erleichtert das Verwalten der identitätszuordnung, Active Directory Lightweight Directory Services (AD LDS) konfigurieren und Einrichten von UNIX- und Linux-Kennwort- und Flatfile-Dateien.
- **Volumebereitstellungspunkt** ermöglicht den Zugriff auf Volumes, die unter eine NFS-Freigabe mit NFS Version 4.1 eingebunden.
- Die **Port Multiplexing** Feature unterstützt den RPC-Port multiplexer (Port 2049), die firewallfreundliche und vereinfacht die NFS-Bereitstellung.

## <a name="nfs-version-3-continuous-availability"></a>Fortlaufende Verfügbarkeit von NFS V3

NFS V3-Clients können schnell und transparent geplante Failover ohne Datenverlust mit mehr Verfügbarkeit und geringere Ausfallzeiten haben. Während des failoverprozesses ist schneller für Clients für NFS-Version 3, da:

- Die clustering-Infrastruktur ermöglicht jetzt eine Ressource pro Netzwerknamen, anstatt eine Ressource pro Freigabe, die Failoverzeit für Ressourcen erheblich verbessert.
- Failover-Pfade in einem NFS-Server werden für eine bessere Leistung optimiert.
- Platzhalter-Registrierung in einem NFS-Server ist nicht mehr erforderlich, und die Failover werden mehr optimiert.
- Nach einem Failoverprozess Network Status Monitor (NSM) Benachrichtigungen versendet werden, und Clients müssen nicht mehr warten, TCP-Timeouts für die Verbindung für den Server.

Beachten Sie, dass Server für NFS ein transparentes Failover nur bei manueller Auslösung unterstützt, was meist während einer geplanten Wartung erfolgt. Wenn ein ungeplantes Failover auftritt, verlieren NFS-Clients die Verbindung. Server für NFS keine auch eine Integration mit dem Filter. Dies bedeutet Folgendes: Wenn eine lokale App oder SMB-Sitzung versucht, auf eine Datei zuzugreifen, auf die ein NFS-Client unmittelbar nach einem geplanten Failover auch zugreift, kann der NFS-Client seine Verbindung verlieren (es erfolgt kein transparentes Failover).

## <a name="deployment-and-manageability-improvements"></a>Verbesserungen bei der Bereitstellung und verwaltbarkeit

Bereitstellen und Verwalten von NFS wurde folgendermaßen verbessert:

- Mehr als 40 neue Windows PowerShell-Cmdlets erleichtern das Konfigurieren und Verwalten von NFS-Dateifreigaben. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps).
- Identitätszuordnung wird mit einem lokalen Flatfile zuordnungsspeicher und neue Windows PowerShell-Cmdlets für die Konfiguration der identitätszuordnung verbessert.
- Die grafische Benutzeroberfläche des Server-Manager ist einfacher zu verwenden.
- Der neue WMI-Anbieter für Version 2 ist zur einfacheren Verwaltung verfügbar.
- Der RPC-Port multiplexer (Port 2049) ist firewallfreundlich und vereinfacht die Bereitstellung von NFS.

## <a name="server-manager-information"></a>Informationen zum Server-Manager

In Server-Manager- oder der neueren [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) -Hinzufügen von Rollen und Features-Assistenten verwenden, um den Server für NFS-Rollendienst hinzuzufügen (unter der Datei- und iSCSI-Services-Rolle). Allgemeine Informationen zum Installieren von Features finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>). Server für NFS-Tools enthalten, die Dienste für Network-Datei-System-MMC-Snap-in zum Verwalten des Servers für NFS und -Client für NFS-Komponenten. Das Snap-in verwenden, können Sie den Server für NFS-Komponenten, die auf dem Computer installierten verwalten. Server für NFS enthält auch mehrere Verwaltungstools der Windows-Befehlszeile:

- **Einbinden** stellt Sie eine remote NFS-Freigabe (auch bekannt als einen Export) lokal aus, und ordnet es zu einem lokalen Laufwerkbuchstaben auf dem Windows-Clientcomputer.
- **Nfsadmin** Verwalten der Konfigurationseinstellungen des Servers für NFS und -Client für NFS-Komponenten.
- **Nfsshare** konfiguriert NFS-freigabeeinstellungen für Ordner, die mithilfe von Server für NFS freigegeben werden.
- **Nfsstat** anzeigt, oder setzt Statistiken von aufrufen, die vom Server für NFS empfangen.
- **Showmount** zeigt bereitgestellten Dateisystemen, die vom Server für NFS exportiert.
- **Umount** NFS eingebundenen Laufwerke entfernt.

NFS unter Windows Server 2012 führt das NFS-Modul für Windows PowerShell mit mehreren neuen-Cmdlets für NFS. Diese Cmdlets bieten eine einfache Möglichkeit, die NFS-Verwaltungsaufgaben zu automatisieren. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps).

## <a name="additional-information"></a>Weitere Informationen

Die folgende Tabelle enthält zusätzliche Ressourcen für Ihre Evaluierung von NFS.

|Inhaltstyp|Verweise|
|---|---|
|Bereitstellung|[Network File System bereitstellen](deploy-nfs.md)|
|Vorgänge|[NFS-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|Verwandte Technologien|[Speicher in WindowsServer](../storage.md)|