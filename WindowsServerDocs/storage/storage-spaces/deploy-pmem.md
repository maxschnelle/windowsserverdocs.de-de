---
title: Grundlagen und Bereitstellen des persistenten Speicher
description: Ausführliche Informationen auf welche Arbeitsspeicher geht und wie sie mit Speicherplätzen in Windows Server-2019 direkte eingerichtet wird.
keywords: "\"Direkte Speicherplätze\", persistenten Speicher, Pmem, S2D-Speicher"
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: ed4b2669ad35a2ce0f818c65f7024ce905d9e4d6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280048"
---
---
# <a name="understand-and-deploy-persistent-memory"></a>Grundlagen und Bereitstellen des persistenten Speicher

>Gilt für: Windows Server 2019

Persistente Speicher (oder PMem) ist eine neue Art von Memory-Technologie, die eine eindeutige Kombination aus kostengünstige hohe Kapazitäten und Persistenz bietet. In diesem Thema wird die grundlegende PMem und die Schritte, mit Windows Server-2019 mit "direkte Speicherplätze" bereitstellen.

## <a name="background"></a>Hintergrund

PMem ist ein Typ von nicht flüchtigen DRAM (NVDIMM), die die Geschwindigkeit der DRAM, jedoch behält der Speicherinhalt über Power-Zyklen (den Speicherinhalt werden, auch wenn Systeme ausfallen bei einem nicht erwarteten Stromausfall, vom Benutzer initiierten Herunterfahrens, Systemabsturz usw.). Aus diesem Grund ist Reaktivierung aus, wo Sie aufgehört bedeutend schneller, da der Inhalt, der den Arbeitsspeicher nicht erneut geladen werden. Ein anderes eindeutiges Merkmal ist, dass PMem Byte adressierbar, was, dass Sie auch diese als Speicher verwenden können bedeutet (Was ist daher möglicherweise hören Sie PMem speicherklassenspeicher genannt wird).


Um einige dieser Vorteile anzuzeigen, sehen wir uns dieses Demo von Microsoft Ignite 2018:

[![Microsoft Ignite 2018 Pmem demo](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

Alle Speichersystem, die Fehlertoleranz unbedingt Kopien verteilte Schreibvorgänge, die über das Netzwerk übertragen und Back-End-Schreibvorgang Amplification verursacht. Aus diesem Grund werden die absoluten größten IOPS-Benchmark-Werte in der Regel nur Lesevorgänge erzielt, insbesondere, wenn das Speichersystem allgemein gebräuchlichen Optimierungen zum Lesen aus der lokalen Kopie, wann immer möglich, besitzt die "direkte Speicherplätze" ist.

**Lesevorgänge auf 100 % bietet der Cluster 13,798,674 IOPS.**

![Datensatz 13.7m IOPS-screenshot](media/deploy-pmem/iops-record.png)

Wenn Sie das Video genauer ansehen, werden Sie feststellen, des Thatwhat sogar weitere erfolgreiche Drag & Drop ist die Wartezeit: sogar auf mehr als 13.7 M-IOPS, meldet das Dateisystem in Windows Latenz, die durchgängig weniger als 40 µs ist! (Das ist das Symbol für Mikrosekunden, die ein-Millionstel einer Sekunde an.) Dies ist bedeutend schneller als was typische All-Flash-Anbietern man heute angekündigt werden soll.

Zusammen bieten "direkte Speicherplätze" in Windows Server-2019 und Intel® Optane™ DC persistenten Speicher bahnbrechende Leistung. Dieser branchenweit führenden HCI Benchmark über 13.7 m IOPS-Wert, mit vorhersagbare und äußerst niedrige Latenz und ist mehr als das doppelte unsere vorherigen branchenweit führenden-Benchmark 6,7 m IOPS-Wert. Ist dieses Mal wurde benötigt nur 12 Serverknoten zu 25 % weniger als zwei Jahren.

![IOPS-Effizienz](media/deploy-pmem/iops-gains.png)

Die Hardware, die verwendet wurde ein 12-Server-Cluster mit drei-Wege-Spiegelung und getrennt von ReFS-Volumes, **12** x Intel® S2600WFT, **384 GiB** Arbeitsspeicher, Kern 2 x 28 "CascadeLake" **1,5 TB**Intel® Optane™ DC persistenten Speicher als Cache **32 TB** NVMe (4 x 8 TB Intel® DC P4510) als Kapazität **2** x Mellanox ConnectX-4-25 Gbit/s

In der folgenden Tabelle verfügt über die volle Leistungszahlen: 

| Benchmark                   | Leistung         |
|-----------------------------|---------------------|
| 4K 100 % zufällig lesen         | 13,8 Millionen IOPS   |
| 4 K 90/10 % zufälliger Lese-/Schreibzugriff | 9.45 Millionen IOPS   |
| Sequenzielle Lese-2MB         | 549 GBIT/s Durchsatz |

### <a name="supported-hardware"></a>Unterstützte Hardware

Die folgende Tabelle zeigt unterstützte persistenten Speicherhardware für 2019 für Windows Server und Windows Server 2016. Beachten Sie, dass Intel Optane speziell sowohl Arbeitsspeicher und app-Direct-Modus unterstützt. Windows Server-2019 unterstützt Vorgänge im gemischten Modus.

| Persistent Memory-Technologie                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **NVDIMM-N-** im App-Direct-Modus                                       | Unterstützt                | Unterstützt                |
| **Intel Optane™ DC persistenten Speicher** im App-Direct-Modus             | Nicht unterstützt            | Unterstützt                |
| **Intel Optane™ DC persistenten Speicher** im 2-Level-Memory-Modus (2LM) | Nicht unterstützt            | Unterstützt                |

Nun, fangen Sie in der Konfiguration der persistenten Speicher.

## <a name="interleave-sets"></a>Interleave von Gruppen

### <a name="understanding-interleave-sets"></a>Grundlegendes zu einem interleave von Gruppen

Denken Sie daran, dass das NVDIMM-N in einem Slot standard DIMM (Speicher) befindet, platzieren Daten näher an den Prozessor (also verringert die Latenz und eine bessere Leistung abrufen). Um auf diese zu erstellen, ist ein Interleave Set beim Erstellen von zwei oder mehr NVDIMMs eine N-Wege-Interleave konfigurieren, um verteilt Lese-/Schreibvorgänge für erhöhten Durchsatz bereitzustellen. Die am häufigsten verwendeten Setups sind 2-Wege- oder 4-Wege-Überlappung.

Überlappende Gruppen können im BIOS einer Plattform zu mehreren persistenten Speicher-Geräten, die als einen einzigen logischen Datenträger auf Windows Server angezeigt werden häufig erstellt werden. Jeder persistenten Speicher logischer Datenträger enthält einen verschachtelten Satz von physischen Geräten mit:

```PowerShell
Get-PmemDisk
```

Eine Beispiel für die Ausgabe wird unten gezeigt:

```
DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Wir sehen, dass der logische Pmem Datenträger #2 physische Geräten Id20 und Id120 und logische Pmem Datenträger #3 physische Geräte der Id1020 und Id1120. Wir können auch einen bestimmten Pmem Datenträger zu Get-PmemPhysicalDevice zum Abrufen von alle seine physische NVDIMMs in die Interleave festlegen, wie unten gezeigt feed.


```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice
```

Eine Beispiel für die Ausgabe wird unten gezeigt:

```
DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleave-sets"></a>Konfigurieren von Sets verschachteln

Um einen Interleave-Satz zu konfigurieren, führen Sie das folgende PowerShell-Cmdlet aus:

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

Dies zeigt alle persistenten Speicher-Regionen, die auf einem Datenträger logischen persistenten Speicher auf dem System nicht zugewiesen.

Zum Anzeigen aller dem persistenten Speicher-Geräte-Informationen in das System, einschließlich Gerätetyp und Standort können Integrität und Betriebsstatus usw. Sie das folgende Cmdlet auf dem lokalen Server ausführen:

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

Da wir zur Verfügung, nicht verwendete Pmem Region verfügen, können wir neue persistenten Speicher-Datenträger erstellen. Wir können mehrere persistente Speicher-Datenträger, die mit den nicht verwendeten Bereichen von erstellen:

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

Ater Dies erfolgt, können wir die Ergebnisse mit finden Sie unter:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Es ist erwähnenswert, dass wir ausgeführt haben, können **Get-PhysicalDisk | In dem MediaType - Eq SCM** anstelle von **Get-PmemDisk** um die gleichen Ergebnisse zu erhalten. Der neu erstellten persistenten Speicher, Datenträger entspricht 1:1 für Laufwerke, die in PowerShell und Windows Admin Center angezeigt werden.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>Verwenden von persistenten Speicher für den Cache oder Kapazität

"Direkte Speicherplätze" in Windows Server-2019 unterstützt die Verwendung von persistenten Speicher als ein Cache oder ein Kapazität-Laufwerk. Finden Sie in diesem [Dokumentation](understand-the-cache.md) für Weitere Informationen zum Einrichten von Cache und die Kapazität.

## <a name="creating-a-dax-volume"></a>Erstellen eine DAX-Volume

### <a name="understanding-dax"></a>Grundlegendes zu DAX

Es gibt zwei Methoden für den Zugriff auf persistenten Speicher. Die Überladungen sind:

1. **Direkter Zugriff auf (DAX)** , das ausgeführt wird, wie Speicher, um die geringste Latenz zu erhalten. Die app ändert direkt den persistenten Speicher, den Stapel zu umgehen. Beachten Sie, dass dies nur mit NTFS verwendet werden kann.
2. **Blockieren des Zugriffs**, das ausgeführt wird, wie Speicher für app-Kompatibilität. Die Daten fließen über den Stapel bei diesem Setup aus, und dies kann mit NTFS und ReFS verwendet werden.

Ein Beispiel hierfür sehen Sie nachfolgend:

![DAX-stack](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>Konfigurieren von DAX

Wir müssen PowerShell-Cmdlets verwenden, um ein DAX-Volume auf einem persistenten Speicher zu erstellen. Mithilfe der **- IsDax** Switch, wir können Formatieren eines Volumes DAX aktiviert werden.

```PowerShell
Format-Volume -IsDax:$true
```

Der folgende Codeausschnitt hilft Sie eine DAX-Volume auf einem persistenten Speicher-Datenträger zu erstellen.

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

## <a name="monitoring-health"></a>Überwachen des Zustands

Wenn Sie persistenten Speicher verwenden, stehen einige Unterschiede bei der die zu gestalten:

1. Persistenten Speicher erstellen nicht physischen Datenträger, Leistungsindikatoren, sodass Sie nicht sehen, dass wenn in den Diagrammen Windows Admin Center angezeigt werden.
2. Persistenten Speicher erstellt keine Storport 505-Daten, damit Sie proaktiv ausreißererkennung erhalten.

Abgesehen, dass ist die überwachungsoberfläche für identisch mit einem beliebigen anderen physischen Datenträger. Sie können die Integrität eines persistenten Speicher Datenträgers durch Ausführen von Abfragen:

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

**HealthStatus** zeigt an, wenn der persistente Speicher, Datenträger fehlerfrei ist. Die **UnsafeshutdownCount** verfolgt die Anzahl der Herunterfahren, die diesen logischen Datenträger zu Datenverlusten führen kann. Es ist die Summe der die Anzahl der unsicheren Herunterfahren aller zugrunde liegenden permanenten Speicher Geräte des Datenträgers. Wir können auch die folgenden Befehle aus, um Integritätsinformationen für die Abfrage. Die **OperationalStatus** und **OperationalDetails** enthalten weitere Informationen zum Integritätsstatus.

So fragen Sie die Integrität des persistenten Speicher-Gerät:

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Dies zeigt, welches Gerät persistenten Speicher fehlerhaft ist. Das Gerät fehlerhaft ( **"DeviceID"** ) 20 beachtet die Groß-und Kleinschreibung im obigen Beispiel. Die **PhysicalLocation** von BIOS können Sie identifizieren die persistenten Speicher Gerät befindet sich im fehlerhaften Zustand versetzt.

## <a name="replacing-persistent-memory"></a>Ersetzen persistenten Speicher

Oben beschrieben, wie den Integritätsstatus Ihrer persistenten Speicher angezeigt. Wenn Sie ein fehlerhaftes Modul ersetzen möchten, müssen Sie den permanenten Speicher, Datenträger erneut bereitstellen (siehe die Schritte, die wir oben beschriebenen).

Bei der Problembehandlung müssen Sie möglicherweise verwenden **Remove-PmemDisk**, das einen bestimmte permanente Speicher, Datenträger entfernt. Wir können alle aktuellen persistente Datenträger durch entfernen:

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

Es ist wichtig zu beachten, dass das Entfernen eines Datenträgers persistenten Speicher zu Datenverlust auf diesem Datenträger führt.

Ist ein anderes Cmdlet müssen Sie möglicherweise **Initialize-PmemPhysicalDevice**, wird der Bereich für die Speicherung Bezeichnung auf den Geräten physischen persistenten Speicher initialisiert. Dies kann verwendet werden, um beschädigte Bezeichnung Speicherinformationen für den persistenten Speicher-Geräten zu löschen.

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

Es ist wichtig zu beachten, dass dieser Befehl als letzte Möglichkeit verwendet werden soll, um persistenten Speicher zu beheben Probleme im Zusammenhang mit. Dies führt zu Datenverlust auf den persistenten Speicher.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Integritätsverwaltung für Storage-Class Memory (NVDIMM-N) in Windows](storage-class-memory-health.md)
- [Grundlegendes zum Cache](understand-the-cache.md)