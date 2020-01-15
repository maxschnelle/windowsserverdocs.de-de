---
title: Übersicht über DFS-Replikation
ms.date: 03/08/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 22f9e25763217cbbfdfd8a4ab099344f23138344
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949713"
---
# <a name="dfs-replication-overview"></a>Übersicht über DFS-Replikation

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (halbjährlicher Kanal)

DFS-Replikation ist ein Rollen Dienst in Windows Server, der es Ihnen ermöglicht, Ordner (einschließlich derjenigen, auf die durch einen DFS-Namespace Pfad verwiesen wird) über mehrere Server und Standorte effizient zu replizieren. Bei der DFS-Replikation handelt es sich um eine effiziente Replikations-Engine mit mehreren Mastern, mit der Ordner zwischen Servern über Netzwerkverbindungen mit begrenzter Bandbreite fortlaufend synchronisiert werden können. Er ersetzt den Datei Replikations Dienst (File Replication Service, FRS) als Replikations-Engine für DFS-Namespaces sowie zum Replizieren des Active Directory Domain Services (AD DS) SYSVOL-Ordners in Domänen, die die Domänen Funktionsebene Windows Server 2008 oder höher verwenden.

Für die DFS-Replikation wird ein Komprimierungsalgorithmus verwendet, der als Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) bezeichnet wird. Mit RDC werden Änderungen an den Daten in einer Datei erkannt, und es wird ermöglicht, dass mit der DFS-Replikation nur die geänderten Dateiblöcke repliziert werden und nicht die ganze Datei.

Weitere Informationen zum Replizieren von SYSVOL mithilfe von DFS-Replikation finden Sie unter [Migrieren der SYSVOL-Replikation zu DFS-Replikation](migrate-sysvol-to-dfsr.md).

Wenn Sie DFS-Replikation verwenden möchten, müssen Sie Replikations Gruppen erstellen und den Gruppen replizierte Ordner hinzufügen. Replikations Gruppen, replizierte Ordner und Mitglieder sind in der folgenden Abbildung dargestellt.

![Eine Replikations Gruppe, die eine Verbindung zwischen zwei Mitgliedern enthält, die jeweils über ein paar replizierte Ordner verfügen](media/dfsr-overview.gif)

Diese Abbildung zeigt, dass eine Replikations Gruppe eine Gruppe von Servern ist, die als Mitglieder bezeichnet werden und an der Replikation von mindestens einem replizierten Ordner beteiligt sind. Ein replizierter Ordner ist ein Ordner, der für jedes Mitglied synchronisiert bleibt. In der Abbildung gibt es zwei replizierte Ordner: Projekte und Vorschläge. Wenn sich die Daten in jedem replizierten Ordner ändern, werden die Änderungen über die Verbindungen zwischen den Mitgliedern der Replikations Gruppe repliziert. Die Verbindungen zwischen allen Membern bilden die Replikations Topologie.
Wenn Sie mehrere replizierte Ordner in einer einzelnen Replikations Gruppe erstellen, wird das Bereitstellen von replizierten Ordnern vereinfacht, da die Topologie, der Zeitplan und die Bandbreiten Einschränkung für die Replikations Gruppe auf jeden replizierten Ordner angewendet werden. Zum Bereitstellen zusätzlicher replizierter Ordner können Sie Dfsradmin. exe verwenden oder die Anweisungen in einem Assistenten befolgen, um den lokalen Pfad und die Berechtigungen für den neuen replizierten Ordner zu definieren.

Jeder replizierte Ordner weist eindeutige Einstellungen auf, wie z. b. Datei-und Unterordner Filter, sodass Sie verschiedene Dateien und Unterordner für jeden replizierten Ordner herausfiltern können.

Die in jedem Element gespeicherten replizierten Ordner können sich auf unterschiedlichen Volumes im Mitglied befinden, und die replizierten Ordner müssen keine freigegebenen Ordner oder Teile eines Namespaces sein. Mit dem DFS-Verwaltungs-Snap-in können Sie jedoch problemlos replizierte Ordner freigeben und optional in einem vorhandenen Namespace veröffentlichen.

Sie können DFS-Replikation mithilfe der DFS-Verwaltung, mit den Dfsradmin-und Dfsrdiag-Befehlen oder mithilfe von Skripts, die WMI anrufen, verwalten.

## <a name="requirements"></a>Anforderungen

Vor dem Bereitstellen der DFS-Replikation müssen die Server wie folgt konfiguriert werden:

- Aktualisieren Sie das Schema Active Directory Domain Services (AD DS), sodass es Windows Server 2003 R2 oder spätere Schema Ergänzungen einschließt. Sie können keine schreibgeschützten replizierten Ordner mit den Schema Ergänzungen für Windows Server 2003 R2 oder älter verwenden.
- Stellen Sie sicher, dass sich alle Server in einer Replikationsgruppe in der gleichen Gesamtstruktur befinden. Eine serverübergreifende Replikation über verschiedene Gesamtstrukturen hinweg ist nicht möglich.
- Installieren Sie die DFS-Replikation auf allen Servern, die als Mitglieder einer Replikationsgruppe fungieren sollen.
- Erkundigen Sie sich beim Hersteller der verwendeten Antivirensoftware, ob diese mit der DFS-Replikation kompatibel ist.
- Ermitteln Sie sämtliche zu replizierende Ordner, die sich auf Volumes mit dem NTFS-Dateisystem befinden. Das robuste Dateisystem (Resilient File System, ReFS) und das FAT-Dateisystem werden von der DFS-Replikation nicht unterstützt. Auch eine Replizierung von Inhalten auf freigegebenen Clustervolumes wird von der DFS-Replikation nicht unterstützt.

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilität mit virtuellen Azure-Computern

Die Verwendung von DFS-Replikation auf einem virtuellen Computer in Azure wurde mit Windows Server getestet. Es gibt jedoch einige Einschränkungen und Anforderungen, die Sie befolgen müssen.

- Wenn Sie einen Server, auf dem die DFS-Replikation nicht nur zum Replizieren des SYSVOL-Ordners verwendet wird, mithilfe von Momentaufnahmen oder gespeicherten Zuständen wiederherstellen, tritt bei der DFS-Replikation ein Fehler auf. In diesem Fall müssen spezielle Schritte zur Datenbankwiederherstellung ausgeführt werden. Ebenso sollten Sie die virtuellen Computer nicht exportieren, Klonen oder kopieren. Weitere Informationen finden Sie in Artikel [2517913](https://support.microsoft.com/kb/2517913) in der Microsoft Knowledge Base sowie unter [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/).
- Wenn Sie Daten in einem replizierten Ordner sichern, der auf einem virtuellen Computer gehostet wird, müssen Sie die Sicherungssoftware vom virtuellen Gastcomputer verwenden.
- DFS-Replikation erfordert Zugriff auf physische oder virtuelle Domänen Controller – es ist nicht möglich, direkt mit Azure AD zu kommunizieren.
- Die DFS-Replikation erfordert eine VPN-Verbindung zwischen Ihren lokalen Replikationsgruppenmitgliedern und allen in Azure-VMs gehosteten Mitgliedern. Sie müssen auch den lokalen Router (z. B. Forefront Threat Management Gateway) so konfigurieren, dass die VPN-Verbindung über die RPC-Endpunktzuordnung (Port 135) und einen zufällig zugewiesenen Port zwischen 49152 und 65535 weitergeleitet wird. Sie können das Cmdlet Set-dfsrmachineconfiguration oder das Befehlszeilen Tool Dfsrdiag verwenden, um anstelle des zufälligen Ports einen statischen Port anzugeben. Weitere Informationen zur Festlegung eines statischen Ports für die DFS-Replikation finden Sie unter [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration). Informationen über das Öffnen verknüpfter Ports für die Verwaltung von Windows Server finden Sie im Artikel [832017](https://support.microsoft.com/kb/832017) in der Microsoft Knowledge Base.

Weitere Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie auf der [Microsoft Azure web site](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="installing-dfs-replication"></a>Installieren von DFS-Replikation

DFS-Replikation ist ein Teil der Datei-und Speicherdienste-Rolle. Die Verwaltungs Tools für DFS (DFS-Verwaltung, das DFS-Replikation-Modul für Windows PowerShell und Befehlszeilen Tools) werden separat als Teil der Remoteserver-Verwaltungstools installiert.

Installieren Sie DFS-Replikation, indem Sie das [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), Server-Manager oder PowerShell verwenden, wie in den folgenden Abschnitten beschrieben.

### <a name="to-install-dfs-by-using-server-manager"></a>So installieren Sie DFS mithilfe des Server-Managers

1. Klicken Sie im Server-Manager auf **Verwalten**und anschließend auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.

2. Wählen Sie auf der Seite **Serverauswahl** den Server oder die virtuelle Festplatte (Virtual Hard Disk, VHD) eines virtuellen Computers im Offlinemodus aus, auf dem Sie DFS installieren möchten.

3. Wählen Sie die zu installierenden Rollendienste und Features aus.

    - Wählen Sie zum Installieren des DFS-Replikation Dienstanbieter auf der Seite **Server Rollen** die Option **DFS-Replikation**aus.

    - Erweitern Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools**, erweitern Sie **Rollenverwaltungstools**, erweitern Sie **Tools für Dateidienste**, und wählen Sie anschließend **DFS-Verwaltungstools**aus.

         Die **DFS-Verwaltungs Tools** installieren das DFS-Verwaltungs-Snap-in, die DFS-Replikation-und DFS-Namespaces-Module für Windows PowerShell sowie Befehlszeilen Tools, aber es werden keine DFS-Dienste auf dem Server installiert.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>So installieren Sie DFS-Replikation mithilfe von Windows PowerShell

Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, und geben Sie dann den folgenden Befehl ein, wobei < Name\> der Rollen Dienst oder das Feature ist, das Sie installieren möchten (in der folgenden Tabelle finden Sie eine Liste der relevanten Rollen Dienst-oder Featurenamen):

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

Geben Sie Folgendes ein, um die DFS-Replikation und die verteiltes Dateisystem Tools des Remoteserver-Verwaltungstools Features zu installieren:

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>Weitere Informationen:

- [Übersicht über DFS-Namespaces und-DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [Prüfliste: Bereitstellen DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [Prüfliste: Verwalten von DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [Bereitstellen von DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Verwalten von DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Problembehandlung DFS-Replikation](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
