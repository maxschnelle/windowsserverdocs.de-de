---
title: Cluster-Gruppen
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 01/30/2019
description: Dieser Artikel beschreibt das Szenario der Cluster-Gruppen
ms.localizationpriority: medium
ms.openlocfilehash: 2deeb6968f910e80bacb2354ad2e575060a7797a
ms.sourcegitcommit: 07aefbdbb0eedb42aaed3d195c2429310c761da0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "9041006"
---
# Clustergruppen

> Gilt für: Windows Server Insider Preview-Build 17650 und höher

Cluster-Gruppen ist die neue Cloud Scale-Out-Technologie in dieser Preview-Version, die Anzahl der Cluster-Knoten in einer einzelnen Software Defined Data Center (SDDC)-Cloud Größenordnungen erhöht. Ein Cluster ist eine lose Gruppierung von mehrere Failovercluster: Computing, Speicher oder hyperkonvergente. Cluster legt Technologie virtuellen Computer Fluidität über Member-Cluster in einer Cluster-Gruppe und einen einheitlichen Speicher-Namespace über eine Gruppe zur Unterstützung der virtuellen Computer Fluidität. 

Während beibehalten vorhandenen Failovercluster-Verwaltung auf Member Clustern auftreten, bietet eine Instanz des Clusters außerdem Schlüssel Anwendungsfälle um Lifecycle Management zu dem Aggregat. Diese Evaluierungshandbuch für Windows Server Preview-Szenario bietet Ihnen die erforderlichen Hintergrundinformationen sowie eine schrittweise Anleitung, um zu bewerten, Cluster-Gruppen-Technologie mithilfe von PowerShell. 

## Einführung in die Technologie

Cluster-Gruppen-Technologie wurde entwickelt, um bestimmte Kundenanfragen betrieben Software Defined Datacenter (SDDC) Wolken bei einer Skalierung von erfüllen. Cluster-Sätze Wertversprechen in diesem Release Preview kann wie folgt zusammengefasst werden:  

- Zu einer deutlichen Erhöhung der unterstützten SDDC-Cloud-Niveau für die Ausführung von hoch verfügbare virtuelle Computer durch die Kombination von mehrere kleinere Cluster in eine einzelne große Fabric sogar Beibehaltung der Software Fehlertoleranz Grenze zu einem einzelnen cluster
- Verwalten der gesamte Failovercluster-Lebenszyklus, einschließlich Integration und Zurückziehen Clustern, ohne eine Beeinträchtigung der Verfügbarkeit der Mandanten virtuellen Maschinen, über passt migrieren virtuelle Computer über diese großen Fabric
- Das Compute-Storage-Verhältnis in Ihre zusammengeführten problemlos ändern, ich
- Profitieren von [Azure-ähnlichen Fehlerdomänen und Verfügbarkeit legt](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) über Cluster im ersten virtuellen Computer Platzierung und nachfolgende VM-migration
- Sortiment verschiedene Generationen der CPU-Hardware im selben Cluster festlegen Fabric, sogar Beibehaltung einzelne Fehlerdomänen homogenen für maximale Effizienz.  Bitte beachten Sie, dass die Empfehlung von derselben Hardware in jedem einzelnen Cluster sowie den gesamten Cluster Satz weiterhin vorhanden ist.

Aus einer high-Level-Ansicht ist dies welche Cluster Sätze aussehen könnten.

![Cluster legt Lösung anzeigen](media\Cluster-sets-Overview\Cluster-sets-solution-View.png)

Die folgenden bietet eine kurze Zusammenfassung der einzelnen Elemente in der obigen Abbildung:

**Management-cluster**

Management-Cluster in einem Cluster handelt es sich um einen Failovercluster, die die hoch verfügbare Management-Ebene des die gesamten Cluster und die einheitliche Speicher-Namespace (Cluster festlegen Namespace) Empfehlung sofs (Scale-Out-Datei Server, kontaktieren) hostet. Ein Management-Cluster ist logisch getrennt von Element-Cluster, die die VM-Arbeitslasten ausgeführt. Dadurch wird den Cluster, der Verwaltungsebene robustes auf eine lokalisierte für den gesamten Cluster-Fehler, z. B. einem Stromausfall eines Clusters Member.   

**Member-cluster**

Ein Mitglied-Cluster in einem Cluster ist in der Regel eine herkömmliche zusammengeführte Cluster virtuellen Computer und "direkte Speicherplätze" Workloads ausgeführt. Mehrere Member Cluster teilnehmen in einer einzelnen Gruppe Clusterbereitstellung, bilden die größere SDDC-Cloud-Struktur. Member Cluster unterscheiden sich von einem Management-Cluster in zwei wichtige Aspekte: Member Cluster teilnehmen Fehlerdomäne Verfügbarkeit Konstrukte und gemeinsamen Member Clustern werden auch auf virtuellen Hostcomputer und "direkte Speicherplätze" Workloads Größe. Set virtuellen Maschinen im Cluster, die über Cluster hinweg in einem Cluster zu verschieben müssen aus diesem Grund nicht auf dem Management-Cluster gehostet werden.

**Cluster festlegen Namespace-Verweis sofs kontaktieren**

Ein Cluster Satz Namespace-Verweis (Cluster festlegen Namespace) sofs kontaktieren ist ein Scale-Out-Dateiserver in dem eine Freigabe Empfehlung – vom Typ 'SimpleReferral' neu eingeführt wurden in diesem Release Preview jede SMB-Freigabe auf die Cluster festlegen Namespace sofs kontaktieren ist.  Diese Referenz ermöglicht Server Message Block (SMB) Clients den Zugriff auf das Ziel SMB-Freigabe verweist, die auf den Member Cluster sofs kontaktieren. Cluster festgelegt Namespace-Verweis sofs kontaktieren ist eine leichte Referenzmechanismus und daher nimmt in der e/a-Pfad. Die SMB-Referenzen unbefristet auf jedem der Client-Knoten zwischengespeichert, und der Cluster-Gruppen-Namespace dynamisch automatisch aktualisiert diese Verweise wie erforderlich.

**Cluster, der master**

In einem Cluster die Kommunikation zwischen den Member Clustern lose verknüpft ist, und wird durch einen neuen Clusterressource mit dem Namen "Cluster Master festlegen" (CS-Master) koordiniert. Wie jede andere Clusterressource ist CS-Master hoch verfügbarer und flexibel in Bezug auf die einzelnen Member Clusterfehler und/oder die Management-Cluster-Knoten-Fehler. Durch einen neuen Cluster Festlegen von WMI-Anbieter bietet CS-Master den Management-Endpunkt für alle-Clusters Verwaltbarkeit Interaktionen.

**Cluster-Satz-worker**

Bei einer Bereitstellung mit Cluster festlegen interagiert der CS-Master mit einer neuen Clusterressource für den Member Clustern "Cluster festlegen Worker" (CS-Worker) aufgerufen. CS-Worker fungiert als die einzige Bindeglied auf dem Cluster aus, um die lokalen Cluster-Interaktionen zu koordinieren, wie es die CS-Master. Beispiele für solche Interaktionen sind Platzierung virtueller Maschinen und Cluster-lokale Ressource inventarisieren. Es gibt nur ein, die CS-Worker-Instanz für die einzelnen des Elements in einer Cluster-Cluster. 

**Fehlerdomäne**

Eine Fehlerdomäne ist die Gruppierung der Software und Hardware-Artefakte, die der Administrator bestimmt konnte zusammen fehl, wenn ein Fehler auftritt.  Während ein Administrator eine oder mehrere Cluster zusammen als eine Fehlerdomäne bestimmen kann, kann jeder Knoten im eine Fehlerdomäne in einem Verfügbarkeit teilnehmen. Cluster legt fest, indem Design Blätter die Entscheidung der Fehlertoleranz Domäne Grenze Bestimmung an den Administrator, der über Kenntnisse mit Data Center Topologie Aspekte – z. B. PDU, Netzwerke –, Mitglied Cluster teilen. 

**Festlegen der Verfügbarkeit**

Ein Satz Verfügbarkeit hilft den gewünschten Redundanz gruppierten Workloads über Fehlerdomänen, konfigurieren Organisieren in einen Satz Verfügbarkeit und Bereitstellung von Workloads in dieser Gruppe Verfügbarkeit Administrator. Nehmen wir an, wenn Sie eine Anwendung mit zwei Ebenen bereitstellen, wird empfohlen, dass Sie mindestens zwei virtuellen Computern in eine Verfügbarkeit, legen Sie für jede Ebene, um sicherzustellen, dass wenn eine Fehlerdomäne in dieser Verfügbarkeit ausfällt, Ihre Anwendung mindestens wird konfigurieren Legen Sie einen virtuellen Computer in jeder Ebene auf eine andere Fehlerdomäne für die gleiche Verfügbarkeit gehostet.

## Gründe für die Verwendung Cluster-Gruppen

Cluster-Gruppen bietet den Vorteil der Skalierung ohne Kompromisse bei der resilienz.  

Cluster-Gruppen können für mehrere Cluster clustering zusammen eine große Fabric, zu erstellen, während es sich bei jedem Cluster unabhängige für resilienz, bleibt.  Sie haben z. B. eine mehrere 4-Knoten-HCI Cluster Ausführen von virtuellen Computern.  Jedem Cluster enthält die resilienz für sich selbst erforderlich sind.  Wenn der Speicher oder Speicher voll ist, ist Skalieren im nächsten Schritt.  Mit skalieren, gibt es einige Optionen und Vorschlägen.

1. Mehr Speicher für den aktuellen Cluster hinzufügen.  Bei direkte Speicherplätze kann dies schwierig sein wie die genaue gleichen Modell/Firmware-Laufwerke möglicherweise nicht verfügbar sind.  Die Betrachtung der Wiederherstellungszeiten auch berücksichtigt werden müssen.
2. Fügen Sie mehr Arbeitsspeicher hinzu.  Was geschieht, wenn sind Sie sich auf den Speicher überlastet, die die Computer verarbeiten können?  Was geschieht, wenn alle verfügbaren Arbeitsspeicher-Steckplätze voll sind?
3. Zusätzliche Compute-Knoten mit Laufwerken im aktuellen Cluster hinzufügen.  Dadurch gelangen uns zu Option 1 berücksichtigt werden müssen.
4. Erwerben Sie einen völlig neuen cluster

Dies ist die Cluster-Gruppen enthält, in denen den Vorteil der Skalierung.  Wenn ich meine Cluster in einer Cluster-Gruppe hinzufügen, kann ich nutzen Speicher oder Speicher, die möglicherweise auf einem anderen Cluster ohne zusätzliche Einkäufe verfügbar.  Aus der Perspektive eines resilienz soll Hinzufügen zusätzlicher Knoten zu einem direkte Speicherplätze nicht zusätzliche stimmen für Quorum bereitzustellen.  Als genannten [hier](drive-symmetry-considerations.md)kann ein Storage Spaces Direct-Cluster den Verlust von 2 Knoten überleben, bevor Sie fortfahren, nach unten.  Wenn Sie einen 4-Knoten-HCI Cluster verfügen, 3 Knoten ausfallen dauert nach unten den gesamten Cluster.  Wenn Sie einen 8-Knoten-Cluster verfügen, 3 Knoten ausfallen dauert nach unten den gesamten Cluster.  Cluster-Sätze, auf denen zwei 4-Knoten-HCI Cluster in der Gruppe ist, 2 Knoten in einem HCI abstürzt und 1 Knoten in der anderen HCI abstürzt, beide Cluster einrichten bleiben.  Ist es besser, eine große "direkte Speicherplätze" 16-Knoten-Cluster erstellen oder Teilen Sie ihn in vier 4-Knoten-Cluster und Cluster verwenden?  Mit vier 4-Knoten-Cluster mit Cluster Sätze bietet den selben Maßstab, aber eine bessere resilienz, mehrere Compute-Knoten (unerwartet oder für die Wartung), nach unten wechseln können und Produktion bleibt.

## Aspekte der Bereitstellung von Cluster-Gruppen

Wenn in Erwägung ziehen, wenn Cluster-Gruppen ist etwas, das Sie verwenden müssen, sollten Sie diese Fragen:

- Müssen Sie die aktuellen HCI Compute und Speicher Skalierung Grenzen zu wechseln?
- Sind alle Compute und Speicher nicht identisch identisch?
- Können Sie live virtuelle Computer zwischen Clustern migrieren?
- Möchten Sie diesen Azure-ähnlichen Verfügbarkeit und Fehlerdomänen über mehrere Cluster?
- Müssen Sie die Zeit zum Betrachten Sie alle Ihre Cluster, um zu bestimmen, in denen alle neuen virtuellen Computern platziert werden müssen?

Ihre Antwort "Ja" dann Cluster Sets ist, was erforderlich ist.

Es gibt einige andere Elemente zu berücksichtigen, in denen eine größere SDDC Ihre allgemeine Daten-Center-Strategien verändern kann.  SQL Server ist ein gutes Beispiel.  Erfordert verschieben SQL Server-VMs zwischen Clustern die Lizenzierung von SQL auf weitere Knoten ausgeführt?  

## Dateiserver mit horizontaler Skalierung und Cluster-Gruppen

In Windows Server 2019 es gibt eine neue Scale-Out-Datei-Serverrolle Infrastruktur sofs (Scale-Out-Datei Server, kontaktieren) aufgerufen. 

Die folgenden Aspekte gelten für eine Rolle Infrastruktur sofs kontaktieren:

1.  Es kann nur eine Infrastruktur sofs kontaktieren Cluster-Rolle auf einem Failovercluster sein. Infrastruktur sofs kontaktieren Rolle wird erstellt, indem die "**-Infrastruktur**" Parameter für das **Add-ClusterScaleOutFileServerRole** -Cmdlet zu wechseln.  Beispiel:

        Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure

2.  Jedes CSV-Volume automatisch in das Failover erstellt löst die Erstellung einer SMB-Freigabe mit einem automatisch generierten Namen basierend auf den Namen des CSV-Volumes. Ein Administrator kann nicht direkt erstellen oder Ändern von SMB-Freigaben unter einer Rolle sofs kontaktieren außer über CSV-Volume erstellen/ändern Vorgänge.

3.  Zusammengeführte Konfigurationen ermöglicht eine Infrastruktur sofs kontaktieren SMB-Client (Hyper-V-Host) mit garantierte fortlaufenden Verfügbarkeit (CA) an die Infrastruktur sofs kontaktieren SMB-Server kommunizieren. Dieser zusammengeführte SMB Loopback Zertifizierungsstelle erfolgt über virtuelle Computer Zugriff auf ihre virtuellen Datenträger (VHDx)-Dateien, in denen die besitzende Identität der virtuellen Maschine zwischen dem Client und Server weitergeleitet wird. Diese Identität-Weiterleitung ermöglicht ACL-Verknüpfung VHDx-Dateien, ebenso wie bei standardmäßigen zusammengeführte Cluster-Konfigurationen wie vor.

Nachdem eine Reihe Cluster erstellt wurde, verwendet der Cluster-Satz-Namespace eine Infrastruktur sofs kontaktieren auf jedem der Member-Cluster, und außerdem eine Infrastruktur sofs kontaktieren im Cluster Management.

Zum Zeitpunkt wird ein Member-Cluster hinzugefügt eine Reihe Cluster der Administrator den Namen des eine Infrastruktur sofs kontaktieren auf diesem Cluster gibt an, ob eine bereits vorhanden ist. Wenn die Infrastruktur sofs kontaktieren nicht vorhanden ist, wird eine neue Infrastruktur sofs kontaktieren-Rolle auf den neuen Member Cluster durch diesen Vorgang erstellt. Wenn eine Rolle Infrastruktur sofs kontaktieren bereits auf dem Cluster Member vorhanden ist, umbenannt das Hinzufügen eines Elements implizit in den angegebenen Namen nach Bedarf. Alle vorhandenen Singleton SMB-Server oder nicht - Infrastruktur sofs kontaktieren Rollen auf dem Mitglied die Cluster belassen werden vom Cluster festgelegten genutzte. 

Zum Zeitpunkt der Cluster erstellt wird, muss der Administrator die Möglichkeit, ein bereits vorhandenes AD-Computer-Objekt als Namespacestamm für den auf dem Management-Cluster. Clustervorgänge Set-Erstellung die Infrastruktur sofs kontaktieren Cluster-Rolle auf dem Management-Cluster erstellen oder benennt die vorhandene Infrastruktur sofs kontaktieren Rolle für Member Cluster genau wie zuvor beschrieben. Die Infrastruktur sofs Kontaktieren des Clusters Management wird verwendet, da Cluster Namespace-Verweis (Cluster festlegen Namespace) sofs kontaktieren festgelegt. Es bedeutet lediglich, dass jede SMB-Freigabe auf dem Cluster Namespace, die sofs kontaktieren einer Empfehlung Freigabe – vom Typ 'SimpleReferral' festgelegt - neu eingeführt wurden in dieser Preview-Version ist.  Diese Referenz ermöglicht, dass die SMB-Clients Zugriff auf das Ziel, die SMB-Freigabe auf den Member Cluster sofs kontaktieren gehostet. Cluster festgelegt Namespace-Verweis sofs kontaktieren ist eine leichte Referenzmechanismus und daher nimmt in der e/a-Pfad. Die SMB-Referenzen unbefristet auf der einzelnen Clientknoten zwischengespeichert und der Cluster-Gruppen-Namespace dynamisch updates automatisch diese Verweise nach Bedarf

## Erstellen eines Satzes Cluster

### Voraussetzungen

Beim Erstellen eines Clusters festlegen, werden Sie die folgenden Voraussetzungen empfohlen:

1. Konfigurieren eines Management-Clients die neueste Windows Server-Insider-Version.
2. Installieren Sie den Failovercluster-Tools auf diesem Verwaltungsserver.
3. Erstellen Sie die Cluster-Mitglieder (mindestens zwei Cluster mit mindestens zwei freigegebene Clustervolumes auf jedem Cluster)
4. Erstellen Sie einen Cluster von Management (physisch oder Gast) an, der die Member Cluster überspannt.  Dadurch wird sichergestellt, dass die Verwaltungsebene weiterhin verfügbar trotz möglich Member Clusterfehler Cluster festlegt.

### Schritte

1. Erstellen Sie einen neuen Cluster aus drei Clustern festgelegt werden, wie in die erforderlichen Komponenten definiert.  Die folgenden Diagramm zeigt ein Beispiel für Cluster zu erstellen.  Der Name des Clusters legen Sie in diesem Beispiel wird **CSMASTER**sein.

   | Clusternamen               | Infrastruktur sofs kontaktieren Namen für die spätere Verwendung | 
   |----------------------------|-------------------------------------------|
   | SET-CLUSTER                | SOFS KONTAKTIEREN-CLUSTERSET                           |
   | CLUSTER1                   | SOFS KONTAKTIEREN-CLUSTER1                             |
   | CLUSTER2                   | SOFS KONTAKTIEREN-CLUSTER2                             |

2. Nachdem alle Cluster erstellt wurden, verwenden Sie die folgenden Befehle, um dem Cluster Satz Master erstellen.

        New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER

3. Auf einem Cluster-Server Cluster, Hinzufügen der unten würde verwendet werden kann.

        Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
        Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2

   > [!NOTE]
   > Wenn Sie eine statische IP-Adresse-Schema verwenden, müssen Sie *– StaticAddress x.x.x.x* zum Befehl " **New-ClusterSet** " einfügen.

4. Nachdem Sie den Cluster aus Cluster-Mitglieder festlegen erstellt haben, können Sie die Knoten und dessen Eigenschaften auflisten.  Alle Member Cluster in der Cluster aufgelistet werden:

        Get-ClusterSetMember -CimSession CSMASTER

5. Um alle Member Cluster im Cluster festgelegt, einschließlich der Clusterknotens Management aufzulisten:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode

6. Listen Sie alle Knoten aus der Member-Clustern:

        Get-ClusterSetNode -CimSession CSMASTER

7. Listen Sie alle Ressourcengruppen über den Cluster festgelegt:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup 

8. Überprüfen des Clusters fest Erstellungsprozesses erstellt eine SMB-Freigabe (als Volume1 oder der der CSV-Ordner mit der Bereichsname wird der Name der dem Dateiserver-Infrastruktur und den Pfad als beide mit der Bezeichnung gekennzeichnet) auf die Infrastruktur sofs kontaktieren für jedes Clustermitglied CSV-Volume:

        Get-SmbShare -CimSession CSMASTER

8. Cluster-Gruppen hat Debug-Protokolle, die für die Überprüfung erfasst werden können.  Legen Sie der Cluster sowohl Cluster Debug-Protokolle können für alle Mitglieder und dem Management-Cluster gesammelt werden.

        Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>

9. Konfigurieren Sie die Kerberos- [Eingeschränkte Delegierung](https://blogs.technet.microsoft.com/virtualization/2017/02/01/live-migration-via-constrained-delegation-with-kerberos-in-windows-server-2016/) zwischen alle Cluster.

10. Konfigurieren Sie den Cross-Cluster virtuellen Computer Livemigration Authentifizierungstyp Kerberos auf jedem Knoten im Cluster-Set.

        foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }

11. Fügen Sie der lokalen Administratorgruppe auf jedem Knoten im Cluster Satz der Management-Cluster hinzu.

        foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }

## Erstellen von neuen virtuellen Computern und Cluster-Gruppen hinzufügen

Nach dem Erstellen des Clusters, besteht der nächste Schritt für neue virtuelle Computer erstellen.  In der Regel wann virtuelle Computer erstellen und diese zu einem Cluster hinzufügen, müssen Sie einige Tests in Clustern, finden am besten auf ausgeführt werden kann.  Dieser Überprüfung können gehören:

- Wie viel Arbeitsspeicher auf den Clusterknoten verfügbar ist?
- Wie viel Speicherplatz auf dem Clusterknoten verfügbar ist?
- Erfordert die virtuellen Computer bestimmte Speicherbedarf (d. h. meiner virtuellen Computer SQL Server, fahren Sie mit einem Cluster schnellere Laufwerke; ausgeführt werden soll oder der Infrastruktur virtuelle Computer ist nicht so wichtig, und kann auf langsameren Laufwerke ausgeführt).

Sobald diese Fragen beantwortet werden, können Sie den virtuellen Computer auf dem Sie auf die benötigte Cluster erstellen.  Einer der Vorteile der Cluster-Gruppen ist, dass der Cluster-Gruppen Kontrollen für Sie erledigen, und platzieren Sie den virtuellen Computer auf den optimalen Knoten.

Die folgenden Befehle werden beide identifizieren optimalen Cluster und Bereitstellen des virtuellen Computers hinzu.  In dem Beispiel unten haben ein neuer virtuellen Computer erstellt angeben, dass mindestens 4 GB Speicher steht für den virtuellen Computer und 1 virtuellen Prozessors nutzen werden müssen.

- Stellen Sie sicher, dass 4gb für den virtuellen Computer verfügbar ist
- Legen Sie den virtuellen Prozessor verwendet bei 1
- Stellen Sie sicher, dass es mindestens 10 % CPU für den virtuellen Computer verfügbar

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

Wenn es abgeschlossen ist, erhalten Sie Informationen zum virtuellen Computer und, in dem er gespeichert wurde.  Im obigen Beispiel würde als anzuzeigen:

        State         : Running
        ComputerName  : 1-S2D2

Würden Sie damit nicht genügend Arbeitsspeicher, cpu, oder der verfügbare Speicherplatz auf dem virtuellen Computer hinzufügen, werden Sie die Fehlermeldung angezeigt:

      Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.  

Nachdem der virtuelle Computer erstellt wurde, wird es in Hyper-V-Manager auf dem angegebenen spezifischen Knoten angezeigt.  Als ein Cluster virtuellen Computer und in den Cluster und, der Befehl unten ist hinzufügen.  

        Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1

Wenn es abgeschlossen ist, wird die Ausgabe aussehen:

         Id  VMName  State  MemberName  PSComputerName
         --  ------  -----  ----------  --------------
          1  CSVM1      On  CLUSTER1    CSMASTER

Wenn Sie einen Cluster mit vorhandenen virtuellen Computern hinzugefügt haben, müssen die virtuellen Computer auch mit Cluster registriert werden Sätze so registrieren Sie alle virtuellen Computer gleichzeitig, den zu verwendenden Befehl:

        Get-ClusterSetMember -name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER

Der Prozess ist jedoch nicht abgeschlossen, muss der Pfad zu dem virtuellen Computer auf den Namespace der Cluster-Gruppe hinzugefügt werden.

Z. B. ein vorhandener Cluster hinzugefügt wird und sie verfügt über vorkonfigurierte virtuelle Computer die wohnen auf den lokalen Cluster Shared Volumes (CSV), wäre der Pfad für die VHDX "C:\ClusterStorage\Volume1\MYVM\Virtual schwer Disks\MYVM.vhdx. ungefähr  Eine Speichermigration müsste gelingen, als CSV-Pfade entwurfsbedingt lokal auf einem einzelnen Cluster sind. Folglich kann nicht zugegriffen werden mit dem virtuellen Computer Nachdem sie live sind über Member Cluster migriert. 

In diesem Beispiel wurde der Cluster, der Verwendung von Add-ClusterSetMember mit dem Infrastruktur Scale-Out-Dateiserver als sofs kontaktieren-CLUSTER3 CLUSTER3 hinzugefügt.  Um die Konfiguration des virtuellen Computers und den Speicher zu verschieben, ist der Befehl:

        Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM

Nach Abschluss wird eine Warnung angezeigt:

        WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running.  For more information view the report file below.
        WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.

Diese Warnung kann ignoriert werden, da die Warnung wird "keine Änderungen in der virtuellen Computer Speicher Rollenkonfiguration erkannt wurden".  Der Grund für die Warnung als den tatsächlichen physischen Speicherort wird nicht geändert. nur die Konfigurationspfade. 

Weitere Informationen zum Verschieben-VMStorage überprüfen Sie diesen [Link](https://docs.microsoft.com/powershell/module/hyper-v/move-vmstorage?view=win10-ps). 

Live Migration eines virtuellen Computers zwischen anderen Cluster Satz Clustern entspricht nicht wie in der Vergangenheit. In Szenarien mit nicht-Cluster-Satz wäre die Schritte:

1. Entfernen Sie die Rolle des virtuellen Computers aus dem Cluster.
2. Livemigration des virtuellen Computers auf einen Knoten Mitglied von einem anderen Cluster.
3. Fügen Sie dem virtuellen Computer als eine neue Rolle für den virtuellen Computer zum Cluster hinzu.

Mit Cluster legt diese Schritte sind nicht erforderlich, und nur ein Befehl ist erforderlich.  Beispielsweise ich eine VM-Clusters aus CLUSTER1 auf Knoten 2-CL3 auf CLUSTER3 verschieben möchten.  Der einzelne Befehl wäre:

        Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3

Bitte beachten Sie, dass dies nicht die Dateien des virtuellen Computers Speicher oder Konfiguration bewegt.  Dies ist nicht erforderlich, da der Pfad zu dem virtuellen Computer als \\SOFS-CLUSTER1\VOLUME1 bleibt.  Nachdem Sie ein virtuellen Computer registriert wurde mit Cluster hat den Infrastruktur-Dateiserver-Freigabepfad, die Laufwerke und virtuelle Computer erfordern nicht auf demselben Computer wie der virtuelle Computer wird.

## Erstellen die Verfügbarkeit legt Fehlerdomänen

Wie in der Einführung beschrieben, können Azure-ähnlichen Fehlerdomänen und Verfügbarkeit Gruppen in einem Cluster konfiguriert werden.  Dies ist besonders bei der ersten virtuellen Computer Standorte und Migrationen zwischen Clustern.  

Im folgenden Beispiel stehen vier Clustern teilnehmen, die Cluster-Gruppe.  Innerhalb des Satzes wird eine logische Fehlerdomäne mit zwei Clustern und eine Fehlerdomäne erstellt, mit den anderen zwei Clustern erstellt werden.  Diese zwei Fehlerdomänen umfasst die Availabiilty festlegen. 

Im folgenden Beispiel werden CLUSTER1 CLUSTER2 und in eine Fehlerdomäne **FD1** aufgerufen, während CLUSTER3 und CLUSTER4 in eine Fehlerdomäne **FD2**aufgerufen werden.  Aufgerufen, der Verfügbarkeit Satz **CSMASTER-AS** und die zwei Fehlerdomänen besteht.

Um die Fehlerdomänen zu erstellen, können Sie die Befehle sind:

        New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

        New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"

Um sicherzustellen, dass sie erfolgreich erstellt wurde, kann mit der zugehörigen Ausgabe angezeigt Get-ClusterSetFaultDomain ausgeführt werden.

        PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

        PSShowComputerName    : True
        FaultDomainType       : Logical
        ClusterName           : {CLUSTER1, CLUSTER2}
        Description           : This is my first fault domain
        FDName                : FD1
        Id                    : 1
        PSComputerName        : CSMASTER

Nun, da die Fehlerdomänen erstellt wurden, legen Sie die Verfügbarkeit erstellt werden muss.

        New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2

Zum Validieren erstellt wurde, verwenden Sie dann:

        Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER

Wenn Sie neuen virtuelle Computer zu erstellen, müssen Sie dann Parameters - AvailabilitySet als Teil der Bestimmung des optimalen Knotens verwenden.  Daher würde es dann etwa wie folgt aussehen:

        # Identify the optimal node to create a new virtual machine
        $memoryinMB=4096
        $vpcount = 1
        $av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
        $targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
        $secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
        $cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

Beim Entfernen eines Clusters aus Cluster wird aufgrund der verschiedenen Lebenszyklen. Es gibt Situationen, die bei ein Cluster aus einer Reihe Cluster entfernt werden muss. Als bewährte Vorgehensweise sollten alle Cluster Satz virtuellen Computer aus dem Cluster verschoben werden. Dies kann mithilfe der Befehle **Move-ClusterSetVM** und **Verschieben-VMStorage** durchgeführt werden.

Wenn die virtuellen Computer auch nicht verschoben werden, Cluster-Gruppen führt jedoch eine Reihe von Aktionen, um eine intuitive Ergebnis an dem Administrator bereitzustellen.  Wenn der Cluster aus einer Reihe entfernt wird, werden alle verbleibenden Cluster Satz gehosteter virtuellen Computer auf dem Cluster entfernt wird einfach hoch verfügbare virtuelle Computer gebunden zu diesem Cluster, vorausgesetzt, dass sie in ihren Speicher zugreifen.  Cluster-Gruppen werden von Inventar auch automatisch aktualisiert werden:

- Nicht mehr Nachverfolgen der Integrität des Clusters jetzt entfernt und den darauf ausgeführten virtuellen Computern
- Entfernt aus Cluster Satz Namespace- und alle Verweise auf Freigaben auf dem Cluster jetzt entfernt

Beispielsweise wäre der Befehl zum CLUSTER1 Cluster aus Cluster-Gruppen zu entfernen:

        Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER

## Häufig gestellte Fragen

**Frage:** In Meine Cluster festgelegt ist kann ich auf nur mithilfe von hyperkonvergenten Clustern beschränkt? <br>
**Antwort:** Nein.  Sie können mit herkömmlichen Clustern "direkte Speicherplätze" verwenden.

**Frage:** Kann ich meine Cluster festlegen über System Center Virtual Machine Manager verwalten? <br>
**Antwort:** System Center Virtual Machine Manager unterstützt derzeit keine Cluster-Gruppen <br><br> **Frage:** Können Windows Server 2012 R2 oder 2016 Clustern im gleichen Cluster nebeneinander existieren? <br>
**Frage:** Kann ich Arbeitslasten off Windows Server 2012 R2 migrieren oder beitreten 2016 Cluster, indem Sie einfach die Cluster, den gleichen Cluster einrichten? <br>
**Antwort:** Cluster-Gruppen ist eine neue Technologie eingeführt in Windows Server Preview-Builds daher als solches ist nicht vorhanden in früheren Versionen. Älter OS-basierten Clustern können eine Reihe Cluster nicht beitreten. Cluster Operating System parallele Upgrades Technologie sollten jedoch die Migrationsfunktionen bereitstellen, die Sie benötigen diese Cluster auf Windows Server 2019 aktualisieren.

**Frage:** Können Cluster-Gruppen zulassen skalieren Speicher oder (eigenständig) berechnet? <br>
**Antwort:** Ja, indem Sie einfach eine direkte Speicherplatz oder herkömmliche Hyper-V-Cluster hinzufügen. Cluster-Gruppen ist es eine einfache Änderung der Compute-Storage-Verhältnis sogar in einem hyperkonvergenten Cluster.

**Frage:** Was ist die Management-Tools für Cluster Sets <br>
**Antwort:** PowerShell oder WMI in dieser Version.

**Frage:** Wie funktioniert die Livemigration Cross-Cluster mit Prozessoren der verschiedenen Generationen?  <br>
**Antwort:** Cluster-Gruppen nicht Prozessor Unterschiede zu umgehen und Vorrang vor, was Hyper-V derzeit unterstützt.  Aus diesem Grund muss prozessorkompatibilitätsmodus mit schnelle Migrationen verwendet werden.  Die Empfehlung für Cluster Sets ist die Verwendung die gleichen Prozessorhardware in jedem einzelnen Cluster sowie der gesamten Cluster festlegen für live-Migrationen zwischen Clustern auftreten.

**Frage:** Können meine Cluster Satz virtuelle Computer automatisch Failover bei einem Clusterfehler?  <br>
**Antwort:** In dieser Version kann virtuellen Maschinen im Cluster Satz nur manuell live-migriert über Cluster sein. jedoch nicht automatisch Failovercluster. 

**Frage:** Wie sicherstellen wir, dass der Speicher für Cluster Serverausfälle robustes ist? <br>
**Antwort:** Verwenden Sie Cross-Cluster Storage Replica (SR) Lösung über Member Cluster, um zu erkennen, die Speicher-resilienz, um die Clusterfehler.

**Frage:** Ich verwende Speicher Replikat (SR) über Member Cluster repliziert. Cluster Set-Namespace Speicher UNC-Pfade Änderung auf SR-Failover auf dem Replikat Ziel "direkte Speicherplätze"-Cluster verwenden? <br>
**Antwort:** In dieser Version erfolgt nicht mit SR-Failover eine solche Cluster Satz Namespace Empfehlung Änderung. Informieren Sie Microsoft wissen, ob dieses Szenario ist entscheidend für Sie und wie Sie sie verwenden möchten.

**Frage:** Es ist möglich, Failover-VMs über Fehlerdomänen im Notfall (beispielsweise die gesamte Fehlerdomäne ausgefallen)? <br>
**Antwort:** Nein, beachten Sie diese Cross-Cluster-Failover in einer logischen Fehlertoleranz Domäne wird noch nicht unterstützt. 

**Frage:** Kann meine Cluster Span-Cluster in mehrere Websites (oder DNS-Domänen) festgelegt? <br> 
**Antwort:** Dies ist ein Szenario nicht getestet und nicht sofort für die Produktion Unterstützung geplant. Informieren Sie Microsoft wissen, ob dieses Szenario ist entscheidend für Sie und wie Sie sie verwenden möchten.

**Frage:** Dient zum Cluster mit IPv6 festlegen? <br>
**Antwort:** IPv4 und IPv6 werden wie bei Failoverclustern mit Cluster unterstützt.

**Frage:** Was sind die Active Directory-Gesamtstruktur-Anforderungen für Cluster, legt <br>
**Antwort:** Alle Member Cluster müssen in derselben AD-Gesamtstruktur sein.

**Frage:** Wie viele Cluster oder Knoten kann Teil eines einzigen Clusters werden festgelegt? <br>
**Antwort:** In der Vorschau, cluster-Gruppen getestet und unterstützt bis zu 64 insgesamt Clusterknoten. Allerdings Cluster legt Architektur, die sich auf viel größeren Grenzwerte und nicht etwas, das bei begrenzt ist. Informieren Sie Microsoft wissen, ob größerem ist entscheidend für Sie und wie Sie sie verwenden möchten.

**Frage:** Werden für alle "direkte Speicherplätze"-Cluster in einem Cluster einen einzelnen Speicherpool Formular? <br>
**Antwort:** Nein. "Direkte Speicherplätze"-Storage-Technologie arbeitet weiterhin in einem einzigen Cluster und nicht über Member-Cluster in einer Cluster-Gruppe.

**Frage:** Ist der Cluster Namespace hoch verfügbare festgelegt? <br>
**Antwort:** Ja, wird der Cluster-Satz-Namespace über einen kontinuierlich verfügbar (CA) Empfehlung sofs kontaktieren Namespace-Server, auf dem Management-Cluster bereitgestellt. Microsoft empfiehlt, genügend Anzahl virtueller Maschinen von Member-Clustern, um lokalisierte für den gesamten Cluster-Fehler, robustes sicher. Allerdings wird um unvorhergesehene schwerwiegende Fehler auftreten – z. B. alle virtuellen Computer in der Management-Cluster gleichzeitig ausfallen – zu berücksichtigen die Empfehlung Informationen darüber dauerhaft in jedem Satz Cluster, sogar über Neustarts hinweg zwischengespeichert.
 
**Frage:** Dient zum Cluster-Namespace-basierte Speicherzugriff speicherleistung verlangsamen in einem Cluster festlegen? <br>
**Antwort:** Nein. Cluster-Satz-Namespace bietet einen Overlay-Referral-Namespace in einem Cluster Set – vom Konzept her wie verteilt Datei System Namespaces (DFSN). Und im Gegensatz zu DFSN, alle Cluster Namespace Referral-Metadaten erfolgt automatisch und auf allen Knoten ohne Eingreifen Administrator automatisch aktualisiert wird also nahezu gar keine Leistungsaufwand in den Speicher Zugriffspfad. 

**Frage:** Wie kann ich Cluster-Metadaten sichern? <br>
**Antwort:** Dieser Leitfaden ist identisch mit dem Failovercluster. Das System Zustand Backup wird den Status des Clusters sowie sichern.  Über Windows Server-Sicherung können Sie wieder her, der nur einen Knoten Cluster-Datenbank (die nie aufgrund etliche korrigierten wir haben Logik notwendig sein sollte) festzulegen oder eine autorisierend wiederherstellen, um die gesamte Clusterdatenbank ein Rollback auf allen Knoten ausführen. Im Fall von Cluster-Gruppen empfiehlt Microsoft, solche eine autoritativ Wiederherstellung zunächst auf macht die Member Cluster zu dann Management bei Bedarf. 
