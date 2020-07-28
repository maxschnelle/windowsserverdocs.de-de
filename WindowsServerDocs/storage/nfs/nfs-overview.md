---
title: Network File System (Übersicht)
description: Erläutert, worum es sich bei dem Netzwerkdatei System handelt.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: aff9fbdfa6dc97cb644e207efdae9c44533c320b
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181746"
---
# <a name="network-file-system-overview"></a>Network File System (Übersicht)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden der Rollen Dienst "Netzwerkdatei System" und die Features in der Server Rolle "Datei-und Speicherdienste" in Windows Server beschrieben. Network File System (NFS) bietet eine Dateifreigabe Lösung für Unternehmen mit heterogenen Umgebungen, die sowohl Windows-als auch nicht-Windows-Computer enthalten.

## <a name="feature-description"></a>Featurebeschreibung

Mithilfe des NFS-Protokolls können Sie Dateien zwischen Computern unter Windows und anderen nicht-Windows-Betriebssystemen (z. b. Linux oder Unix) übertragen.

NFS in Windows Server umfasst Server für NFS und Client für NFS. Ein Computer, auf dem Windows Server ausgeführt wird, kann Server für NFS verwenden, um als NFS-Datei Server für andere nicht-Windows-Client Computer zu fungieren. Client für NFS ermöglicht einem Windows-basierten Computer mit Windows Server den Zugriff auf Dateien, die auf einem nicht-Windows-NFS-Server gespeichert sind.

## <a name="windows-and-windows-server-versions"></a>Windows-und Windows Server-Versionen

Windows unterstützt je nach Betriebssystemversion und-Familie mehrere Versionen des NFS-Clients und-Servers.

| Betriebssysteme | NFS-Server Versionen |NFS-Client Versionen|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | N/V | NFSv2, NFSv3 |
| Windows Server 2008, Windows Server 2008 R2 | NFSv2, NFSv3 | NFSv2, NFSv3 |
| Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 | NFSv2, NFSv3, nfsv 4.1  | NFSv2, NFSv3 |

## <a name="practical-applications"></a>Praktische Anwendung

Es folgen einige Möglichkeiten, NFS zu verwenden:

- Verwenden Sie einen Windows NFS-Dateiserver, um Multiprotokollzugriff auf dieselbe Dateifreigabe über SMB-und NFS-Protokolle von Clients mit mehreren Plattformen zu ermöglichen.
- Stellen Sie einen Windows NFS-Dateiserver in einer vorwiegend nicht-Windows-Betriebssystemumgebung bereit, um nicht-Windows-Client Computern den Zugriff auf NFS-Dateifreigaben zu ermöglichen.
- Migrieren von Anwendungen von einem Betriebssystem zu einem anderen, indem die Daten in Dateifreigaben gespeichert werden, auf die über SMB-und NFS-Protokolle zugegriffen

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

Neue und geänderte Funktionen in Network File System enthalten Unterstützung für die NFS-Version 4,1 und eine verbesserte Bereitstellung und Verwaltbarkeit. Weitere Informationen zu neuen oder geänderten Funktionen in Windows Server 2012 finden Sie in der folgenden Tabelle:

|Feature/Funktionalität|Neu oder aktualisiert|BESCHREIBUNG|
|---|---|---|
|[NFS-Version 4,1](#nfs-version-41)|Neu|Erhöhung der Sicherheit, Leistung und Interoperabilität im Vergleich zu NFS Version 3.|
|[NFS-Infrastruktur](#nfs-infrastructure)|Aktualisiert|Verbessert Bereitstellung und Verwaltbarkeit und erhöht die Sicherheit.|
|[NFS Version 3 fortlaufende Verfügbarkeit](#nfs-version-3-continuous-availability)|Aktualisiert|Verbessert die kontinuierliche Verfügbarkeit für NFS Version 3-Clients.|
|[Verbesserungen bei der Bereitstellung und](#deployment-and-manageability-improvements)|Aktualisiert|Ermöglicht Ihnen die einfache Bereitstellung und Verwaltung von NFS mit neuen Windows PowerShell-Cmdlets und einem neuen WMI-Anbieter.|

## <a name="nfs-version-41"></a>NFS-Version 4,1

Die NFS-Version 4,1 implementiert zusätzlich zu einigen der optionalen Aspekte von [RFC 5661](https://tools.ietf.org/html/rfc5661)alle erforderlichen Aspekte:

- **Pseudo Dateisystem**, ein Dateisystem, das den physischen und logischen Namespace trennt und mit NFS Version 3 und NFS Version 2 kompatibel ist. Für das exportierte Dateisystem, das Teil des Pseudo Dateisystems ist, wird ein Alias bereitgestellt.
- Zusammen **gesetzte RPCs** kombinieren relevante Vorgänge und reduzieren die Zeichen haftigkeit.
- **Sitzungen und Sitzungs abkürzen** ermöglichen nur eine Semantik und ermöglichen eine kontinuierliche Verfügbarkeit und bessere Leistung bei Verwendung mehrerer Netzwerke zwischen NFS 4,1-Clients und dem NFS-Server.

## <a name="nfs-infrastructure"></a>NFS-Infrastruktur

Im folgenden werden die Verbesserungen an der gesamten NFS-Infrastruktur in Windows Server 2012 ausführlich erläutert:

- Die XDR-Transport Infrastruktur ( **Remote Procedure Callcenter)/External Datendarstellung (XDR)** , die vom Winsock-Netzwerkprotokoll unterrichtet wird, ist sowohl für den Server für NFS als auch für den Client für NFS verfügbar. Dies ersetzt die Transport Device Interface (TDI), bietet bessere Unterstützung und bietet eine bessere Skalierbarkeit und Empfangs seitige Skalierung (Receive Side Scaling, RSS).
- Das Feature " **RPC-Port Multiplexer** " ist firewallfreundlich (weniger zu verwaltende Ports) und vereinfacht die Bereitstellung von NFS.
- Automatisch **abgestimmte Caches und Thread Pools** sind Ressourcen Verwaltungsfunktionen der neuen RPC/XDR-Infrastruktur, die dynamisch sind und automatisch Caches und Thread Pools basierend auf der Arbeitsauslastung optimieren. Dadurch wird die beim Optimieren von Parametern beteiligte Rätselraten vollständig entfernt, und es wird eine optimale Leistung erzielt, sobald NFS bereitgestellt wird.
- **Neue Kerberos-Datenschutz Implementierung und Authentifizierungs Optionen** mit zusätzlich zur Unterstützung von Kerberos-Datenschutz (Krb5p) sowie den vorhandenen krb5-und krb5i-Authentifizierungs Optionen.
- Die Cmdlets für die **Identitäts Zuordnung von Windows PowerShell-Modulen** vereinfachen die Verwaltung der Identitäts Zuordnung, das Konfigurieren von Active Directory Lightweight Directory Services (AD LDS) und das Einrichten von UNIX-und Linux-Kennwort-und Flatfiles.
- Mit dem **volumeeinstellungspunkt** können Sie auf Volumes zugreifen, die unter einer NFS-Freigabe mit NFS-4,1 Version
- Das Feature " **Port Multiplexing** " unterstützt den RPC-Port Multiplexer (Port 2049), der firewallfreundlich ist und die NFS-Bereitstellung vereinfacht.

## <a name="nfs-version-3-continuous-availability"></a>NFS Version 3 fortlaufende Verfügbarkeit

NFS Version 3-Clients können über schnelle und transparente geplante Failover mit mehr Verfügbarkeit und geringerer Ausfallzeit verfügen. Der Failoverprozess ist für NFS-Clients der Version 3 schneller:

- Die Clustering-Infrastruktur ermöglicht jetzt eine Ressource pro Netzwerkname anstelle einer Ressource pro Freigabe, wodurch die Failoverzeit der Ressourcen erheblich verbessert wird.
- Failoverpfade innerhalb eines NFS-Servers werden optimiert, um die Leistung zu verbessern.
- Die Platzhalter Registrierung in einem NFS-Server ist nicht mehr erforderlich, und die Failover sind fein optimiert.
- NSM-Benachrichtigungen (Network Statusmonitor) werden nach einem Failoverprozess gesendet, und Clients müssen nicht mehr darauf warten, dass TCP-Timeouts erneut eine Verbindung mit dem Failover-Server herstellen.

Beachten Sie, dass Server für NFS ein transparentes Failover nur bei manueller Auslösung unterstützt, was meist während einer geplanten Wartung erfolgt. Wenn ein ungeplantes Failover auftritt, verlieren NFS-Clients die Verbindung. Der Server für NFS verfügt auch über keine Integration in den Filter zum Fortsetzen des Schlüssels. Dies bedeutet Folgendes: Wenn eine lokale App oder SMB-Sitzung versucht, auf eine Datei zuzugreifen, auf die ein NFS-Client unmittelbar nach einem geplanten Failover auch zugreift, kann der NFS-Client seine Verbindung verlieren (es erfolgt kein transparentes Failover).

## <a name="deployment-and-manageability-improvements"></a>Verbesserungen bei der Bereitstellung und

Das Bereitstellen und Verwalten von NFS hat sich wie folgt verbessert:

- Über 40 neue Windows PowerShell-Cmdlets vereinfachen die Konfiguration und Verwaltung von NFS-Dateifreigaben. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](/powershell/module/nfs/?view=win10-ps).
- Die Identitäts Zuordnung wird durch einen lokalen flatfilemapping-Speicher und neue Windows PowerShell-Cmdlets zum Konfigurieren der Identitäts Zuordnung verbessert.
- Die Server-Manager grafische Benutzeroberfläche ist einfacher zu verwenden.
- Der neue WMI-Anbieter der Version 2 ist zur einfacheren Verwaltung verfügbar.
- Der RPC-Port Multiplexer (Port 2049) ist firewallfreundlich und vereinfacht die Bereitstellung von NFS.

## <a name="server-manager-information"></a>Informationen zum Server-Manager

Verwenden Sie den Assistenten zum Hinzufügen von Rollen und Features in Server-Manager oder das neuere [Windows Admin Center](../../manage/windows-admin-center/overview.md) , um den Server für NFS-Rollen Dienst (unter der Rolle "Datei" und "iSCSI-Dienste") hinzuzufügen. Allgemeine Informationen zum Installieren von Features finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](</previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>). Zu den Server für NFS-Tools gehört das MMC-Snap-in für das Netzwerkdatei System, um den Server für NFS-und Client für NFS-Komponenten zu verwalten. Mithilfe des-Snap-Ins können Sie den-Server für NFS-Komponenten verwalten, die auf dem Computer installiert sind. Server für NFS enthält auch mehrere Windows-Befehlszeilen-Verwaltungs Tools:

- Beim **einbinden** wird eine Remote-NFS-Freigabe (auch als Export bezeichnet) lokal bereitgestellt und einem lokalen Laufwerk Buchstaben auf dem Windows-Client Computer zugeordnet.
- **Nbsadmin** verwaltet die Konfigurationseinstellungen des Servers für NFS und Client für NFS-Komponenten.
- **Nfsshare** konfiguriert NFS-Freigabe Einstellungen für Ordner, die mithilfe von Server für NFS freigegeben werden.
- **Nfsstat** zeigt eine Statistik der von Server für NFS empfangenen Aufrufe an oder setzt diese zurück.
- **Showmount** zeigt eingebundene Dateisysteme an, die vom Server für NFS exportiert wurden.
- Durch die Bereitstellung werden von NFS eingebundene **Laufwerke entfernt.**

Mit NFS in Windows Server 2012 wird das NFS-Modul für Windows PowerShell mit mehreren neuen Cmdlets speziell für NFS eingeführt. Diese Cmdlets bieten eine einfache Möglichkeit zum Automatisieren von NFS-Verwaltungsaufgaben. Weitere Informationen finden Sie unter [NFS-Cmdlets in Windows PowerShell](/powershell/module/nfs/?view=win10-ps).

## <a name="additional-information"></a>Zusätzliche Informationen

Die folgende Tabelle enthält zusätzliche Ressourcen zum Auswerten von NFS.

|Inhaltstyp|Referenzen|
|---|---|
|Bereitstellung|[Network File System bereitstellen](deploy-nfs.md)|
|Operationen (Operations)|[NFS-Cmdlets in Windows PowerShell](/powershell/module/nfs/?view=win10-ps)|
|Verwandte Technologien|[Speicher](../storage.yml)|
