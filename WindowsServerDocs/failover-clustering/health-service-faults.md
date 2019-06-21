---
title: Integritätsdienst-Dienstfehler
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 72b1593503db75aa275b9eb45c8342cee6724001
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280396"
---
# <a name="health-service-faults"></a>Integritätsdienst-Dienstfehler
> Gilt für: Windows Server 2019, Windows Server 2016

## <a name="what-are-faults"></a>Was sind Fehler

Der Integritätsdienst überwacht ständig Ihre "direkte Speicherplätze"-Cluster zum Erkennen von Problemen und zum Generieren von "Fehler". Ein neues Cmdlet zeigt aktuelle Fehler, sodass Sie problemlos die Integrität Ihrer Bereitstellung zu überprüfen, ohne den Blick auf jede Entität oder wiederum feature. Fehler sind auf Präzision, leichte Verständlichkeit und Umsetzbarkeit ausgelegt.  

Jeder Fehler enthält fünf wichtige Felder:  

-   Nach Schweregrad
-   Beschreibung des Problems
-   Empfohlene nächste Schritte zum Beheben des Problems
-   Identifizierende Informationen zur fehlerbehafteten Entität
-   Die physische Stelle (falls zutreffend)

Es folgt ein Beispiel eines typischen Fehlers:  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > Die physische Stelle wird von der Konfiguration der Fehlerdomäne abgeleitet. Weitere Informationen zu Fehlerdomänen finden Sie unter [Fehlerdomänen in Windows Server 2016](fault-domains.md). Wenn Sie diese Informationen nicht angeben, ist das Feld mit der Stelle weniger hilfreich, sodass z. B. nur die Steckplatznummer angezeigt wird.  

## <a name="root-cause-analysis"></a>Analyse der Grundursache

Der Integritätsdienst kann die potenzielle ursächlichkeit zwischen Entitäten, um zu ermitteln, und kombinieren die Fehler, die Folgen der gleichen zugrunde liegenden Problems sind Fehler. Durch erkennen von Kausalketten ergeben sich kürzere Berichte. Z. B. wenn ein Server ausgefallen ist, wird erwartet, als alle Laufwerke auf dem Server auch ohne Konnektivität ist. Aus diesem Grund wird für die zugrunde liegende Ursache: in diesem Fall der Server nur ein Fehler ausgelöst.  

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Um aktuelle Fehler in PowerShell anzuzeigen, führen Sie dieses Cmdlet aus:

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

Dadurch werden alle Fehler, die den gesamten "direkte Speicherplätze"-Cluster sich darauf auswirken zurückgegeben. In den meisten Fällen beziehen sich diese Fehler, Hardware oder Konfiguration zu erhalten. Wenn keine Fehler vorhanden sind, gibt dieses Cmdlet nichts zurück.  

>[!NOTE]
> In einer nicht produktiven Umgebungen und auf eigenes Risiko können Sie mit diesem Feature experimentieren, selbst Fehler auslösen – z. B. durch einen physischen Datenträger ausbauen oder einen Knoten herunterfahren. Nach der Fehler angezeigt wurde, fügen Sie erneut die physischen Datenträger oder Neustarten des Knotens und der Fehler wieder verschwindet.

Sie können auch Fehler anzeigen, die sich nur auf bestimmte Volumes oder Dateifreigaben mit den folgenden Cmdlets auswirken:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

Dadurch werden alle Fehler, die betreffen nur die spezifische Volume oder die Dateifreigabe zurückgegeben. In den meisten Fällen beziehen sich diese Fehler kapazitätsplanung, die resilienz von Daten oder Funktionen wie Storage Quality-of-Service "oder" Funktion "Speicherreplikat" ein. 

## <a name="usage-in-net-and-c"></a>Nutzung in .NET undC#

### <a name="connect"></a>Verbinden

Um den Health-Dienst abzufragen, müssen Sie zum Herstellen einer **CimSession** mit dem Cluster. Zu diesem Zweck Sie einige Aufgaben benötigen, die nur im vollständigen .NET verfügbar sind, das heißt, Sie sofort diese direkt aus einer Web- oder mobilen app nicht möglich. Diese Codebeispiele verwenden C\#am einfachsten Wahl für diese Data Access-Ebene.

``` 
...
using System.Security;
using Microsoft.Management.Infrastructure;

public CimSession Connect(string Domain = "...", string Computer = "...", string Username = "...", string Password = "...")
{
    SecureString PasswordSecureString = new SecureString();
    foreach (char c in Password)
    {
        PasswordSecureString.AppendChar(c);
    }

    CimCredential Credentials = new CimCredential(
        PasswordAuthenticationMechanism.Default, Domain, Username, PasswordSecureString);
    WSManSessionOptions SessionOptions = new WSManSessionOptions();
    SessionOptions.AddDestinationCredentials(Credentials);
    Session = CimSession.Create(Computer, SessionOptions);
    return Session;
}
```

Der angegebene Benutzername sollte ein lokaler Administrator des Ziels Computer.

Es wird empfohlen, dass Sie das Kennwort erstellen, **SecureString** direkt aus der Benutzereingabe in Echtzeit, also ihr Kennwort nie im Arbeitsspeicher gespeichert in Klartext. Dadurch wird eine Vielzahl von Sicherheitsrisiken zu verringern. Aber in der Praxis ist es wie oben beschrieben zu erstellen ist üblich für Zwecke der Erstellung von Prototypen.

### <a name="discover-objects"></a>Ermitteln von Objekten

Mit der **CimSession** eingerichtet, können Sie Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) auf dem Cluster Abfragen.

Bevor Sie einen Fehler oder Metriken abrufen können, müssen Sie Instanzen von mehreren relevanten Objekte abzurufen. Zunächst wird die **MSFT\_StorageSubSystem** auf dem Cluster "direkte Speicherplätze" darstellt. Verwenden, die, erhalten Sie alle **MSFT\_StorageNode** im Cluster und jede **MSFT\_Volume**, Datenvolumes. Abschließend müssen Sie die **MSFT\_StorageHealth**, den Health-Dienst, zu.

```
CimInstance Cluster;
List<CimInstance> Nodes;
List<CimInstance> Volumes;
CimInstance HealthService;

public void DiscoverObjects(CimSession Session)
{
    // Get MSFT_StorageSubSystem for Storage Spaces Direct
    Cluster = Session.QueryInstances(@"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageSubSystem")
        .First(Instance => (Instance.CimInstanceProperties["FriendlyName"].Value.ToString()).Contains("Cluster"));

    // Get MSFT_StorageNode for each cluster node
    Nodes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageNode", null, "StorageSubSystem", "StorageNode").ToList();

    // Get MSFT_Volumes for each data volume
    Volumes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToVolume", null, "StorageSubSystem", "Volume").ToList();

    // Get MSFT_StorageHealth itself
    HealthService = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageHealth", null, "StorageSubSystem", "StorageHealth").First();
}
```

Hierbei handelt es sich um die gleichen Objekte Sie im PowerShell erhalten-Cmdlets wie über **Get-StorageSubSystem**, **Get-StorageNode**, und **Get-Volume**.

Es stehen die gleichen Eigenschaften, die am dokumentiert [Storage Management API Classes](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx).

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

### <a name="query-faults"></a>Abfrage-Fehler

Rufen Sie **Diagnose** abzurufenden aktuelle Fehler im Bereich einer an das Ziel **CimInstance**, Cluster oder ein Volume sein.

Die vollständige Liste von Fehlern, die in jeder Bereich in Windows Server 2016 verfügbar ist im folgenden dokumentiert.

```       
public void GetFaults(CimSession Session, CimInstance Target)
{
    // Set Parameters (None)
    CimMethodParametersCollection FaultsParams = new CimMethodParametersCollection();
    // Invoke API
    CimMethodResult Result = Session.InvokeMethod(Target, "Diagnose", FaultsParams);
    IEnumerable<CimInstance> DiagnoseResults = (IEnumerable<CimInstance>)Result.OutParameters["DiagnoseResults"].Value;
    // Unpack
    if (DiagnoseResults != null)
    {
        foreach (CimInstance DiagnoseResult in DiagnoseResults)
        {
            // TODO: Whatever you want!
        }
    }
}
```

### <a name="optional-myfault-class"></a>Optional: MyFault-Klasse

Es kann sinnvoll für die Sie zum Erstellen und speichern Ihre eigenen Darstellung von Fehlern. Beispielsweise **MyFault** Klasse speichert verschiedene Schlüsseleigenschaften von Fehlern, einschließlich der **FaultId**, die später verwendet werden können, ordnen aktualisieren oder entfernen die Benachrichtigungen oder dedupliziert, mehrere Male auf, aus irgendeinem Grund ist der gleiche Fehler erkannt.

```       
public class MyFault {
    public String FaultId { get; set; }
    public String Reason { get; set; }
    public String Severity { get; set; }
    public String Description { get; set; }
    public String Location { get; set; }

    // Constructor
    public MyFault(CimInstance DiagnoseResult)
    {
        CimKeyedCollection<CimProperty> Properties = DiagnoseResult.CimInstanceProperties;
        FaultId     = Properties["FaultId"                  ].Value.ToString();
        Reason      = Properties["Reason"                   ].Value.ToString();
        Severity    = Properties["PerceivedSeverity"        ].Value.ToString();
        Description = Properties["FaultingObjectDescription"].Value.ToString();
        Location    = Properties["FaultingObjectLocation"   ].Value.ToString();
    }
}
```

```
List<MyFault> Faults = new List<MyFault>;

foreach (CimInstance DiagnoseResult in DiagnoseResults)
{
    Faults.Add(new Fault(DiagnoseResult));
}
```

Die vollständige Liste der Eigenschaften in jeder Fehler (**DiagnoseResult**) finden Sie unten.

### <a name="fault-events"></a>Fehlerereignisse

Wenn der Fehler erstellt wird, entfernt oder aktualisiert werden, generiert der Integritätsdienst WMI-Ereignisse. Diese zu synchronisieren der Anwendungszustand ohne häufiger Abruf von entscheidender Bedeutung sind, und können sich mit Dingen wie dem Senden von e-Mail-Benachrichtigungen, z. B. wann. Dieser Beispielcode verwendet das Entwurfsmuster "Beobachter" um diese Ereignisse zu abonnieren, erneut aus.

Zuerst abonnieren **MSFT\_StorageFaultEvent** Ereignisse.

```      
public void ListenForFaultEvents()
{
    IObservable<CimSubscriptionResult> Events = Session.SubscribeAsync(
        @"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageFaultEvent");
    // Subscribe the Observer
    FaultsObserver<CimSubscriptionResult> Observer = new FaultsObserver<CimSubscriptionResult>(this);
    IDisposable Disposeable = Events.Subscribe(Observer);
}   
```

Als Nächstes Implementieren eines observers, deren **OnNext()** Methode wird aufgerufen, wenn ein neues Ereignis generiert wird.

Jedes Ereignis enthält **ChangeType** , der angibt, ob ein Fehler, entfernt oder aktualisierte erstellt wird, und die relevanten **FaultId**.

Darüber hinaus enthalten sie alle Eigenschaften der der Fehler selbst.

```
class FaultsObserver : IObserver
{
    public void OnNext(T Event)
    {
        // Cast
        CimSubscriptionResult SubscriptionResult = Event as CimSubscriptionResult;

        if (SubscriptionResult != null)
        {
            // Unpack            
            CimKeyedCollection<CimProperty> Properties = SubscriptionResult.Instance.CimInstanceProperties;
            String ChangeType = Properties["ChangeType"].Value.ToString();
            String FaultId = Properties["FaultId"].Value.ToString();

            // Create
            if (ChangeType == "0")
            {
                Fault MyNewFault = new MyFault(SubscriptionResult.Instance);
                // TODO: Whatever you want!
            }
            // Remove
            if (ChangeType == "1")
            {
                // TODO: Use FaultId to find and delete whatever representation you have...
            }
            // Update
            if (ChangeType == "2")
            {
                // TODO: Use FaultId to find and modify whatever representation you have...
            }
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Nothing
    }
}
```

### <a name="understand-fault-lifecycle"></a>Grundlegendes zum Lebenszyklus von Fehler

Fehler sind nicht dazu gedacht, "sehen" oder durch den Benutzer aufgelöst markiert werden soll. Sie werden erstellt, wenn der Integritätsdienst ein Problem überwacht, und sie werden automatisch entfernt, und nur dann, wenn der Integritätsdienst nicht mehr das Problem beobachten können. Im Allgemeinen gibt an, dass das Problem behoben wurde.

Allerdings können in einigen Fällen Fehler vom Integritätsdienst (z. B. nach einem Failover, oder aufgrund eines zeitweiligen Verbindungsproblemen usw.) erneut gefunden. Aus diesem Grund es möglicherweise sinnvoll, Ihre eigenen Darstellung von Fehlern, beibehalten, damit Sie problemlos deduplizieren können. Dies ist besonders wichtig, wenn Sie e-Mail-Benachrichtigungen oder eine entsprechende senden.

### <a name="properties-of-faults"></a>Eigenschaften von Fehlern

Diese Tabelle zeigt verschiedene Schlüsseleigenschaften des Fault-Objekts. Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageDiagnoseResult** -Klasse im *storagewmi.mof*.

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Grund                    | "Das Volume verfügbaren Speicherplatz ausgeführt wird."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | Rack A06, RU 25, Slot 11                                        |
| RecommendedActions        | {"Erweitern Sie Volumes" ","Migrieren Sie Workloads auf andere Volumes.""}   |

**FaultId** eindeutig innerhalb des Bereichs eines Clusters.

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} = {"Informational", "Warnung" und "Error"} oder entsprechende Farben wie Blau, Gelb und Rot.

**FaultingObjectDescription** Teil der Informationen zu Hardware, Software-Objekte in der Regel leer.

**FaultingObjectLocation** nach Informationen zu Hardware, leere in der Regel für Software-Objekte.

**Recommendedactions:** Liste mit empfohlenen Aktionen, die unabhängig sind und in keiner bestimmten Reihenfolge. Diese Liste ist heute oft der Länge 1.

## <a name="properties-of-fault-events"></a>Eigenschaften der Fehlerereignisse

Diese Tabelle zeigt verschiedene Schlüsseleigenschaften des Ereignisses Fehler. Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageFaultEvent** -Klasse im *storagewmi.mof*.

Beachten Sie die **ChangeType**, der angibt, ob ein Fehler, entfernt oder aktualisiert erstellt wird, und die **FaultId**. Ein Ereignis enthält auch alle Eigenschaften des betreffenden Fehlers aus.

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Grund                    | "Das Volume verfügbaren Speicherplatz ausgeführt wird."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | Rack A06, RU 25, Slot 11                                        |
| RecommendedActions        | {"Erweitern Sie Volumes" ","Migrieren Sie Workloads auf andere Volumes.""}   |

**ChangeType** ChangeType = { 0, 1, 2 } = { "Create", "Remove", "Update" }.

## <a name="coverage"></a>Abdeckung

In Windows Server 2016 bietet der Integritätsdienst die folgende Abdeckung für Fehler:  

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* Schweregrad: Warnung
* Grund: *"Der physische Datenträger konnte."*
* RecommendedAction: *"Ersetzen Sie die physischen Datenträger".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* Schweregrad: Warnung
* Grund: *"Verbindung mit dem physikalischen Datenträger wurde getrennt."*
* RecommendedAction: *"Überprüfen Sie, dass der physische Datenträger funktionieren und ordnungsgemäß verbunden ist."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* Schweregrad: Warnung
* Grund: *"Für der physische Datenträger wird wiederholt eine nicht reagierende Benutzeroberfläche weist auf."*
* RecommendedAction: *"Ersetzen Sie die physischen Datenträger".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* Schweregrad: Warnung
* Grund: *"Ein Fehler des physischen Datenträgers wird vorhergesagt, bald stattfinden."*
* RecommendedAction: *"Ersetzen Sie die physischen Datenträger".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* Schweregrad: Warnung
* Grund: *"Der physische Datenträger wird isoliert, da sie von Ihrem Lösungsanbieter nicht unterstützt wird."*
* RecommendedAction: *"Ersetzen Sie den physischen Datenträger mit unterstützte Hardware."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* Schweregrad: Warnung
* Grund: *"Der physische Datenträger ist in Quarantäne, da die Firmwareversion nicht von Ihrem Lösungsanbieter unterstützt wird."*
* RecommendedAction: *"Aktualisieren der Firmware auf dem physischen Datenträger auf die Zielversion".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* Schweregrad: Warnung
* Grund: *"Der physische Datenträger hat ein Unbekannter Metadaten."*
* RecommendedAction: *"Dieser Datenträger kann Daten aus einer unbekannten-Speicherpool enthalten. Stellen Sie sicher, dass es keine sinnvollen Daten auf diesem Datenträger zunächst den Datenträger zurückgesetzt."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* Schweregrad: Warnung
* Grund: *"Fehlerhafte Versuch zum Aktualisieren der Firmware auf dem physischen Datenträger."*
* RecommendedAction: *"Versuchen Sie es mithilfe ein anderes Firmware binäre."*

### <a name="virtual-disk-2"></a>**Virtual Disk (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* Schweregrad: Informationen
* Grund: *"Einige Daten auf diesem Volume ist nicht vollständig ausfallsicher. Es bleibt zugegriffen werden kann."*
* RecommendedAction: *"Wiederherstellen der ausfallsicherheit der Daten".*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.Detached
* Schweregrad: Kritisch
* Grund: *"Das Volume ist nicht möglich. Einige Daten möglicherweise verloren."*
* RecommendedAction: *"Überprüfen die physischen und/oder Netzwerkkonnektivität aller Speichergeräte. Sie können aus einer Sicherung wiederherstellen müssen."*

### <a name="pool-capacity-1"></a>**Poolkapazität (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* Schweregrad: Warnung
* Grund: *"Der Speicherpool muss nicht die minimale empfohlene reservierte Kapazität. Dadurch kann Ihre Fähigkeit, Daten Stabilität bei Fehlern bei der Umwandlung Laufwerk wiederherstellen eingeschränkt."*
* RecommendedAction: *"Zusätzlichen Kapazität dem Speicherpool hinzufügen oder Kapazität freizugeben. Die empfohlene reservieren variiert je nach der Bereitstellung, aber es ist ungefähr 2 Laufwerken-Wert, der Kapazität."*

### <a name="volume-capacity-2sup1sup"></a>**Volumekapazität (2)** <sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* Schweregrad: Warnung
* Grund: *"Das Volume verfügbaren Speicherplatz ausgeführt wird."*
* RecommendedAction: *"Erweitern Sie das Volume oder Migrieren Sie Workloads auf andere Volumes."*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* Schweregrad: Kritisch
* Grund: *"Das Volume verfügbaren Speicherplatz ausgeführt wird."*
* RecommendedAction: *"Erweitern Sie das Volume oder Migrieren Sie Workloads auf andere Volumes."*

### <a name="server-3"></a>**Server (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft.Health.FaultType.Server.Down
* Schweregrad: Kritisch
* Grund: *"Der Server nicht erreichbar."*
* RecommendedAction: *"Starten oder Server ersetzen".*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft.Health.FaultType.Server.Isolated
* Schweregrad: Kritisch
* Grund: *"Der Server ist isoliert, aus dem Cluster aufgrund von Konnektivitätsproblemen."*
* RecommendedAction: *"Wenn Isolation weiterhin besteht, überprüfen Sie die Netzwerke aus, oder Migrieren Sie Workloads auf andere Knoten."*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft.Health.FaultType.Server.Quarantined
* Schweregrad: Kritisch
* Grund: *"Der Server wird vom Cluster aufgrund von periodischen Fehlern isoliert."*
* RecommendedAction: *"Den Server ersetzen oder das Netzwerk reparieren".*

### <a name="cluster-1"></a>**Cluster (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* Schweregrad: Kritisch
* Grund: *"Der Cluster ist ein Ausfall des Servers sinkt."*
* RecommendedAction: *"Überprüfen Sie die Witness-Ressource, und starten Sie nach Bedarf neu. Starten Sie, oder Ersetzen Sie ausgefallene Server."*

### <a name="network-adapterinterface-4"></a>**/ Netzwerkschnittstellenkarte (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* Schweregrad: Warnung
* Grund: *"Die Netzwerkschnittstelle wurde getrennt werden."*
* RecommendedAction: *"Schließen Sie die Netzwerkkabel wieder."*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft.Health.FaultType.NetworkInterface.Missing
* Schweregrad: Warnung
* Grund: *"Dem Server {Server} ist, fehlt der Netzwerk-Adapter, die mit Clusternetzwerk {Clusternetzwerk} verbunden."*
* RecommendedAction: *"Verbinden Sie den Server, auf das Clusternetzwerk fehlt."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Hardware
* Schweregrad: Warnung
* Grund: *"Die Netzwerkschnittstelle ist einen Hardwarefehler aufgetreten."*
* RecommendedAction: *"Replace Netzwerkschnittstellenadapters."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disabled
* Schweregrad: Warnung
* Grund: *"Die Netzwerkschnittstelle {Netzwerkschnittstelle} ist nicht aktiviert und wird nicht verwendet."*
* RecommendedAction: *"Aktivieren der Netzwerkschnittstelle".*

### <a name="enclosure-6"></a>**Gehäuse (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* Schweregrad: Warnung
* Grund: *"Kommunikation mit dem Storage-Gehäuse wurde unterbrochen."*
* RecommendedAction: *"Starten Sie, oder Ersetzen Sie das Speichersystem."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.FanError
* Schweregrad: Warnung
* Grund: *"Der Lüfter an Position {Position} des Speichergehäuse ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen des Lüfters im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* Schweregrad: Warnung
* Grund: *"Aktuelle Sensor an Position {Position} des Speichergehäuse ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen eines aktuellen Sensors im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* Schweregrad: Warnung
* Grund: *"An Position {Position} des Speichergehäuse Spannungssensors ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen eines Spannungssensors im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* Schweregrad: Warnung
* Grund: *"Der e/a-Controller an Position {Position} des Speichergehäuse ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen eines e/a-Controllers im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* Schweregrad: Warnung
* Grund: *"An Position {Position} des Speichergehäuse Temperatursensor ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen Sie ein Temperatursensors überwacht im Speichergehäuse."*

### <a name="firmware-rollout-3"></a>**Rollout der Firmware (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* Schweregrad: Warnung
* Grund: *"Kann zurzeit nicht Fortschritte macht, beim Ausführen der Rollout der Firmware."*
* RecommendedAction: *"Überprüfen Sie alle Speicherplätze fehlerfrei sind und dass keine Fehlerdomäne derzeit im Wartungsmodus befindet."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* Schweregrad: Warnung
* Grund: *"Firmware Rollout wurde aufgrund nicht gelesen werden oder unerwartete Firmware-Version-Informationen nach dem Anwenden eines Firmwareupdates abgebrochen."*
* RecommendedAction: *"Neustart Firmware einführen, sobald das Firmware-Problem gelöst wurde."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* Schweregrad: Warnung
* Grund: *"Firmware Rollout wurde aufgrund von zu viele physische Datenträger, die einen Firmware-Update-Versuch fehlschlagen abgebrochen."*
* RecommendedAction: *"Neustart Firmware einführen, sobald das Firmware-Problem gelöst wurde."*

### <a name="storage-qos-3sup2sup"></a>**QoS für Speicher (3)** <sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* Schweregrad: Warnung
* Grund: *"Speicherdurchsatz ist nicht ausreichend, um Reserven zu erfüllen."*
* RecommendedAction: *"Konfigurieren Sie QoS-Speicherrichtlinien."*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorQos.LostCommunication
* Schweregrad: Warnung
* Grund: *"Der Speicher-QoS-Richtlinien-Manager hat die Kommunikation mit dem Volume verloren" ausgegeben.*
* RecommendedAction: *"Bitte Neustarten Sie Knoten {Knoten}"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* Schweregrad: Warnung
* Grund: *"Einen oder mehrere Speicher-Consumer (normalerweise VMs) sind eine nicht vorhandene Richtlinie mit der Id {Id} verwenden".*
* RecommendedAction: *"Erstellen Sie alle fehlenden-QoS-Speicherrichtlinien neu."*

<sup>1</sup> gibt an, auf dem Volume verfügt über 80 % voll ist (niedriger Schweregrad) oder 90 % voll (hoher Schweregrad) erreicht.  
<sup>2</sup> gibt an, dass einige .vhd(s) auf dem Volume wurden nicht erfüllt die IOPS-Mindestwert von über 10 % (niedrig), 30 % (hoch) oder 50 % (kritisch) 24-Stunden-Fenster.  

>[!NOTE]
> Die Integrität von Speichergehäusekomponenten wie Lüfter, Netzteile und Sensoren wird von SES (SCSI Enclosure Services) abgeleitet. Wenn Ihr Anbieter diese Informationen nicht bereitstellt, kann der Integritätsdienst sie nicht anzeigen.  

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
