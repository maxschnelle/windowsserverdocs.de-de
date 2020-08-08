---
title: Cluster Sätze
manager: eldenc
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/30/2019
description: Dieser Artikel beschreibt das Szenario mit Cluster Sätzen.
ms.localizationpriority: medium
ms.openlocfilehash: b5b3f36cbc6627b13d2bba678cc1aeec02e57d81
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961164"
---
# <a name="cluster-sets"></a>Clustergruppen

> Gilt für: Windows Server 2019

Cluster Sätze sind die neue Cloud-Technologie für horizontales Skalieren in der Windows Server 2019-Version, die die Anzahl der Cluster Knoten in einer einzelnen SDDC-Cloud (Software-Defined Data Center) in der Größe vergrößert. Bei einem Cluster Satz handelt es sich um eine lose gekoppelte Gruppierung mehrerer Failovercluster: COMPUTE-, Speicher-oder hyperkonvergierte Gruppierungen. Die Technologie von Cluster Sätzen ermöglicht die Flüssigkeit der virtuellen Maschine über Mitglieder Cluster innerhalb eines Cluster Satzes hinweg und einen vereinheitlichten Speicher Namespace über die Menge hinweg, um die Geschwindigkeit virtueller Computer zu unterstützen.

Bei der Beibehaltung der vorhandenen Failovercluster-Verwaltungsfunktionen auf Mitglieds Clustern bietet eine clusterset-Instanz zusätzlich wichtige Anwendungsfälle im Zusammenhang mit der Lebenszyklus Verwaltung für das Aggregat. Dieses Evaluierungs Handbuch für Windows Server 2019-Szenarien bietet Ihnen die erforderlichen Hintergrundinformationen sowie schrittweise Anleitungen zum Auswerten von Clustergruppen mithilfe von PowerShell.

## <a name="technology-introduction"></a>Einführung in die Technologie

Die Technologie von Cluster Sätzen wird so entwickelt, dass bestimmte Kundenanforderungen bei der Skalierung von Betriebs Software definierte Rechenzentrums Clouds (SDDC) erfüllt werden. Der Wert eines Cluster Sets kann wie folgt zusammengefasst werden:

- Erhöhen Sie die unterstützte SDDC-cloudskalierung für die Ausführung hoch verfügbarer virtueller Computer, indem Sie mehrere kleinere Cluster in einem einzelnen großen Fabric kombinieren, auch wenn die Softwarefehler Grenze auf einem einzelnen Cluster beibehalten wird.
- Verwalten des gesamten failoverclusterlebens Zyklus, einschließlich des Onboarding-und Außerbetriebnahme von Clustern, ohne Auswirkungen auf die Verfügbarkeit der Mandanten-VMS zu haben
- Einfaches Ändern der COMPUTE-zu-Speicher-Quote in der hyperkonvergierten I
- Profitieren Sie von [Azure-ähnlichen Fehler Domänen und Verfügbarkeits Gruppen](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) über Cluster hinweg bei der ersten Platzierung virtueller Maschinen und der nachfolgenden Migration virtueller Computer
- Kombinieren Sie verschiedene Generationen von CPU-Hardware mit dem gleichen Cluster Satz-Fabric, auch wenn Sie die einzelnen Fehler Domänen für maximale Effizienz einheitlich halten. Beachten Sie, dass die Empfehlung der gleichen Hardware immer noch in jedem einzelnen Cluster und dem gesamten Cluster Satz vorhanden ist.

Aus einer Ansicht auf hoher Ebene können Cluster Sätze aussehen.

![Lösungs Ansicht für Cluster Sätze](media/Cluster-sets-Overview/Cluster-sets-solution-View.png)

Im folgenden finden Sie eine kurze Zusammenfassung der einzelnen Elemente in der obigen Abbildung:

**Verwaltungscluster**

Bei einem Verwaltungs Cluster in einem Cluster Satz handelt es sich um einen Failovercluster, der die hoch verfügbare Verwaltungsebene des gesamten Cluster Satzes und des Unified Storage-Namespace (Cluster Satz Namespace) für den Verweis Dateiserver mit horizontaler Skalierung (sofs) hostet. Ein Verwaltungs Cluster ist logisch von Mitglieds Clustern entkoppelt, von denen die Arbeits Auslastungen virtueller Computer ausgeführt werden. Dadurch kann die Verwaltungsebene des Clusters anfällig für alle lokalisierten Cluster weiten Fehler sein, z. b. einen Stromausfall eines Mitglieds Clusters.

**Mitglieds Cluster**

Bei einem Mitglieds Cluster in einem Cluster Satz handelt es sich in der Regel um einen herkömmlichen hyperkonvergenten Cluster mit virtuellen Maschinen und direkte Speicherplätze Workloads. Mehrere Mitglieds Cluster sind Teil einer einzelnen Cluster Satz Bereitstellung und bilden so das größere SDDC-Cloud-Fabric. Mitglieds Cluster unterscheiden sich in zwei wichtigen Aspekten von einem Verwaltungs Cluster: Mitglieds Cluster sind Teil der Fehler Domänen-und Verfügbarkeits Gruppen-Konstrukte, und Mitglieds Cluster sind ebenfalls zum Hosten virtueller Maschinen und direkte Speicherplätze Arbeits Auslastungen skaliert. Virtuelle Computer für Clustergruppen, die über Cluster Grenzen in einem Cluster Satz hinweg verschoben werden, dürfen aus diesem Grund nicht auf dem Verwaltungs Cluster gehostet werden.

**Cluster Satz-Namespace Verweis-sofs**

Ein Cluster Satz-Namespace Verweis (Cluster Set Namespace) sofs ist eine Dateiserver mit horizontaler Skalierung, wobei jede SMB-Freigabe auf dem Cluster Satz Namespace sofs eine Verweis Freigabe – vom Typ "simplereferral" ist, die in Windows Server 2019 neu eingeführt wurde. Mit diesem Verweis können SMB-Clients (Server Message Block) auf die SMB-Ziel Freigabe zugreifen, die auf dem Mitglieds Cluster-sofs gehostet wird. Der clusterset-Namespace Verweis-sofs ist ein einfacher Verweis Mechanismus und ist daher nicht Teil des e/a-Pfads. Die SMB-Verweise werden auf den einzelnen Client Knoten ständig zwischengespeichert, und der Cluster legt Namespaces automatisch automatisch aktualisiert.

**Cluster Satz Master**

In einem Cluster Satz ist die Kommunikation zwischen den Mitglieds Clustern lose gekoppelt und wird von einer neuen Cluster Ressource mit dem Namen "Cluster Satz Master" (CS-Master) koordiniert. Wie jede andere Cluster Ressource ist CS-Master hoch verfügbar und anfällig für Cluster Ausfälle einzelner Mitglieder und/oder Fehler des Verwaltungs Cluster Knotens. Über einen neuen Cluster Satz-WMI-Anbieter stellt CS-Master den Verwaltungs Endpunkt für alle Interaktionen mit der Verwaltbarkeit von Clustergruppen bereit.

**Cluster Satz-Worker**

In einer Cluster Satz Bereitstellung interagiert der CS-Master mit einer neuen Cluster Ressource auf den Mitglieds Clustern, die als "clusterset-Worker" (CS-Worker) bezeichnet werden. CS-Worker fungiert als einzige Verbindung auf dem Cluster, um die lokalen Cluster Interaktionen zu orchestrieren, die vom CS-Master angefordert werden. Beispiele für derartige Interaktionen sind z. b. die Platzierung virtueller Maschinen und die Ressourcen Inventur für lokale Cluster Ressourcen. Es gibt nur eine CS-Worker-Instanz für jeden Mitglieds Cluster in einem Cluster Satz.

**Fehler Domäne**

Eine Fehler Domäne ist die Gruppierung von Software-und Hardware Artefakten, die der Administrator beim Auftreten eines Fehlers möglicherweise fehlschlägt. Obwohl ein Administrator einen oder mehrere Cluster als Fehler Domäne bezeichnen könnte, könnte jeder Knoten in einer Fehler Domäne in einer Verfügbarkeits Gruppe teilnehmen. Cluster Sätze werden Überlegungen zur Identifizierung von Fehler Domänen an den Administrator weitergeleitet, der mit den Überlegungen zur Topologie von Rechenzentren gut vertraut ist – z. b. PDU, Netzwerk –, die Mitglied Cluster gemeinsam nutzen.

**Verfügbarkeitsgruppe**

Eine Verfügbarkeits Gruppe unterstützt den Administrator dabei, die gewünschte Redundanz von gruppierten Arbeits Auslastungen für Fehler Domänen zu konfigurieren, indem Sie diese in einer Verfügbarkeits Gruppe organisieren und Workloads in dieser Verfügbarkeits Gruppe Nehmen wir an, wenn Sie eine Anwendung mit zwei Ebenen bereitstellen, empfehlen wir, dass Sie mindestens zwei virtuelle Computer in einer Verfügbarkeits Gruppe für jede Ebene konfigurieren, um sicherzustellen, dass bei Ausfall einer Fehler Domäne in dieser Verfügbarkeits Gruppe mindestens ein virtueller Computer auf jeder Ebene in einer anderen Fehler Domäne derselben Verfügbarkeits Gruppe gehostet wird.

## <a name="why-use-cluster-sets"></a>Gründe für die Verwendung von Cluster Sätzen

Cluster Sätze bieten den Vorteil der Skalierung, ohne die Resilienz zu beeinträchtigen.

Cluster Sätze ermöglichen das Clustering mehrerer Cluster, um ein großes Fabric zu erstellen, während jeder Cluster unabhängig von der Resilienz bleibt. Beispielsweise verfügen Sie über mehrere HCI-Cluster mit 4 Knoten, auf denen virtuelle Computer ausgeführt werden. Jeder Cluster bietet die erforderliche Resilienz für sich selbst. Wenn der Speicher oder der Arbeitsspeicher aufgefüllt wird, ist das zentrale hochskalieren der nächste Schritt. Beim zentralen hochskalieren gibt es einige Optionen und Überlegungen.

1. Fügen Sie dem aktuellen Cluster weiteren Speicherplatz hinzu. Mit direkte Speicherplätze kann dies schwierig sein, da genau dieselbe Modell-/firmwarelaufwerke nicht verfügbar sind. Die Überlegung der Neuerstellungs Zeiten muss ebenfalls berücksichtigt werden.
2. Fügen Sie weiteren Arbeitsspeicher hinzu. Was geschieht, wenn Sie den Arbeitsspeicher, der von den Computern verarbeitet werden kann, abgleichen?  Was geschieht, wenn alle verfügbaren Speicher Slots voll sind?
3. Fügen Sie dem aktuellen Cluster zusätzliche Computeknoten mit Laufwerken hinzu. Dadurch wird die Option 1 benötigt.
4. Erwerben eines vollständigen neuen Clusters

An dieser Stelle bietet Cluster Sätze den Vorteil der Skalierung. Wenn ich meine Cluster zu einem Cluster Satz hinzufüge, kann ich Speicher oder Arbeitsspeicher nutzen, der in einem anderen Cluster möglicherweise ohne zusätzliche Käufe verfügbar ist. Aus Sicht der Resilienz bietet das Hinzufügen zusätzlicher Knoten zu einem direkte Speicherplätze keine weiteren Stimmen für das Quorum. Wie [hier](drive-symmetry-considerations.md)erwähnt, kann ein direkte Speicherplätze Cluster den Verlust von zwei Knoten überstehen, bevor er ausfällt. Wenn Sie über einen HCI-Cluster mit vier Knoten verfügen, wird der gesamte Cluster durch 3 Knoten herunterfahren. Wenn Sie über einen Cluster mit 8 Knoten verfügen, wird der gesamte Cluster durch 3 Knoten herunterfahren. Bei Cluster Sätzen mit zwei HCI-Clustern mit 4 Knoten in der Gruppe werden zwei Knoten in einem HCI heruntergeschaltet und ein Knoten im anderen HCI heruntergeschaltet. beide Cluster bleiben erhalten. Empfiehlt es sich, einen großen 16-Knoten-direkte Speicherplätze Cluster zu erstellen oder in vier Knoten mit vier Knoten zu unterbrechen und Cluster Sätze zu verwenden?  Das vorhanden sein von vier Clustern mit vier Knoten und Cluster Sätzen bietet die gleiche Skalierbarkeit, aber eine bessere Resilienz darin, dass mehrere Computeknoten ausfallen können (unerwartet oder für Wartung) und die Produktion verbleibt.

## <a name="considerations-for-deploying-cluster-sets"></a>Überlegungen zum Bereitstellen von Cluster Sätzen

Berücksichtigen Sie bei der Überlegung, ob Cluster Sätze verwendet werden müssen, die folgenden Fragen:

- Müssen Sie über die aktuellen HCI-COMPUTE-und Speicher Skalierungs Limits hinausgehen?
- Sind alle Compute-und Speicheranforderungen nicht identisch?
- Werden virtuelle Computer zwischen Clustern Live migriert?
- Möchten Sie die Verfügbarkeits Gruppen von Azure-ähnlichen Computern und Fehler Domänen über mehrere Cluster hinweg angleichen?
- Müssen Sie sich die Zeit nehmen, sich alle Cluster anzusehen, um zu bestimmen, wo neue virtuelle Computer platziert werden müssen?

Wenn die Antwort "Ja" lautet, benötigen Sie Cluster Sätze.

Es gibt noch einige andere Punkte, die in Erwägung gezogen werden müssen, wenn ein größerer SDDC Ihre allgemeinen Rechenzentrums Strategien möglicherweise ändert. SQL Server ist ein gutes Beispiel. Erfordert das Verschieben von SQL Server virtuellen Maschinen zwischen Clustern die Lizenzierung von SQL für die Verwendung auf zusätzlichen Knoten?

## <a name="scale-out-file-server-and-cluster-sets"></a>Dateiserver mit horizontaler Skalierung und Cluster Sätze

In Windows Server 2019 gibt es eine neue Datei Server Rolle mit horizontaler Skalierung namens Infrastructure Dateiserver mit horizontaler Skalierung (sofs).

Die folgenden Überlegungen gelten für eine Infrastruktur-sofs-Rolle:

1. In einem Failovercluster kann es höchstens eine Infrastruktur-sofs-Cluster Rolle geben. Die Infrastruktur-sofs-Rolle wird erstellt, indem der Switch-Parameter "**-Infrastructure**" für das Cmdlet " **Add-clusterscaleoutfileserverrole** " angegeben wird. Zum Beispiel:

    ```PowerShell
    Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure
    ```

2. Jedes CSV-Volume, das im Failover erstellt wird, löst automatisch die Erstellung einer SMB-Freigabe mit einem automatisch generierten Namen auf Grundlage des CSV-Volumenamens aus. Ein Administrator kann SMB-Freigaben unter einer sofs-Rolle nicht direkt erstellen oder ändern, außer über CSV-Volume Create/Modify-Vorgänge.

3. In hyperkonvergierten Konfigurationen ermöglicht ein-Infrastruktur-sofs einem SMB-Client (Hyper-V-Host) die Kommunikation mit der garantierten kontinuierlichen Verfügbarkeit (ca) mit dem Infrastruktur-sofs-SMB-Server. Diese hyperkonvergierte SMB-Loopback Zertifizierungsstelle wird über virtuelle Computer erreicht, die auf Ihre vhdx-Dateien (Virtual Disk) zugreifen, bei denen die Identität des besitzenden virtuellen Computers zwischen dem Client und dem Server weitergeleitet wird. Diese Identitäts Weiterleitung ermöglicht die ACL-vhdx-Dateien genau wie bei standardmäßigen hyperkonvergierten Cluster Konfigurationen wie zuvor.

Nachdem ein Cluster Satz erstellt wurde, basiert der Cluster Satz-Namespace auf einem Infrastruktur-sofs auf jedem der Mitglieds Cluster und zusätzlich auf einem Infrastruktur-sofs im Verwaltungs Cluster.

Wenn einem Cluster Satz ein Mitglieds Cluster hinzugefügt wird, gibt der Administrator den Namen eines Infrastruktur-sofs in diesem Cluster an, sofern bereits ein Cluster vorhanden ist. Wenn die Infrastruktur-sofs nicht vorhanden ist, wird von diesem Vorgang eine neue Infrastruktur-sofs-Rolle auf dem neuen Mitglieds Cluster erstellt. Wenn eine Infrastruktur-sofs-Rolle bereits auf dem Mitglieds Cluster vorhanden ist, benennt der Add-Vorgang Sie nach Bedarf implizit in den angegebenen Namen um. Alle vorhandenen Singleton-SMB-Server oder nicht-Infrastruktur-sofs-Rollen auf den Mitglieds Clustern bleiben vom Cluster Satz nicht ausgelastet.

Zum Zeitpunkt der Erstellung des Cluster Satzes hat der Administrator die Möglichkeit, ein bereits vorhandenes AD-Computer Objekt als Namespace Stamm auf dem Verwaltungs Cluster zu verwenden. Bei der Erstellung von Cluster Satz-Vorgängen wird die Infrastruktur-sofs-Cluster Rolle auf dem Verwaltungs Cluster erstellt, oder die vorhandene Infrastruktur-sofs-Rolle wird wie zuvor für Mitglieder Cluster beschrieben umbenannt. Die Infrastruktur-sofs im Verwaltungs Cluster wird als Cluster Satz-Namespace Referenz (Cluster Set Namespace) sofs verwendet. Es bedeutet einfach, dass jede SMB-Freigabe im Cluster Satz Namespace sofs eine Verweis Freigabe – vom Typ "simplereferral" ist, die in Windows Server 2019 neu eingeführt wurde. Dieser Verweis ermöglicht SMB-Clients den Zugriff auf die SMB-Ziel Freigabe, die auf dem Mitglieds Cluster-sofs gehostet wird. Der clusterset-Namespace Verweis-sofs ist ein einfacher Verweis Mechanismus und ist daher nicht Teil des e/a-Pfads. Die SMB-Verweise werden auf den einzelnen Client Knoten ständig zwischengespeichert, und der Cluster legt Namespaces automatisch automatisch aktualisiert. diese Verweise werden bei Bedarf automatisch aktualisiert.

## <a name="creating-a-cluster-set"></a>Erstellen eines Cluster Satzes

### <a name="prerequisites"></a>Voraussetzungen

Wenn Sie einen Cluster Satz erstellen, werden die folgenden Voraussetzungen empfohlen:

1. Konfigurieren Sie einen Verwaltungs Client, auf dem Windows Server 2019 ausgeführt wird.
2. Installieren Sie die Failoverclustertools auf diesem Management Server.
3. Erstellen von Cluster Mitgliedern (mindestens zwei Cluster mit mindestens zwei freigegebenen Clustervolumes auf jedem Cluster)
4. Erstellen Sie einen Verwaltungs Cluster (physisch oder Gast), der die Mitglieder Cluster überschreitet. Mit diesem Ansatz wird sichergestellt, dass die Verwaltungsebene des Clusters weiterhin verfügbar ist, obwohl mögliche Mitglieder Cluster Fehler auftreten.

### <a name="steps"></a>Schritte

1. Erstellen Sie einen neuen Cluster Satz aus drei Clustern, wie in den Voraussetzungen definiert. Das folgende Diagramm enthält ein Beispiel für zu erstellende Cluster. Der Name des Cluster Satzes in diesem Beispiel ist **csmaster**.

   | Clustername | Der später zu verwendende Infrastruktur-sofs-Name |
   |--------------|-------------------------------------------|
   | Set-Cluster  | sofs-clusterset                           |
   | CLUSTER1     | Sofs-CLUSTER1                             |
   | CLUSTER2     | Sofs-CLUSTER2                             |

2. Nachdem alle Cluster erstellt wurden, verwenden Sie den folgenden Befehl, um den Cluster Satz Master zu erstellen:

    ```PowerShell
    New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER
    ```

3. Verwenden Sie den unten aufgeführten Befehl, um dem Cluster Satz einen Cluster Server hinzuzufügen:

    ```PowerShell
    Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
    Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2
    ```

   > [!NOTE]
   > Wenn Sie ein statisches IP-Adress Schema verwenden, müssen Sie *-staticaddress x. x. x. x* in den **New-clusterset** -Befehl einschließen.

4. Nachdem Sie den Cluster aus den Cluster Mitgliedern erstellt haben, können Sie die Knotengruppe und deren Eigenschaften auflisten. So zählen Sie alle Mitglieds Cluster im Cluster Satz auf:

    ```PowerShell
    Get-ClusterSetMember -CimSession CSMASTER
    ```

5. So zählen Sie alle Mitglieds Cluster in der Clustergruppe einschließlich der Verwaltungs Cluster Knoten auf:

    ```PowerShell
    Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode
    ```

6. So Listen Sie alle Knoten aus den Mitglieds Clustern auf

    ```PowerShell
    Get-ClusterSetNode -CimSession CSMASTER
    ```

7. So Listen Sie alle Ressourcengruppen im Cluster Satz auf:

    ```PowerShell
    Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup
    ```

8. Um zu überprüfen, ob beim Erstellen eines Cluster Satzes eine SMB-Freigabe (identifiziert als volume1 oder die Bezeichnung des CSV-Ordners) erstellt wurde, ist ScopeName der Infrastruktur Datei Server Name und der Pfad beide in der Infrastruktur-sofs für das CSV-Volume jedes Cluster Mitglieds:

    ```PowerShell
    Get-SmbShare -CimSession CSMASTER
    ```

9. Cluster Satz-Debugprotokolle können zur Überprüfung gesammelt werden. Sowohl der Cluster Satz als auch die Cluster-Debugprotokolle können für alle Mitglieder und den Verwaltungs Cluster erfasst werden:

    ```PowerShell
    Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>
    ```

10. Konfigurieren Sie die eingeschränkte Kerberos- [Delegierung](https://techcommunity.microsoft.com/t5/virtualization/live-migration-via-constrained-delegation-with-kerberos-in/ba-p/382334) zwischen allen Mitgliedern der Clustergruppe.

11. Konfigurieren Sie den Authentifizierungstyp für die Live Migration der Cluster übergreifenden virtuellen Maschine auf jedem Knoten im Cluster Satz mit Kerberos.

    ```PowerShell
    foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }
    ```

12. Fügen Sie der lokalen Gruppe Administratoren auf jedem Knoten im Cluster Satz den Verwaltungs Cluster hinzu.

    ```PowerShell
    foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }
    ```

## <a name="creating-new-virtual-machines-and-adding-to-cluster-sets"></a>Erstellen neuer virtueller Maschinen und hinzufügen zu Cluster Sätzen

Nachdem Sie den Cluster Satz erstellt haben, besteht der nächste Schritt im Erstellen neuer virtueller Maschinen. Normalerweise müssen Sie beim Erstellen virtueller Maschinen und beim Hinzufügen zu einem Cluster einige Überprüfungen an den Clustern durchführen, um festzustellen, ob die Anwendung am besten geeignet ist. Diese Überprüfungen können Folgendes umfassen:

- Wie viel Arbeitsspeicher ist auf den Cluster Knoten verfügbar?
- Wie viel Speicherplatz ist auf den Cluster Knoten verfügbar?
- Erfordert der virtuelle Computer bestimmte Speicheranforderungen (d. h. Ich möchte, dass meine SQL Server virtuellen Maschinen zu einem Cluster mit schnelleren Laufwerken wechseln, oder der virtuelle Computer der Infrastruktur ist nicht so kritisch und kann auf langsameren Laufwerken ausgeführt werden).

Nachdem Sie diese Fragen beantwortet haben, erstellen Sie den virtuellen Computer auf dem Cluster, den Sie benötigen. Einer der Vorteile von Cluster Sätzen besteht darin, dass Cluster Sätze diese Überprüfungen ausführen und den virtuellen Computer auf dem optimalen Knoten platzieren.

Mit den folgenden Befehlen wird der optimale Cluster identifiziert und der virtuelle Computer darauf bereitgestellt. Im folgenden Beispiel wird ein neuer virtueller Computer erstellt, der angibt, dass mindestens 4 Gigabyte Arbeitsspeicher für den virtuellen Computer verfügbar sind und dass er einen virtuellen Prozessor nutzen muss.

- Stellen Sie sicher, dass 4 GB für den virtuellen Computer verfügbar sind.
- Legen Sie den bei 1 verwendeten virtuellen Prozessor fest.
- Stellen Sie sicher, dass mindestens 10% CPU für den virtuellen Computer verfügbar ist.

```PowerShell
# Identify the optimal node to create a new virtual machine
$memoryinMB=4096
$vpcount = 1
$targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10
$secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
$cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

# Deploy the virtual machine on the optimal node
Invoke-Command -ComputerName $targetnode.name -scriptblock { param([String]$storagepath); New-VM CSVM1 -MemoryStartupBytes 3072MB -path $storagepath -NewVHDPath CSVM.vhdx -NewVHDSizeBytes 4194304 } -ArgumentList @("\\SOFS-CLUSTER1\VOLUME1") -Credential $cred | Out-Null

Start-VM CSVM1 -ComputerName $targetnode.name | Out-Null
Get-VM CSVM1 -ComputerName $targetnode.name | fl State, ComputerName
```

Wenn der Vorgang abgeschlossen ist, erhalten Sie die Informationen zum virtuellen Computer und zum Speicherort des virtuellen Computers. Im obigen Beispiel würde Folgendes angezeigt werden:

```
State         : Running
ComputerName  : 1-S2D2
```

Wenn Sie nicht genügend Arbeitsspeicher, CPU-Kapazität oder Speicherplatz zum Hinzufügen des virtuellen Computers haben, wird der folgende Fehler angezeigt:

```
Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.
```

Nachdem der virtuelle Computer erstellt wurde, wird er auf dem angegebenen Knoten im Hyper-V-Manager angezeigt. Verwenden Sie den folgenden Befehl, um den virtuellen Computer als Cluster Satz hinzuzufügen und ihn dem Cluster hinzuzufügen:

```PowerShell
Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1
```

Wenn der Vorgang abgeschlossen ist, lautet die Ausgabe wie folgt:

```
Id  VMName  State  MemberName  PSComputerName
--  ------  -----  ----------  --------------
 1  CSVM1     On   CLUSTER1    CSMASTER
```

Wenn Sie einen Cluster mit vorhandenen virtuellen Computern hinzugefügt haben, müssen die virtuellen Computer auch bei Cluster Sätzen registriert werden. Um alle diese virtuellen Computer gleichzeitig zu registrieren, muss der folgende Befehl verwendet werden:

```PowerShell
Get-ClusterSetMember -Name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER
```

Der Prozess ist jedoch noch nicht beendet, da der Pfad zum virtuellen Computer dem Cluster Satz-Namespace hinzugefügt werden muss.

Beispielsweise wird ein vorhandener Cluster hinzugefügt und verfügt über vorkonfigurierte virtuelle Computer, die sich auf dem lokalen freigegebenes Clustervolume (CSV) befinden. Der Pfad für die vhdx-Datei würde etwa wie folgt lauten: "c:\clusterstorage\volume1\myvm\virtual Hard disks\myvm.vhdx". Es muss eine Speicher Migration durchgeführt werden, da CSV-Pfade in einem Cluster mit einem einzelnen Mitglied erstellt werden und daher nicht für die virtuelle Maschine zugänglich sind, sobald Sie Live in Mitglieds Clustern migriert sind.

In diesem Beispiel wurde CLUSTER3 dem Cluster Satz mithilfe von Add-clustersetmember mit der Infrastruktur Dateiserver mit horizontaler Skalierung als sofs-CLUSTER3 hinzugefügt. Um die Konfiguration und den Speicher des virtuellen Computers zu verschieben, lautet der Befehl wie folgt:

```PowerShell
Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM
```

Sobald der Vorgang abgeschlossen ist, erhalten Sie eine Warnung:

```
WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running. For more information view the report file below.
WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.
```

Diese Warnung kann ignoriert werden, weil die Warnung "Es wurden keine Änderungen in der Speicherkonfiguration der Rolle für virtuelle Computer erkannt" angezeigt wird. Der Grund für die Warnung, weil der tatsächliche physische Speicherort nicht geändert wird. nur die Konfigurations Pfade.

Weitere Informationen zu "Move-vmstorage" finden Sie unter diesem [Link](/powershell/module/hyper-v/move-vmstorage?view=win10-ps).

Die Live Migration einer virtuellen Maschine zwischen unterschiedlichen Clustergruppen Clustern ist nicht mit der in der Vergangenheit identisch. In Szenarien, in denen es sich nicht um Cluster Sätze handelt, sind folgende Schritte erforderlich:

1. Entfernen Sie die Rolle für virtuelle Computer aus dem Cluster.
2. Live Migration der virtuellen Maschine zu einem Mitglieds Knoten eines anderen Clusters.
3. Fügen Sie den virtuellen Computer dem Cluster als neue Rolle für virtuelle Computer hinzu.

Bei Cluster Sätzen sind diese Schritte nicht erforderlich, und nur ein Befehl ist erforderlich. Legen Sie zunächst mithilfe des folgenden Befehls alle Netzwerke fest, die für die Migration verfügbar sein sollen:

```PowerShell
Set-VMHost -UseAnyNetworkForMigration $true
```

Beispielsweise möchte ich einen virtuellen Computer für den Cluster Satz von CLUSTER1 auf Node2-CL3 auf CLUSTER3 verschieben. Der einzige Befehl lautet wie folgt:

```PowerShell
Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3
```

Beachten Sie, dass dadurch nicht der Speicher oder die Konfigurationsdateien des virtuellen Computers verschoben werden. Dies ist nicht erforderlich, da der Pfad zum virtuellen Computer weiterhin \\ \\ SOFS-CLUSTER1\VOLUME1. Wenn ein virtueller Computer mit Cluster Sätzen registriert ist, muss der Pfad der Infrastruktur Datei Server Freigabe sein, und die Laufwerke und die virtuelle Maschine müssen sich nicht auf demselben Computer wie der virtuelle Computer befinden.

## <a name="creating-availability-sets-fault-domains"></a>Erstellen von Verfügbarkeits Gruppen

Wie in der Einführung beschrieben, können Azure-ähnliche Fehler Domänen und Verfügbarkeits Gruppen in einem Cluster Satz konfiguriert werden. Dies ist nützlich für die Platzierung von ersten virtuellen Computern und Migrationen zwischen Clustern.

Im folgenden Beispiel sind vier Cluster am Cluster Satz beteiligt. Innerhalb des Satzes wird eine logische Fehler Domäne mit zwei Clustern und einer Fehler Domäne erstellt, die mit den anderen beiden Clustern erstellt wurde. Diese beiden Fehler Domänen bestehen aus der Verfügbarkeits Gruppe.

Im folgenden Beispiel werden CLUSTER1 und CLUSTER2 in einer Fehler Domäne mit dem Namen **FD1** angezeigt, während CLUSTER3 und CLUSTER4 sich in einer Fehler Domäne mit dem Namen **FD2**befinden. Die Verfügbarkeits Gruppe wird **als csmaster-as** bezeichnet und besteht aus den beiden Fehler Domänen.

Um die Fehler Domänen zu erstellen, sind die folgenden Befehle:

```PowerShell
New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"
```

Um sicherzustellen, dass Sie erfolgreich erstellt wurden, kann Get-clustersetfehlerdomain mit der angezeigten Ausgabe ausgeführt werden.

```PowerShell
PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

PSShowComputerName    : True
FaultDomainType       : Logical
ClusterName           : {CLUSTER1, CLUSTER2}
Description           : This is my first fault domain
FDName                : FD1
Id                    : 1
PSComputerName        : CSMASTER
```

Nachdem die Fehler Domänen erstellt wurden, muss die Verfügbarkeits Gruppe erstellt werden.

```PowerShell
New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2
```

Um zu überprüfen, ob er erstellt wurde, verwenden Sie Folgendes:

```PowerShell
Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER
```

Wenn Sie neue virtuelle Maschinen erstellen, müssen Sie den Parameter "-availabilityset" im Rahmen der Ermittlung des optimalen Knotens verwenden. So sieht es in etwa wie folgt aus:

```PowerShell
# Identify the optimal node to create a new virtual machine
$memoryinMB=4096
$vpcount = 1
$av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
$targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
$secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
$cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)
```

Entfernen eines Clusters aus Cluster Sätzen aufgrund verschiedener Lebenszyklen. Es gibt Zeiten, in denen ein Cluster aus einem Cluster Satz entfernt werden muss. Als bewährte Vorgehensweise sollten alle virtuellen Computer mit Cluster Satz aus dem Cluster verschoben werden. Dies kann mithilfe der Befehle **Move-clustersetvm** und **Move-vmstorage** erreicht werden.

Wenn die virtuellen Computer jedoch nicht ebenfalls verschoben werden, führt Cluster Sätze eine Reihe von Aktionen aus, um dem Administrator ein intuitives Ergebnis zu bieten. Wenn der Cluster aus der Gruppe entfernt wird, werden alle verbleibenden virtuellen Computer Gruppen, die auf dem zu entfernenden Cluster gehostet werden, einfach zu hoch verfügbaren virtuellen Computern, die an diesen Cluster gebunden sind, vorausgesetzt, dass Sie Zugriff auf den Speicher haben. Cluster Sätze aktualisieren das Inventar auch automatisch wie folgt:

- Die Integrität des jetzt entfernten Clusters und der darauf laufenden virtuellen Maschinen werden nicht mehr nachverfolgt.
- Entfernt aus dem Cluster Satz Namespace und allen Verweisen auf Freigaben, die auf dem jetzt entfernten Cluster gehostet werden.

Beispielsweise wäre der Befehl zum Entfernen des CLUSTER1-Clusters aus Cluster Sätzen wie folgt:

```PowerShell
Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER
```

## <a name="frequently-asked-questions-faq"></a>Häufig gestellte Fragen (FAQ)

**Frage:** Kann ich in meinem Cluster Satz nur hyperkonvergierte Cluster verwenden? <br>
**Antwort:** Nein. Sie können direkte Speicherplätze mit herkömmlichen Clustern kombinieren.

**Frage:** Kann ich meinen Cluster Satz über System Center Virtual Machine Manager verwalten? <br>
**Antwort:** System Center Virtual Machine Manager unterstützt derzeit keine Cluster Sätze. <br><br> **Frage:** Können Windows Server 2012 R2-oder 2016-Cluster gemeinsam im gleichen Cluster Satz vorhanden sein? <br>
**Frage:** Kann ich Workloads von Windows Server 2012 R2-oder 2016-Clustern migrieren, indem diese Cluster einfach demselben Cluster Satz beitreten? <br>
**Antwort:** Bei Cluster Sätzen handelt es sich um eine neue Technologie, die in Windows Server 2019 eingeführt wird und daher in früheren Versionen nicht vorhanden ist. Betriebssystem basierte Cluster auf Betriebssystemebene können keinem Cluster Satz beitreten. Die Technologie für parallele Upgrades des Cluster Betriebssystems sollte jedoch die Migrations Funktionalität bereitstellen, nach der Sie suchen, indem Sie diese Cluster auf Windows Server 2019 aktualisieren.

**Frage:** Kann ich mit Cluster Sätzen Speicher oder COMPUTE (allein) Skalieren? <br>
**Antwort:** Ja, durch einfaches Hinzufügen eines Speicherplatzes direkt oder eines herkömmlichen Hyper-V-Clusters. Bei Cluster Sätzen ist es eine einfache Änderung des Compute-zu-Speicher-Verhältnisses, auch in einem hyperkonvergenten Cluster Satz.

**Frage:** Was sind die Verwaltungs Tools für Cluster Sätze? <br>
**Antwort:** PowerShell oder WMI in dieser Version.

**Frage:** Wie funktioniert die Cluster übergreifende Live Migration mit Prozessoren unterschiedlicher Generationen?  <br>
**Antwort:** Cluster Sätze können nicht um Prozessor Unterschiede umgehen und ersetzen, was Hyper-V derzeit unterstützt. Daher muss der Prozessor Kompatibilitätsmodus bei schnellen Migrationen verwendet werden. Die Empfehlung für Cluster Sätze besteht darin, die gleiche Prozessor Hardware in jedem einzelnen Cluster und den gesamten Cluster Satz für Live Migrationen zwischen Clustern zu verwenden.

**Frage:** Kann bei einem Cluster Fehler ein automatisches Failover für virtuelle Computer festgelegt werden?  <br>
**Antwort:** In dieser Version können virtuelle Computer für Clustergruppen nur manuell zwischen Clustern Live migriert werden. ein automatisches Failover ist jedoch nicht möglich.

**Frage:** Wie stellen wir sicher, dass der Speicher anfällig für Cluster Ausfälle ist? <br>
**Antwort:** Verwenden Sie die Cluster-Cluster Speicher Replikat Lösung (SR) für Mitglieder Cluster, um die speicherresilienz bei Cluster Fehlern zu erkennen.

**Frage:** Ich verwende Speicher Replikat (SR) für die Replikation über Mitglieder Cluster. Ändern sich die UNC-Pfade für Cluster Satz-Namespace Speicher bei einem SR-Failover auf das Replikat Ziel direkte Speicherplätze Cluster? <br>
**Antwort:** In dieser Version erfolgt eine solche Änderung des Cluster Satz-Namespace Verweises nicht bei einem SR-Failover. Bitte informieren Sie Microsoft, ob dieses Szenario für Sie von entscheidender Bedeutung ist und wie Sie es verwenden möchten.

**Frage:** Ist es möglich, bei einer Notfall Wiederherstellung ein Failover für virtuelle Computer auf Fehler Domänen durchzusetzen (z. h. die gesamte Fehler Domäne ist ausgefallen)? <br>
**Antwort:** Nein, beachten Sie, dass das Cluster übergreifende Failover innerhalb einer logischen Fehler Domäne noch nicht unterstützt wird.

**Frage:** Kann ein Cluster Satz Cluster an mehreren Standorten (oder DNS-Domänen) umfassen? <br>
**Antwort:** Hierbei handelt es sich um ein nicht getesteter Szenario, das nicht sofort für die Produktion vorgesehen ist. Bitte informieren Sie Microsoft, ob dieses Szenario für Sie von entscheidender Bedeutung ist und wie Sie es verwenden möchten.

**Frage:** Funktioniert der Cluster Satz mit IPv6? <br>
**Antwort:** Sowohl IPv4 als auch IPv6 werden bei Cluster Sätzen wie bei Failoverclustern unterstützt.

**Frage:** Was sind die Active Directory Gesamtstruktur Anforderungen für Cluster Sätze? <br>
**Antwort:** Alle Mitglieds Cluster müssen sich in derselben AD-Gesamtstruktur befinden.

**Frage:** Wie viele Cluster oder Knoten können Teil eines einzelnen Cluster Satzes sein? <br>
**Antwort:** In Windows Server 2019 wurden Clustergruppen getestet und bis zu 64 Gesamtzahl der Cluster Knoten unterstützt. Die Architektur von Cluster Sätzen skaliert jedoch auf wesentlich größere Grenzwerte und ist nicht für eine Beschränkung hart codiert. Teilen Sie Microsoft mit, ob größere Skalierbarkeit für Sie von entscheidender Bedeutung ist und wie Sie die Verwendung planen.

**Frage:** Bilden alle direkte Speicherplätze Cluster in einem Cluster Satz einen einzelnen Speicherpool? <br>
**Antwort:** Nein. Direkte Speicherplätze Technologie wird immer noch innerhalb eines einzelnen Clusters und nicht über Mitglieder Cluster in einem Cluster Satz hinweg betrieben.

**Frage:** Ist der Cluster Satz Namespace hoch verfügbar? <br>
**Antwort:** Ja, der Cluster Satz-Namespace wird über einen fortlaufend verfügbaren verweisverweisnamespace Server (ca) bereitgestellt, der auf dem Verwaltungs Cluster ausgeführt wird. Microsoft empfiehlt, dass Sie über eine ausreichende Anzahl von virtuellen Computern aus Mitglieds Clustern verfügen, damit Sie sich gegen lokalisierte Cluster weite Ausfälle anfällig machen. Um jedoch unvorhergesehene schwerwiegende Fehler zu berücksichtigen – z. b. alle virtuellen Computer im Verwaltungs Cluster gleichzeitig heruntergefahren werden – werden die Verweis Informationen zusätzlich in jedem Cluster Satz Knoten dauerhaft zwischengespeichert, auch bei Neustarts.

**Frage:** Verlangsamt der auf dem Cluster festgelegte Namespace basierte Speicherzugriff die Speicherleistung in einem Cluster Satz. <br>
**Antwort:** Nein. Der clusterset-Namespace bietet einen Überlagerungs-Referenz Namespace in einem Cluster Satz – konzeptionell wie verteiltes Dateisystem Namespaces (DFSN). Und im Gegensatz zu DFSN werden alle clusterset-Namespace-Verweis Metadaten automatisch aufgefüllt und automatisch auf allen Knoten aktualisiert, ohne dass ein Administrator Eingriff ausgeführt wird, sodass der Speicherzugriffs Pfad fast keinen zusätzlichen Leistungs Aufwand erfordert.

**Frage:** Wie kann ich Cluster Satz Metadaten sichern? <br>
**Antwort:** Diese Anleitung ist identisch mit der des Failoverclusters. Mit der System Status Sicherung wird auch der Cluster Status gesichert. Durch Windows Server-Sicherung können Sie eine Wiederherstellung der Cluster Datenbank eines Knotens durchführen (was nie benötigt wird, weil eine Reihe von Selbstkorrektur Logik vorhanden ist) oder eine autorisierende Wiederherstellung durchführen, um ein Rollback für die gesamte Cluster Datenbank über alle Knoten auszuführen. Im Fall von Cluster Sätzen empfiehlt Microsoft, eine solche autorisierende Wiederherstellung zunächst auf dem Mitglieds Cluster und dann auf den Verwaltungs Cluster durchgeführt werden.
