---
title: DFS-Replikation – Übersicht
ms.date: 03/08/2019
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 6a68d27ec7c1d06e070d18362de68e12ecbf9578
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950754"
---
# <a name="dfs-replication-overview"></a>DFS-Replikation – Übersicht

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (halbjährlicher Kanal)

Die DFS-Replikation ist ein Rollendienst in Windows Server, der eine effiziente Replikation von Ordnern (einschließlich denjenigen, auf die durch einen DFS-Namespacepfad verwiesen wird) über mehrere Server und Standorte hinweg ermöglicht. Bei der DFS-Replikation handelt es sich um eine effiziente Replikations-Engine mit mehreren Mastern, mit der Ordner zwischen Servern über Netzwerkverbindungen mit begrenzter Bandbreite fortlaufend synchronisiert werden können. Sie ersetzt den Dateireplikationsdienst (File Replication Service, FRS) als Replikations-Engine für DFS-Namespaces sowie zum Replizieren des SYSVOL-Ordners von Active Directory Domain Services (AD DS) in Domänen, die die Domänenfunktionsebene Windows Server 2008 oder höher verwenden.

Für die DFS-Replikation wird ein Komprimierungsalgorithmus verwendet, der als Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) bezeichnet wird. Mit RDC werden Änderungen an den Daten in einer Datei erkannt, und es wird ermöglicht, dass mit der DFS-Replikation nur die geänderten Dateiblöcke repliziert werden und nicht die ganze Datei.

Weitere Informationen zum Replizieren von SYSVOL mithilfe der DFS-Replikation findest du unter [Migrieren der SYSVOL-Replikation zur DFS-Replikation](migrate-sysvol-to-dfsr.md).

Um die DFS-Replikation zu verwenden, musst du Replikationsgruppen erstellen und den Gruppen replizierte Ordner hinzufügen. Replikationsgruppen, replizierte Ordner und Mitglieder werden in der folgenden Abbildung veranschaulicht.

![Eine Replikationsgruppe, die eine Verbindung zwischen zwei Mitgliedern enthält, die jeweils über einige replizierte Ordner verfügen](media/dfsr-overview.gif)

Diese Abbildung veranschaulicht, dass eine Replikationsgruppe eine Reihe von Servern umfasst, die als Mitglieder bezeichnet werden und an der Replikation von mindestens einem replizierten Ordner beteiligt sind. Ein replizierter Ordner ist ein Ordner, der auf jedem Mitglied stets synchronisiert ist. In der Abbildung gibt es zwei replizierte Ordner: „Projects“ und „Proposals“. Wenn sich die Daten in den einzelnen replizierten Ordnern ändern, werden die Änderungen über die Verbindungen zwischen den Mitgliedern der Replikationsgruppe repliziert. Die Verbindungen zwischen allen Mitgliedern bilden die Replikationstopologie.
Die Erstellung mehrerer replizierter Ordner in einer einzelnen Replikationsgruppe vereinfacht das Bereitstellen von replizierten Ordnern, da die Topologie, der Zeitplan und die Bandbreiteneinschränkung für die Replikationsgruppe auf jeden replizierten Ordner angewendet werden. Zum Bereitstellen zusätzlicher replizierter Ordner kannst du „Dfsradmin.exe“ verwenden oder die Anweisungen in einem Assistenten befolgen, um den lokalen Pfad und Berechtigungen für den neuen replizierten Ordner zu definieren.

Jeder replizierte Ordner verfügt über eindeutige Einstellungen, wie z. B. Datei- und Unterordnerfilter, sodass du für jeden replizierten Ordner verschiedene Dateien und Unterordner herausfiltern kannst.

Die auf den einzelnen Mitgliedern gespeicherten replizierten Ordner können sich auf unterschiedlichen Volumes im Mitglied befinden, und die replizierten Ordner müssen keine freigegebenen Ordner oder Teile eines Namespace sein. Das DFS-Verwaltungs-Snap-in vereinfacht es jedoch, replizierte Ordner freizugeben und optional in einem vorhandenen Namespace zu veröffentlichen.

Die DFS-Replikation kann mithilfe der DFS-Verwaltung, mit den Befehlen „DfsrAdmin“ und „Dfsrdiag“ oder mit Skripts verwaltet werden, die WMI aufrufen.

## <a name="requirements"></a>Anforderungen

Vor dem Bereitstellen der DFS-Replikation müssen die Server wie folgt konfiguriert werden:

- Aktualisiere das AD DS-Schema (Active Directory Domain Services) so, dass es Schemaerweiterungen für Windows Server 2003 R2 oder höher umfasst. Bei Verwendung von Schemaerweiterungen für Windows Server 2003 R2 oder frühere Versionen können keine schreibgeschützten replizierten Ordner verwendet werden.
- Stellen Sie sicher, dass sich alle Server in einer Replikationsgruppe in der gleichen Gesamtstruktur befinden. Eine serverübergreifende Replikation über verschiedene Gesamtstrukturen hinweg ist nicht möglich.
- Installieren Sie die DFS-Replikation auf allen Servern, die als Mitglieder einer Replikationsgruppe fungieren sollen.
- Erkundigen Sie sich beim Hersteller der verwendeten Antivirensoftware, ob diese mit der DFS-Replikation kompatibel ist.
- Ermitteln Sie sämtliche zu replizierende Ordner, die sich auf Volumes mit dem NTFS-Dateisystem befinden. Das robuste Dateisystem (Resilient File System, ReFS) und das FAT-Dateisystem werden von der DFS-Replikation nicht unterstützt. Auch eine Replizierung von Inhalten auf freigegebenen Clustervolumes wird von der DFS-Replikation nicht unterstützt.

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilität mit virtuellen Azure-Computern

Die Verwendung der DFS-Replikation auf einem virtuellen Computer in Azure wurde mit Windows Server getestet, es gibt jedoch einige Einschränkungen und Anforderungen, die befolgt werden müssen.

- Wenn Sie einen Server, auf dem die DFS-Replikation nicht nur zum Replizieren des SYSVOL-Ordners verwendet wird, mithilfe von Momentaufnahmen oder gespeicherten Zuständen wiederherstellen, tritt bei der DFS-Replikation ein Fehler auf. In diesem Fall müssen spezielle Schritte zur Datenbankwiederherstellung ausgeführt werden. Dementsprechend solltest du keine virtuellen Computer exportieren, klonen oder kopieren. Weitere Informationen finden Sie in Artikel [2517913](https://support.microsoft.com/kb/2517913) in der Microsoft Knowledge Base sowie unter [Safely Virtualizing DFSR](https://techcommunity.microsoft.com/t5/storage-at-microsoft/safely-virtualizing-dfsr/ba-p/424671).
- Wenn du Daten in einem replizierten Ordner sicherst, der auf einem virtuellen Computer gehostet wird, musst du die Sicherungssoftware vom virtuellen Gastcomputer verwenden.
- Die DFS-Replikation erfordert Zugriff auf physische oder virtualisierte Domänencontroller, da eine direkte Kommunikation mit Azure AD nicht möglich ist.
- Die DFS-Replikation erfordert eine VPN-Verbindung zwischen deinen lokalen Replikationsgruppenmitgliedern und allen in Azure-VMs gehosteten Mitgliedern. Du musst auch den lokalen Router (z. B. Forefront Threat Management Gateway) so konfigurieren, dass die VPN-Verbindung über die RPC-Endpunktzuordnung (Port 135) und einen zufällig zugewiesenen Port zwischen 49152 und 65535 weitergeleitet wird. Du kannst das Set-DfsrMachineConfiguration-Cmdlet oder das Befehlszeilentool „Dfsrdiag“ verwenden, um einen statischen Port anstelle des zufälligen Ports anzugeben. Weitere Informationen zur Festlegung eines statischen Ports für die DFS-Replikation finden Sie unter [Set-DfsrServiceConfiguration](/powershell/module/dfsr/set-dfsrserviceconfiguration). Informationen über das Öffnen verknüpfter Ports für die Verwaltung von Windows Server finden Sie im Artikel [832017](https://support.microsoft.com/kb/832017) in der Microsoft Knowledge Base.

Weitere Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie auf der [Microsoft Azure web site](/azure/virtual-machines/).

## <a name="installing-dfs-replication"></a>Installieren der DFS-Replikation

Die DFS-Replikation ist Teil der Rolle „Datei- und Speicherdienste“. Die Verwaltungstools für DFS (DFS-Verwaltung, das DFS-Replikationsmodul für Windows PowerShell sowie Befehlszeilentools) werden separat im Rahmen der Remoteserver-Verwaltungstools installiert.

Installiere die DFS-Replikation mithilfe von [Windows Admin Center](../../manage/windows-admin-center/overview.md), Server-Manager oder PowerShell, wie in den folgenden Abschnitten beschrieben.

### <a name="to-install-dfs-by-using-server-manager"></a>So installieren Sie DFS mithilfe des Server-Managers

1. Klicken Sie im Server-Manager auf **Verwalten**und anschließend auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.

2. Wählen Sie auf der Seite **Serverauswahl** den Server oder die virtuelle Festplatte (Virtual Hard Disk, VHD) eines virtuellen Computers im Offlinemodus aus, auf dem Sie DFS installieren möchten.

3. Wählen Sie die zu installierenden Rollendienste und Features aus.

    - Um den DFS-Replikationsdienst zu installieren, wähle auf der Seite **Serverrollen** die Option **DFS-Replikation** aus.

    - Erweitern Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools**, erweitern Sie **Rollenverwaltungstools**, erweitern Sie **Tools für Dateidienste**, und wählen Sie anschließend **DFS-Verwaltungstools**aus.

         Im Rahmen der **DFS-Verwaltungstools** werden auf dem Server das DFS-Verwaltungs-Snap-in, DFS-Replikations- und DFS-Namespacemodule für Windows PowerShell sowie Befehlszeilentools, aber keine DFS-Dienste installiert.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>So installierst du die DFS-Replikation mithilfe von Windows PowerShell

Öffne eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, und gib den folgenden Befehl ein, wobei <name\> für den zu installierenden Rollendienst bzw. für das zu installierende Feature steht. Eine Liste mit relevanten Rollendienst- oder Featurenamen findest du in der folgenden Tabelle:

```PowerShell
Install-WindowsFeature <name>
```

|Rollendienst oder Feature|Name|
|---|---|
|DFS-Replikation|`FS-DFS-Replication`|
|DFS-Verwaltungstools|`RSAT-DFS-Mgmt-Con`|

Geben Sie beispielsweise Folgendes ein, um die DFS-Tools zu installieren, die Teil der Remoteserver-Verwaltungstools sind:

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

Gib Folgendes ein, um die DFS-Replikation und die DFS-Tools zu installieren, die Teil der Remoteserver-Verwaltungstools sind:

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="additional-references"></a>Weitere Verweise

- [Übersicht über DFS-Namespaces und DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127250(v%3dws.11))
- [Prüfliste: Bereitstellen der DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc772201(v%3dws.11))
- [Prüfliste: Verwalten der DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc755035(v%3dws.11))
- [Bereitstellen der DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc770925(v%3dws.11))
- [Verwalten der DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc770925(v%3dws.11))
- [Problembehandlung bei der DFS-Replikation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732802(v%3dws.11))
