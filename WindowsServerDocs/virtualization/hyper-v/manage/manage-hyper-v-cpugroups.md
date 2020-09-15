---
title: Ressourcen Steuerelemente für virtuelle Maschinen
description: Verwenden von VM-CPU-Gruppen
author: allenma
ms.prod: windows-server
ms.date: 06/18/2018
ms.topic: article
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: dc26dbe6bda9dc4f4f9b2bd99b3b8400555651ac
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077187"
---
# <a name="virtual-machine-resource-controls"></a>Ressourcen Steuerelemente für virtuelle Maschinen

> Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

In diesem Artikel werden die Hyper-V-Ressourcen-und Isolations Steuerelemente für virtuelle Computer beschrieben  Diese Funktionen, die wir als VM-CPU-Gruppen oder einfach "CPU-Gruppen" bezeichnen, wurden in Windows Server 2016 eingeführt.  Mit CPU-Gruppen können Hyper-V-Administratoren die CPU-Ressourcen des Hosts auf virtuellen Gast Computern besser verwalten und zuordnen.  Mithilfe von CPU-Gruppen können Hyper-V-Administratoren folgende Aktionen ausführen:

* Erstellen Sie Gruppen von virtuellen Computern, wobei jede Gruppe über unterschiedliche Belegungen der gesamten CPU-Ressourcen des Virtualisierungshosts verfügt, die für die gesamte Gruppe freigegeben sind. Dadurch kann der Host Administrator Dienst Klassen für verschiedene Typen von VMS implementieren.

* Legen Sie CPU-Ressourcen Limits auf bestimmte Gruppen fest. Diese "Gruppen Abdeckung" legt die obere Grenze für die Host-CPU-Ressourcen fest, die von der gesamten Gruppe genutzt werden können, und erzwingt effektiv die gewünschte Dienstklasse für diese Gruppe.

* Beschränken Sie eine CPU-Gruppe so, dass Sie nur auf einem bestimmten Satz der Prozessoren des Host Systems ausgeführt wird. Dies kann verwendet werden, um VMS zu isolieren, die zu verschiedenen CPU-Gruppen gehören.

## <a name="managing-cpu-groups"></a>Verwalten von CPU-Gruppen

CPU-Gruppen werden über den Hyper-V-hostcomputedienst oder HCS verwaltet. Im Blog des Microsoft-Virtualisierungsteams finden Sie eine gute Beschreibung der HCS, der dazugehörigen Informationen, Links zu den HCS-APIs und weitere Informationen zum Microsoft-virtualisierungsteamblog im Beitrag [Introducing the Host Compute Service (HCS)](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/).

>[!NOTE]
>Nur die HCS können zum Erstellen und Verwalten von CPU-Gruppen verwendet werden. die WMI-und PowerShell-Verwaltungs Schnittstellen von Hyper-V-Manager unterstützen keine CPU-Gruppen.

Microsoft stellt ein Befehlszeilen-Hilfsprogramm (cpugroups.exe) im [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=865968) zur Verfügung, das die HCS-Schnittstelle zum Verwalten von CPU-Gruppen verwendet.  Dieses Hilfsprogramm kann auch die CPU-Topologie eines Hosts anzeigen.

## <a name="how-cpu-groups-work"></a>Funktionsweise von CPU-Gruppen

Die Zuordnung von hostcomputeressourcen über CPU-Gruppen hinweg wird durch den Hyper-V-Hypervisor erzwungen, indem eine berechnete CPU-Gruppe verwendet wird. Die CPU-Gruppen Abdeckung ist ein Bruchteil der CPU-Gesamtkapazität für eine CPU-Gruppe. Der Wert der Gruppen Abdeckung hängt von der Gruppenklasse bzw. der zugewiesenen Prioritätsstufe ab. Das Ende der berechneten Gruppe kann als "Zahl der CPU-Zeit in LP" betrachtet werden. Dieses Gruppen Budget ist freigegeben. wenn nur ein einzelner virtueller Computer aktiv war, könnte die CPU-Belegung der gesamten Gruppe für sich selbst verwendet werden.

Das Limit für die CPU-Gruppe wird als G = *n* x *C*berechnet, wobei Folgendes gilt:

- *G* ist die Menge der Host-LP, die der Gruppe zugewiesen werden soll.
- *n* ist die Gesamtanzahl der logischen Prozessoren (LPs) in der Gruppe.
- *C* ist die maximale CPU-Belegung – d. h. die für die Gruppe gewünschte Dienstklasse, ausgedrückt als Prozentsatz der gesamten computekapazität des Systems.

Nehmen Sie beispielsweise eine CPU-Gruppe, die mit 4 logischen Prozessoren (LPs) konfiguriert ist, und eine Obergrenze von 50%.

- G = n * C
- G = 4 * 50%
- G = 2 LP-Wert CPU-Zeit für die gesamte Gruppe

In diesem Beispiel wird der CPU-Zeit von 2 LP die CPU-Zeit von 2 LP zugewiesen.

Beachten Sie, dass das Gruppen Limit unabhängig von der Anzahl von virtuellen Computern oder virtuellen Prozessoren, die an die Gruppe gebunden sind, und unabhängig vom Zustand (z. b. Herunterfahren oder starten) der virtuellen Computer, die der CPU-Gruppe zugewiesen sind, gilt. Daher erhält jeder an die gleiche CPU-Gruppe gebundene virtuelle Computer einen Bruchteil der Gesamt-CPU-Belegung der Gruppe. Dies ändert sich mit der Anzahl der VMS, die an die CPU-Gruppe gebunden sind. Daher muss bei virtuellen Computern, die an eine CPU-Gruppe gebunden oder ungebunden sind, das Gesamtlimit für die CPU-Gruppe umgelesen und so festgelegt werden, dass die gewünschte Obergrenze pro VM beibehalten wird. Die Software Schicht des VM-Host Administrators oder der Virtualisierungsverwaltung ist für die Verwaltung von Gruppen Limits nach Bedarf zuständig, um die gewünschte CPU-Ressourcen Zuordnung pro VM zu erzielen.

## <a name="example-classes-of-service"></a>Beispiele für Dienst Klassen

Sehen wir uns einige einfache Beispiele an. Angenommen, der Hyper-V-Host Administrator möchte zwei Dienst Ebenen für Gast-VMS unterstützen:

1. Eine Low-End-Ebene "C". Wir legen dieser Ebene 10% der Compute-Ressourcen des gesamten Hosts zu.

1. Eine mittlere "B"-Ebene. Dieser Ebene werden 50% der Compute-Ressourcen des gesamten Hosts zugeordnet.

An dieser Stelle in unserem Beispiel wird bestätigt, dass keine anderen CPU-Ressourcen Steuerungen verwendet werden, wie z. b. einzelne VM-Caps, Gewichtungen und Reserven.
Einzelne VM-Caps sind jedoch wichtig, da wir später etwas später sehen werden.

Der Einfachheit halber gehen wir davon aus, dass jeder virtuelle Computer über 1 VP verfügt und dass der Host über 8 LPs verfügt. Wir beginnen mit einem leeren Host.

Zum Erstellen der Ebene "B" legt der Host-adminstartor die Gruppen Abdeckung auf 50% fest:

- G = n * C
- G = 8 * 50%
- G = 4 LP CPU-Zeit für die gesamte Gruppe

Der Host Administrator fügt einen einzelnen virtuellen Computer der Ebene "B" hinzu.
An diesem Punkt kann der VM "B" der Ebene "B" höchstens 50% der CPU des Hosts oder das Äquivalent von 4 LPs in unserem Beispiel System verwenden.

Nun fügt der Administrator einen zweiten virtuellen Computer der Ebene "Ebene B" hinzu. Die Zuordnung der CPU-Gruppe – wird gleichmäßig auf alle virtuellen Computer aufgeteilt. Wir haben insgesamt 2 virtuelle Computer in Gruppe b, sodass jeder virtuelle Computer nun die Hälfte der Gruppe b insgesamt 50%, 25% oder die Entsprechung von 2 LPs der COMPUTE-Zeit erhält.

## <a name="setting-cpu-caps-on-individual-vms"></a>Festlegen von CPU-Caps auf einzelnen VMS

Zusätzlich zum Gruppen Limit kann jede VM auch eine einzelne "VM-Obergrenze" aufweisen. Die CPU-Ressourcenkontrolle pro VM, einschließlich einer CPU-Abdeckung, Gewichtung und Reserve, ist seit der Einführung Teil von Hyper-V.
In Kombination mit einer Gruppen Abdeckung gibt eine VM-Obergrenze die maximale CPU-Kapazität an, die jeder VP erhalten kann. Dies gilt auch, wenn für die Gruppe CPU-Ressourcen verfügbar sind.

Beispielsweise kann es vorkommen, dass der Host Administrator eine VM-Obergrenze von 10% auf "C"-VMS platzieren möchte.
Dies ist auch der Fall, wenn sich die meisten VPS "C" im Leerlauf befinden, kann jeder VP nie mehr als 10% erhalten.
Ohne eine VM-Obergrenze könnten "C"-VMS die Leistung auf der Basis der durch ihre Ebene zulässigen Stufen erreichen.

## <a name="isolating-vm-groups-to-specific-host-processors"></a>Isolieren von VM-Gruppen für bestimmte Host Prozessoren

Hyper-V-Host Administratoren können auch die Möglichkeit haben, Compute-Ressourcen für einen virtuellen Computer zu verwenden.
Stellen Sie sich z. b. vor, dass der Administrator eine Premium-VM mit einer Klasse von 100% anbieten möchte.
Diese Premium-VMS erfordern außerdem die niedrigste Zeit für Zeitplanung und Jitter. Das heißt, Sie werden möglicherweise nicht von einem anderen virtuellen Computer aufgehoben.
Um diese Trennung zu erreichen, kann eine CPU-Gruppe auch mit einer bestimmten LP-Affinitäts Zuordnung konfiguriert werden.

Um z. b. in unserem Beispiel eine "A"-VM auf dem Host zu integrieren, erstellt der Administrator eine neue CPU-Gruppe und legt die Prozessor Affinität der Gruppe auf eine Teilmenge der LPs des Hosts fest.
Die Gruppen B und C werden den verbleibenden LPs zugeordnet.
Der Administrator könnte einen einzelnen virtuellen Computer in Gruppe a erstellen, der dann exklusiven Zugriff auf alle LPs in Gruppe a hätte, während die Gruppen B und C der niedrigeren Ebene die verbleibenden LPs freigeben würden.

## <a name="segregating-root-vps-from-guest-vps"></a>Trennen von Stamm-VPS von Gast-VPS

Standardmäßig wird in Hyper-V auf jeder zugrunde liegenden physischen LP eine Stamm-VP erstellt.
Diese Stamm-VPS sind der System LPs strikt 1:1 zugeordnet und werden nicht migriert – das heißt, dass jeder Stamm-VP immer auf derselben physischen LP ausgeführt wird.
Gast-VPS können auf jeder verfügbaren LP ausgeführt werden und werden die Ausführung mit Stamm-VPS freigeben.

Es kann jedoch wünschenswert sein, die Stamm-VP-Aktivität von Gast-VPS vollständig zu trennen.
Sehen Sie sich unser Beispiel oben an, in dem wir einen virtuellen Premium-Tarif "a" implementieren.
Um sicherzustellen, dass die VPS der "A"-VM die geringstmögliche Latenz und "Jitter" oder die Zeitplanung aufweisen, möchten wir Sie auf einem dedizierten Satz von LPs ausführen und sicherstellen, dass der Stamm nicht auf diesen LPs ausgeführt wird.

Dies kann mithilfe einer Kombination aus der "minroot"-Konfiguration erreicht werden, wodurch die Host-Betriebssystem Partition auf eine Teilmenge der logischen Gesamt Systemprozessoren und mindestens eine affininitisierte CPU-Gruppe beschränkt wird.

Der Virtualisierungshost kann so konfiguriert werden, dass die Host Partition auf bestimmte LPs beschränkt wird, wobei eine oder mehrere CPU-Gruppen den verbleibenden LPs zugeordnet werden.
Auf diese Weise können die Stamm-und Gast Partitionen auf dedizierten CPU-Ressourcen und vollständig isoliert und ohne CPU-Freigabe ausgeführt werden.

Weitere Informationen zur Konfiguration von "minroot" finden Sie unter [Hyper-V-Host-CPU-Ressourcenverwaltung](./manage-hyper-v-minroot-2016.md).

## <a name="using-the-cpugroups-tool"></a>Verwenden des cpugroups-Tools

Sehen wir uns nun einige Beispiele für die Verwendung des cpugroups-Tools an.

>[!NOTE]
>Befehlszeilenparameter für das cpugroups-Tool werden nur mithilfe von Leerzeichen als Trennzeichen übergeben. Keine Zeichen "/" oder "-" sollten den gewünschten Befehls Zeilenschalter fortsetzen.

### <a name="discovering-the-cpu-topology"></a>Ermitteln der CPU-Topologie

Das Ausführen von cpugroups mit der getcputopology-Funktion gibt Informationen zum aktuellen System zurück, wie unten dargestellt, einschließlich des LP-Indexes, des NUMA-Knotens, zu dem die LP gehört, der Paket-und Kern-IDs und des Stamm-VP-Index.

Das folgende Beispiel zeigt ein System mit 2 CPU-Sockets und NUMA-Knoten, insgesamt 32 LPs und Multithreading aktiviert und so konfiguriert, dass minroot mit 8 Stamm-VPS und 4 von jedem NUMA-Knoten aktiviert wird.
Die LPs mit Stamm-VPS haben einen rootvpindex >= 0; LPs mit einem rootvpindex von "-1" sind für die Stamm Partition nicht verfügbar, werden jedoch weiterhin vom Hypervisor verwaltet und führen Gast-VPS wie von anderen Konfigurationseinstellungen zugelassen aus.

```console
C:\vm\tools>CpuGroups.exe GetCpuTopology

LpIndex NodeNumber PackageId CoreId RootVpIndex
------- ---------- --------- ------ -----------
      0          0         0      0           0
      1          0         0      0           1
      2          0         0      1           2
      3          0         0      1           3
      4          0         0      2          -1
      5          0         0      2          -1
      6          0         0      3          -1
      7          0         0      3          -1
      8          0         0      4          -1
      9          0         0      4          -1
     10          0         0      5          -1
     11          0         0      5          -1
     12          0         0      6          -1
     13          0         0      6          -1
     14          0         0      7          -1
     15          0         0      7          -1
     16          1         1     16           4
     17          1         1     16           5
     18          1         1     17           6
     19          1         1     17           7
     20          1         1     18          -1
     21          1         1     18          -1
     22          1         1     19          -1
     23          1         1     19          -1
     24          1         1     20          -1
     25          1         1     20          -1
     26          1         1     21          -1
     27          1         1     21          -1
     28          1         1     22          -1
     29          1         1     22          -1
     30          1         1     23          -1
     31          1         1     23          -1
```

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>Beispiel 2 – Drucken aller CPU-Gruppen auf dem Host

Hier werden alle CPU-Gruppen auf dem aktuellen Host, die groupID, die CPU-Abdeckung der Gruppe und die der Gruppe zugewiesenen LPs aufgelistet.

Beachten Sie, dass gültige Werte für die CPU-Abdeckung im Bereich [0, 65536] liegen und dass diese Werte die Gruppen Abdeckung in Prozent (z. b. 32768 = 50%) Ausdrücken.

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>Beispiel 3 – Drucken einer einzelnen CPU-Gruppe

In diesem Beispiel Fragen wir eine einzelne CPU-Gruppe mithilfe der groupid als Filter ab.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>Beispiel 4 – Erstellen einer neuen CPU-Gruppe

Hier erstellen wir eine neue CPU-Gruppe, die die Gruppen-ID und den Satz von LPs angibt, der der Gruppe zugewiesen werden soll.

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

Zeigen Sie jetzt die neu hinzugefügte Gruppe an.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>Beispiel 5 – Festlegen der CPU-Gruppen Abdeckung auf 50%

Hier legen wir das Limit für die CPU-Gruppe auf 50% fest.

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

Nun bestätigen wir unsere Einstellung, indem wir die soeben aktualisierte Gruppe anzeigen.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>Beispiel 6 – Drucken von CPU-Gruppen-IDs für alle virtuellen Computer auf dem Host

```console
C:\vm\tools>CpuGroups.exe GetVmGroup

VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36ab08cb-3a76-4b38-992e-000000000002
```

### <a name="example-7--unbind-a-vm-from-the-cpu-group"></a>Beispiel 7 – Aufheben der Bindung eines virtuellen Computers an die CPU-Gruppe

Wenn Sie einen virtuellen Computer aus einer CPU-Gruppe entfernen möchten, legen Sie die cpugroupid der VM auf die GUID NULL fest. Dadurch wird die Bindung der VM an die CPU-Gruppe entbindet.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000

C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>Beispiel 8 – Binden eines virtuellen Computers an eine vorhandene CPU-Gruppe

Hier fügen wir eine VM zu einer vorhandenen CPU-Gruppe hinzu.
Beachten Sie, dass der virtuelle Computer nicht an eine vorhandene CPU-Gruppe gebunden werden darf, oder das Festlegen der CPU-Gruppen-ID schlägt fehl.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

Vergewissern Sie sich nun, dass der virtuelle Computer in der gewünschten CPU-Gruppe ist.

```console
C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36AB08CB-3A76-4B38-992E-000000000001
```

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>Beispiel 9 – Drucken aller VMS gruppiert nach CPU-Gruppen-ID

```console
C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId                           VmName                                 VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36ab08cb-3a76-4b38-992e-000000000003     P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004     P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>Beispiel 10 – Drucken aller VMs für eine einzelne CPU-Gruppe

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>Beispiel 11 – Versuch, eine nicht leere CPU-Gruppe zu löschen

Nur leere CPU-Gruppen – d. h. CPU-Gruppen ohne gebundene VMs – können gelöscht werden.
Beim Versuch, eine nicht leere CPU-Gruppe zu löschen, tritt ein Fehler auf.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>Beispiel 12 – Aufheben der Bindung des einzigen virtuellen Computers an eine CPU-Gruppe und Löschen der Gruppe

In diesem Beispiel verwenden wir mehrere Befehle zum Überprüfen einer CPU-Gruppe, zum Entfernen der einzelnen VM, die zu dieser Gruppe gehört, und zum Löschen der Gruppe.

Zuerst zählen wir die VMs in unserer Gruppe.

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

Wir sehen, dass nur eine einzelne VM mit dem Namen "G1" zu dieser Gruppe gehört.
Entfernen Sie den virtuellen Computer mit dem Namen "G1" aus unserer Gruppe, indem Sie die Gruppen-ID der VM auf NULL festlegen.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

Und überprüfen Sie unsere Änderung...

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

Nachdem die Gruppe nun leer ist, können wir Sie problemlos löschen.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

Vergewissern Sie sich, dass die Gruppe nicht mehr vorhanden ist.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>Beispiel 13 – Binden eines virtuellen Computers an seine ursprüngliche CPU-Gruppe

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000002

C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId VmName VmId
------------------------------------ -------------------------------- ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002 G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002 G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36AB08CB-3A76-4B38-992E-000000000002 G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000003 P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004 P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```