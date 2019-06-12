---
title: Cluster-Gruppen
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 01/30/2019
description: In diesem Artikel wird das Cluster-Sets-Szenario beschrieben.
ms.localizationpriority: medium
ms.openlocfilehash: 349b69835ae68c626e886cad30f4d5a89d358372
ms.sourcegitcommit: a3958dba4c2318eaf2e89c7532e36c78b1a76644
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719705"
---
# <a name="cluster-sets"></a>Cluster-Gruppen

> Gilt für: Windows Server 2019

Legt der Cluster ist die neue Cloud-Scale-Out-Technologie, die in der 2019 für Windows Server-Version, die die Anzahl Clusterknoten in einer einzelnen Softwareupdates definiert Data Center (SDDC) Cloud um ein Vielfaches erhöht wird. Ein Clustersatz ist eine lose verbundene Gruppierung mehrere Failovercluster: compute, Speicher oder hyper-konvergiert. Cluster wird Technologie ermöglicht VM Fluidität für Element-Cluster in einen Clustersatz und ein Namespace für ein einheitliches über eine Gruppe zur Unterstützung von VM-Fluidität festgelegt.

Beim Beibehalten der vorhandenen Failovercluster-Verwaltung auf Member Clustern auftreten, bietet eine Set-Clusterinstanz darüber wichtigsten Anwendungsfälle für die lebenszyklusverwaltung auf das Aggregat. In diesem Evaluierungshandbuch für Windows Server 2019-Szenario bietet die erforderlichen Hintergrundinformationen und schrittweise Anleitungen zum Auswerten von Clustertechnologie-Sets mithilfe von PowerShell.

## <a name="technology-introduction"></a>Einführung in die Technologie

Legt Clustertechnologie wurde entwickelt, um bestimmte kundenanforderungen betreiben (Software definiert Datacenter, SDDC)-Clouds nach Maß zu erfüllen. Wertbeitrag für Cluster legt möglicherweise wie folgt zusammengefasst werden:  

- Erhöhen Sie die unterstützten SDDC-Cloud-Skalierung für die Ausführung von hoch verfügbaren virtuellen Maschinen durch die Kombination von mehreren kleinerer Clusters in einem einzigen großen Fabric, gleichzeitig auch die Grenze der Software-Fehler in einem einzigen Cluster erheblich
- Verwalten der gesamten Failovercluster-Lebenszyklus, einschließlich der Integration und zum abkoppeln von Clustern, ohne Beeinträchtigung der Mandanten-VM-Verfügbarkeit, über die Migration auch virtuelle Computer für diese großen Fabric
- Einfach ändern, die Compute-Storage-Verhältnis in Ihre hyper-konvergiert ich
- Profitieren Sie von [-ähnlichen Azure-Fehlerdomänen und Verfügbarkeitsgruppen](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) für Cluster in der ersten VM-Platzierung und weiteren VM-Migration
- Und kombinieren unterschiedliche prozessorgenerationen CPU-Hardware im selben Cluster festlegen Fabric auch, wenn einzelne Fehlerdomänen für maximale Effizienz bei homogene beibehalten.  Beachten Sie, dass die Empfehlung der gleichen Hardware noch vorhanden ist, in jedem einzelnen Cluster sowie den gesamten Cluster-Satz ist.

Von einem auf hoher Ebene ist dies welcher Cluster legt aussehen können.

![Cluster legt Lösung anzeigen](media/Cluster-sets-Overview/Cluster-sets-solution-View.png)

Im folgenden finden Sie eine kurze Zusammenfassung der einzelnen Elemente in der Abbildung oben:

**Verwaltungscluster**

Verwaltungscluster in einem Clustersatz ist ein Failovercluster, der die hoch verfügbare Verwaltungsebene die gesamten Cluster und die Referenz für unified Storage-Namespace (Cluster festlegen Namespace) Skalierung (Scale-Out-Datei Server, SOFS) hostet. Ein verwaltungscluster ist logisch entkoppelte aus Element-Clustern, die arbeitsauslastungen virtueller Computer ausgeführt. Dadurch wird den Clustersatz Verwaltungsebene robuste auf alle für den gesamten Cluster-Ausfällen, z. B. Stromausfall eines Clusters Member.   

**Member-cluster**

Ein Member-Cluster in einem Clustersatz ist in der Regel einen herkömmlichen hyperkonvergenten Cluster virtuelle Computer und arbeitsauslastungen mit "direkte Speicherplätze". Mehrere Member Cluster Teilnahme an einer Bereitstellung der einzelnen Cluster, der größeren SDDC-Cloud-Struktur bilden. Member-Cluster unterscheiden sich von einem verwaltungscluster in zwei wichtige Aspekte: Member-Clustern beteiligt Fehlerdomäne verfügbarkeitsgruppe erstellt und Member-Clustern sind auch Host-VM und angepasst "direkte Speicherplätze"-Workloads. Auf dem verwaltungscluster aus diesem Grund muss der Cluster die virtuellen Computer, die über die clustergrenzen hinweg in einem Cluster verschieben nicht gehostet werden.

**Cluster eingerichtet, Namespace-Verweis SOFS**

Ein Cluster Satz Namespace-Verweis (Cluster festlegen Namespace) SOFS handelt es sich um einen Scale-Out File Server, die bei dem jede SMB-Freigabe auf dem Cluster festlegen Namespace SOFS eine Verweis-Freigabe – vom Typ "SimpleReferral" in Windows Server-2019 neu eingeführt wird. Diese Referenz ermöglicht Server Message Block (SMB)-Clients Zugriff auf das Ziel, SMB-Freigabe, auf dem Cluster Member SOFS gehostet. Namespace-Verweis SOFS ist ein Lightweight-Weiterleitungsmechanismus und ist daher nicht Teil festlegen in der e/a-Pfad. Die SMB-Verweise werden Anreiz für jede der Client-Knoten zwischengespeichert und der Cluster legt Namespace dynamisch aktualisiert automatisch diese Verweise nach Bedarf.

**Master Clustersatz**

In einer Menge Cluster die Kommunikation zwischen den Clustern Member lose verknüpft und wird durch eine neue Clusterressource namens "Cluster Master festlegen" (CS-Master) koordiniert. Wie jede andere Clusterressource ist CS-Master an hoch verfügbare und einzelne Member-Clusterfehler bzw. die Knoten Verwaltung Clusterfehler resilienz. Durch einen neuen Cluster Festlegen von WMI-Anbieter bietet CS-Master den verwaltungsendpunkt für alle Cluster eingerichtet Verwaltbarkeit Interaktionen.

**Festlegen des Workers als Cluster**

In einer Bereitstellung für Cluster festgelegt werden die CS-Master mit neuen Clusterressource für das Element namens "Cluster festlegen Worker" (CS-Worker) Cluster interagiert. CS-Worker fungiert als einzige Verbindungsglied auf dem Cluster die Interaktionen für lokalen Cluster orchestrieren, die CS-Master-Anforderung. Beispiele für solche Interaktionen sind Platzierung virtueller Maschinen und Cluster-lokalen Ressource zu erfassen. Es gibt nur eine CS-Worker-Instanz für jede der in ein Clustersatz zu Clustern. 

**Fehlerdomäne**

Eine Fehlerdomäne ist die Gruppierung von Software und Hardware-Elemente, die der Administrator könnte zusammen fehlschlagen, wenn ein Fehler auftritt.  Während der Administrator ein oder mehrere Cluster zusammen als eine Fehlerdomäne festlegen kann, kann jeder Knoten in einer Fehlerdomäne in einer verfügbarkeitsgruppe teilnehmen. Cluster legt fest, indem Entwurf lässt die Entscheidung der Fault Domain Grenze Bestimmungskoeffizient an den Administrator, der sich hervorragend mit Überlegungen zur Topologie von Data Center – z. B. PDU, networking –, dass Member-Clustern verwenden. 

**Verfügbarkeitsgruppe**

Eine verfügbarkeitsgruppe unterstützt den Administrator bei gewünschten Redundanz der geclusterten arbeitsauslastungen auf Fehlerdomänen zu konfigurieren, indem Sie organisieren, die in einer verfügbarkeitsgruppe und Bereitstellung von Workloads in dieser verfügbarkeitsgruppe. Nehmen wir an, wenn Sie eine Anwendung mit zwei Ebenen bereitstellen, es wird empfohlen, dass Sie über mindestens zwei virtuelle Computer in einer verfügbarkeitsgruppe für jede Ebene, um sicherzustellen, dass Ihre Anwendung bei Ausfall einer Fehlerdomäne in dieser verfügbarkeitsgruppe mindestens verfügen wird konfigurieren ein virtueller Computer auf jeder Ebene, die auf einer anderen Fehlerdomäne, einer verfügbarkeitsgruppe gehostet.

## <a name="why-use-cluster-sets"></a>Warum verwenden Sie Cluster-Elemente

Cluster-Gruppen bietet den Vorteil der Skalierung ohne Einbußen bei der resilienz.  

Cluster legt können für mehrere Cluster clustering zusammen eine große-Struktur zu erstellen, solange jeder Cluster für resilienz unabhängig ist.  Z. B. eine mehrere 4-Knoten HCI man Cluster mit virtuellen Computern.  Jeder Cluster enthält, die resilienz für sich selbst erforderlich sind.  Wenn der Speicher- oder Arbeitsspeicher ansammeln beginnt, ist das Skalieren der nächste Schritt aus.  Mit zentral hochskalieren, gibt es einige Optionen und Überlegungen.

1. Fügen Sie mehr Speicher auf den aktuellen Cluster hinzu.  Mit "direkte Speicherplätze" kann dies knifflig sein, da die genau gleiche Modell/Firmware-Laufwerke möglicherweise nicht verfügbar.  Die Betrachtung der Wiederherstellungszeiten ebenfalls berücksichtigt werden müssen.
2. Fügen Sie weiteren Arbeitsspeicher hinzu.  Was geschieht, wenn sind Sie für den Speicher zuweilen, die die Computer behandelt werden können?  Was geschieht, wenn alle verfügbare Speichersteckplätze voll sind?
3. Fügen Sie zusätzliche Computeknoten mit Laufwerken, die in den aktuellen Cluster hinzu.  Dies führt uns zurück zu Option 1, die berücksichtigt werden müssen.
4. Erwerben eines ganz neuen Clusters

Dies ist, in dem Cluster legt bietet des Vorteil der Skalierung.  Wenn ich meine Cluster in einen Clustersatz hinzufügen, kann ich nutzen Speicher oder Speicher, die auf einem anderen Cluster ohne zusätzliche Käufe verfügbar sein können.  Vom Standpunkt der resilienz soll Hinzufügen weiterer Knoten zur einen "direkte Speicherplätze" nicht zusätzliche stimmen für das Quorum zu bieten.  Wie bereits erwähnt [hier](drive-symmetry-considerations.md), einem Cluster für direkte Speicherplätze den Verlust von 2 Knoten überstehen können, vor dem Ausfall.  Wenn Sie einen Cluster mit 4 Knoten HCI verfügen, 3 Knoten ausfallen wird im gesamten Cluster außer Betrieb zu nehmen.  Wenn Sie einen Cluster mit 8 Knoten verfügen, 3 Knoten ausfallen wird im gesamten Cluster außer Betrieb zu nehmen.  Mit Cluster-Sätzen, die über zwei Cluster mit 4 Knoten HCI in der Gruppe verfügt, 2 Knoten in einem HCI ausfallen, und 1 Knoten in der anderen HCI ausfallen, beide Cluster ununterbrochen verfügbar sein.  Ist es besser, erstellen Sie einen großen 16 Knoten "direkte Speicherplätze"-Cluster oder Teilen Sie ihn in vier 4-Knoten-Cluster und Cluster Sets verwenden?  Mit vier 4-Knoten-Cluster mit dem Cluster legt bietet die gleichen Skala, aber eine höhere Flexibilität, da mehrere Compute-Knoten (unerwartet beendet oder zur Wartung) ausfallen können, und die Produktion bleibt.

## <a name="considerations-for-deploying-cluster-sets"></a>Überlegungen zur Bereitstellung von Cluster-Gruppen

Wenn Sie erwägen, wenn Cluster legt ist etwas, das Sie verwenden möchten, beachten Sie diese Fragen:

- Möchten Sie die aktuellen HCI COMPUTE- und Speicherressourcen Kapazitätsgrenzen hinausgehen?
- Sind alle COMPUTE- und Speicherressourcen nicht genauso wie identisch?
- Können Sie live für virtuelle Maschinen zwischen Clustern migrieren?
- Möchten Sie Azure-ähnlichen Computer-Verfügbarkeitsgruppen und Fehlerdomänen auf mehrere Cluster?
- Möchten Sie nehmen die Zeit, sehen Sie sich alle Ihre Cluster, um zu bestimmen, in dem alle neuen virtuellen Computer platziert werden müssen?

Ihre Antwort "Ja" lautet, klicken Sie dann legt der Cluster ist, benötigen Sie.

Es gibt einige andere Elemente zu berücksichtigen, in dem eine größere SDDC Ihre gesamten Data Center-Strategien ändern können.  SQL Server ist ein gutes Beispiel.  Erfordert Verschieben von SQL Server-Computer zwischen Clustern die Lizenzierung von SQL auf zusätzlichen Knoten ausführen?  

## <a name="scale-out-file-server-and-cluster-sets"></a>Scale-Out Dateiserver und die Cluster-sets

In Windows Server-2019 besteht eine neue Serverrolle für Dateiserver mit horizontaler Skalierung wird aufgerufen, Infrastruktur-Skalierung (Scale-Out-Datei Server, SOFS) zur Verfügung. 

Die folgenden Überlegungen gelten für eine Infrastruktur SOFS-Rolle:

1.  Es kann jeweils nur ein Infrastruktur SOFS-Clusterrolle auf einem Failovercluster vorhanden sein. Infrastruktur-SOFS-Rolle wird erstellt, indem die " **-Infrastruktur**" switch-Parameter, um die **hinzufügen-ClusterScaleOutFileServerRole** Cmdlet.  Zum Beispiel:

        Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure

2.  Jedem CSV-Volume, das automatisch erstellt, das Failover löst die Erstellung einer SMB-Freigabe mit einem automatisch generierten Namen basierend auf dem CSV-Volume-Namen. Ein Administrator kann nicht direkt erstellen oder Ändern von SMB-Freigaben unter einer SOFS-Rolle, außer über CSV-Volume erstellen/ändern-Vorgänge.

3.  In Konfigurationen für hyper-konvergiert ermöglicht einem SOFS-Infrastruktur einen SMB-Client (Hyper-V-Host) für die Kommunikation mit garantierter fortlaufende Verfügbarkeit (CA) zum Infrastruktur SOFS SMB-Server. Dieses zusammengeführte SMB-Loopback Zertifizierungsstelle erfolgt über VMs, die Zugriff auf ihren virtuellen Festplattendateien (VHDx), in dem der übergeordneten Identität der virtuellen Maschine zwischen Client und Server weitergeleitet wird. Identität Weiterleitung ermöglicht ACL ähnelte VHDx-Dateien wie standard hyperkonvergenten Cluster entspricht der Konfiguration vor.

Nachdem ein Clustersatz erstellt wurde, verwendet der Cluster-Set-Namespace eines SOFS-Infrastruktur auf jedem von der Members-Clustern und außerdem eines SOFS-Infrastruktur, in dem verwaltungscluster.

Zum Zeitpunkt wird ein Clusters Element hinzugefügt, ein Clustersatz der Administrator den Namen eines SOFS-Infrastruktur auf diesem Cluster gibt an, ob bereits eine vorhanden ist. Wenn es sich bei den SOFS-Infrastruktur nicht vorhanden ist, wird eine neue Infrastruktur SOFS-Rolle auf dem neuen Element Cluster durch diesen Vorgang erstellt. Wenn eine Infrastruktur SOFS-Rolle bereits auf dem Cluster Member vorhanden ist, benennt der Vorgang zum Hinzufügen implizit es mit dem angegebenen Namen nach Bedarf. Alle vorhandenen Singleton-SMB-Server, oder nicht - Infrastruktur SOFS-Rollen auf dem Element das Cluster verlassen, sind sehr von dem Clustersatz. 

Zum Zeitpunkt der Erstellung der Clustersatz ist, kann der Administrator die Möglichkeit, einen bereits vorhandenen AD-Computer-Objekt als Namespacestamm auf dem verwaltungscluster verwenden. Cluster Satz Vorgänge zur Erstellung die Infrastruktur SOFS-Clusterrolle auf dem verwaltungscluster erstellen oder benennt die vorhandene Infrastruktur SOFS-Rolle für Member Cluster einfach wie zuvor beschrieben. Die SOFS-Infrastruktur, auf dem verwaltungscluster wird verwendet, wie Namespace-Verweis (Cluster festlegen Namespace) SOFS festlegen. Es bedeutet lediglich, dass jede SMB-Freigabe auf dem Cluster Namespace, die SOFS eine Verweis-Freigabe – vom Typ "SimpleReferral" festgelegt – neu in Windows Server-2019 eingeführt wird.  Diese Referenz ermöglicht, dass SMB-Clients den Zugriff auf das Ziel, die SMB-Freigabe auf dem Cluster Member SOFS gehostet. Namespace-Verweis SOFS ist ein Lightweight-Weiterleitungsmechanismus und ist daher nicht Teil festlegen in der e/a-Pfad. Die SMB-Verweise Anreiz für jede der Client-Knoten zwischengespeichert und der Cluster legt Namespace dynamisch aktualisiert automatisch diese Verweise nach Bedarf

## <a name="creating-a-cluster-set"></a>Erstellen eines Cluster-Satzes

### <a name="prerequisites"></a>Vorraussetzungen

Beim Erstellen eines Clusters festgelegt werden, sollten Sie folgende Voraussetzungen:

1. Konfigurieren Sie einen Verwaltungsclient, der unter Windows Server-2019.
2. Installieren Sie den Failovercluster-Tools auf diesem Verwaltungsserver ein.
3. Erstellen der Clustermitglieder (mindestens zwei Cluster mit mindestens zwei freigegebenen Clustervolumes auf jedem Cluster)
4. Erstellen eines Management-Clusters (physisch oder Gast), das die Member-Cluster überspannt.  Dieser Ansatz wird sichergestellt, dass die Cluster-Sätze, die Verwaltungsebene weiterhin trotz Clusterfehler möglich Member zur Verfügung.

### <a name="steps"></a>Schritte

1. Erstellen eines neuen Clusters aus drei Clustern festgelegt werden, wie in den Voraussetzungen definiert.  Die unter Diagramm bietet ein Beispiel für den Cluster zu erstellen.  Der Name des Clusters festlegen, die in diesem Beispiel **CSMASTER**.

   | Clustername               | Infrastruktur-SOFS-Name für die spätere Verwendung | 
   |----------------------------|-------------------------------------------|
   | SET-CLUSTER                | SOFS-CLUSTERSET                           |
   | CLUSTER1                   | SOFS-CLUSTER1                             |
   | CLUSTER2                   | SOFS-CLUSTER2                             |

2. Sobald alle Cluster erstellt wurden, verwenden Sie die folgenden Befehle zum Erstellen des Clusters Satz Master an.

        New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER

3. Hinzufügen eines Cluster-Servers auf dem Clustersatz der im folgenden verwendet werden.

        Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
        Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2

   > [!NOTE]
   > Wenn Sie eine statische IP-Adresse-Schema verwenden, müssen Sie aufnehmen *- StaticAddress x.x.x.x* auf die **New-ClusterSet** Befehl.

4. Nachdem Sie den Clustersatz aus Clustermitgliedern erstellt haben, können Sie die Gruppe von Knoten und deren Eigenschaften auflisten.  Um die Member-Cluster in den Cluster aufzulisten:

        Get-ClusterSetMember -CimSession CSMASTER

5. Um die Member-Cluster im Cluster festlegen, einschließlich der Clusterknoten Management aufzulisten:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode

6. So Listen Sie alle Knoten von der Members-Clustern:

        Get-ClusterSetNode -CimSession CSMASTER

7. Legen Sie zum Auflisten aller Ressourcengruppen im Cluster aus:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup 

8. Legen zum Überprüfen des Clusters Erstellungsprozess erstellt einen SMB-Freigabe (bezeichnet als Volume1 oder alle der Ordner "CSV" mit der der Name der dem Dateiserver-Infrastruktur und den Pfad als ScopeName mit der Bezeichnung) auf dem SOFS-Infrastruktur für jedes Clustermitglied CSV-Volume:

        Get-SmbShare -CimSession CSMASTER

8. Cluster legt hat es sich um Debugprotokolle wünschen, die zur Überprüfung gesammelt werden können.  Sowohl der Cluster eingerichtet und Debugprotokolle Cluster können für alle Mitglieder und dem verwaltungscluster erfasst werden.

        Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>

9. Konfigurieren von Kerberos [eingeschränkte Delegierung](https://blogs.technet.microsoft.com/virtualization/2017/02/01/live-migration-via-constrained-delegation-with-kerberos-in-windows-server-2016/) Mengenelemente zwischen allen Clustern.

10. Konfigurieren Sie den clusterübergreifenden-VM-live-Migration-Authentifizierungstyp für Kerberos auf jedem Knoten in den Cluster eingerichtet.

        foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }

11. Fügen Sie auf der lokalen Administratorgruppe auf jedem Knoten im Clustersatz des verwaltungsclusters hinzu.

        foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }

## <a name="creating-new-virtual-machines-and-adding-to-cluster-sets"></a>Erstellen neuer virtueller Maschinen und auf Cluster hinzufügen

Nach dem Erstellen des Clusters festlegen, wird im nächsten Schritts zum Erstellen neuen virtueller Maschinen.  Wenn es Zeit zum Erstellen von virtuellen Computern und in einem Cluster hinzufügen, müssen Sie in der Regel einige Überprüfungen finden Sie unter der sie möglicherweise am besten führen auf den Cluster.  Es konnte diese Prüfungen umfassen:

- Wie viel Arbeitsspeicher auf den Clusterknoten verfügbar ist?
- Wie viel Speicherplatz auf den Clusterknoten verfügbar ist?
- Der virtuelle Computer erfordern bestimmte speicheranforderungen (d. h. ich möchte meine SQL Server-Computer zu einem Cluster unter schnellere Laufwerke; wechseln oder meine virtuellen Computer der Infrastruktur ist nicht so wichtig und kann auf die langsameren Laufwerken ausgeführt).

Sobald diese Fragen beantwortet werden, erstellen Sie den virtuellen Computer, auf dem Cluster, den Sie auf die benötigte.  Einer der Vorteile von Cluster-Sätzen ist, dass der Cluster diese Überprüfungen für Sie erledigt und platzieren Sie den virtuellen Computer auf den optimalen Knoten.

Die folgenden Befehle beide identifiziert den optimalen Cluster und die virtuelle Maschine bereitstellen, damit.  In der folgenden Beispiel wird eine neue virtuelle Maschine erstellt, angeben, dass mindestens 4 GB Arbeitsspeicher für den virtuellen Computer verfügbar ist und es 1 virtuellen Prozessor verwenden muss.

- Stellen Sie sicher, dass 4gb für den virtuellen Computer verfügbar ist
- Legen Sie den virtuellen Prozessor mit 1 verwendet
- Stellen Sie sicher, es ist mindestens 10 % für den virtuellen Computer verfügbare CPU-Leistung

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

Wenn der Vorgang abgeschlossen ist, erhalten Sie die Informationen zum virtuellen Computer und, in dem sie abgelegt wurde.  Im obigen Beispiel würden sie als anzeigen:

        State         : Running
        ComputerName  : 1-S2D2

Würden Sie, dass nicht genügend Arbeitsspeicher, cpu und Speicherplatz auf den virtuellen Computer hinzufügen, erhalten Sie den Fehler:

      Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.  

Nachdem der virtuelle Computer erstellt wurde, wird es im Hyper-V-Manager auf dem angegebenen bestimmten Knoten angezeigt.  Hinzufügen ein Clusters festgelegt VM und den Cluster den Befehl unten.  

        Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1

Wenn der Vorgang abgeschlossen ist, wird die Ausgabe aussehen:

         Id  VMName  State  MemberName  PSComputerName
         --  ------  -----  ----------  --------------
          1  CSVM1      On  CLUSTER1    CSMASTER

Wenn Sie einen Cluster mit vorhandenen virtuellen Computer hinzugefügt haben, müssen die virtuellen Computer auch beim Cluster registriert werden, legt so registrieren Sie all die virtuellen Computer gleichzeitig angezeigt werden, der Befehl verwendet wird:

        Get-ClusterSetMember -name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER

Der Prozess ist jedoch nicht abgeschlossen, wie der Pfad zu dem virtuellen Computer auf den Cluster-Set-Namespace hinzugefügt werden muss.

Zum Beispiel ein vorhandener Cluster hinzugefügt und verfügt über vorkonfigurierte virtuelle Computer der wohnen auf dem lokalen freigegebenes Clustervolume (CSV), wäre der Pfad für die VHDX etwas Ähnliches wie in "C:\ClusterStorage\Volume1\MYVM\Virtual schwer Disks\MYVM.vhdx.  Eine Speichermigration erreicht werden, da es sich bei Entwurf, die lokal auf einem einzelnen Element Cluster CSV-Pfade werden müssten. Daher werden keine an den virtuellen Computer zugegriffen werden kann, sobald sie aktiv sind. für Member Cluster migriert. 

In diesem Beispiel wurde die Infrastruktur Scale-Out File Server als SOFS-CLUSTER3 hinzufügen-ClusterSetMember mit dem Clustersatz CLUSTER3 hinzugefügt.  Um die Konfiguration des virtuellen Computers und den Speicher zu verschieben, wird der Befehl lautet:

        Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM

Sobald der Vorgang abgeschlossen ist, wird eine Warnung angezeigt:

        WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running.  For more information view the report file below.
        WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.

Diese Warnung kann ignoriert werden, da die Warnung ist "keine Änderungen in der VM-Rollenkonfiguration Speicher erkannt wurden".  Der Grund für die Warnung als den tatsächlichen physischen Speicherort wird nicht geändert werden. nur der Konfigurationspfade. 

Weitere Informationen zu Move-VMStorage, finden Sie in dieser [Link](https://docs.microsoft.com/powershell/module/hyper-v/move-vmstorage?view=win10-ps). 

Live Migration einer virtuellen Maschine zwischen anderen-Cluster-Set-Clustern ist nicht dasselbe wie in der Vergangenheit. In Szenarien ohne Cluster-Satz wäre die Schritte aus:

1. Entfernen Sie die Rolle für virtuelle Maschinen, aus dem Cluster.
2. die Livemigration der virtuellen Computer auf einen Elementknoten eines anderen Clusters.
3. Fügen Sie den virtuellen Computer im Cluster als eine neue VM-Rolle hinzu.

Mit Cluster diese Schritte sind nicht erforderlich, und nur ein Befehl ist erforderlich.  Zunächst sollten Sie alle Netzwerke für die Migration mit dem Befehl festlegen:

    Set-VMHost -UseAnyNetworkMigration $true

Beispielsweise möchte ich eine VM-Clusters auf CLUSTER3 von CLUSTER1 in NODE2-CL3 zu verschieben.  Die einzelne Befehl wäre:

        Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3

Beachten Sie, dass dies nicht der VM-Speicher oder in Konfigurationsdateien verschoben wird.  Dies ist nicht erforderlich, da der Pfad zu dem virtuellen Computer weiterhin \\SOFS-CLUSTER1\VOLUME1.  Nachdem Sie ein virtuellen Computer registriert wurde mit Cluster hat den Freigabepfad Infrastruktur File Server, der Laufwerke und virtuelle Computer ist nicht erforderlich wird, auf dem gleichen Computer wie der virtuelle Computer.

## <a name="creating-availability-sets-fault-domains"></a>Erstellen die Verfügbarkeit legt Fehlerdomänen

Wie in der Einführung beschrieben wird, können Azure-ähnliche Fehlerdomänen und Verfügbarkeitsgruppen in einem Cluster konfiguriert werden.  Dies ist nützlich für die ursprüngliche virtuelle Maschine Platzierungen und Migrationen zwischen Clustern.  

Im folgenden Beispiel vier Cluster vorliegen Teilnahme an dem Clustersatz.  In der Gruppe wird eine logische Fehlerdomäne und zwei der Cluster und einer Fehlerdomäne, der mit den anderen beiden Clustern erstellt wurden erstellt.  Diese zwei Fehlerdomänen werden die Gruppe Availabiilty umfassen. 

Im folgenden Beispiel CLUSTER1, und CLUSTER2 werden in einer Fehlerdomäne namens **FD1** während CLUSTER3 und CLUSTER4 in einer Fehlerdomäne aufgerufen werden **FD2**.  Die verfügbarkeitsgruppe wird aufgerufen, **CSMASTER-AS** und zwei Fehlerdomänen umfassen.

Um die Fehlerdomänen zu erstellen, müssen Sie die Befehle sind:

        New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

        New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"

Um sicherzustellen, dass sie erfolgreich erstellt wurden, kann die Get-ClusterSetFaultDomain mit der Ausgabe ausgeführt werden.

        PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

        PSShowComputerName    : True
        FaultDomainType       : Logical
        ClusterName           : {CLUSTER1, CLUSTER2}
        Description           : This is my first fault domain
        FDName                : FD1
        Id                    : 1
        PSComputerName        : CSMASTER

Nun, dass die Fehlerdomänen erstellt wurden, legen Sie die Verfügbarkeit erstellt werden muss.

        New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2

Um die Validierung erstellt wurde, verwenden Sie dann:

        Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER

Wenn Sie neuen virtuelle Computer zu erstellen, müssten Sie dann mit dem AvailabilitySet - Parameter der Ermittlung des optimalen Knotens.  Daher würde es dann etwa wie folgt aussehen:

        # Identify the optimal node to create a new virtual machine
        $memoryinMB=4096
        $vpcount = 1
        $av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
        $targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
        $secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
        $cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

Einen Cluster aus Cluster entfernen, die aufgrund von verschiedenen Lebenszyklen legt diese fest. Es gibt Situationen, die bei ein Cluster aus einem Cluster entfernt werden muss. Als bewährte Methode sollten alle Cluster virtuelle Computer des Clusters verschoben werden. Dies geschieht mithilfe der **Move-ClusterSetVM** und **Move-VMStorage** Befehle.

Wenn die virtuellen Computer auch nicht verschoben werden, legt der Cluster führt jedoch eine Reihe von Aktionen, die eine intuitive Ergebnis zu erzielen, an dem Administrator.  Wenn der Cluster aus der Gruppe entfernt wird, werden alle verbleibenden Cluster virtuellen Computern im Cluster entfernt wird einfach hoch verfügbare virtuelle Maschinen, die mit diesem Cluster, vorausgesetzt, dass sie Zugriff auf ihren Speicher haben gebunden.  Cluster-legt werden den Bestand von auch automatisch aktualisiert werden:

- Keine Überwachung der Integrität des Clusters nun entfernt und die virtuellen Computer ausgeführt wird
- Entfernt aus der Cluster-Set-Namespace und alle Verweise auf Freigaben, die im Cluster jetzt entfernt

Beispielsweise wäre der Befehl zum Cluster legt den Cluster CLUSTER1 aufheben:

        Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER

## <a name="frequently-asked-questions-faq"></a>Häufig gestellte Fragen

**Frage:** In meinem Cluster festgelegt ist bin ich auf die Nutzung der hyperkonvergenten Cluster begrenzt? <br>
**Antwort:** Nein.  Sie können mit herkömmlichen Cluster "direkte Speicherplätze" kombinieren.

**Frage:** Kann ich meinen Cluster eingerichtet über System Center Virtual Machine Manager verwalten? <br>
**Antwort:** System Center Virtual Machine Manager unterstützt derzeit keine Cluster legt <br><br> **Frage:** Können Windows Server 2012 R2 oder 2016-Cluster in demselben Cluster gleichzeitig vorhanden sein? <br>
**Frage:** Kann ich migrieren Sie Workloads aus Windows Server 2012 R2 oder beitreten 2016-Cluster, indem Sie einfach diese Cluster, die demselben Cluster eingerichtet? <br>
**Antwort:** Cluster-Gruppen ist eine neue Technologie in Windows Server-2019, also als solches eingeführt, in früheren Versionen nicht vorhanden. Kompatible OS-basierten Clustern können ein Clustersatz nicht beitreten. Clusterbetriebssystem parallele Upgrades Technologie sollten jedoch die Migrationsfunktion bereitstellen, die Sie suchen ein Upgrade dieser Cluster auf Windows Server-2019.

**Frage:** Können Cluster legt lassen Sie mich skalieren Sie Speicher oder (eigenständig) berechnen? <br>
**Antwort:** Ja, einfach einen Storage Space Direct "oder" traditionellen Hyper-V-Cluster hinzufügen. Cluster-Sets ist es eine unkomplizierte Änderung Compute-Storage-Verhältnisses sogar in einem hyperkonvergenten Cluster-Satz.

**Frage:** Was ist die Management-Tools für Cluster legt <br>
**Antwort:** PowerShell oder WMI in dieser Version.

**Frage:** Wie funktioniert die clusterübergreifende live-Migration mit Prozessoren der unterschiedlichen prozessorgenerationen?  <br>
**Antwort:** Clustersätze nicht umgehen, prozessorunterschiede und ersetzen, was derzeit Hyper-V unterstützt.  Aus diesem Grund muss der prozessorkompatibilitätsmodus mit quick-Migrationen verwendet werden.  Die Empfehlung für Cluster-Gruppen ist die Verwendung der gleichen Prozessorhardware in jedem einzelnen Cluster sowie den gesamten Cluster eingerichtet für live-Migrationen zwischen Clustern auftreten.

**Frage:** Können meine Clustersatz virtuelle Computer automatisch ein Failover in einem Clusterfehler?  <br>
**Antwort:** In dieser Version möglich Cluster virtuelle Computer nur manuell live-Migration zwischen Clustern; jedoch nicht automatisch Failover. 

**Frage:** Wie können wir sicherstellen, dass Speicher robust gegenüber Fehlern ist? <br>
**Antwort:** Verwenden Sie clusterübergreifende Speicherreplikat (SR) Lösung für Element-Cluster, um die Storage-resilienz gegenüber clusterfehlern zu nutzen.

**Frage:** Ich verwende Speicherreplikat (SR), um auf Member-Cluster zu replizieren. Cluster Speicherung von Namespace Änderung der UNC-Pfade bei SR-Failover zum Replikat "direkte Speicherplätze" Zielcluster verwenden? <br>
**Antwort:** In dieser Version tritt eine solche Cluster Satz Namespace Verweis Änderung nicht mit SR-Failover. Informieren Sie Microsoft, die wissen, ob es sich bei diesem Szenario ist wichtig für Sie und wie Sie sie verwenden möchten.

**Frage:** Es ist möglich, Failover für virtuelle Computer auf Fehlerdomänen in Notfall (z. B. die gesamte Fehlerdomäne ausgefallen)? <br>
**Antwort:** Nein, beachten Sie, dass clusterübergreifende das Failover in einen logischen Fehler Domäne wird noch nicht unterstützt. 

**Frage:** Kann mein Cluster Span-Cluster in mehreren Sites (oder DNS-Domänen) festlegen? <br> 
**Antwort:** Dies ist ein Szenario nicht getestet und für die Unterstützung für die Produktion nicht sofort geplant. Informieren Sie Microsoft, die wissen, ob es sich bei diesem Szenario ist wichtig für Sie und wie Sie sie verwenden möchten.

**Frage:** Wird für Cluster mit IPv6 festgelegt? <br>
**Antwort:** IPv4 und IPv6 werden wie bei Failoverclustern mit Cluster unterstützt.

**Frage:** Legt die Active Directory-Gesamtstruktur Anforderungen für cluster <br>
**Antwort:** Alle Member-Cluster muss sich in derselben AD-Gesamtstruktur.

**Frage:** Wie viele Cluster oder Knoten kann Teil eines einzelnen Clusters werden festgelegt? <br>
**Antwort:** In Windows Server-2019, clustersätze getestet und unterstützt bis zu 64 insgesamt Clusterknoten. Allerdings Cluster Architektur, die sich auf viel größeren Einschränkungen festgelegt und ist nicht hartcodiert für einen Grenzwert ist. Informieren Sie Microsoft, die wissen, ob es sich bei größerem Umfang ist wichtig für Sie und wie Sie sie verwenden möchten.

**Frage:** Werden alle "direkte Speicherplätze"-Cluster in einem Clustersatz mit einen einzelnen Speicherpool bilden? <br>
**Antwort:** Nein. Storage Spaces Direct-Technologie arbeitet immer noch in einem einzigen Cluster, und nicht für alle Member-Clustern in einem Clustersatz.

**Frage:** Wird der Cluster hoch verfügbaren Namespace festgelegt? <br>
**Antwort:** Ja, wird der Cluster-Set-Namespace über einen kontinuierlich verfügbaren (CA) Verweis SOFS-Namespaceserver, die auf dem verwaltungscluster ausgeführt bereitgestellt. Microsoft empfiehlt die Verwendung von ausreichende Anzahl von virtuellen Computern von der Members-Clustern, diese zu Ausfällen für den gesamten Cluster stabil zu machen. Allerdings wird um unvorhergesehene schwerwiegenden Ausfällen – z. B. alle virtuellen Computer in den verwaltungscluster, die zur gleichen Zeit ausfällt – berücksichtigen die Verweisinformationen darüber dauerhaft in jedem Clusterknoten für die Gruppe, auch bei Neustarts zwischengespeichert.
 
**Frage:** Wird der Cluster in einem Clustersatz Verlangsamung der Leistung der Namespace-basierte datenspeicherung und Zugriff festgelegt? <br>
**Antwort:** Nein. Cluster-Set-Namespace bietet einen Overlay-Verweis-Namespace in einer Cluster-Gruppe – vom Konzept her wie Distributed Datei System Namespaces (DFSN). Und im Gegensatz zu DFSN, alle Cluster Satz Namespace Verweis Metadaten automatisch aufgefüllt und automatisch aktualisiert werden, auf allen Knoten ohne jegliches Eingreifen des Administrators, gibt es also praktisch keinen zusätzlichen Verwaltungsaufwand im Storage-Zugriffspfad. 

**Frage:** Wie kann ich die Cluster-Metadaten sichern? <br>
**Antwort:** Diese Anleitung ist identisch mit der Failover-Cluster. Die Systemstatussicherung wird auch der Clusterstatus sichern.  Über Windows Server-Sicherung möglich, Wiederherstellungen von nur einem Knoten des Cluster-Datenbank (die nie aufgrund von Selbstheilende Programmlogik, die wir haben etliche notwendig sein sollte) oder eine autorisierende Wiederherstellung aus, um ein Rollback die gesamten Cluster-Datenbank auf allen Knoten. Im Fall von Cluster-Sets empfiehlt Microsoft, zuerst tun von solchen eine autorisierende Wiederherstellung auf den Member-Cluster und dann auf dem verwaltungscluster, bei Bedarf.
