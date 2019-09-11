---
title: Begrenzen der Zuordnung von Volumes in direkte Speicherplätze
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: faf9547833764e9075e86515d1f486a5a3f61ff8
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872078"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>Begrenzen der Zuordnung von Volumes in direkte Speicherplätze
> Gilt für: Windows Server 2019

In Windows Server 2019 wird eine Option eingeführt, mit der die Zuordnung von Volumes in direkte Speicherplätze manuell getrennt wird. Dadurch kann die Fehlertoleranz unter bestimmten Bedingungen erheblich erhöht werden, es werden jedoch einige zusätzliche Überlegungen zur Verwaltung und Komplexität auferlegt. In diesem Thema wird erläutert, wie es funktioniert und wie es Beispiele in PowerShell gibt.

   > [!IMPORTANT]
   > Diese Funktion ist neu in Windows Server 2019. Es ist in Windows Server 2016 nicht verfügbar. 

## <a name="prerequisites"></a>Erforderliche Komponenten

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![Grünes Häkchen.](media/delimit-volume-allocation/supported.png) Verwenden Sie diese Option, wenn Folgendes gilt:

- Ihr Cluster verfügt über sechs oder mehr Server; immer
- Ihr Cluster verwendet nur die [drei-Wege-Spiegelungs](storage-spaces-fault-tolerance.md#mirroring) Resilienz.

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![Rotes X-Symbol.](media/delimit-volume-allocation/unsupported.png) Verwenden Sie diese Option nicht, wenn Folgendes geschieht:

- Ihr Cluster verfügt über weniger als sechs Server. noch
- Ihr [Cluster verwendet die](storage-spaces-fault-tolerance.md#parity) Resilienz der Parität oder der [Spiegelungs Beschleunigung](storage-spaces-fault-tolerance.md#mirror-accelerated-parity) .

## <a name="understand"></a>Grundlegende Informationen

### <a name="review-regular-allocation"></a>Review: reguläre Zuordnung

Bei der regulären drei-Wege-Spiegelung ist das Volume in viele kleine "Platten" unterteilt, die dreimal kopiert und gleichmäßig auf alle Laufwerke in jedem Server im Cluster verteilt werden. Weitere Informationen finden Sie in [diesem Deep Dive-Blog](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/).

![Diagramm, das anzeigt, dass das Volume in drei Stapel von Platten aufgeteilt und gleichmäßig auf jeden Server verteilt ist.](media/delimit-volume-allocation/regular-allocation.png)

Diese Standard Zuordnung maximiert parallele Lese-und Schreibvorgänge, was zu einer besseren Leistung führt, und ist in ihrer Einfachheit ansprechend: jeder Server ist gleich ausgelastet, jedes Laufwerk ist gleichmäßig ausgelastet, und alle Volumes bleiben online oder werden gleichzeitig offline geschaltet. Jedes Volume kann bis zu zwei gleichzeitige Ausfälle überstehen, wie [Diese Beispiele](storage-spaces-fault-tolerance.md#examples) veranschaulichen.

Mit dieser Zuordnung können Volumes jedoch drei gleichzeitige Fehler nicht überstehen. Wenn drei Server gleichzeitig ausfallen oder wenn Laufwerke auf drei Servern gleichzeitig ausfallen, ist der Zugriff auf Volumes nicht mehr möglich, weil mindestens einige Laufwerke (mit sehr hoher Wahrscheinlichkeit) den exakt drei Festplatten oder Servern zugeordnet sind, bei denen ein Fehler aufgetreten ist.

Im folgenden Beispiel schlagen Server 1, 3 und 5 gleichzeitig fehl. Obwohl viele-Platten über noch Kopien aufweisen, sind einige nicht wie folgt:

![Das Diagramm zeigt drei von sechs in rot markierten Servern, und das Gesamt Volume ist rot.](media/delimit-volume-allocation/regular-does-not-survive.png)

Das Volume wird offline geschaltet und kann erst wieder hergestellt werden, wenn die Server wieder hergestellt wurden.

### <a name="new-delimited-allocation"></a>Neu: durch Trennzeichen getrennte Zuordnung

Bei einer durch Trennzeichen getrennten Zuordnung geben Sie eine Teilmenge der zu verwendenden Server an (mindestens drei für die drei-Wege-Spiegelung). Das Volume ist in Volumes unterteilt, die drei Mal kopiert werden, wie z. b. vor, aber anstelle der Zuordnung über jeden Server **werden die Platten nur der von Ihnen angegebenen Teilmenge der Server zugeordnet**.

![Diagramm, das anzeigt, dass das Volume in drei Stapel von Platten aufgeteilt und nur auf drei von sechs Servern verteilt wird.](media/delimit-volume-allocation/delimited-allocation.png)

#### <a name="advantages"></a>Vorteile

Mit dieser Zuordnung wird das Volume wahrscheinlich drei gleichzeitige Fehler überstehen: in diesem Fall wird die Wahrscheinlichkeit für das Überleben von 0% (mit regulärer Zuordnung) auf 95% (mit einer durch Trennzeichen getrennten Zuordnung) erhöht! Dies liegt intuitiv daran, dass Sie nicht von den Servern 4, 5 oder 6 abhängig ist, sodass Sie nicht von ihren Fehlern betroffen sind.

Im obigen Beispiel schlagen Server 1, 3 und 5 gleichzeitig fehl. Da durch eine durch Trennzeichen getrennte Zuordnung sichergestellt wurde, dass Server 2 eine Kopie jeder Platte enthält, verfügt jede Platte über eine über Lebensende Kopie, und das Volume bleibt online und zugänglich:

![Das Diagramm zeigt drei von sechs in rot markierten Servern, aber das Gesamt Volume ist grün.](media/delimit-volume-allocation/delimited-does-survive.png)

Die Lebensdauer Wahrscheinlichkeit hängt von der Anzahl der Server und anderen Faktoren ab – weitere Informationen finden Sie in der [Analyse](#analysis) .

#### <a name="disadvantages"></a>Nachteile

Durch Trennzeichen getrennte Zuordnung werden zusätzliche Verwaltungs Aspekte und die Komplexität berücksichtigt:

1. Der-Administrator ist dafür verantwortlich, die Zuordnung der einzelnen Volumes zu begrenzen, um die Speicherauslastung über mehrere Server hinweg auszugleichen und eine hohe Wahrscheinlichkeit für das Überleben aufrechtzuerhalten, wie im Abschnitt mit den [bewährten Methoden](#best-practices) beschrieben.

2. Reservieren Sie mit einer durch Trennzeichen getrennten Zuordnung das Äquivalent eines **Kapazitäts Laufwerks pro Server (ohne Maximum)** . Dies ist mehr als die [veröffentlichte Empfehlung](plan-volumes.md#choosing-the-size-of-volumes) für die reguläre Zuordnung, die bei vier Kapazitäts Laufwerken insgesamt liegt.

3. Wenn ein Server ausfällt und ersetzt werden muss, wie unter [Entfernen eines Servers und seiner Laufwerke](remove-servers.md#remove-a-server-and-its-drives)beschrieben, ist der Administrator für das Aktualisieren der Abgrenzung betroffener Volumes verantwortlich, indem der neue Server hinzugefügt und das fehlerhafte –-Beispiel unten entfernt wird.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Sie können das `New-Volume` Cmdlet zum Erstellen von Volumes in direkte Speicherplätze verwenden.

So erstellen Sie z. b. ein reguläres Volume mit drei-Wege-Spiegelung:

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>Erstellen eines Volumes und begrenzen der Zuordnung

So erstellen Sie ein Volume mit drei-Wege-Spiegelung und begrenzen die Zuordnung:

1. Weisen Sie zuerst die Server in Ihrem Cluster der Variablen `$Servers`zu:

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > In direkte Speicherplätze bezieht sich der Begriff "Speicher Skalierungs Einheit" auf den gesamten rohspeicher, der mit einem Server verbunden ist, einschließlich direkt angefügter Laufwerke und direkt angeschlossenen externen Gehäusen mit Laufwerken. In diesem Kontext ist es identisch mit "Server".

2. Geben Sie an, welche Server mit dem `-StorageFaultDomainsToUse` neuen Parameter und durch Indizierung in `$Servers`verwendet werden sollen. Um z. b. die Zuordnung zum ersten, zweiten und dritten Server (Indizes 0, 1 und 2) zu begrenzen:

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2]
    ```

### <a name="see-a-delimited-allocation"></a>Anzeigen einer durch Trennzeichen getrennten Zuordnung

Um zu sehen, wie *myvolume* zugeordnet ist, `Get-VirtualDiskFootprintBySSU.ps1` verwenden Sie das Skript in [Anhang](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  0       0       0      
```

Beachten Sie, dass nur Server1, Server2 und Server3 Platten von *myvolume*enthalten.

### <a name="change-a-delimited-allocation"></a>Ändern einer durch Trennzeichen getrennten Zuordnung

Verwenden Sie die `Add-StorageFaultDomain` neuen `Remove-StorageFaultDomain` -und-Cmdlets, um zu ändern, wie die Zuordnung getrennt ist.

Um beispielsweise *myvolume* auf einen Server zu verschieben, gehen Sie wie folgt vor:

1. Geben Sie an, dass der vierte Server die Festplatten von *myvolume*speichern **kann** :

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[3]
    ```

2. Geben Sie an, dass der erste Server keine Platten von *myvolume*speichern **kann** :

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. Ausgleichen Sie den Speicherpool neu, damit die Änderungen wirksam werden:

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

![Diagramm, das zeigt, wie die Platten von den Servern 1, 2 und 3 zu den Servern 2, 3 und 4 migriert werden.](media/delimit-volume-allocation/move.gif)

Sie können den Fortschritt des Ausgleichs mit `Get-StorageJob`überwachen.

Vergewissern Sie sich nach Abschluss des Vorgangs, dass *myvolume* verschoben wurde `Get-VirtualDiskFootprintBySSU.ps1` , indem Sie es erneut ausführen.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  0       0      
```

Beachten Sie, dass server1 keine Platten von *myvolume* mehr enthält – sondern auch Server04.

## <a name="best-practices"></a>Empfohlene Methoden

Im folgenden finden Sie die empfohlenen Vorgehensweisen bei der Verwendung von durch Trennzeichen getrennten Volumes:

### <a name="choose-three-servers"></a>Auswählen von drei Servern

Begrenzen Sie jedes drei-Wege-Spiegelungs Volume auf drei Server, nicht mehr.

### <a name="balance-storage"></a>Ausgleichen des Speichers

Gleichgewicht der Menge an Speicher, die jedem Server zugewiesen ist, und berücksichtigt der Volumegröße.

### <a name="every-delimited-allocation-unique"></a>Alle durch Trennzeichen getrennten Zuordnungen eindeutig

Um die Fehlertoleranz zu maximieren, machen Sie die Zuordnung der einzelnen Volumes eindeutig, d. h., Sie verwendet nicht *alle* Server mit einem anderen Volume (einige Überlappungen sind okay). Bei N Servern gibt es eine eindeutige Kombination aus "n Choose 3" – Dies bedeutet das, was für einige allgemeine Cluster Größen bedeutet:

| Anzahl der Server (N) | Anzahl eindeutiger, durch Trennzeichen getrennter Zuordnungen (N auswählen 3) |
|-----------------------|-----------------------------------------------------|
| 6                     | 20                                                  |
| 8                     | 56                                                  |
| 12                    | 220                                                 |
| 16                    | 560                                                 |

   > [!TIP]
   > Betrachten Sie diese hilfreiche Überprüfung von [Combinatorics, und wählen Sie Notation](https://betterexplained.com/articles/easy-permutations-and-combinations/)aus.

Im folgenden Beispiel wird die Fehlertoleranz maximiert – jedes Volume verfügt über eine eindeutige, durch Trennzeichen getrennte Zuordnung:

![eindeutige Zuordnung](media/delimit-volume-allocation/unique-allocation.png)

Im nächsten Beispiel verwenden die ersten drei Volumes die gleiche getrennte Zuordnung (zu den Servern 1, 2 und 3), und die letzten drei Volumes verwenden die gleiche getrennte Zuordnung (zu den Servern 4, 5 und 6). Dadurch wird die Fehlertoleranz nicht maximiert: Wenn drei Server ausfallen, können mehrere Volumes offline geschaltet werden, und der Zugriff auf einmal ist nicht mehr möglich.

![nicht eindeutige Zuordnung](media/delimit-volume-allocation/non-unique-allocation.png)

## <a name="analysis"></a>Experten

In diesem Abschnitt wird die mathematische Wahrscheinlichkeit abgeleitet, mit der ein Volume online und zugänglich (oder gleichermaßen der erwartete Anteil des gesamten Speichers, der Online und zugänglich bleibt) als Funktion der Anzahl von Fehlern und der Clustergröße angezeigt wird.

   > [!NOTE]
   > Dieser Abschnitt ist ein optionales Lesevorgang. Wenn Sie die mathematische Informationen sehen möchten, lesen Sie die Informationen unter! Wenn dies nicht der gibt, machen Sie sich keine Sorgen: Die [Verwendung von PowerShell](#usage-in-powershell) und [bewährten Methoden](#best-practices) ist alles, was Sie benötigen, um eine getrennte Zuordnung erfolgreich zu implementieren.

### <a name="up-to-two-failures-is-always-okay"></a>Bis zu zwei Fehler sind immer okay.

Jedes drei-Wege-Spiegelungs Volume kann bis zu zwei Fehler gleichzeitig überstehen, wie [Diese Beispiele](storage-spaces-fault-tolerance.md#examples) veranschaulichen, unabhängig von der Zuordnung. Wenn zwei Laufwerke ausfallen oder bei zwei Servern ein Fehler auftritt bzw. eines von beiden, dann bleibt jedes drei-Wege-Spiegelungs Volume online und zugänglich, auch bei normaler Zuordnung.

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>Mehr als die Hälfte des Cluster Fehlers ist nie okay

Im umgekehrten Fall, dass mehr als die Hälfte der Server oder Laufwerke im Cluster gleichzeitig ausfallen, geht das [Quorum verloren](understand-quorum.md) , und jedes drei-Wege-Spiegelungs Volume wechselt in den Offline Modus und ist unabhängig von dessen Zuordnung nicht mehr verfügbar.

### <a name="what-about-in-between"></a>Wie sieht es zwischen aus?

Wenn drei oder mehr Fehler gleichzeitig auftreten, aber mindestens die Hälfte der Server und Laufwerke weiterhin aktiv sind, bleiben Volumes mit durch Trennzeichen getrennten Zuordnungen möglicherweise Online und zugänglich, je nachdem, welche Server Fehler aufweisen. Wir führen die Zahlen aus, um die genauen Chancen zu ermitteln.

Nehmen Sie zur Vereinfachung an, dass Volumes unabhängig von den oben genannten bewährten Methoden unabhängig und identisch verteilt sind und dass ausreichend eindeutige Kombinationen für die Zuordnung aller Volumes verfügbar sind. Die Wahrscheinlichkeit, dass ein bestimmtes Volume nicht mehr vorhanden ist, ist auch der erwartete Anteil des gesamten Speichers, der durch die Linearität der Erwartung überlebt wird. 

Bei **N** Servern, von denen **F** Fehler hat, wird ein Volume, das **3** von Ihnen zugeordnet ist, nur dann offline geschaltet, wenn alle **drei** in den **f** -Fehler auftreten. Es gibt **(N auswählen F)** Möglichkeiten für **F** -Fehler, von denen **(f-Auswahl 3)** dazu führt, dass das Volume offline geschaltet wird und nicht mehr auf Sie zugegriffen werden kann. Die Wahrscheinlichkeit kann wie folgt ausgedrückt werden:

![P_offline = Fc3/NCF](media/delimit-volume-allocation/probability-volume-offline.png)

In allen anderen Fällen bleibt das Volume online und zugänglich:

![P_online = 1 – (Fc3/NCF)](media/delimit-volume-allocation/probability-volume-online.png)

In den folgenden Tabellen werden die Wahrscheinlichkeit für einige gemeinsame Cluster Größen und bis zu 5 Fehler ausgewertet. Dadurch wird die Fehlertoleranz durch die getrennte Zuordnung im Vergleich zur regulären Zuordnung in jedem Fall in Erwägung gezogen.

### <a name="with-6-servers"></a>Mit 6 Servern

| Zuordnung                           | Wahrscheinlichkeit, dass ein Fehler auftritt | Wahrscheinlichkeit für das überstehen von 2 Fehlern | Wahrscheinlichkeit von drei Fehlern | Wahrscheinlichkeit für das überstehen von 4 Fehlern | Wahrscheinlichkeit von fünf Fehlern |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regulär, auf alle 6 Server verteilt | 100%                               | 100%                                | 1,0                                  | 1,0                                  | 1,0                                  |
| Begrenzt auf nur drei Server          | 100%                               | 100%                                | 95,0%                               | 1,0                                  | 1,0                                  |

   > [!NOTE]
   > Nach mehr als 3 Fehlern von 6 Gesamt Servern verliert der Cluster das Quorum.

### <a name="with-8-servers"></a>Mit 8 Servern

| Zuordnung                           | Wahrscheinlichkeit, dass ein Fehler auftritt | Wahrscheinlichkeit für das überstehen von 2 Fehlern | Wahrscheinlichkeit von drei Fehlern | Wahrscheinlichkeit für das überstehen von 4 Fehlern | Wahrscheinlichkeit von fünf Fehlern |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regulär, auf alle 8 Server verteilt | 100%                               | 100%                                | 1,0                                  | 1,0                                  | 1,0                                  |
| Begrenzt auf nur drei Server          | 100%                               | 100%                                | 98,2%                               | 94.3%                               | 1,0                                  |

   > [!NOTE]
   > Nach mehr als 4 Fehlern von 8 Gesamt Servern verliert der Cluster das Quorum.

### <a name="with-12-servers"></a>Mit 12 Servern

| Zuordnung                            | Wahrscheinlichkeit, dass ein Fehler auftritt | Wahrscheinlichkeit für das überstehen von 2 Fehlern | Wahrscheinlichkeit von drei Fehlern | Wahrscheinlichkeit für das überstehen von 4 Fehlern | Wahrscheinlichkeit von fünf Fehlern |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regulär, auf alle 12 Server verteilt | 100%                               | 100%                                | 1,0                                  | 1,0                                  | 1,0                                  |
| Begrenzt auf nur drei Server           | 100%                               | 100%                                | 99,5%                               | 99,2%                               | 98,7%                               |

### <a name="with-16-servers"></a>Mit 16 Servern

| Zuordnung                            | Wahrscheinlichkeit, dass ein Fehler auftritt | Wahrscheinlichkeit für das überstehen von 2 Fehlern | Wahrscheinlichkeit von drei Fehlern | Wahrscheinlichkeit für das überstehen von 4 Fehlern | Wahrscheinlichkeit von fünf Fehlern |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Regulär, auf alle 16 Server verteilt | 100%                               | 100%                                | 1,0                                  | 1,0                                  | 1,0                                  |
| Begrenzt auf nur drei Server           | 100%                               | 100%                                | 99,8%                               | 99,8%                               | 99,8%                               |

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="can-i-delimit-some-volumes-but-not-others"></a>Kann ich einige Volumes begrenzen, aber keine anderen?

Ja. Sie können pro Volume auswählen, ob die Zuordnung begrenzt werden soll.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>Ändert die durch Trennzeichen getrennte Zuordnung die Funktionsweise der Laufwerk Ersetzung?

Nein, es ist das gleiche wie bei der regulären Zuordnung.

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Fehlertoleranz in direkte Speicherplätze](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>Anhang

Mit diesem Skript können Sie sehen, wie Ihre Volumes zugeordnet werden.

Um es wie oben beschrieben zu verwenden, kopieren/einfügen und speichern `Get-VirtualDiskFootprintBySSU.ps1`unter.

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
