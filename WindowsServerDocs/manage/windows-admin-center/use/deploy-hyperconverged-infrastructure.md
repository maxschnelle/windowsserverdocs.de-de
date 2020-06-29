---
title: Bereitstellen hyperkonvergierter Infrastrukturen mit dem Windows Admin Center
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.prod: windows-server
ms.technology: manage
ms.date: 11/04/2019
ms.openlocfilehash: 088fb7b8f03ab7e575b562572f2e29e1b5774760
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474487"
---
# <a name="deploy-hyperconverged-infrastructure-with-windows-admin-center"></a>Bereitstellen hyperkonvergierter Infrastrukturen mit dem Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Sie können Windows Admin Center, [Version 1910](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) oder höher, verwenden, um eine hyperkonvergierte Infrastruktur mithilfe von mindestens zwei passenden Windows-Servern bereitzustellen. Dieses neue Feature ist ein mehrstufiger Workflow, der Sie durch die Installation von Features, das Konfigurieren von Netzwerken, das Erstellen des Clusters und das Bereitstellen von direkte Speicherplätze und/oder Software-Defined Networking (SDN) (sofern ausgewählt) führt.

![Screenshot des Workflows für die Cluster Erstellung](../media/deploy-hyperconverged-infrastructure/deployment-workflow-screenshot.png)

  > [!Important]
  > Diese Funktion befindet sich in der aktiven Entwicklung. Es ist in der Vorschau verfügbar, sodass Sie es früh ausprobieren und Feedback geben können.

## <a name="preview-the-workflow"></a>Anzeigen einer Vorschau des Workflows

### <a name="1-prerequisites"></a>1. Voraussetzungen

Der Clustererstellungs-Workflow im Windows Admin Center führt keine Bare-Metal-Betriebssystem Installation aus. Daher müssen Sie Windows Server zunächst auf jedem Server installieren. Die unterstützten Versionen sind Windows Server 2016, Windows Server 2019 und Windows Server Insider Preview. Sie müssen jeden Server auch der gleichen Active Directory Domäne beitreten, in der das Windows Admin Center ausgeführt wird, bevor Sie den Workflow starten.

### <a name="2-install-windows-admin-center"></a>2. Installieren Sie das Windows Admin Center.

Befolgen Sie die Anweisungen zum [herunterladen und installieren](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) der neuesten Version von Windows Admin Center.

### <a name="3-install-the-cluster-creation-extension"></a>3. Installieren der Erweiterung für die Cluster Erstellung

Der Workflow für die Cluster Erstellung wird über den Windows Admin Center-Erweiterungs Feed übermittelt und aktualisiert. Dadurch können wir uns Ihr Feedback widmen und während der Vorschau Phase schneller Verbesserungen vornehmen.

Um die Erweiterung zu installieren, starten Sie Windows Admin Center und dann Folgendes:

1.  Wählen Sie in der oberen rechten Ecke das Symbol "Einstellungen" aus.
2.  Navigieren zu Erweiterungen
3.  Suchen der Erweiterung für die Cluster Erstellung
4.  Wählen Sie installieren

![Screenshots der vier Schritte zum Installieren der Erweiterung für die Cluster Erstellung](../media/deploy-hyperconverged-infrastructure/how-to-install.png)

Wählen Sie nach der Installation in der Dropdown Liste in der oberen linken Ecke die Erweiterung für die Cluster Erstellung aus:

![Screenshot des Starts der Erweiterung für die Cluster Erstellung](../media/deploy-hyperconverged-infrastructure/how-to-launch.png)

## <a name="limitations-of-the-preview-release"></a>Einschränkungen der Vorschauversion

Der Clustererstellungs-Workflow befindet sich in der aktiven Entwicklung – mit anderen Worten, er ist nicht fertig.

Im folgenden sind einige Einschränkungen der aktuellen Vorschauversion aufgeführt:

1.  **Domänen Anforderungen.** Der Workflow erfordert derzeit, dass jeder Server, den Sie hinzufügen, bereits mit derselben Active Directory Domäne verknüpft ist, in der Windows Admin Center ausgeführt wird.
2.  **Skript anzeigen.** Mit der aktuellen Vorschauversion können Sie die Skripts, die der Workflow ausführt, nicht mithilfe der Skript Funktionalität anzeigen im Windows Admin Center anzeigen, und Sie können auch keinen vollständigen Bericht zu allen Vorgängen herunterladen, die am Ende aufgetreten sind. Wir wissen, dass dies für viele Benutzer wichtig ist – bleiben Sie dran. Verwenden Sie in der Zwischenzeit die unten angegebenen Cmdlets, um zu [sehen, was passiert](#see-whats-happening).
3.  **Fortsetzen oder wieder starten.** Obwohl Sie Teile durch den Workflow beenden können, verarbeitet das aktuelle Vorschau Release nicht das fortsetzen, wo Sie aufgehört haben, und kann es nicht vollständig bereinigen, bevor Sie beginnen. Wenn Sie für Tests wiederholt auf denselben Servern bereitstellen möchten, verwenden Sie die unten angegebenen Cmdlets, um den Vorgang [rückgängig zu machen und zu starten](#undo-and-start-over).
4.  **Remote Zugriff auf den direkten Speicher (RDMA).** Das aktuelle Vorschau Release kann RDMA-Netzwerke nicht aktivieren, die häufig mit hyperkonvergierter Infrastruktur verwendet werden. Vervollständigen Sie den Workflow vorerst, ohne RDMA zu aktivieren, und verwenden Sie dann andere Tools, um RDMA genau wie sonst zu aktivieren.

Abgesehen von der Behebung dieser Einschränkungen gibt es unzählige potenzielle Features, die in zukünftigen Versionen hinzugefügt werden können: Anwenden von Windows-Updates, Konfigurieren eines Zeugen für das Cluster Quorum, importieren virtueller Maschinen usw. Um uns bei der Priorisierung der gewünschten Features zu unterstützen, teilen Sie uns das [Feedback](#feedback) wie unten beschrieben mit.

## <a name="see-whats-happening"></a>Sehen Sie sich an, was passiert

Verwenden Sie diese Windows PowerShell-Cmdlets, um zu sehen, wie der Workflow ausgeführt wird.

Verwenden Sie das-Cmdlet, um anzuzeigen, welche Windows-Features installiert sind `Get-WindowsFeature` . Beispiel:

```PowerShell
Get-WindowsFeature "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "BitLocker"
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-1.png)

  > [!Note]
  > Welche Features installiert werden, hängt vom Typ des ausgewählten Clusters ab.

So zeigen Sie Netzwerkadapter und deren Eigenschaften an, z. B. Name, IPv4-Adressen und VLAN-ID:

```PowerShell
Get-NetAdapter | Where Status -Eq "Up" | Sort InterfaceAlias | Format-Table Name, InterfaceDescription, Status, LinkSpeed, VLANID, MacAddress
Get-NetAdapter | Where Status -Eq "Up" | Get-NetIPAddress -AddressFamily IPv4 -ErrorAction SilentlyContinue | Sort InterfaceAlias | Format-Table InterfaceAlias, IPAddress, PrefixLength
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-2.png)

So zeigen Sie virtuelle Hyper-V-Switches und die Kombination von physischen Netzwerkadaptern an:

```PowerShell
Get-VMSwitch
Get-VMSwitchTeam
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-3.png)

Führen Sie zum Anzeigen der virtuellen Netzwerkadapter des Hosts ggf. Folgendes aus:

```PowerShell
Get-VMNetworkAdapter -ManagementOS | Format-Table Name, IsManagementOS, SwitchName
Get-VMNetworkAdapterTeamMapping -ManagementOS | Format-Table NetAdapterName, ParentAdapter
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-4.png)

Führen Sie Folgendes aus, um den aktuellen Failovercluster und dessen Mitglieds Knoten anzuzeigen:

```PowerShell
Get-Cluster
Get-ClusterNode
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-5.png)

So überprüfen Sie, ob direkte Speicherplätze aktiviert ist und den Standard Speicherpool, der automatisch erstellt wird:

```PowerShell
Get-ClusterStorageSpacesDirect
Get-StoragePool -IsPrimordial $False
```

![Screenshot der PowerShell-Ausgabe](../media/deploy-hyperconverged-infrastructure/script-out-6.png)

## <a name="undo-and-start-over"></a>Rückgängig machen und beginnen

Verwenden Sie diese Windows PowerShell-Cmdlets, um vom Workflow vorgenommene Änderungen rückgängig zu machen und zu beginnen.

### <a name="remove-virtual-machines-or-other-clustered-resources"></a>Entfernen von virtuellen Computern oder anderen geclusterten Ressourcen

Wenn Sie virtuelle Computer oder andere geclusterte Ressourcen erstellt haben, z. b. die Netzwerk Controller für Software-Defined Networking, entfernen Sie Sie zuerst.

Verwenden Sie z. b. Folgendes, um Ressourcen nach dem Namen zu entfernen:

```PowerShell
Get-ClusterResource -Name "<NAME>" | Remove-ClusterResource
```

### <a name="undo-the-storage-steps"></a>Rückgängig machen der Speicher Schritte

Wenn Sie direkte Speicherplätze aktiviert haben, deaktivieren Sie dieses Skript:

> [!Warning]
> Mit diesen Cmdlets werden alle Daten in direkte Speicherplätze Volumes dauerhaft gelöscht. Dies kann nicht rückgängig gemacht werden.

```PowerShell
Get-VirtualDisk | Remove-VirtualDisk
Get-StoragePool -IsPrimordial $False | Remove-StoragePool
Disable-ClusterS2D
```

### <a name="undo-the-clustering-steps"></a>Rückgängig machen der Clustering-Schritte

Wenn Sie einen Cluster erstellt haben, entfernen Sie ihn mit diesem Cmdlet:

```PowerShell
Remove-Cluster -CleanUpAD
```

Um auch Cluster Validierungs Berichte zu entfernen, führen Sie dieses Cmdlet auf jedem Server aus, der Teil des Clusters war:

```PowerShell
Get-ChildItem C:\Windows\cluster\Reports\ | Remove-Item
```

### <a name="undo-the-networking-steps"></a>Rückgängigmachen der Netzwerk Schritte

Führen Sie diese Cmdlets auf jedem Server aus, der Teil des Clusters war.

Wenn Sie einen virtuellen Hyper-V-Switch erstellt haben:

```PowerShell
Get-VMSwitch | Remove-VMSwitch
```

> [!Note]
> `Remove-VMSwitch`Mit dem-Cmdlet werden alle virtuellen Adapter automatisch entfernt, und der Switch-Embedded-Team Vorgang physischer Adapter wird rückgängig machen.

Wenn Sie die Eigenschaften des Netzwerkadapters geändert haben, z. b. Name, IPv4-Adresse und VLAN-ID:

> [!Warning]
> Mit diesen Cmdlets werden Netzwerkadapter Namen und IP-Adressen entfernt. Stellen Sie sicher, dass Sie über die erforderlichen Informationen verfügen, um eine Verbindung herzustellen, z. b. einen Adapter für die Verwaltung, der aus dem folgenden Skript ausgeschlossen wird. Stellen Sie außerdem sicher, dass Sie wissen, wie die Server in Bezug auf physische Eigenschaften wie Mac-Adresse, nicht nur den Namen des Adapters in Windows verbunden sind.

```PowerShell
Get-NetAdapter | Where Name -Ne "Management" | Rename-NetAdapter -NewName $(Get-Random)
Get-NetAdapter | Where Name -Ne "Management" | Get-NetIPAddress -ErrorAction SilentlyContinue | Where AddressFamily -Eq IPv4 | Remove-NetIPAddress
Get-NetAdapter | Where Name -Ne "Management" | Set-NetAdapter -VlanID 0
```

Sie sind jetzt bereit, um den Workflow zu starten.

## <a name="feedback"></a>Feedback

In dieser Vorschauversion geht es um Ihr Feedback. Hier sind einige Möglichkeiten, wie Sie unser Team erreichen können:

- [Übermitteln und abstimmen von featureanfragen auf UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Besuchen Sie das Forum zum Windows Admin Center in der Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- E-Mail HCI-Bereitstellung [at] Microsoft.com
- Tweet zu[@servermgmt](https://twitter.com/servermgmt)

## <a name="report-an-issue"></a>Melden eines Problems

Verwenden Sie die oben aufgeführten Kanäle, um ein Problem mit dem Cluster Erstellungs Workflow zu melden.

Fügen Sie nach Möglichkeit die folgenden Informationen ein, um uns bei der schnellen Reproduktion und Lösung Ihres Problems zu unterstützen:

- Typ des Clusters, den Sie ausgewählt haben (Beispiel: *"hyperkonvergiert"*)
- Schritt, in dem das Problem aufgetreten ist (Beispiel: *"3,2 CREATE Cluster"*)
- Version der Erweiterung für die Cluster Erstellung. Wechseln Sie zu **Einstellungen**  >  **Erweiterungen**  >  **installierte Erweiterungen** , und sehen Sie sich die Spalte **Version** an (Beispiel: *"1.0.30"*).
- Fehlermeldungen, ob auf dem Bildschirm oder in der Browser Konsole, die Sie öffnen können, indem Sie **F12**drücken.
- Alle anderen relevanten Informationen zu Ihrer Umgebung

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Hallo, Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)
- [Bereitstellen von direkten Speicherplätzen](https://docs.microsoft.com/windows-server/storage/storage-spaces/deploy-storage-spaces-direct)
