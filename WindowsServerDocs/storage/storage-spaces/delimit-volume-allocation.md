---
title: Begrenzen der Zuordnung von Volumes in direkte Speicherplätze
ms.author: cosmosdarwin
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: 6dac775d3e92a0f7a076800d5c07af2776720c1d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960953"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>Begrenzen der Zuordnung von Volumes in direkte Speicherplätze
> Gilt für: Windows Server 2019

In Windows Server 2019 wird eine Option eingeführt, mit der die Zuordnung von Volumes in direkte Speicherplätze manuell getrennt wird. Dadurch kann die Fehlertoleranz unter bestimmten Bedingungen erheblich erhöht werden, es werden jedoch einige zusätzliche Überlegungen zur Verwaltung und Komplexität auferlegt. In diesem Thema wird erläutert, wie es funktioniert und wie es Beispiele in PowerShell gibt.

   > [!IMPORTANT]
   > Diese Funktion ist neu in Windows Server 2019. Es ist in Windows Server 2016 nicht verfügbar.

## <a name="prerequisites"></a>Voraussetzungen

### <a name="green-checkmark-icon-consider-using-this-option-if"></a>![Grünes Häkchen.](media/delimit-volume-allocation/supported.png) Verwenden Sie diese Option, wenn Folgendes gilt:

- Ihr Cluster verfügt über sechs oder mehr Server; immer
- Ihr Cluster verwendet nur die [drei-Wege-Spiegelungs](storage-spaces-fault-tolerance.md#mirroring) Resilienz.

### <a name="red-x-icon-do-not-use-this-option-if"></a>![Rotes X-Symbol.](media/delimit-volume-allocation/unsupported.png) Verwenden Sie diese Option nicht, wenn Folgendes geschieht:

- Ihr Cluster verfügt über weniger als sechs Server. noch
- Ihr [Cluster verwendet die](storage-spaces-fault-tolerance.md#parity) Resilienz der Parität oder der [Spiegelungs Beschleunigung](storage-spaces-fault-tolerance.md#mirror-accelerated-parity) .

## <a name="understand"></a>Informationen

### <a name="review-regular-allocation"></a>Review: reguläre Zuordnung

Bei der regulären drei-Wege-Spiegelung ist das Volume in viele kleine "Platten" unterteilt, die dreimal kopiert und gleichmäßig auf alle Laufwerke in jedem Server im Cluster verteilt werden. Weitere Informationen finden Sie in [diesem Deep Dive-Blog](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959).

![Diagramm, das anzeigt, dass das Volume in drei Stapel von Platten aufgeteilt und gleichmäßig auf jeden Server verteilt ist.](media/delimit-volume-allocation/regular-allocation.png)

Diese Standard Zuordnung maximiert parallele Lese-und Schreibvorgänge, was zu einer besseren Leistung führt, und ist in ihrer Einfachheit ansprechend: jeder Server ist gleich ausgelastet, jedes Laufwerk ist gleichmäßig ausgelastet, und alle Volumes bleiben online oder werden gleichzeitig offline geschaltet. Jedes Volume kann bis zu zwei gleichzeitige Ausfälle überstehen, wie [Diese Beispiele](storage-spaces-fault-tolerance.md#examples) veranschaulichen.

Mit dieser Zuordnung können Volumes jedoch drei gleichzeitige Fehler nicht überstehen. Wenn drei Server gleichzeitig ausfallen oder wenn Laufwerke auf drei Servern gleichzeitig ausfallen, ist der Zugriff auf Volumes nicht mehr möglich, weil mindestens einige Laufwerke (mit sehr hoher Wahrscheinlichkeit) den exakt drei Festplatten oder Servern zugeordnet sind, bei denen ein Fehler aufgetreten ist.

Im folgenden Beispiel schlagen Server 1, 3 und 5 gleichzeitig fehl. Obwohl viele-Platten über noch Kopien aufweisen, sind einige nicht wie folgt:

![Das Diagramm zeigt drei von sechs in rot markierten Servern, und das Gesamt Volume ist rot.](media/delimit-volume-allocation/regular-does-not-survive.png)

Das Volume wird offline geschaltet und kann erst wieder hergestellt werden, wenn die Server wieder hergestellt wurden.

### <a name="new-delimited-allocation"></a>Neu: durch Trennzeichen getrennte Zuordnung

Bei einer durch Trennzeichen getrennten Zuordnung geben Sie eine Teilmenge der zu verwendenden Server an (mindestens vier). Das Volume ist in Volumes unterteilt, die drei Mal kopiert werden, wie z. b. vor, aber anstelle der Zuordnung über jeden Server **werden die Platten nur der von Ihnen angegebenen Teilmenge der Server zugeordnet**.

Wenn Sie z. b. über einen Cluster mit 8 Knoten verfügen (Knoten 1 bis 8), können Sie ein Volume angeben, das sich nur auf Datenträgern in den Knoten 1, 2, 3, 4 befinden soll.
#### <a name="advantages"></a>Vorteile

Mit der Beispiel Zuordnung wird das Volume wahrscheinlich drei gleichzeitige Fehler überstehen. Wenn die Knoten 1, 2 und 6 ausfallen, sind nur zwei der Knoten, die die drei Kopien der Daten für das Volume enthalten, ausfallen, und das Volume bleibt online.

Die Lebensdauer Wahrscheinlichkeit hängt von der Anzahl der Server und anderen Faktoren ab – weitere Informationen finden Sie in der [Analyse](#analysis) .

#### <a name="disadvantages"></a>Nachteile

Durch Trennzeichen getrennte Zuordnung werden zusätzliche Verwaltungs Aspekte und die Komplexität berücksichtigt:

1. Der-Administrator ist dafür verantwortlich, die Zuordnung der einzelnen Volumes zu begrenzen, um die Speicherauslastung über mehrere Server hinweg auszugleichen und eine hohe Wahrscheinlichkeit für das Überleben aufrechtzuerhalten, wie im Abschnitt mit den [bewährten Methoden](#best-practices) beschrieben.

2. Reservieren Sie mit einer durch Trennzeichen getrennten Zuordnung das Äquivalent eines **Kapazitäts Laufwerks pro Server (ohne Maximum)**. Dies ist mehr als die [veröffentlichte Empfehlung](plan-volumes.md#choosing-the-size-of-volumes) für die reguläre Zuordnung, die bei vier Kapazitäts Laufwerken insgesamt liegt.

3. Wenn ein Server ausfällt und ersetzt werden muss, wie unter [Entfernen eines Servers und seiner Laufwerke](remove-servers.md#remove-a-server-and-its-drives)beschrieben, ist der Administrator für das Aktualisieren der Abgrenzung betroffener Volumes verantwortlich, indem der neue Server hinzugefügt und das fehlerhafte –-Beispiel unten entfernt wird.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Sie können das `New-Volume` Cmdlet zum Erstellen von Volumes in direkte Speicherplätze verwenden.

So erstellen Sie z. b. ein reguläres Volume mit drei-Wege-Spiegelung:

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>Erstellen eines Volumes und begrenzen der Zuordnung

So erstellen Sie ein Volume mit drei-Wege-Spiegelung und begrenzen die Zuordnung:

1. Weisen Sie zuerst die Server in Ihrem Cluster der Variablen zu `$Servers` :

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > In direkte Speicherplätze bezieht sich der Begriff "Speicher Skalierungs Einheit" auf den gesamten rohspeicher, der mit einem Server verbunden ist, einschließlich direkt angefügter Laufwerke und direkt angeschlossenen externen Gehäusen mit Laufwerken. In diesem Kontext ist es identisch mit "Server".

2. Geben Sie an, welche Server mit dem neuen `-StorageFaultDomainsToUse` Parameter und durch Indizierung in verwendet werden sollen `$Servers` . Um z. b. die Zuordnung zum ersten, zweiten, dritten und vierten Server (Indizes 0, 1, 2 und 3) zu begrenzen:

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2,3]
    ```

### <a name="see-a-delimited-allocation"></a>Anzeigen einer durch Trennzeichen getrennten Zuordnung

Um zu sehen, wie *myvolume* zugeordnet ist, verwenden Sie das `Get-VirtualDiskFootprintBySSU.ps1` Skript in [Anhang](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  100 GB  0       0
```

Beachten Sie, dass nur Server1, Server2, Server3 und Server4 Platten von *myvolume*enthalten.

### <a name="change-a-delimited-allocation"></a>Ändern einer durch Trennzeichen getrennten Zuordnung

Verwenden Sie die neuen `Add-StorageFaultDomain` -und- `Remove-StorageFaultDomain` Cmdlets, um zu ändern, wie die Zuordnung getrennt ist.

Um beispielsweise *myvolume* auf einen Server zu verschieben, gehen Sie wie folgt vor:

1. Geben Sie an, dass der fünfte Server die Festplatten von *myvolume*speichern **kann** :

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[4]
    ```

2. Geben Sie an, dass der erste Server keine Platten von *myvolume*speichern **kann** :

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. Ausgleichen Sie den Speicherpool neu, damit die Änderungen wirksam werden:

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

Sie können den Fortschritt des Ausgleichs mit überwachen `Get-StorageJob` .

Vergewissern Sie sich nach Abschluss des Vorgangs, dass *myvolume* verschoben wurde, indem Sie es `Get-VirtualDiskFootprintBySSU.ps1` erneut ausführen.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  100 GB  0
```

Beachten Sie, dass server1 keine Platten von *myvolume* mehr enthält – sondern auch Server5.

## <a name="best-practices"></a>Bewährte Methoden

Im folgenden finden Sie die empfohlenen Vorgehensweisen bei der Verwendung von durch Trennzeichen getrennten Volumes:

### <a name="choose-four-servers"></a>Vier Server auswählen

Begrenzen Sie jedes drei-Wege-Spiegelungs Volume auf vier Server, nicht mehr.

### <a name="balance-storage"></a>Ausgleichen des Speichers

Gleichgewicht der Menge an Speicher, die jedem Server zugewiesen ist, und berücksichtigt der Volumegröße.

### <a name="stagger-delimited-allocation-volumes"></a>Durch Trennzeichen getrennte Zuordnungs Volumes Staffeln

Um die Fehlertoleranz zu maximieren, machen Sie die Zuordnung der einzelnen Volumes eindeutig, d. h., Sie verwendet nicht *alle* Server mit einem anderen Volume (einige Überlappungen sind okay).

Beispielsweise auf einem System mit acht Knoten: Volume 1: Server 1, 2, 3, 4 Volume 2: Server 5, 6, 7, 8 Volume 3: Server 3, 4, 5, 6 Volume 4: Server 1, 2, 7, 8

## <a name="analysis"></a>Analyse

In diesem Abschnitt wird die mathematische Wahrscheinlichkeit abgeleitet, mit der ein Volume online und zugänglich (oder gleichermaßen der erwartete Anteil des gesamten Speichers, der Online und zugänglich bleibt) als Funktion der Anzahl von Fehlern und der Clustergröße angezeigt wird.

   > [!NOTE]
   > Dieser Abschnitt ist ein optionales Lesevorgang. Wenn Sie die mathematische Informationen sehen möchten, lesen Sie die Informationen unter! Aber falls nicht, machen Sie sich keine Sorgen: die [Verwendung in PowerShell](#usage-in-powershell) und die [bewährten Methoden](#best-practices) sind alles, was Sie benötigen, um die getrennte Zuordnung erfolgreich zu implementieren.

### <a name="up-to-two-failures-is-always-okay"></a>Bis zu zwei Fehler sind immer okay.

Jedes drei-Wege-Spiegelungs Volume kann bis zu zwei Fehler gleichzeitig überstehen, unabhängig von dessen Zuordnung. Wenn zwei Laufwerke ausfallen oder bei zwei Servern ein Fehler auftritt bzw. eines von beiden, dann bleibt jedes drei-Wege-Spiegelungs Volume online und zugänglich, auch bei normaler Zuordnung.

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>Mehr als die Hälfte des Cluster Fehlers ist nie okay

Im umgekehrten Fall, dass mehr als die Hälfte der Server oder Laufwerke im Cluster gleichzeitig ausfallen, geht das [Quorum verloren](understand-quorum.md) , und jedes drei-Wege-Spiegelungs Volume wechselt in den Offline Modus und ist unabhängig von dessen Zuordnung nicht mehr verfügbar.

### <a name="what-about-in-between"></a>Wie sieht es zwischen aus?

Wenn drei oder mehr Fehler gleichzeitig auftreten, aber mindestens die Hälfte der Server und die Laufwerke weiterhin aktiv sind, bleiben Volumes mit durch Trennzeichen getrennten Zuordnungen möglicherweise Online und zugänglich, je nachdem, welche Server Fehler aufweisen.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="can-i-delimit-some-volumes-but-not-others"></a>Kann ich einige Volumes begrenzen, aber keine anderen?

Ja. Sie können pro Volume auswählen, ob die Zuordnung begrenzt werden soll.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>Ändert die durch Trennzeichen getrennte Zuordnung die Funktionsweise der Laufwerk Ersetzung?

Nein, es ist das gleiche wie bei der regulären Zuordnung.

## <a name="additional-references"></a>Weitere Verweise

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Fehlertoleranz in direkte Speicherplätze](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>Anhang

Mit diesem Skript können Sie sehen, wie Ihre Volumes zugeordnet werden.

Um es wie oben beschrieben zu verwenden, kopieren/einfügen und speichern unter `Get-VirtualDiskFootprintBySSU.ps1` .

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
