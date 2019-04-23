---
Title: Übersicht über die DFS-Replikation
ms.date: 03/08/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 17fa97e28d099806c9280e42dd900e8d6c708641
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850241"
---
# <a name="dfs-replication-overview"></a>Übersicht über die DFS-Replikation

> Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008, WindowsServer (Halbjährlicher Kanal)

DFS-Replikation ist ein Rollendienst in Windows Server, die effiziente Replizierung von Ordnern (einschließlich jenen, auf, die durch einen DFS-Namespacepfad verwiesen wird) über mehrere Server und Orte hinweg ermöglicht. Bei der DFS-Replikation handelt es sich um ein effizientes Replikationsmodul mit mehreren Mastern, mit dem Ordner zwischen Servern über Netzwerkverbindungen mit begrenzter Bandbreite fortlaufend synchronisiert werden können. Er ersetzt den Dateireplikationsdienst (FRS) als die Replikations-Engine aus, für die DFS-Namespaces sowie zum Replizieren des Ordners SYSVOL für Active Directory Domain Services (AD DS) in Domänen, die Windows Server 2008 oder höher Domänenfunktionsebene verwenden.

Für die DFS-Replikation wird ein Komprimierungsalgorithmus verwendet, der als Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) bezeichnet wird. Mit RDC werden Änderungen an den Daten in einer Datei erkannt, und es wird ermöglicht, dass mit der DFS-Replikation nur die geänderten Dateiblöcke repliziert werden und nicht die ganze Datei.

Weitere Informationen über die Replikation von SYSVOL mit DFS-Replikation finden Sie unter [migrieren Sie die SYSVOL-Replikation, DFS-Replikation](migrate-sysvol-to-dfsr.md).

Um die DFS-Replikation verwenden zu können, müssen Sie Replikationsgruppen erstellen und replizierte Ordner, die den Gruppen hinzufügen. Replikationsgruppen, replizierte Ordner und Elemente werden in der folgenden Abbildung dargestellt.

![Eine Replikationsgruppe, die eine Verbindung zwischen zwei Member enthält, replizierte jeweils mehrere Ordner](media\dfsr-overview.gif)

Diese Abbildung zeigt, dass eine Replikationsgruppe enthalten eine Gruppe von Servern, die als Mitglieder bezeichnet ist, die an einen oder mehrere replizierte Ordner der Replikation beteiligt ist. Ein replizierter Ordner ist ein Ordner, der auf jedem Mitglied synchronisiert bleibt. Es gibt zwei replizierte Ordner, in der Abbildung: Projekte und Vorschläge. Wenn die Daten in jeder replizierten Ordner geändert wird, werden die Änderungen in Verbindungen zwischen den Mitgliedern der Replikationsgruppe repliziert. Die Verbindungen zwischen allen Mitgliedern bilden die Replikationstopologie.
Erstellen mehrere replizierte Ordner, in einer einzelnen Replikationsgruppe vereinfacht den Prozess der Bereitstellung von replizierte Ordner, da die Topologie, Zeitplan und für die Replikationsgruppe für die bandbreitenbeschränkung für jeden replizierten Ordner gelten. Zum Bereitstellen zusätzlicher replizierte Ordner können Dfsradmin.exe oder eine führen Sie die Anweisungen des Assistenten Sie zum Definieren der lokale Pfad und die Berechtigungen für den neuen replizierten Ordner.

Jeden replizierten Ordner hat eindeutige Einstellungen, z. B. Dateien und Unterordner filtern, damit Sie verschiedene Dateien und Unterordner für jeden replizierten Ordner herausfiltern können.

Für jedes Element gespeicherten replizierten Ordner befinden sich auf unterschiedlichen Volumes in das Element, und der replizierte Ordner müssen nicht freigegebene Ordner oder Teil eines Namespaces sein. Allerdings erleichtert das DFS-Verwaltungs-Snap-in geben replizierten Ordner frei, und veröffentlichen Sie sie optional in einem vorhandenen Namespace.

Sie können die DFS-Replikation mithilfe von DFS-Verwaltung, DfsrAdmin und Dfsrdiag Befehle oder Skripts, die WMI-aufrufen verwalten.

## <a name="requirements"></a>Anforderungen

Vor dem Bereitstellen der DFS-Replikation müssen die Server wie folgt konfiguriert werden:

- Aktualisieren Sie das Schema der Active Directory Domain Services (AD DS), um Windows Server 2003 R2 oder höher schemaerweiterungen einzuschließen. Sie können keine schreibgeschützten replizierten Ordnern mit dem Windows Server 2003 R2 oder älteren schemaergänzungen.
- Stellen Sie sicher, dass sich alle Server in einer Replikationsgruppe in der gleichen Gesamtstruktur befinden. Eine serverübergreifende Replikation über verschiedene Gesamtstrukturen hinweg ist nicht möglich.
- Installieren Sie die DFS-Replikation auf allen Servern, die als Mitglieder einer Replikationsgruppe fungieren sollen.
- Erkundigen Sie sich beim Hersteller der verwendeten Antivirensoftware, ob diese mit der DFS-Replikation kompatibel ist.
- Ermitteln Sie sämtliche zu replizierende Ordner, die sich auf Volumes mit dem NTFS-Dateisystem befinden. Das robuste Dateisystem (Resilient File System, ReFS) und das FAT-Dateisystem werden von der DFS-Replikation nicht unterstützt. Auch eine Replizierung von Inhalten auf freigegebenen Clustervolumes wird von der DFS-Replikation nicht unterstützt.

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilität mit virtuellen Azure-Computern

Mithilfe der DFS-Replikation auf einem virtuellen Computer in Azure wurde mit Windows Server getestet; Es gibt jedoch einige Einschränkungen und Anforderungen, die Sie befolgen müssen.

- Wenn Sie einen Server, auf dem die DFS-Replikation nicht nur zum Replizieren des SYSVOL-Ordners verwendet wird, mithilfe von Momentaufnahmen oder gespeicherten Zuständen wiederherstellen, tritt bei der DFS-Replikation ein Fehler auf. In diesem Fall müssen spezielle Schritte zur Datenbankwiederherstellung ausgeführt werden. Dementsprechend sollten Sie keine virtuellen Computer exportieren, klonen oder kopieren. Weitere Informationen finden Sie in Artikel [2517913](http://support.microsoft.com/kb/2517913) in der Microsoft Knowledge Base sowie unter [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/).
- Wenn Sie Daten in einem replizierten Ordner sichern, der auf einem virtuellen Computer gehostet wird, müssen Sie die Sicherungssoftware vom virtuellen Gastcomputer verwenden.
- DFS-Replikation erfordert Zugriff auf physische oder virtualisierte Domänencontroller – es kann nicht direkt mit Azure AD kommunizieren.
- Die DFS-Replikation erfordert eine VPN-Verbindung zwischen Ihren lokalen Replikationsgruppenmitgliedern und allen in Azure-VMs gehosteten Mitgliedern. Sie müssen auch den lokalen Router (z. B. Forefront Threat Management Gateway) so konfigurieren, dass die VPN-Verbindung über die RPC-Endpunktzuordnung (Port 135) und einen zufällig zugewiesenen Port zwischen 49152 und 65535 weitergeleitet wird. Sie können das Cmdlet "Set-DfsrMachineConfiguration" oder das Befehlszeilentool Dfsrdiag verwenden, um einen statischen Port anstelle des zufälligen Ports anzugeben. Weitere Informationen zur Festlegung eines statischen Ports für die DFS-Replikation finden Sie unter [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration). Informationen über das Öffnen verknüpfter Ports für die Verwaltung von Windows Server finden Sie im Artikel [832017](http://support.microsoft.com/kb/832017) in der Microsoft Knowledge Base.

Weitere Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie auf der [Microsoft Azure web site](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="installing-dfs-replication"></a>Installieren DFS-Replikation

DFS-Replikation ist ein Bestandteil der Datei- und Speicherdienste-Rolle. Die Verwaltungstools für DFS (DFS-Verwaltung der DFS-Replikation-Modul für Windows PowerShell sowie Befehlszeilentools) werden separat als Teil der Remoteserver-Verwaltungstools installiert.

Installieren Sie DFS-Replikation mit [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), Server-Manager oder PowerShell, wie in den nächsten Abschnitten beschrieben.

### <a name="to-install-dfs-by-using-server-manager"></a>So installieren Sie DFS mithilfe des Server-Managers

1. Klicken Sie im Server-Manager auf **Verwalten** und anschließend auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.

2. Wählen Sie auf der Seite **Serverauswahl** den Server oder die virtuelle Festplatte (Virtual Hard Disk, VHD) eines virtuellen Computers im Offlinemodus aus, auf dem Sie DFS installieren möchten.

3. Wählen Sie die zu installierenden Rollendienste und Features aus.

    - So installieren Sie DFS-Replikationsdiensts, auf die **Serverrollen** Seite **DFS-Replikation**.

    - Erweitern Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools**, erweitern Sie **Rollenverwaltungstools**, erweitern Sie **Tools für Dateidienste**, und wählen Sie anschließend **DFS-Verwaltungstools** aus.

         **DFS-Verwaltungstools** installiert installiert die DFS-Verwaltungs-Snap-in, das DFS-Replikation und DFS-Namespaces-Module für Windows PowerShell und Befehlszeilentools, aber keine DFS-Dienste nicht auf dem Server.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>So installieren Sie DFS-Replikation mithilfe von Windows PowerShell

Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, und geben Sie dann den folgenden Befehl ein, wobei < Name\> ist der Rollendienst oder Feature, das Sie installieren möchten (siehe die folgende Tabelle enthält eine Liste mit relevanten Rollendienst- oder Featurenamen):

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

Um die DFS-Replikation und die Teile von DFS-Tools für das Feature der Remoteserver-Verwaltungstools zu installieren, geben Sie Folgendes ein:

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>Siehe auch

- [Übersicht über DFS-Namespaces und DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [Prüfliste: DFS-Replikation bereitstellen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [Prüfliste: Verwalten der DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [Bereitstellen von DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Verwalten von DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Problembehandlung bei der DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
