---
title: Trennen Sie die Zuordnung von Volumes im "direkte Speicherplätze"
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: c93cbf4ba418f6702cf8747508605952d993508d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889051"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>Trennen Sie die Zuordnung von Volumes im "direkte Speicherplätze"
> Gilt für: Windows Server Insider Preview Build 17093 und höher

Windows Server Insider Preview führt eine Option aus, um die Zuordnung von Volumes in direkte Speicherplätze manuell zu trennen. Dies erzwingt damit deutlich Fehlertoleranz unter bestimmten Bedingungen erhöhen kann jedoch einige zusätzliche Überlegungen zur und Komplexität. In diesem Thema wird erläutert, wie es funktioniert, und die Beispiele in PowerShell.

   > [!IMPORTANT]
   > Dieses Feature ist neu in Windows Server Insider Preview Build 17093 und höher. Es ist nicht in Windows Server 2016 verfügbar. Laden wir IT-Experten zum Verknüpfen der [Windows Server Insider-Programm](https://aka.ms/serverinsider) an uns Feedback dazu, was wir tun können, um Windows-Server, die besser für Ihre Organisation geeignet zu machen.

## <a name="prerequisites"></a>Vorraussetzungen

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![Grünes Häkchen-Symbol.](media/delimit-volume-allocation/supported.png) Erwägen Sie diese Option, wenn:

- Der Cluster enthält sechs oder mehr Server; und
- Ihr Cluster verwendet nur [drei-Wege-Spiegelung](storage-spaces-fault-tolerance.md#mirroring) resilienz

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![Rotes X-Symbol.](media/delimit-volume-allocation/unsupported.png) Verwenden Sie diese Option nicht verfügbar, wenn:

- Der Cluster enthält weniger als sechs Server; oder
- Ihr Cluster verwendet [Parität](storage-spaces-fault-tolerance.md#parity) oder [Mirror-beschleunigte Parität](storage-spaces-fault-tolerance.md#mirror-accelerated-parity) resilienz

## <a name="understand"></a>Grundlegende Informationen

### <a name="review-regular-allocation"></a>Überprüfen: reguläre Zuordnung

Mit regulären drei-Wege-Spiegelung, ist das Volume in viele kleine "bereichszuweisungen", die drei Mal kopiert und gleichmäßig auf alle Laufwerke auf jedem Server im Cluster unterteilt. Weitere Informationen finden Sie in [diesen Blog tieferer Einblick in](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/).

![Das Diagramm zeigt das Volume wird in drei Aufruflisten von bereichszuweisungen unterteilt und gleichmäßig auf jedem Server.](media/delimit-volume-allocation/regular-allocation.png)

Diese standardzuweisung maximiert die parallele liest und schreibt, was eine bessere Leistung und wird in seiner Einfachheit attraktiv: alle Server gleichmäßig ausgelastet ist, alle Laufwerke gleichermaßen voll ist und alle Volumes online bleiben oder zusammen offline geschaltet. Jedes Volume ist garantiert, bis zu zwei gleichzeitige Ausfälle, als überbrücken [in diesen Beispielen](storage-spaces-fault-tolerance.md#examples) veranschaulichen.

Allerdings können nicht mit dieser Zuordnung, Volumes drei gleichzeitiger Ausfälle überstehen. Wenn drei Server gleichzeitig ein Fehler auftritt oder wenn Laufwerke auf drei Servern auf einmal ausfallen, werden die Volumes nicht zugegriffen werden kann, da zumindest eine gewisse bereichszuweisungen (mit sehr hoher Wahrscheinlichkeit) für die genaue drei Laufwerke oder der Server, die nicht zugeordnet wurden.

Im folgenden Beispiel fehl, Server, 1, 3 und 5 zur gleichen Zeit. Obwohl viele bereichszuweisungen überstehen von Kopien verfügen, andere nicht:

![Das Diagramm zeigt drei der sechs Server in Rot und die Gesamtanzahl verarbeiteter hervorgehoben ist rot.](media/delimit-volume-allocation/regular-does-not-survive.png)

Das Volume wird offline geschaltet und wird nicht zugegriffen werden kann, bis der Server wiederhergestellt werden.

### <a name="new-delimited-allocation"></a>Neu: getrennte Zuordnung

Mit durch Trennzeichen getrennten Verteilung Geben Sie eine Teilmenge von Servern (mindestens drei Replikate für die drei-Wege-Spiegelung) verwendet. Das Volume wird in unterteilt bereichszuweisungen, die kopiert werden dreimal aus, wie zuvor, aber anstatt für jeden Server, zuzuweisen **die bereichszuweisungen zugewiesen werden nur die Teilmenge von Servern, die Sie angeben,**.

![Das Diagramm zeigt das Volume wird in drei Aufruflisten von bereichszuweisungen unterteilt und nur für drei der sechs Server verteilt.](media/delimit-volume-allocation/delimited-allocation.png)

#### <a name="advantages"></a>Vorteile

Mit dieser Zuordnung, das Volume ist wahrscheinlich auf drei gleichzeitige Ausfälle überbrücken: in der Tat die Wahrscheinlichkeit, Überleben erhöht, von 0 % (mit regulären Zuordnung) auf 95 % (mit durch Trennzeichen getrennten-Zuteilung) in diesem Fall! Intuitiv ist, da sie nicht davon abhängt Server, 4, 5 oder 6, damit sie die Fehler nicht betroffen ist.

Im Beispiel oben fehl, Server, 1, 3 und 5 zur gleichen Zeit. Da durch Trennzeichen getrennten Zuordnung, dass es sich bei diesem Server 2 eine Kopie jeder Slab enthält sichergestellt, jede Slab survivor Kopie und das Volume bleibt online und zugänglich ist:

![Das Diagramm zeigt drei der sechs Server rot markiert, aber das Gesamtvolumen grün ist.](media/delimit-volume-allocation/delimited-does-survive.png)

Orientierungshandbuch Wahrscheinlichkeit hängt von der Anzahl von Servern und anderen Faktoren – Siehe [Analysis](#analysis) Details.

#### <a name="disadvantages"></a>Nachteile

Durch Trennzeichen getrennten Zuweisung erzwingt einige zusätzliche Überlegungen zur und Komplexität:

1. Der Administrator ist verantwortlich für die Zuordnung von jedem Volume zum Ausgleichen der Auslastung des Gesamtspeicherplatzes auf Servern und einzuhalten hohen Wahrscheinlichkeit überleben, begrenzen, wie beschrieben in der [bewährte Methoden](#best-practices) Abschnitt.

2. Reservieren Sie mit durch Trennzeichen getrennten Zuordnung sowie die Entsprechung der **Laufwerk mit einer Kapazität pro Server (mit kein Maximum)**. Dies ist mehr als die [Empfehlung veröffentlicht](plan-volumes.md#choosing-the-size-of-volumes) für die regulären Zuordnung, welche ergibt Kapazität vier Laufwerke insgesamt.

3. Wenn ein Server ausfällt und ersetzt werden wie in beschrieben, muss [Entfernen eines Servers sowie deren Laufwerke](remove-servers.md#remove-a-server-and-its-drives), der Administrator ist verantwortlich für die Abgrenzung der betroffenen Volumes den neuen Server hinzufügen und Entfernen der fehlerhaften ein – Beispiel für aktualisieren unten.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Sie können die `New-Volume` Cmdlet zum Erstellen von Volumes im "direkte Speicherplätze".

Um beispielsweise ein Volume regulären drei-Wege-Spiegelung zu erstellen:

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>Erstellen Sie ein Volume aus, und Trennen von die Zuordnung

So erstellen Sie ein Volume für die drei-Wege-Spiegelung und seine Zuordnung zu begrenzen:

1. Weisen Sie die Server in Ihrem Cluster zuerst auf die Variable `$Servers`:

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > In "direkte Speicherplätze" bezieht sich auf alle im unformatierten Speicher, die auf einem Server, einschließlich direkt angeschlossener Laufwerke und direkt angeschlossene externe Gehäuse mit Laufwerken angefügt "der Begriff 'Speicherskalierungseinheit'". In diesem Kontext ist es identisch mit "Server".

2. Geben Sie die Server für die Verwendung mit dem neuen `-StorageFaultDomainsToUse` Parameter und die Indizierung `$Servers`. Für z. B. trennen die Zuordnung zu den ersten, zweiten und dritten Server (Indizes 0, 1 und 2):

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2]
    ```

### <a name="see-a-delimited-allocation"></a>Finden Sie eine durch Trennzeichen getrennten Zuordnung

Um finden Sie unter wie *MyVolume* ist zugeordnet ist, verwenden Sie die `Get-VirtualDiskFootprintBySSU.ps1` Skript im [Anhang](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  0       0       0      
```

Beachten Sie, dass nur Server1, Server2 und Server3 enthält bereichszuweisungen von *MyVolume*.

### <a name="change-a-delimited-allocation"></a>Eine durch Trennzeichen getrennten Zuordnung ändern

Verwenden Sie die neue `Add-StorageFaultDomain` und `Remove-StorageFaultDomain` Cmdlets so ändern, wie die Zuordnung getrennt wird.

Um beispielsweise verschieben *MyVolume* von einem Server:

1. Angeben, die den vierten Server **können** speichern bereichszuweisungen von *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[3]
    ```

2. Angeben, die den ersten Server **kann nicht** speichern bereichszuweisungen von *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. Ausgleichen Sie im Speicherpool für die Änderung wirksam wird:

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

![Das Diagramm zeigt, dass die bereichszuweisungen En-Masse von Servern, 1, 2 und 3 an Server 2, 3 und 4 migrieren.](media/delimit-volume-allocation/move.gif)

Sie können den Fortschritt der der Ausgleich mit `Get-StorageJob`.

Sobald sie abgeschlossen ist, überprüfen Sie Sie, ob *MyVolume* wurde mit `Get-VirtualDiskFootprintBySSU.ps1` erneut aus.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  0       0      
```

Beachten Sie, die keine Server1 enthält Platinen sowie Bänder von *MyVolume* mehr – stattdessen Server04 wird.

## <a name="best-practices"></a>Empfohlene Methoden

Hier sind die bewährten Methoden zu befolgen, wenn Sie mithilfe von Volume-Zuordnung als Trennzeichen:

### <a name="choose-three-servers"></a>Wählen Sie die drei Server

Trennen Sie die einzelnen Volumes drei-Wege-Spiegelung auf drei Servern nicht mehr.

### <a name="balance-storage"></a>Guthaben-Speicher

Wägen Sie, wie viel Speicher zugeordnet wird, auf jedem Server, der Volumegröße berücksichtigt.

### <a name="every-delimited-allocation-unique"></a>Jeder eindeutige, durch Trennzeichen getrennten speicherbelegung

Um Fehlertoleranz zu maximieren, stellen jedes Volume die Zuordnung eindeutig ist, d. h., es gibt keine frei *alle* seine Server mit einem anderen Volume (überschneidungen ist in Ordnung). Mit N-Servern, es gibt eindeutige Kombinationen "N wählen Sie 3" – Hier ist also für einige gängige Clustergrößen:

| Anzahl von Servern (N) | Anzahl der eindeutigen Trennzeichen Zuordnungen (N wählen Sie Option 3) |
|-----------------------|-----------------------------------------------------|
| 6                     | 20                                                  |
| 8                     | 56                                                  |
| 12                    | 220                                                 |
| 16                    | 560                                                 |

   > [!TIP]
   > Betrachten Sie diese hilfreiche Überprüfung der [Combinatorics, und wählen Sie die Notation](https://betterexplained.com/articles/easy-permutations-and-combinations/).

Es folgt ein Beispiel, die Fehlertoleranz zu maximieren: jedes Volume verfügt über eine eindeutige, durch Trennzeichen getrennten Zuweisung:

![unique-allocation](media/delimit-volume-allocation/unique-allocation.png)

Im Gegensatz dazu im nächsten Beispiel, die ersten drei Volumes verwenden die gleiche durch Trennzeichen getrennten speicherzuweisung (für Server, 1, 2 und 3), und die letzten drei Volumes verwenden die gleiche durch Trennzeichen getrennten speicherzuweisung (für Server, 4, 5 und 6). Dies keine Fehlertoleranz zu maximieren: Wenn drei Server Fehler auftreten, mehrere Volumes offline geschaltet und mehr auf einmal zugegriffen werden können.

![non-unique-allocation](media/delimit-volume-allocation/non-unique-allocation.png)

## <a name="analysis"></a>Analyse

In diesem Abschnitt abgeleitet wird, die mathematische Wahrscheinlichkeit, dass ein Volume online und zugänglich bleiben (oder gleichwertig, den erwarteten Anteil der Gesamtstrategie für speichernutzung, die online und zugänglich bleibt) als Funktion der Anzahl von Fehlern und die Größe des Clusters.

   > [!NOTE]
   > Dieser Abschnitt ist optional lesen. Wenn Sie bestrebt, die Berechnungen finden Sie unter sind, lesen Sie weiter! Aber falls nicht, keine Sorge: [Verwendung in PowerShell](#usage-in-powershell) und [bewährte Methoden](#best-practices) Sie müssen lediglich zur erfolgreichen Implementierung von durch Trennzeichen getrennten Zuordnung.

### <a name="up-to-two-failures-is-always-okay"></a>Bis zu zwei Ausfällen ist immer zulässig

Jedes Volume drei-Wege-Spiegelung kann überstehen bis zu zwei zur gleichen Zeit, als [in diesen Beispielen](storage-spaces-fault-tolerance.md#examples) zu veranschaulichen, unabhängig von die Zuordnung. Wenn zwei Laufwerke ein Fehler auftritt, oder zwei Server oder eines einzelnen, alle drei-Wege-Spiegelung Volume online und zugänglich ist, auch bei regulären Zuordnung bleibt.

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>Mehr als die Hälfte der Ausfall eines ist nicht in Ordnung

Im Gegensatz dazu im äußersten Fall, bei denen mehr als die Hälfte der Server oder Laufwerke im Cluster gleichzeitig [Quorum verloren gegangen ist](understand-quorum.md) und alle drei-Wege-Spiegelung-Volume wird offline geschaltet und nicht mehr zugegriffen werden, unabhängig von die Zuordnung.

### <a name="what-about-in-between"></a>Was dazwischen?

Wenn drei oder mehr Fehler, gleichzeitig auftreten aber mindestens die Hälfte der Server und die Laufwerke noch aktiv sind, können Volumes mit durch Trennzeichen getrennten Zuordnung bleiben, online und zugänglich ist, je nachdem, welche Server Fehler auftreten. Führen Sie zunächst die Zahlen, um die genauen Chancen zu ermitteln.

Angenommen Sie, der Einfachheit halber Volumes sind unabhängig voneinander und genauso wie verteilte (IID) gemäß der oben genannten bewährten Methoden und, dass eindeutige Kombinationen sind verfügbar für jedes Volume die Zuordnung eindeutig sein. Die Wahrscheinlichkeit, die jedes Volume überdauert ist auch den erwarteten Anteil der gesamten Speicher, der von Linearität der Erwartung zurückgegriffen werden kann. 

Erhält **N** Server, von denen **F** liegen vor, ein Volume zugeordneten **3** davon geht offline If-und-only-If alle **3** gehören zu den  **F** mit Fehlern. Es gibt **(N auswählen F)** Möglichkeiten für **F** Fehler auftreten, von denen **(F wählen Sie Option 3)** führen das Volume offline geschaltet und als nicht zugegriffen werden kann. Die Wahrscheinlichkeit ausgedrückt werden kann:

![P_offline = Fc3 / NcF](media/delimit-volume-allocation/probability-volume-offline.png)

In allen anderen Fällen bleibt das Volume, online und zugänglich ist:

![P_online = 1 – (Fc3 / NcF)](media/delimit-volume-allocation/probability-volume-online.png)

In den folgenden Tabellen ausgewertet, die Wahrscheinlichkeit für einige gängige Clustergrößen und bis zu 5 Fehler anzeigt, dass durch Trennzeichen getrennten Zuordnung erhöht die Fehlertoleranz im Vergleich zu regulären Zuordnung in jedem Fall berücksichtigt wird.

### <a name="with-6-servers"></a>Mit 6-Servern

| Zuordnung                           | Wahrscheinlichkeit von 1 Fehler überstehen | Wahrscheinlichkeit von überstehen von Ausfällen von 2 | Wahrscheinlichkeit von überstehen von Ausfällen von 3 | Wahrscheinlichkeit von überstehen von Ausfällen von 4 | Wahrscheinlichkeit von überstehen von Ausfällen von 5 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regelmäßige, auf alle 6 Server verteilt. | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| Um nur 3 Server getrennt          | 100%                               | 100%                                | 95.0%                               | 0%                                  | 0%                                  |

   > [!NOTE]
   > Nach dem Fehler 6 Gesamtanzahl Server mehr als 3 verliert der Cluster das Quorum.

### <a name="with-8-servers"></a>Mit 8-Server

| Zuordnung                           | Wahrscheinlichkeit von 1 Fehler überstehen | Wahrscheinlichkeit von überstehen von Ausfällen von 2 | Wahrscheinlichkeit von überstehen von Ausfällen von 3 | Wahrscheinlichkeit von überstehen von Ausfällen von 4 | Wahrscheinlichkeit von überstehen von Ausfällen von 5 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regelmäßige, auf alle 8 Server verteilt. | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| Um nur 3 Server getrennt          | 100%                               | 100%                                | 98.2%                               | 94.3%                               | 0%                                  |

   > [!NOTE]
   > Nach mehr als 4 Ausfälle bei insgesamt 8-Server verliert der Cluster das Quorum.

### <a name="with-12-servers"></a>Mit 12 Servern

| Zuordnung                            | Wahrscheinlichkeit von 1 Fehler überstehen | Wahrscheinlichkeit von überstehen von Ausfällen von 2 | Wahrscheinlichkeit von überstehen von Ausfällen von 3 | Wahrscheinlichkeit von überstehen von Ausfällen von 4 | Wahrscheinlichkeit von überstehen von Ausfällen von 5 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regelmäßige, auf alle 12 Server verteilt. | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| Um nur 3 Server getrennt           | 100%                               | 100%                                | 99.5%                               | 99.2%                               | 98.7%                               |

### <a name="with-16-servers"></a>Mit 16 Server

| Zuordnung                            | Wahrscheinlichkeit von 1 Fehler überstehen | Wahrscheinlichkeit von überstehen von Ausfällen von 2 | Wahrscheinlichkeit von überstehen von Ausfällen von 3 | Wahrscheinlichkeit von überstehen von Ausfällen von 4 | Wahrscheinlichkeit von überstehen von Ausfällen von 5 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regelmäßige, über alle 16 Server verteilt. | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| Um nur 3 Server getrennt           | 100%                               | 100%                                | 99.8%                               | 99.8%                               | 99.8%                               |

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="can-i-delimit-some-volumes-but-not-others"></a>Kann ich einige Volumes, aber in anderen trennen?

Ja. Sie können pro Volume angibt, ob auswählen oder nicht zum Begrenzen der Zuordnung.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>Ändert durch Trennzeichen getrennten Zuordnung die Funktionsweise von Laufwerk ersetzt?

Nein, es ist dieselbe wie bei regulären Zuordnung.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Fehlertoleranz in "direkte Speicherplätze"](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>Anhang

Dieses Skript können Sie sehen, wie Ihre Volumes zugeordnet sind.

Um es zu verwenden wie oben beschrieben, kopieren und einfügen und speichern Sie als `Get-VirtualDiskFootprintBySSU.ps1`.

```PowerShell
Function ConvertTo-PrettyCapacity {
    Param (
        [Parameter(
            Mandatory = $True,
            ValueFromPipeline = $True
            )
        ]
    [Int64]$Bytes,
    [Int64]$RoundTo = 0
    )
    If ($Bytes -Gt 0) {
        $Base = 1024
        $Labels = ("bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        $Order = [Math]::Floor( [Math]::Log($Bytes, $Base) )
        $Rounded = [Math]::Round($Bytes/( [Math]::Pow($Base, $Order) ), $RoundTo)
        [String]($Rounded) + " " + $Labels[$Order]
    }
    Else {
        "0"
    }
    Return
}

Function Get-VirtualDiskFootprintByStorageFaultDomain {

    ################################################
    ### Step 1: Gather Configuration Information ###
    ################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Gathering configuration information..." -Status "Step 1/4" -PercentComplete 00

    $ErrorCannotGetCluster = "Cannot proceed because 'Get-Cluster' failed."
    $ErrorNotS2DEnabled = "Cannot proceed because the cluster is not running Storage Spaces Direct."
    $ErrorCannotGetClusterNode = "Cannot proceed because 'Get-ClusterNode' failed."
    $ErrorClusterNodeDown = "Cannot proceed because one or more cluster nodes is not Up."
    $ErrorCannotGetStoragePool = "Cannot proceed because 'Get-StoragePool' failed."
    $ErrorPhysicalDiskFaultDomainAwareness = "Cannot proceed because the storage pool is set to 'PhysicalDisk' fault domain awareness. This cmdlet only supports 'StorageScaleUnit', 'StorageChassis', or 'StorageRack' fault domain awareness."

    Try  {
        $GetCluster = Get-Cluster -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetCluster
    }

    If ($GetCluster.S2DEnabled -Ne 1) {
        throw $ErrorNotS2DEnabled
    }

    Try  {
        $GetClusterNode = Get-ClusterNode -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetClusterNode
    }

    If ($GetClusterNode | Where State -Ne Up) {
        throw $ErrorClusterNodeDown
    }

    Try {
        $GetStoragePool = Get-StoragePool -IsPrimordial $False -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetStoragePool
    }

    If ($GetStoragePool.FaultDomainAwarenessDefault -Eq "PhysicalDisk") {
        throw $ErrorPhysicalDiskFaultDomainAwareness
    }

    ###########################################################
    ### Step 2: Create SfdList[] and PhysicalDiskToSfdMap{} ###
    ###########################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing physical disk information..." -Status "Step 2/4" -PercentComplete 25

    $SfdList = Get-StorageFaultDomain -Type ($GetStoragePool.FaultDomainAwarenessDefault) | Sort FriendlyName # StorageScaleUnit, StorageChassis, or StorageRack

    $PhysicalDiskToSfdMap = @{} # Map of PhysicalDisk.UniqueId -> StorageFaultDomain.FriendlyName
    $SfdList | ForEach {
        $StorageFaultDomain = $_
        $_ | Get-StorageFaultDomain -Type PhysicalDisk | ForEach {
            $PhysicalDiskToSfdMap[$_.UniqueId] = $StorageFaultDomain.FriendlyName
        }
    }

    ##################################################################################################
    ### Step 3: Create VirtualDisk.FriendlyName -> { StorageFaultDomain.FriendlyName -> Size } Map ###
    ##################################################################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing virtual disk information..." -Status "Step 3/4" -PercentComplete 50

    $GetVirtualDisk = Get-VirtualDisk | Sort FriendlyName

    $VirtualDiskMap = @{}

    $GetVirtualDisk | ForEach {
        # Map of PhysicalDisk.UniqueId -> Size for THIS virtual disk
        $PhysicalDiskToSizeMap = @{}
        $_ | Get-PhysicalExtent | ForEach {
            $PhysicalDiskToSizeMap[$_.PhysicalDiskUniqueId] += $_.Size
        }
        # Map of StorageFaultDomain.FriendlyName -> Size for THIS virtual disk
        $SfdToSizeMap = @{}
        $PhysicalDiskToSizeMap.keys | ForEach {
            $SfdToSizeMap[$PhysicalDiskToSfdMap[$_]] += $PhysicalDiskToSizeMap[$_]
        }
        # Store
        $VirtualDiskMap[$_.FriendlyName] = $SfdToSizeMap
    }

    #########################
    ### Step 4: Write-Out ###
    #########################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Formatting output..." -Status "Step 4/4" -PercentComplete 75

    $Output = $GetVirtualDisk | ForEach {
        $Row = [PsCustomObject]@{}

        $VirtualDiskFriendlyName = $_.FriendlyName
        $Row | Add-Member -MemberType NoteProperty "VirtualDiskFriendlyName" $VirtualDiskFriendlyName

        $TotalFootprint = $_.FootprintOnPool | ConvertTo-PrettyCapacity
        $Row | Add-Member -MemberType NoteProperty "TotalFootprint" $TotalFootprint

        $SfdList | ForEach {
            $Size = $VirtualDiskMap[$VirtualDiskFriendlyName][$_.FriendlyName] | ConvertTo-PrettyCapacity
            $Row | Add-Member -MemberType NoteProperty $_.FriendlyName $Size
        }

        $Row
    }

    # Calculate width, in characters, required to Format-Table
    $RequiredWindowWidth = ("TotalFootprint").length + 1 + ("VirtualDiskFriendlyName").length + 1
    $SfdList | ForEach {
        $RequiredWindowWidth += $_.FriendlyName.Length + 1
    }

    $ActualWindowWidth = (Get-Host).UI.RawUI.WindowSize.Width

    If (!($ActualWindowWidth)) {
        # Cannot get window width, probably ISE, Format-List
        Write-Warning "Could not determine window width. For the best experience, use a Powershell window instead of ISE"
        $Output | Format-Table
    }
    ElseIf ($ActualWindowWidth -Lt $RequiredWindowWidth) {
        # Narrower window, Format-List
        Write-Warning "For the best experience, try making your PowerShell window at least $RequiredWindowWidth characters wide. Current width is $ActualWindowWidth characters."
        $Output | Format-List
    }
    Else {
        # Wider window, Format-Table
        $Output | Format-Table
    }
}

Get-VirtualDiskFootprintByStorageFaultDomain
```
