---
title: Verstehen und Bereitstellen von persistentem Speicher
description: Ausführliche Informationen dazu, was beständiger Speicher ist und wie Sie ihn mit "direkte Speicherplätze" in Windows Server 2019 einrichten können.
keywords: Direkte Speicherplätze, persistenter Speicher, pMem, Speicher, S2D
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 549cc6dbeec3d414e886f6ebf32315ae13627812
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71940810"
---
---
# <a name="understand-and-deploy-persistent-memory"></a>Verstehen und Bereitstellen von persistentem Speicher

>Gilt für: Windows Server 2019

Persistenter Speicher (oder pMem) ist eine neue Art von Speichertechnologie, die eine eindeutige Kombination aus kostengünstiger, umfangreicher Kapazität und Persistenz bietet. Dieses Thema enthält Hintergrundinformationen zu pMem und die Schritte zum Bereitstellen der Anwendung mit Windows Server 2019 mit direkte Speicherplätze.

## <a name="background"></a>Hintergrund

PMem ist ein nicht flüchtiger RAM (nvdimm), der seinen Inhalt durch Energie Zyklen beibehält. Die Speicherinhalte verbleiben auch dann, wenn die Systemleistung bei einem unerwarteten Stromausfall, von einem Benutzer initiierten Herunterfahren, einem Systemabsturz usw. ausfällt. Dieses eindeutige Merkmal bedeutet, dass Sie pMem auch als Speicher verwenden können. aus diesem Grund können Sie sehen, dass pMem als "Speicher Klassen Speicher" bezeichnet wird.

Um einige dieser Vorteile anzuzeigen, sehen Sie sich die Demo von Microsoft Ignite 2018 an:

[![Microsoft Ignite 2018 pMem-Demo](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

Alle Speichersysteme, die Fehlertoleranz bereitstellen, machen notwendigerweise verteilte Kopien von Schreibvorgängen aus, die das Netzwerk durchlaufen müssen und die Back-End-Schreib Verstärkung verursacht. Aus diesem Grund werden die absoluten größten IOPS-benchmarknummern in der Regel nur mit Lesevorgängen erzielt, insbesondere wenn das Speichersystem über allgemeine Optimierungen verfügt, um möglichst aus der lokalen Kopie zu lesen, was direkte Speicherplätze.

**Bei 100% Lesevorgängen stellt der Cluster 13.798.674 IOPS bereit.**

![Bildschirm Abbildung von 13,7 Mio. IOPS-Datensatz](media/deploy-pmem/iops-record.png)

Wenn Sie das Video genau ansehen, werden Sie feststellen, dass die Latenz durch eine noch größere Anzahl von Unterbrechungen verringert wird: sogar bei mehr als 13,7 Mio. IOPS meldet das Dateisystem in Windows eine Latenzzeit, die durchgängig weniger als 40 μs ist! (Das ist das Symbol für Mikrosekunden, ein Millionstel einer Sekunde.) Dies ist eine Größenordnung, die schneller ist als die von allen Flash Anbietern, die heute stolz angekündigt werden.

Direkte Speicherplätze in Windows Server 2019 und Intel® optane™ DC persistente Arbeitsspeicher bieten eine bahnbrechende Leistung. Dieser branchenführende HCI-Benchmark mit mehr als 13,7 Mio. IOPS mit vorhersag barer und extrem geringer Latenzzeit ist größer als die doppelte Version von 6.7 Mio. IOPS. Weitere Informationen: dieses Mal benötigte ich nur 12 Server Knoten, 25% vor weniger als zwei Jahren.

![IOPS-Zuwachs](media/deploy-pmem/iops-gains.png)

Bei der verwendeten Hardware handelt es sich um einen 12-Server-Cluster mit drei-Wege-Spiegelung und durch Trennzeichen getrennten Refs-Volumes, **12** x Intel® S2600WFT, **384 gib** Memory, 2 x 28-Core "cascadelake", **1,5 TB** Intel® optane™ DC persistenten Speicher als Cache, **32 TB** nvme ( 4 x 8 TB Intel® DC P4510) als Kapazität, **2** x Mellanox ConnectX-4 25 Gbit/s

Die folgende Tabelle enthält die vollständigen Leistungs Nummern: 

| Richtungs                   | Leistung         |
|-----------------------------|---------------------|
| 4K 100% zufälliger Lesevorgang         | 13,8 Millionen IOPS   |
| 4K 90/10% zufälliger Lese-/Schreibzugriff | 9.450.000 IOPS   |
| 2 MB sequenzieller Lesevorgang         | Durchsatz von 549 GB/s |

### <a name="supported-hardware"></a>Unterstützte Hardware

Die folgende Tabelle zeigt die unterstützte persistente Speicherhardware für Windows Server 2019 und Windows Server 2016. Beachten Sie, dass Intel optane sowohl Speicher (d.h. flüchtig) als auch APP Direct unterstützt (d. h. persistente Modi).

| Persistente Speichertechnologie                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **Nvdimm-N** im persistenten Modus                                  | Unterstützt                | Unterstützt                |
| **Intel optane™ persistenter Speicher** im App-direkt Modus             | Nicht unterstützt            | Unterstützt                |
| **Intel optane™ persistenter Speicher** im Speicher Modus | Unterstützt            | Unterstützt                |

Sehen wir uns nun an, wie Sie persistenten Speicher konfigurieren.

## <a name="interleave-sets"></a>Interleave-Sätze

### <a name="understanding-interleave-sets"></a>Grundlegendes zu Interleave-Sätzen

Beachten Sie, dass sich ein nvdimm in einem standardmäßigen DIMM-Slot (Arbeitsspeicher) befindet, wobei die Daten näher am Prozessor abgelegt werden (wodurch die Latenz reduziert und die Leistung verbessert wird). Um dies zu ermöglichen, wird ein Interleave festgelegt, wenn zwei oder mehr nvdimms eine N-Wege-Interleave-Menge erstellen, um die Lese-/Schreibvorgänge von Streifen für einen höheren Durchsatz bereitzustellen. Die gängigsten Setups sind 2-Wege-oder 4-Wege-Interleaving.

Überlappende Sätze können häufig im BIOS einer Plattform erstellt werden, damit mehrere persistente Speichergeräte als einzelner logischer Datenträger zu Windows Server angezeigt werden. Jeder permanente logische Speicher Datenträger enthält eine verschachtelte Gruppe physischer Geräte durch Ausführen von:

```PowerShell
Get-PmemDisk
```

Eine Beispielausgabe ist unten dargestellt:

```
DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Wir sehen, dass die logische pMem-Datenträger #2 physische Geräte Id20 und Id120 und logischer pMem-Datenträger #3 die physische Geräte Id1020 und Id1120 hat. Wir können auch eine bestimmte pMem-Festplatte an Get-pmemphysicaldevice übergeben, um alle physischen nvdimms im Interleave-Satz abzurufen, wie unten gezeigt.


```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice
```

Eine Beispielausgabe ist unten dargestellt:

```
DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleave-sets"></a>Konfigurieren von Interleave-Sätzen

Um einen Interleave-Satz zu konfigurieren, führen Sie das folgende PowerShell-Cmdlet aus:

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

Dadurch werden alle persistenten Speicherbereiche angezeigt, die keinem logischen permanenten Speicher Datenträger im System zugewiesen sind.

Sie können das folgende Cmdlet auf dem lokalen Server ausführen, um alle persistenten Speichergeräte Informationen im System anzuzeigen (z. b. Gerätetyp, Speicherort, Integritäts-und Betriebsstatus usw.).

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile
                                                                                                                      memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Da wir nicht genutzte pMem-Regionen verfügbar haben, können wir neue persistente Speicher Datenträger erstellen. Wir können mehrere persistente Speicher Datenträger mithilfe der nicht verwendeten Regionen erstellen:

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

Wenn dies der Fall ist, können wir die Ergebnisse sehen, indem wir Folgendes ausführen:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Beachten Sie, dass Sie " **Get-PhysicalDisk" ausführen könnten. Dabei ist "MediaType-EQ SCM** " anstelle von " **Get-pmemdisk** ", um dieselben Ergebnisse zu erhalten. Der neu erstellte persistente Speicher Datenträger entspricht 1:1 den Laufwerken, die in PowerShell und Windows Admin Center angezeigt werden.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>Verwenden von persistenten Speicher für Cache oder Kapazität

Direkte Speicherplätze unter Windows Server 2019 unterstützt die Verwendung von persistentem Speicher als Cache-oder Kapazitäts Laufwerk. Weitere Informationen zum Einrichten von Cache-und Kapazitäts Laufwerken finden Sie in dieser [Dokumentation](understand-the-cache.md) .

## <a name="creating-a-dax-volume"></a>Erstellen eines DAX-Volumes

### <a name="understanding-dax"></a>Grundlegendes zu DAX

Es gibt zwei Methoden, um auf permanenten Speicher zuzugreifen. Die Überladungen sind:

1. **Direkter Zugriff (DAX)** , der wie der Arbeitsspeicher funktioniert, um die geringste Latenz zu erzielen. Die app ändert den persistenten Speicher direkt, wobei der Stapel umgangen wird. Beachten Sie, dass dies nur mit NTFS verwendet werden kann.
2. **Blockieren**Sie den Zugriff, der wie der Speicher für die APP-Kompatibilität funktioniert. Die Daten fließen in diesem Setup in den Stapel und können mit NTFS und Refs verwendet werden.

Ein Beispiel hierfür finden Sie unten:

![DAX-Stapel](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>Konfigurieren von DAX

Wir müssen PowerShell-Cmdlets verwenden, um ein DAX-Volume in einem permanenten Speicher zu erstellen. Mithilfe des **-isdax-** Schalters können wir ein Volume so formatieren, dass es Dax aktiviert ist.

```PowerShell
Format-Volume -IsDax:$true
```

Der folgende Code Ausschnitt hilft Ihnen beim Erstellen eines DAX-Volumes auf einem persistenten Speicher Datenträger.

```PowerShell
# Here we use the first pmem disk to create the volume as an example
$disk = (Get-PmemDisk)[0] | Get-PhysicalDisk | Get-Disk
# Initialize the disk to GPT if it is not initialized
If ($disk.partitionstyle -eq "RAW") {$disk | Initialize-Disk -PartitionStyle GPT}
# Create a partition with drive letter 'S' (can use any available drive letter)
$disk | New-Partition -DriveLetter S -UseMaximumSize


   DiskPath: \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{53f56307-b6
bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                               Size Type
---------------  ----------- ------                                               ---- ----
2                S           16777216                                        251.98 GB Basic

# Format the volume with drive letter 'S' to DAX Volume
Format-Volume -FileSystem NTFS -IsDax:$true -DriveLetter S

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
S                        NTFS           Fixed     Healthy      OK                    251.91 GB 251.98 GB

# Verify the volume is DAX enabled
Get-Partition -DriveLetter S | fl


UniqueId             : {00000000-0000-0000-0000-000100000000}SCMLD\VEN_8980&DEV_097A&SUBSYS_89804151&REV_0018\3&1B1819F6&0&03018089F
                       B63494DB728D8418B3CBBF549997891:WIN-8KGI228ULGA
AccessPaths          : {S:\, \\?\Volume{cf468ffa-ae17-4139-a575-717547d4df09}\}
DiskNumber           : 2
DiskPath             : \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{5
                       3f56307-b6bf-11d0-94f2-00a0c91efb8b}
DriveLetter          : S
Guid                 : {cf468ffa-ae17-4139-a575-717547d4df09}
IsActive             : False
IsBoot               : False
IsHidden             : False
IsOffline            : False
IsReadOnly           : False
IsShadowCopy         : False
IsDAX                : True                   # <- True: DAX enabled
IsSystem             : False
NoDefaultDriveLetter : False
Offset               : 16777216
OperationalStatus    : Online
PartitionNumber      : 2
Size                 : 251.98 GB
Type                 : Basic
```

## <a name="monitoring-health"></a>Überwachen der Integrität

Wenn Sie permanenten Speicher verwenden, gibt es einige Unterschiede bei der Überwachung:

1. Der persistente Speicher erstellt keine Leistungsindikatoren für physische Datenträger, sodass Sie nicht sehen, ob in Diagrammen im Windows Admin Center angezeigt wird.
2. Der persistente Speicher erstellt keine Storport 505-Daten, sodass Sie keine proaktive Ausreißererkennung erhalten.

Abgesehen davon ist die Überwachungsfunktion mit jeder anderen physischen Festplatte identisch. Sie können die Integrität eines permanenten Speicher Datenträgers Abfragen, indem Sie Folgendes ausführen:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Unhealthy    None          True         {20, 120}         2
3          252 GB Healthy      None          True         {1020, 1120}      0

Get-PmemDisk | Get-PhysicalDisk | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails

SerialNumber               HealthStatus OperationalStatus  OperationalDetails
------------               ------------ ------------------ ------------------
802c-01-1602-117cb5fc      Healthy      OK
802c-01-1602-117cb64f      Warning      Predictive Failure {Threshold Exceeded,NVDIMM_N Error}
```

**Healthstatus** zeigt an, ob der persistente Speicher Datenträger fehlerfrei ist. Mit **unsafeshutdowncount** wird die Anzahl der Herunterfahr Vorgänge nachverfolgt, die auf diesem logischen Datenträger zu Datenverlusten führen können. Dies ist die Summe der unsicheren Beendigungs Anzahl aller zugrunde liegenden permanenten Speichergeräte dieses Datenträgers. Wir können auch die folgenden Befehle verwenden, um Integritäts Informationen abzufragen. **OperationalStatus** und **operationaldetails** bieten weitere Informationen zum Integritäts Status.

So Fragen Sie den Zustand des permanenten Speichergeräts ab:

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Dadurch wird angezeigt, welches persistente Speichergerät fehlerhaft ist. Das fehlerhafte Gerät **(Geräte**-ID) 20 entspricht dem Fall im obigen Beispiel. Mithilfe der **PhysicalLocation** von BIOS kann ermittelt werden, welches persistente Speichergerät sich in einem fehlerhaften Zustand befindet.

## <a name="replacing-persistent-memory"></a>Ersetzen von persistenten Speicher

Oben wurde beschrieben, wie Sie den Integritäts Status ihres permanenten Speichers anzeigen. Wenn Sie ein fehlerhafter Modul ersetzen müssen, müssen Sie den persistenten Speicher Datenträger erneut bereitstellen (Weitere Informationen finden Sie in den oben beschriebenen Schritten).

Bei der Problembehandlung müssen Sie möglicherweise **Remove-pmemdisk**verwenden, wodurch ein bestimmter persistenter Speicher Datenträger entfernt wird. Alle aktuellen permanenten Datenträger können wie folgt entfernt werden:

```PowerShell
Get-PmemDisk | Remove-PmemDisk

cmdlet Remove-PmemDisk at command pipeline position 1
Supply values for the following parameters:
DiskNumber: 2

This will remove the persistent memory disk(s) from the system and will result in data loss.
Remove the persistent memory disk(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
Removing the persistent memory disk. This may take a few moments.
```

Beachten Sie, dass das Entfernen eines permanenten Speicher Datenträgers auf diesem Datenträger zu Datenverlusten führt.

Ein weiteres Cmdlet, das Sie möglicherweise benötigen, ist " **initialisieren-pmemphysicaldevice**", mit dem der Speicherbereich "Bezeichnung" auf den physischen permanenten Speichergeräten initialisiert wird. Dies kann verwendet werden, um beschädigte Speicherinformationen für die Bezeichnung auf den persistenten Speichergeräten zu löschen.

```PowerShell
Get-PmemPhysicalDevice | Initialize-PmemPhysicalDevice

This will initialize the label storage area on the physical persistent memory device(s) and will result in data loss.
Initializes the physical persistent memory device(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): A
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
```

Beachten Sie, dass dieser Befehl als letztes Mittel zum Beheben von permanenten speicherbezogenen Problemen verwendet werden sollte. Dies führt zu Datenverlusten im persistenten Speicher.

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Integritäts Verwaltung für Speicher Klassen Speicher (nvdimm-N) in Windows](storage-class-memory-health.md)
- [Grundlegendes zum Cache](understand-the-cache.md)
