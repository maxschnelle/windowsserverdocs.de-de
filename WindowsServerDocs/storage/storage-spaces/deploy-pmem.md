---
title: Grundlagen und Bereitstellung des persistenten Speichers
description: Ausführliche Informationen dazu, was beständiger Speicher ist und wie Sie ihn mit "direkte Speicherplätze" in Windows Server 2019 einrichten können.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 1/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2f5f88ac2ec728e176735ad58d9d67112583c527
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469645"
---
# <a name="understand-and-deploy-persistent-memory"></a>Grundlagen und Bereitstellung des persistenten Speichers

> Gilt für: Windows Server 2019

Persistenter Speicher (oder pMem) ist eine neue Art von Speichertechnologie, die eine eindeutige Kombination aus kostengünstiger, umfangreicher Kapazität und Persistenz bietet. Dieser Artikel bietet Hintergrundinformationen zu pMem und die Schritte zur Bereitstellung in Windows Server 2019 mithilfe direkte Speicherplätze.

## <a name="background"></a>Hintergrund

PMem ist ein nicht flüchtiger RAM (nvdimm), der seinen Inhalt durch Energie Zyklen beibehält. Die Speicherinhalte verbleiben auch dann, wenn die Systemleistung im Fall eines unerwarteten Stromausfalls, von einem Benutzer initiierten herunter Fahrens, eines Systemabsturzes usw. ausfällt. Dieses eindeutige Merkmal bedeutet, dass Sie pMem auch als Speicher verwenden können. Aus diesem Grund werden Sie vielleicht hören, dass Personen auf pMem als Speicher Klassen Speicher verweisen.

Um einige dieser Vorteile anzuzeigen, sehen Sie sich die folgende Demo von Microsoft Ignite 2018 an.

[![Microsoft Ignite 2018 pMem-Demo](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

Alle Speichersysteme, die Fehlertoleranz bereitstellen, machen notwendigerweise verteilte Kopien von Schreibvorgängen. Solche Vorgänge müssen das Netzwerk durchlaufen und den Back-End-Schreib Verkehr verstärken. Aus diesem Grund werden die absoluten größten IOPS-benchmarknummern normalerweise durch Messen von Lesevorgängen erzielt, insbesondere dann, wenn das Speichersystem, wenn möglich, über allgemeine Optimierungen zum Lesen aus der lokalen Kopie verfügt. Direkte Speicherplätze ist dafür optimiert.

**Wenn er nur mit Lesevorgängen gemessen wird, stellt der Cluster 13.798.674 IOPS bereit.**

![Bildschirm Abbildung von 13,7 Mio. IOPS-Datensatz](media/deploy-pmem/iops-record.png)

Wenn Sie das Video genau ansehen, werden Sie feststellen, dass die Latenz durch eine noch größere Anzahl von Unterbrechungen sinkt. Sogar bei mehr als 13,7 Mio. IOPS meldet das Dateisystem in Windows eine Latenzzeit, die konstant weniger als 40 μs! (Das ist das Symbol für Mikrosekunden, ein Millionstel einer Sekunde.) Diese Geschwindigkeit ist eine höhere Reihenfolge, als Sie heutzutage von allen Flash Anbietern angekündigt werden.

Die direkte Speicherplätze im permanenten Speicher von Windows Server 2019 und Intel &reg; optane &trade; DC bieten eine bahnbrechende Leistung. Dieser branchenführende HCI-Benchmark mit mehr als 13,7 Mio. IOPS, eine vorhersagbare und extrem geringe Latenzzeit, ist größer als der bisherige branchenführende Benchmarkwert von 6.7 Mio. IOPS. Weitere Informationen: dieses Mal benötigte ich nur 12 Server Knoten, die &mdash; 25% weniger als zwei Jahre vor dem Zeitpunkt liegen.

![IOPS-Zuwachs](media/deploy-pmem/iops-gains.png)

Die Testhardware war ein 12-Server-Cluster, der für die Verwendung von drei-Wege-Spiegelung und getrennten Refs-Volumes konfiguriert wurde. **12** x Intel &reg; S2600WFT, **384 gib** Memory, 2 x 28-Core "cascadelake", **1,5 TB** Intel &reg; optane &trade; DC Persistent Memory as Cache, **32 TB** nvme (4 x 8 TB Intel &reg; DC P4510) als Kapazität, **2** x Mellanox ConnectX-4 25 Gbit/s.

In der folgenden Tabelle werden die vollständigen Leistungszahlen angezeigt.

| Vergleichstest                   | Leistung         |
|-----------------------------|---------------------|
| 4K 100% zufälliger Lesevorgang         | 13,8 Millionen IOPS   |
| 4K 90/10% zufälliger Lese-/Schreibzugriff | 9.450.000 IOPS   |
| 2 MB sequenzieller Lesevorgang         | Durchsatz von 549 GB/s |

### <a name="supported-hardware"></a>Unterstützte Hardware

In der folgenden Tabelle wird die unterstützte persistente Speicherhardware für Windows Server 2019 und Windows Server 2016 angezeigt.

| Persistente Speichertechnologie                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **Nvdimm-N** im persistenten Modus                                  | Unterstützt                | Unterstützt                |
| **Intel optane &trade; Persistenter DC-Speicher** im App Direct-Modus             | Nicht unterstützt            | Unterstützt                |
| **Intel optane &trade; Persistenter DC-Speicher** im Speicher Modus | Unterstützt            | Unterstützt                |

> [!NOTE]
> Intel optane unterstützt sowohl den *Speicher* Modus (flüchtig) als auch den *App Direct* -Modus (persistent).

> [!NOTE]
> Wenn Sie ein System neu starten, das über mehrere Intel &reg; optane &trade; pMem-Module im App Direct-Modus verfügt, die in mehrere Namespaces aufgeteilt sind, verlieren Sie möglicherweise den Zugriff auf einige oder alle zugehörigen logischen Speicher Datenträger. Dieses Problem tritt auf Windows Server 2019-Versionen auf, die älter sind als Version 1903.
>
> Dieser Verlust des Zugriffs tritt auf, weil ein pMem-Modul untrainiert ist oder andernfalls fehlschlägt, wenn das System gestartet wird. In einem solchen Fall schlagen alle Storage-Namespaces in einem beliebigen pMem-Modul im System fehl, einschließlich Namespaces, die dem fehlerhaften Modul nicht physisch zugeordnet werden.
>
> Wenn Sie den Zugriff auf alle Namespaces wiederherstellen möchten, ersetzen Sie das fehlerhafte Modul.
>
> Wenn ein Modul unter Windows Server 2019 Version 1903 oder höher ausfällt, verlieren Sie nur den Zugriff auf Namespaces, die physisch dem betroffenen Modul zugeordnet sind. Andere Namespaces sind nicht betroffen.

Sehen wir uns nun an, wie Sie persistenten Speicher konfigurieren.

## <a name="interleaved-sets"></a>Verschachtelte Sätze

### <a name="understanding-interleaved-sets"></a>Grundlegendes zu verschachtelten Sätzen

Beachten Sie, dass sich ein nvdimm in einem standardmäßigen DIMM-Slot (Arbeitsspeicher) befindet, mit dem Daten näher an den Prozessor übergeben werden. Diese Konfiguration reduziert die Latenz und verbessert die Abruf Leistung. Um den Durchsatz weiter zu erhöhen, erstellen zwei oder mehr nvdimms eine n-Wege-überlappende Festlegung auf Stripe-Lese-/Schreibvorgänge. Die gängigsten Konfigurationen sind bidirektional oder vier-Wege-Interleaving. Eine verschachtelte Gruppe bewirkt außerdem, dass mehrere persistente Speichergeräte als einzelner logischer Datenträger zu Windows Server angezeigt werden. Sie können das Windows PowerShell-Cmdlet " **Get-pmemdisk** " verwenden, um die Konfiguration dieser logischen Datenträger wie folgt zu überprüfen:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Wir sehen, dass die logische pMem-Datenträger #2 die physischen Geräte Id20 und Id120 und die logische pMem-Datenträger #3 die die physischen Geräte Id1020 und Id1120 verwendet.

Zum Abrufen weiterer Informationen über die überlappende Menge, die von einem logischen Laufwerk verwendet wird, führen **Sie das Get-pmemphysicaldevice** -Cmdlet aus:

```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleaved-sets"></a>Konfigurieren von verschachtelten Gruppen

Zum Konfigurieren einer verschachtelten Gruppe müssen Sie zunächst alle permanenten Speicherbereiche überprüfen, die keinem logischen pMem-Datenträger im System zugewiesen sind. Führen Sie hierzu das folgende PowerShell-Cmdlet aus:

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

Führen Sie das folgende Cmdlet auf dem lokalen Server aus, um alle pMem-Geräteinformationen im System, einschließlich Gerätetyp, Speicherort, Integritäts-und Betriebsstatus usw., anzuzeigen:

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

Da wir über eine nicht genutzte pMem-Region verfügen, können wir neue persistente Speicher Datenträger erstellen. Wir können die nicht verwendete Region verwenden, um mehrere permanente Speicher Datenträger zu erstellen, indem Sie die folgenden Cmdlets ausführen:

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

Anschließend können Sie die Ergebnisse sehen, indem Sie Folgendes ausführen:

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Beachten Sie, dass wir " **Get-PhysicalDisk" ausführen können. Dabei ist "MediaType-EQ SCM** " anstelle von " **Get-pmemdisk** ", um dieselben Ergebnisse zu erhalten. Der neu erstellte pMem-Datenträger entspricht eins-zu-eins-mit Laufwerken, die in PowerShell und im Windows Admin Center angezeigt werden.

### <a name="using-persistent-memory-for-cache-or-capacity"></a>Verwenden von persistenten Speicher für Cache oder Kapazität

Direkte Speicherplätze unter Windows Server 2019 unterstützt die Verwendung von persistentem Speicher als Cache-oder Kapazitäts Laufwerk. Weitere Informationen zum Einrichten von Cache-und Kapazitäts Laufwerken finden Sie Untergrund Legendes [zum Cache in direkte Speicherplätze](understand-the-cache.md).

## <a name="creating-a-dax-volume"></a>Erstellen eines DAX-Volumes

### <a name="understanding-dax"></a>Grundlegendes zu DAX

Es gibt zwei Methoden, um auf permanenten Speicher zuzugreifen. Sie lauten wie folgt:

1. **Direkter Zugriff (DAX)**, der wie der Arbeitsspeicher funktioniert, um die geringste Latenz zu erzielen. Die app ändert den persistenten Speicher direkt, wobei der Stapel umgangen wird. Beachten Sie, dass Sie DAX nur in Kombination mit NTFS verwenden können.
1. **Blockieren**Sie den Zugriff, der wie der Speicher für die APP-Kompatibilität funktioniert. In dieser configuraion fließen die Daten durch den Stapel. Sie können diese Konfiguration in Kombination mit NTFS und Refs verwenden.

Die folgende Abbildung zeigt ein Beispiel für eine DAX-Konfiguration:

![DAX-Stapel](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>Konfigurieren von DAX

Wir müssen PowerShell-Cmdlets verwenden, um ein DAX-Volume auf einem persistenten Speicher Datenträger zu erstellen. Mithilfe des **-isdax-** Schalters können wir ein Volume so formatieren, dass es Dax-aktiviert ist.

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

- Der persistente Speicher erstellt keine Leistungsindikatoren für physische Datenträger, sodass Sie nicht in Diagrammen im Windows Admin Center angezeigt werden.
- Der persistente Speicher erstellt keine Storport 505-Daten, sodass Sie keine proaktive Ausreißererkennung erhalten.

Abgesehen davon ist die Überwachung genauso wie bei jeder anderen physischen Festplatte. Sie können die Integrität eines permanenten Speicher Datenträgers Abfragen, indem Sie die folgenden Cmdlets ausführen:

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

**Healthstatus** zeigt an, ob die pMem-Festplatte fehlerfrei ist.

Mit dem Wert **unsafeshutdowncount** wird die Anzahl der Herunterfahr Vorgänge nachverfolgt, die auf diesem logischen Datenträger zu einem Datenverlust führen können. Dies ist die Summe der unsicheren Beendigungs Anzahl aller zugrunde liegenden pMem-Geräte auf diesem Datenträger. Weitere Informationen zum Integritäts Status erhalten Sie mithilfe des Cmdlets **Get-pmemphysicaldevice** , um Informationen wie **OperationalStatus**zu suchen.

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

Dieses Cmdlet zeigt, welches persistente Speichergerät fehlerhaft ist. Das fehlerhafte Gerät **("** Geräte-ID 20") entspricht dem Fall im vorherigen Beispiel. Mithilfe der **PhysicalLocation** in BIOS kann ermittelt werden, welches persistente Speichergerät sich in einem fehlerhaften Zustand befindet.

## <a name="replacing-persistent-memory"></a>Ersetzen von persistenten Speicher

In diesem Artikel wird beschrieben, wie Sie den Integritäts Status ihres permanenten Speichers anzeigen. Wenn Sie ein fehlerhafter Modul ersetzen müssen, müssen Sie den pMem-Datenträger erneut bereitstellen (Weitere Informationen finden Sie in den zuvor beschriebenen Schritten).

Wenn Sie Probleme beheben, müssen Sie möglicherweise **Remove-pmemdisk**verwenden. Dieses Cmdlet entfernt einen bestimmten permanenten Speicher Datenträger. Wir können alle aktuellen pMem-Datenträger entfernen, indem wir die folgenden Cmdlets ausführen:

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

> [!IMPORTANT]
> Das Entfernen eines permanenten Speicher Datenträgers führt zu Datenverlusten auf diesem Datenträger.

Ein weiteres Cmdlet, das Sie möglicherweise benötigen, ist **Initialize-pmemphysicaldevice**. Mit diesem Cmdlet werden die Speicherbereiche der Bezeichnung auf den physischen permanenten Speichergeräten initialisiert, und die Speicherinformationen für beschädigte Bezeichnungen können auf den pMem-Geräten gelöscht werden.

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

> [!IMPORTANT]
> **Initialize-pmemphysicaldevice** führt zu Datenverlusten im persistenten Speicher. Verwenden Sie es als letzten Ausweg, um persistente speicherbezogene Probleme zu beheben.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Integritätsverwaltung für Speicherklassenspeicher (NVDIMM-N) in Windows](storage-class-memory-health.md)
- [Grundlegendes zum Cache](understand-the-cache.md)
