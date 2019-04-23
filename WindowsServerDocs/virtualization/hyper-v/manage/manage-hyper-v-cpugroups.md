---
title: Die Steuerung der VM-Ressourcen
description: Verwenden von VM-CPU-Gruppen
keywords: Windows 10, Hyper-V
author: allenma
ms.date: 06/18/2018
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: 7c4ddf3e5d2ff58eef844c50960327c27a3e0a3d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854761"
---
>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

# <a name="virtual-machine-resource-controls"></a>Die Steuerung der VM-Ressourcen

Dieser Artikel beschreibt die Hyper-V-Ressourcen und Isolation-Steuerelemente für virtuelle Computer.  Diese Funktionen, die wir als VM-CPU-Gruppen oder nur "CPU-Gruppen" verweisen müssen, wurden in Windows Server 2016 eingeführt.  CPU-Gruppen können Hyper-V-Administratoren zum besseren Verwalten und Zuweisen von Host CPU-Ressourcen in virtuellen Gastcomputern.  Mithilfe von CPU-Gruppen können Hyper-V-Administratoren:

* Erstellen Sie Gruppen von virtuellen Computern, wobei jede Gruppe, die mit unterschiedlichen Zuordnungen dem Virtualisierungshost-Gesamt-CPU-Ressourcen, für die gesamte Gruppe freigegeben. Dadurch kann der hostadministrator Klassen des Diensts für verschiedene Arten von virtuellen Computern implementieren.

* Legen Sie Grenzwerte für CPU-Ressource auf bestimmte Gruppen. Dieses Endes"Gruppe" legt die CPU-Ressourcen, die die gesamte Gruppe erzwingen die gewünschte Klasse des Diensts für diese Gruppe effektiv nutzen kann, die obere Grenze für den Host fest.

* Beschränken Sie eine CPU-Gruppe nur auf eine bestimmte Gruppe von Prozessoren für das Hostsystem ausgeführt. Dies kann verwendet werden, um VMs, die für verschiedene CPU-Gruppen gehören, voneinander zu isolieren.

## <a name="managing-cpu-groups"></a>Verwalten von CPU-Gruppen

CPU-Gruppen werden über die Hyper-V-Host-Compute-Dienst oder HCS verwaltet. Eine hervorragende Beschreibung für die HCS, dessen Genesis, Links zu den HCS-APIs und mehr finden Sie auf der Microsoft Virtualization-Team-Blog, in der Bereitstellung [Einführung in die Host Compute Service (HCS)](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/).

>[!NOTE] 
>Nur der HCS kann zum Erstellen und Verwalten von CPU-Gruppen verwendet werden. Das Hyper-V-Manager-Applet, WMI und PowerShell Management-Schnittstellen unterstützen keine CPU-Gruppen.

Microsoft bietet eine Befehlszeile-Hilfsprogramm, cpugroups.exe, auf die [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=865968) die die HCS-Schnittstelle zum Verwalten von CPU-Gruppen verwendet.  Dieses Hilfsprogramm kann auch die CPU-Topologie eines Hosts anzeigen.

## <a name="how-cpu-groups-work"></a>Funktionsweise von CPU-Netzwerksicherheitsgruppen

Zuordnung von Host-Compute-Ressourcen auf CPU-Gruppen wird von der Hyper-V-Hypervisor, eine berechnete Gruppe Obergrenze für CPU-Verwendung erzwungen. Die Obergrenze der CPU-Gruppe ist ein Bruchteil der gesamten CPU-Kapazität für eine CPU-Gruppe. Der Wert der Gruppe Abdeckung hängt davon ab, der Gruppe oder zugewiesene Prioritätsstufe. Die Obergrenze für das berechnete Gruppe kann als "Anzahl von LP's sollte der CPU-Zeit" betrachtet werden. Diese Gruppe Budget freigegeben werden ist, wenn nur ein einzelner virtueller Computer aktiv waren, damit die gesamte Gruppe CPU-ressourcenzuteilung für sich selbst verwendet werden können.

Die Obergrenze der CPU-Gruppe wird berechnet, als G = *n* x *C*, wobei:

    *G* is the amount of host LP we'd like to assign to the group
    *n* is the total number of logical processors (LPs) in the group
    *C* is the maximum CPU allocation — that is, the class of service desired for the group, expressed as a percentage of the system’s total compute capacity

Betrachten Sie beispielsweise eine konfigurierte mit 4 logischen Prozessoren (LPs), und eine Obergrenze von 50 % CPU-Gruppe.

    G = n * C
    G = 4 * 50%
    G = 2 LP's worth of CPU time for the entire group

In diesem Beispiel wird die CPU-Gruppe G 2 LP's sollte der CPU-Zeit zugeordnet.  

Beachten Sie, die die Obergrenze für die Gruppe angewendet wird, unabhängig von der Anzahl von virtuellen Computern oder virtuellen Prozessoren, die der Gruppe gebunden, und unabhängig vom Status (z. B. Herunterfahren oder gestartet) der virtuellen Computer, die die CPU-Gruppe zugewiesen. Aus diesem Grund jede VM, die an der gleichen Gruppe von CPU-gebunden wird einen Bruchteil der Gruppe Gesamt-CPU-ressourcenzuteilung erhalten und dadurch ändert sich mit der Anzahl von VMs, die der Gruppe "CPU" gebunden. Aus diesem Grund wie VMs gebunden sind oder eine Gruppe von CPU-VMs aufgehoben, muss eine Obergrenze für das gesamte CPU-Gruppe angepasst und die resultierende pro virtuellem Computer Obergrenze gewünscht verwalten. Die VM-hostverwaltung an Administrator "oder" Virtualisierung Softwareschicht ist verantwortlich für die Verwaltung von Gruppe-Caps wie erforderlich, um die gewünschten pro-VM-CPU-ressourcenzuteilung zu erreichen.

## <a name="example-classes-of-service"></a>Beispiel-Klassen des Diensts

Betrachten wir nun einige einfache Beispiele. Zunächst wird davon ausgegangen Sie, dass der Hyper-V-Host-Administrator für zwei Tarife an für Gast-VMs unterstützen möchten:

1. Eine Low-End "C"-Ebene. Wir geben diesem Tarif 10 % der Compute-Ressourcen für den gesamten Host.

1. Eine Ebene mit mittlerem "B". Dieser Tarif ist 50 % der Compute-Ressourcen für den gesamten Host zugeordnet.

In unserem Beispiel werden wir an diesem Punkt bestätigt, dass keine anderen CPU-Ressource Steuerelemente verwendet werden, wie z. B. Clientzugriffspunkten für einzelne VM, Gewichtung und reserviert.
Einzelne VM-Caps sind jedoch wichtig, wie wir etwas später sehen werden.

Der Einfachheit halber gehen wir von jedem virtuellen Computer "1" wurde VP und unseren Hosts 8 LPs hat. Wir beginnen mit einem leeren Host.

Um den Tarif "B" zu erstellen, wird der Host Adminstartor die Obergrenze für die Gruppe auf 50 % festgelegt:

    G = n * C
    G = 8 * 50%
    G = 4 LP's worth of CPU time for the entire group

Der hostadministrator Fügt einer einzelnen Ebene befinden "B" virtuellen Computer hinzu.
An diesem Punkt können unsere Stufe ""B"" virtuellen Computer darf höchstens 50 % sollte der Host CPU oder einer entsprechenden Gruppe von 4 LPs in unserem Beispiel System.

Der Administrator fügt nun eine zweite "Tier-B" virtuellen Computer. Zuordnung von der CPU-Gruppe – wird gleichmäßig auf alle virtuellen Computer. Wir haben insgesamt 2 VMs in Gruppe B, damit jeder virtuelle Computer nun die Hälfte der Gruppe B die Gesamtanzahl von 50 %, 25 % oder das Äquivalent der 2 LPs sollte der Compute-Zeit ruft.

## <a name="setting-cpu-caps-on-individual-vms"></a>Festlegen von CPU-Caps auf einzelnen VMs

Zusätzlich zu die Obergrenze für die Gruppe kann jeder virtuelle Computer auch eine einzelnen "virtuellen Computer Cap" verfügen. Steuerung des pro virtuellem Computer-CPU-Ressourcen, wie z.B. eine Obergrenze für CPU-Gewichtung und reservieren, wurden ein Teil der Hyper-V seit der Einführung.
In Kombination mit einer Obergrenze für die Gruppe gibt eine Obergrenze für die virtuellen Computer die maximale Menge an CPU, die jede VP abrufen können, auch wenn die Gruppe verfügbaren CPU-Ressourcen aufweist.

Beispielsweise möchten die Host-Administrator eine VM-Obergrenze von 10 % auf "C" virtuellen Computern platzieren.
Auf diese Weise auch, wenn die meisten "C" VPs im Leerlauf sind, konnte jeder VP nie mehr als 10 % abgerufen werden.
Ohne Beschränkung für die VM konnte "C" VMs Leistung über die Ebene zulässigen Ebenen opportunistisch erzielen.

## <a name="isolating-vm-groups-to-specific-host-processors"></a>Isolieren von VM-Gruppen auf bestimmten Host-Prozessoren

Hyper-V-Host-Administratoren sollten auch die Möglichkeit, computeressourcen für einen virtuellen Computer zur Verfügung stellen.
Nehmen wir z.B. möchten, dass der Administrator einen Premium-Angebot "ein" virtueller Computer, der eine Klasse Abdeckung von 100 % aufweist.
Diese Premium-VMs auch erfordern die niedrigste Planung Latenz und jitter möglich; d. h., können sie nicht von anderen virtuellen Computern aufheben geplant werden.
Um diese Trennung zu erreichen, kann eine CPU-Gruppe auch mit einer bestimmten LP Affinität Zuordnung konfiguriert werden.

Z. B. zum Anpassen einer VM "ein" auf dem Host in unserem Beispiel der Administrator würde erstellen Sie eine neue CPU-Gruppe, und legen Sie die Prozessor-Affinität auf einen Teil des Hosts LPs der Gruppe.
Um die verbleibenden LPs würde die Gruppen B und C zugeordnet werden.
Der Administrator kann einen einzelnen virtuellen Computer in Gruppe A, die exklusiven Zugriff auf alle LPs in Gruppe A, während die Gruppen B auf vermutlich auf niedriger Ebene erstellen und C die verbleibenden LPs nutzen.

## <a name="segregating-root-vps-from-guest-vps"></a>Stamm VPs vom Gast VPs ausschließen

Standardmäßig wird Hyper-V auf einzelnen zugrunde liegenden physischen LP einen Stamm VP erstellen.
Diese Stamm VPs sind streng zugeordneten 1:1 mit dem System LPs und werden nicht migriert, d. h. jedes Stammelement VP immer auf dem gleichen physischen LP ausgeführt wird.
Gast-VPs kann auf alle verfügbaren LP ausgeführt werden, und Stamm VPs Ausführung freigegeben wird.

Allerdings kann es wünschenswert vollständig separaten Stamm VP-Aktivität von Gast VPs sein.
Betrachten Sie unsere Beispiel oben, in dem wir einen Premium-Tarif "A" virtuellen Computer implementieren.
Um sicherzustellen, dass unsere "A" des virtuellen Computers VPs die geringste Latenz und "jitter" oder Planung Variation verfügen, möchten wir sie auf eine dedizierte Gruppe von LPs ausführen, und stellen Sie sicher, dass das Stammverzeichnis für diese LPs nicht ausgeführt werden kann.

Dies geschieht mithilfe einer Kombination der Konfiguration "Minroot" den Host-Partition für das Betriebssystem begrenzt für die Ausführung auf einem Teil der logischen Prozessoren gesamtverfügbarkeit des Systems zusammen mit einem oder mehr CPU-Gruppen zugeordnet.

Virtualisierungshost kann konfiguriert werden, um die Hostpartition auf spezifische LPs, mit einer oder mehreren CPU-Gruppen zugeordnet, die verbleibenden LPs zu beschränken.
Auf diese Weise kann die Stamm- und Gast-Partitionen auf dedizierten Ressourcen der CPU ausgeführt werden können, und vollständig isoliert werden, ohne CPU-Freigabe.

Weitere Informationen zur Konfiguration "Minroot" finden Sie unter [Hyper-V-Host-CPU-Ressourcenverwaltung](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016).

## <a name="using-the-cpugroups-tool"></a>Mithilfe des Tools CpuGroups

Wir sehen uns einige Beispiele für das CpuGroups-Tool verwenden.

>[!NOTE] 
>Befehlszeilenparameter für das Tool CpuGroups übergeben werden, nur aus Leerzeichen als Trennzeichen verwenden. Keine '/' oder '-' Zeichen sollten den gewünschten Befehlszeilenschalter fortfahren.

### <a name="discovering-the-cpu-topology"></a>Ermitteln die CPU-Topologie

Informationen zum aktuellen Systems befinden, CpuGroups mit der GetCpuTopology Ausführung zurückgegeben werden, wie unten gezeigt, einschließlich der LP-Index, den NUMA-Knoten zu dem gehört die LP, das Paket und Core-IDs und der Stamm VP-Index.

Das folgende Beispiel zeigt ein System mit 2 CPU-Sockets und NUMA-Knoten, maximal 32 LPs und Multi-threading aktiviert und so konfiguriert, dass Minroot mit 8 Stamm VPs, 4 auf jedem NUMA-Knoten.
Der Stamm VPs denen LPs haben eine RootVpIndex > = 0; LPs mit einem RootVpIndex-1 sind nicht verfügbar ist, klicken Sie auf der Stammpartition, jedoch werden vom Hypervisor weiterhin verwaltet und Gast VPs werden ausgeführt werden, weil durch andere Konfigurationseinstellungen zulässig.

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

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>Beispiel 2 – Drucken alle CPU-Gruppen auf dem host

Wir müssen hier alle CPU-Gruppen auf dem aktuellen Host, ihre GroupId, CPU-Obergrenze für die Gruppe und die Indizes im Abschlussarray, der dieser Gruppe zugewiesenen LPs aufgelistet.

Beachten Sie, dass gültige CPU-Obergrenze für Werte im Bereich [0, 65536 liegen] und diese Werte die Obergrenze für die Gruppe in Prozent Express (z. B. 32768 = 50 %).

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>Beispiel 3: Drucken eine einzigen CPU-Gruppe

In diesem Beispiel werden wir eine einzelne CPU-Gruppe verwenden die Gruppen-ID als Filter Abfragen.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>Beispiel 4 – Erstellen einer neuen CPU-Gruppe

Hier erstellen wir eine neue CPU-Gruppe, die angeben, die Gruppen-ID und den Satz von LPs der Gruppe zuweisen.

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

Jetzt zeigen Sie unsere neu hinzugefügte Gruppe aus an.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>Beispiel 5 – festgelegt die Obergrenze der CPU-Gruppe auf 50 %.

Wir werden hier die Obergrenze der CPU-Gruppe auf 50 % festgelegt.

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

Jetzt bestätigen wir unsere Einstellung durch Anzeigen der Gruppe, die wir gerade aktualisiert.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>Beispiel 6 – Print CPU-Gruppen-Ids für alle virtuellen Computer, auf dem host

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

### <a name="example-7--unbind-a-vm-from-the-cpu-group"></a>Beispiel 7 – Unbind eines virtuellen Computers aus der Gruppe "CPU"

Um einen virtuellen Computer aus einer CPU-Gruppe zu entfernen, legen Sie auf CpuGroupId des virtuellen Computers, auf die NULL-GUID. Dies hebt die Bindung auf den virtuellen Computer aus der Gruppe "CPU".

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

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>Beispiel 8 – binden ein virtuellen Computers zu einer vorhandenen CPU-Gruppe

Hier fügen wir einen virtuellen Computer zu einer vorhandenen CPU-Gruppe.
Beachten Sie, dass der virtuelle Computer nicht werden, auf eine beliebige vorhandene CPU-Gruppe gebunden muss oder CPU-Gruppen-Id festlegen fehl.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

Nun, vergewissern Sie sich, dass die VM G1 in der gewünschten CPU-Gruppe ist.

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

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>Beispiel 9: Drucken von allen virtuellen Computern, gruppiert nach CPU-Gruppen-id

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

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>Beispiel 10 – Drucken alle virtuellen Computer für eine einzelne CPU-Gruppe

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>Beispiel 11 – es wird versucht, eine nicht leere CPU-Gruppe löschen

Nur leere CPU-Gruppen – d. h. CPU-Gruppen ohne virtuelle Computer gebunden – kann gelöscht werden.
Es wird versucht, eine nicht leere CPU-Gruppe zu löschen, schlägt fehl.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>Beispiel 12 – die einzige VM aus einer Gruppe von CPU-Bindung und die Gruppe löschen

In diesem Beispiel wir verwenden Sie mehrere Befehle zum Überprüfen einer CPU-Gruppenstatus, entfernen Sie die einzelnen virtuellen Computer, die zu dieser Gruppe gehören, und anschließend die Gruppe löschen.

Erstes Listen wir die virtuellen Computer in dieser Gruppe.

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

Sehen Sie, dass nur eine einzelne VM mit dem Namen G1, dieser Gruppe gehört.
Entfernen Sie die VM G1 wir aus unserer Gruppe durch Gruppen-ID des virtuellen Computers auf NULL festlegen.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

Und die Änderung überprüfen...

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

Nun, da die Gruppe leer ist, können wir problemlos löschen.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

Ein, und bestätigen Sie, dass dieser Gruppe nicht mehr vorhanden ist.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>Beispiel für 13 – binden ein virtuellen Computers wieder mit der ursprünglichen CPU-Gruppe

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
