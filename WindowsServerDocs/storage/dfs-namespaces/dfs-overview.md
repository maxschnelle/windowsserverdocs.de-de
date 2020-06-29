---
title: Übersicht über DFS-Namespaces
ms.prod: windows-server
ms.author: jgerend
manager: daveba
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 06/07/2019
description: In diesem Thema werden DFS-Namespaces beschrieben, bei denen es sich um einen Rollen Dienst in Windows Server handelt, der es Ihnen ermöglicht, freigegebene Ordner auf verschiedenen Servern in einem oder mehreren logisch strukturierten Namespaces zu gruppieren.
ms.openlocfilehash: fd02f0b65cc57300c673d72c7879a80d48747fa2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471884"
---
# <a name="dfs-namespaces-overview"></a>Übersicht über DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (halbjährlicher Kanal)

DFS-Namespaces ist ein Rollen Dienst in Windows Server, der es Ihnen ermöglicht, freigegebene Ordner, die sich auf verschiedenen Servern befinden, in einem oder mehreren logisch strukturierten Namespaces zu gruppieren. Dies ermöglicht es, Benutzern eine virtuelle Ansicht von freigegebenen Ordnern zu ermöglichen, in der ein einzelner Pfad zu Dateien führt, die sich auf mehreren Servern befinden, wie in der folgenden Abbildung dargestellt:

![DFS-Namespaces-Technologieelemente](media/dfs-overview.png)

Im folgenden finden Sie eine Beschreibung der Elemente, die einen DFS-Namespace bilden:

- **Namespace Server** : ein Namespace Server hostet einen Namespace. Der Namespace Server kann ein Mitglieds Server oder ein Domänen Controller sein.
- **Namespace** Stamm: der Namespace Stamm ist der Ausgangspunkt des Namespace. In der vorherigen Abbildung ist der Name des Stamms öffentlich, und der Namespace Pfad lautet " \\ \\ \\ Public". Bei dieser Art von Namespace handelt es sich um einen domänenbasierten Namespace, weil er mit einem Domänen Namen (z. b. "Configuration Manager") beginnt und seine Metadaten in Active Directory Domain Services (AD DS) gespeichert sind. Obwohl ein einzelner Namespace Server in der vorherigen Abbildung dargestellt ist, kann ein Domänen basierter Namespace auf mehreren Namespace Servern gehostet werden, um die Verfügbarkeit des Namespace zu erhöhen.
- **Ordner** : Ordner ohne Ordner Ziele fügen dem-Namespace eine Struktur und eine Hierarchie hinzu, und Ordner mit Ordner Zielen stellen Benutzern tatsächlichen Inhalt bereit. Wenn Benutzer einen Ordner mit Ordner Zielen im-Namespace durchsuchen, erhält der Client Computer einen Verweis, der den Client Computer transparent an eines der Ordner Ziele weiterleitet.
- **Ordner Ziele** : ein Ordner Ziel ist der UNC-Pfad eines freigegebenen Ordners oder ein anderer Namespace, der einem Ordner in einem Namespace zugeordnet ist. Im Ordner Ziel werden Daten und Inhalte gespeichert. In der obigen Abbildung enthält der Ordner "Tools" zwei Ordner Ziele: einen in London und einen in New York, und der Ordner mit dem Namen "Schulungs Handbücher" verfügt über ein einzelnes Ordner Ziel in New York. Ein Benutzer, der die öffentlichen Software Tools von Configuration Manager durchsucht, \\ \\ \\ \\ wird in \\ \\ \\ \\ \\ \\ \\ Abhängigkeit von der Website, in der sich der Benutzer befindet, transparent an den freigegebenen Ordner LDN-SVR-01 Tools oder die Tools NYC-SVR-01 umgeleitet.

In diesem Thema wird erläutert, wie Sie DFS installieren, welche Neuerungen es gibt und wo Sie Evaluierungs-und Bereitstellungs Informationen finden.

Sie können Namespaces mithilfe der DFS-Verwaltung, der [DFS-Namespace (DFSN)-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps), des **dfsutil** -Befehls oder mithilfe von WMI-Skripts verwalten.

## <a name="server-requirements-and-limits"></a>Server Anforderungen und-Einschränkungen

Für die Ausführung der DFS-Verwaltung oder die Verwendung von DFS-Namespaces müssen keine zusätzlichen Hardware- oder Softwareanforderungen erfüllt werden.

Ein Namespace Server ist ein Domänen Controller oder Mitglieds Server, der einen Namespace hostet. Die Anzahl der Namespaces, die Sie auf einem Server hosten können, wird durch das Betriebssystem bestimmt, das auf dem Namespace Server ausgeführt wird.

Server, auf denen die folgenden Betriebssysteme ausgeführt werden, können mehrere Domänen basierte Namespaces zusätzlich zu einem einzelnen eigenständigen Namespace hosten.

- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter und Enterprise Edition
- Windows Server (Halbjährlicher Kanal)

Server, auf denen die folgenden Betriebssysteme ausgeführt werden, können einen einzelnen eigenständigen Namespace hosten:

- Windows Server 2008 R2 Standard

In der folgenden Tabelle werden zusätzliche Faktoren beschrieben, die bei der Auswahl von Servern zum Hosten eines Namespace zu berücksichtigen sind

| Server, auf dem eigenständige Namespaces gehostet werden | Server, auf dem Domänen basierte Namespaces gehostet werden |
| ---                                   |        ---                                |
| Muss ein NTFS-Volume enthalten, um den Namespace zu hosten.|Muss ein NTFS-Volume enthalten, um den Namespace zu hosten. |
| Kann ein Mitglieds Server oder ein Domänen Controller sein.|Muss ein Mitglieds Server oder Domänen Controller in der Domäne sein, in der der Namespace konfiguriert ist. (Diese Anforderung gilt für jeden Namespace Server, der einen bestimmten domänenbasierten Namespace hostet.) |
| Kann von einem Failovercluster gehostet werden, um die Verfügbarkeit des Namespace zu erhöhen.|Bei dem Namespace kann es sich nicht um eine geclusterte Ressource in einem Failovercluster handeln. Sie können jedoch den Namespace auf einem Server suchen, der auch als Knoten in einem Failovercluster fungiert, wenn Sie den Namespace so konfigurieren, dass nur lokale Ressourcen auf diesem Server verwendet werden. |

## <a name="installing-dfs-namespaces"></a>Installieren von DFS-Namespaces

DFS-Namespaces und die DFS-Replikation sind Teil der Rolle %%amp;quot;Datei- und Speicherdienste%%amp;quot;. Die Verwaltungstools für DFS (DFS-Verwaltung, das DFS-Namespaces-Modul für Windows PowerShell sowie Befehlszeilentools) werden separat im Rahmen der Remoteserver-Verwaltungstools installiert.

Installieren Sie DFS-Namespaces mithilfe des [Windows Admin Centers](../../manage/windows-admin-center/understand/windows-admin-center.md), Server-Manager oder PowerShell, wie in den folgenden Abschnitten beschrieben.

### <a name="to-install-dfs-by-using-server-manager"></a>So installieren Sie DFS mithilfe des Server-Managers

1. Klicken Sie im Server-Manager auf **Verwalten**und anschließend auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.

2. Wählen Sie auf der Seite **Serverauswahl** den Server oder die virtuelle Festplatte (Virtual Hard Disk, VHD) eines virtuellen Computers im Offlinemodus aus, auf dem Sie DFS installieren möchten.

3. Wählen Sie die zu installierenden Rollendienste und Features aus.

    - Um den DFS-Namespaces-Dienst zu installieren, wählen Sie auf der Seite **Server Rollen** die Option **DFS-Namespaces**aus.

    - Erweitern Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools**, erweitern Sie **Rollenverwaltungstools**, erweitern Sie **Tools für Dateidienste**, und wählen Sie anschließend **DFS-Verwaltungstools**aus.

         Im Rahmen der **** DFS-Verwaltungstools werden auf dem Server das DFS-Verwaltungs-Snap-In, das DFS-Namespaces-Modul für Windows PowerShell sowie Befehlszeilentools, aber keine DFS-Dienste installiert.

### <a name="to-install-dfs-by-using-windows-powershell"></a>So installieren Sie DFS mithilfe von Windows PowerShell

Öffne eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, und gib den folgenden Befehl ein, wobei <name\> für den zu installierenden Rollendienst bzw. für das zu installierende Feature steht. Eine Liste mit relevanten Rollendienst- oder Featurenamen findest du in der folgenden Tabelle:

```PowerShell
Install-WindowsFeature <name>
```

| Rollendienst oder Feature | Name |
| ----------------------- | ---- |
| DFS-Namespaces          | `FS-DFS-Namespace` |
| DFS-Verwaltungstools    | `RSAT-DFS-Mgmt-Con` |

Geben Sie beispielsweise Folgendes ein, um die DFS-Tools zu installieren, die Teil der Remoteserver-Verwaltungstools sind:

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

Geben Sie Folgendes ein, um die DFS-Namespaces und die verteiltes Dateisystem Tools-Komponenten des Remoteserver-Verwaltungstools Features zu installieren:

```PowerShell
Install-WindowsFeature "FS-DFS-Namespace", "RSAT-DFS-Mgmt-Con"
```

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilität mit virtuellen Azure-Computern

Die Verwendung von DFS-Namespaces auf einer virtuellen Maschine in Microsoft Azure wurde getestet. Es gibt jedoch einige Einschränkungen und Anforderungen, die Sie befolgen müssen.

- Sie können keine Cluster mit eigenständigen Namespaces auf virtuellen Azure-Computern gruppieren.

- Sie können Domänen basierte Namespaces auf virtuellen Azure-Computern hosten, einschließlich Umgebungen mit Azure Active Directory.

Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie in der [Dokumentation zu Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="additional-references"></a>Zusätzliche Referenzen

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

| Inhaltstyp        | Referenzen |
| ------------------  | ----------------|
| **Produktbewertung** | [Neues in DFS-Namespaces und DFS-Replikation in Windows Server](https://technet.microsoft.com/library/dn281957(v=ws.11).aspx) |
| **Bereitstellung**    | [Überlegungen zur Skalierbarkeit von DFS-Namespaces](https://blogs.technet.com/b/filecab/archive/2012/08/26/dfs-namespace-scalability-considerations.aspx) |
| **Vorgänge**    | [DFS-Namespaces: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee404780.aspx) |
| **Communityressourcen** | [TechNet-Forum für Dateidienste und Speicher](https://social.technet.microsoft.com/forums/winserverfiles/threads/) |
| **Protokolle**        | [Datei Dienst Protokolle in Windows Server](https://msdn.microsoft.com/library/cc239318.aspx) (veraltet) |
| **Verwandte Technologien** | [Failoverclustering](../../failover-clustering/failover-clustering-overview.md)|
| **Unterstützung** | [Windows IT Pro-Support](https://www.microsoft.com/itpro/windows/support)|
