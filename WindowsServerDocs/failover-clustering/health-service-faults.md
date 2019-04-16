---
title: Health-Dienst Fehler
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: c9e1fb4568ee93739c49ccc1a13106b09161c5f3
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-faults"></a>Health-Dienst Fehler
> Gilt für WindowsServer 2016

## <a name="what-are-faults"></a>Was sind Fehler?

Der Integritätsdienst überwacht Ihren "direkte Speicherplätze" Cluster um Probleme erkennen und "Fehler" zu generieren. Ein neues Cmdlet zeigt aktuelle Fehler, sodass Sie leicht zu überprüfen, die Integrität Ihrer Bereitstellung ohne jede Entität betrachten oder wiederum Feature. Fehler dienen zur genauen, leicht verständlich und verwendbar sein.  

Jeder Fehler enthält fünf wichtige Felder:  

-   Schweregrad
-   Beschreibung des Problems
-   Empfohlene nächste Schritte zum Beheben des Problems beheben
-   Identifizierende Informationen zur fehlerbehafteten Entität
-   Die physische Stelle (falls zutreffend)

Hier ist z. B. ein typisches Fehlers:  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > Der Standort wird von der Konfiguration der Fehlerdomäne abgeleitet. Weitere Informationen zu Fehlerdomänen finden Sie unter [Fehlerdomänen in Windows Server 2016](fault-domains.md). Wenn Sie diese Informationen nicht angeben, Feld Ort wird weniger hilfreich sein – z. B. können sie nur die Steckplatznummer angezeigt.  

## <a name="root-cause-analysis"></a>Ursachenanalyse

Der Integritätsdienst kann die potenzielle ursächlichkeit unter fehlgeschlagene Entitäten zu identifizieren und zu kombinieren, die Folgen desselben zugrunde liegenden Problems sind. Durch das Erkennen von, ist dies die für weniger ausführliche Berichte. Wenn beispielsweise ein Server ausfällt, wird davon ausgegangen als alle Laufwerke auf dem Server auch ohne Verbindung verwendet werden. Aus diesem Grund wird für die Fehlerursache – in diesem Fall der Server nur ein Fehler ausgelöst.  

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Um aktuelle Fehler in PowerShell anzuzeigen, führen Sie dieses Cmdlet aus:

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

Dies gibt alle Fehler, die den gesamten "direkte Speicherplätze" Cluster beeinflussen. In den meisten Fällen beziehen sich diese Fehler auf Hardware oder Konfiguration. Wenn keine Fehler vorhanden sind, gibt dieses Cmdlet nichts zurück.  

>[!NOTE]
> In einer Produktionsumgebung und auf eigenes Risiko können Sie mit diesem Feature experimentieren, indem Sie selbst Fehler auslösen – z.B. über einen physischen Datenträger ausbauen oder einen Knoten herunterfahren. Nachdem der Fehler angezeigt wird, legen Sie erneut die physischen Datenträger oder durch einen Neustart der Knoten wieder ausgeblendet werden.

Sie können auch Fehler anzeigen, die sich nur auf bestimmte Volumes oder Dateifreigaben mit den folgenden Cmdlets auswirken:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

Dies gibt alle Fehler, die nur der bestimmten Volume oder die Dateifreigabe auswirken. In den meisten Fällen beziehen sich diese Fehler Kapazitäten genau planen, Daten Resilienz oder Features wie Storage Quality-of-Service oder Speicherreplikat. 

## <a name="usage-in-net-and-c"></a>Verwendung in .NET und C#

### <a name="connect"></a>Eine Verbindung herstellen

Zum Abfragen der Integritätsdienst, müssen Sie zum Herstellen einer **CimSession** mit dem Cluster. Zu diesem Zweck Sie einige Dinge benötigt werden, die nur im vollständigen .NET verfügbar sind, d.h. Sie leicht dies direkt von einem Webserver oder mobile Anwendung nicht möglich. Diese Codebeispiele werden C#-, die einfachste Wahl für diese Datenzugriffsschicht verwenden.

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

Der angegebene Benutzername sollte ein lokaler Administrator des Ziels Computer sein.

Es wird empfohlen, dass Sie das Kennwort erstellen, **SecureString** direkt von Benutzereingaben in Echtzeit, also ihr Kennwort wird niemals im Arbeitsspeicher gespeichert in Klartext. Dadurch wird eine Vielzahl von Sicherheitsbedenken verringern. Erstellen sie wie oben in der Praxis allgemeinen Zwecken Prototypen ist jedoch.

### <a name="discover-objects"></a>Ermitteln von Objekten

Mit der **CimSession** eingerichtet wurde, können Sie Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) auf dem Cluster Abfragen.

Bevor Sie Fehler oder Metriken abrufen können, müssen Sie Instanzen von mehreren relevante Objekte abzurufen. Zuerst wird die **MSFT\_StorageSubSystem** des Clusters "direkte Speicherplätze" darstellt. Verwenden, erhalten Sie alle **MSFT\_StorageNode** im Cluster, und alle **MSFT\_Volume**, die Datenvolumes. Abschließend müssen Sie die **MSFT\_StorageHealth**, die Integrität selbst zu bedienen.

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

Hierbei handelt es sich um die gleichen Objekte, die Sie erhalten in PowerShell mithilfe des Cmdlets wie **Get-StorageSubSystem**, **Get-StorageNode**, und **Get-Volume**.

Sie können Zugriff auf die gleichen Eigenschaften behandelt [Storage Management API Classes](https://msdn.microsoft.com/en-us/library/windows/desktop/hh830612(v=vs.85).aspx).

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

### <a name="query-faults"></a>Abfrage Fehler

Aufrufen **Diagnose** zum Abrufen der Bereich für das Ziel aktuelle Fehler **CimInstance**, die den Cluster oder ein Volume sein.

Die vollständige Liste der Fehler, die auf jeder Ebene in Windows Server2016 verfügbar dokumentiert ist.

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

Es kann sinnvoll für das Erstellen und Ihre eigenen Darstellung von Fehlern beibehalten. Zum Beispiel dieses **MyFault** -Klasse enthält mehrere wichtige Eigenschaften von Fehlern, einschließlich der **FaultId**, deren werden können später Update zuordnen oder Entfernen von Benachrichtigungen oder dedupliziert werden, die der gleiche Fehler ist mehrmals aus irgendeinem Grund wird erkannt.

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

Die vollständige Liste der Eigenschaften in jeder Fehler (**DiagnoseResult**) wird im folgenden beschrieben.

### <a name="fault-events"></a>Fehlerereignisse

Wenn Fehler erstellt, entfernt oder aktualisiert werden, generiert der Integritätsdienst WMI-Ereignisse. Diese sind wichtig für das Synchronisieren von App-Status ohne häufig die Abfrage und enthält beispielsweise bestimmen, wann Warnungen über E-Mail, z.B. senden können. Um diese Ereignisse zu abonnieren, wird dieser Code erneut das Entwurfsmuster Beobachter verwendet.

Erstens abonnieren **MSFT\_StorageFaultEvent** Ereignisse.

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

Implementieren Sie als Nächstes einen Beobachter, deren **OnNext()** Methode aufgerufen, wenn ein neues Ereignis generiert wird.

Jedes Ereignis enthält **ChangeType**, der angibt, ob eine Fehlertoleranz, entfernt oder aktualisiert erstellt wird, und die relevanten **FaultId**.

Darüber hinaus enthalten sie alle Eigenschaften des Fehlers, der sich selbst.

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

### <a name="understand-fault-lifecycle"></a>Verstehen der Fehlertoleranz Lebenszyklus

Fehler werden nicht "gesehen" oder vom Benutzer gelöst markiert werden. Sie werden erstellt, wenn der Integritätsdienst ein Problem verwendet, und sie werden automatisch entfernt, und nur, wenn der Integritätsdienst nicht mehr das jeweilige Problem auftritt, können. Im Allgemeinen zeigt dies an, dass das Problem behoben wurde.

Jedoch können in einigen Fällen Fehler vom Integritätsdienst (z.B. nach einem Failover, oder aufgrund von vorübergehenden Konnektivität usw.) erneut ermittelt werden. Aus diesem Grund kann sinnvoll ist, Ihre eigenen Darstellung von Fehlern, beibehalten, damit Sie leicht dedupliziert werden können. Dies ist besonders wichtig, wenn Sie Warnungen über E-Mail oder einer entsprechenden Gruppe senden.

### <a name="properties-of-faults"></a>Eigenschaften von Fehlern

Diese Tabelle enthält mehrere wichtige Eigenschaften des Objekts Fehlertoleranz. Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageDiagnoseResult** -Klasse im *storagewmi.mof*.

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Grund                    | "Das Volume ist nicht genügend Speicherplatz zur Verfügung ausgeführt."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | Rack A06, RU 25, Steckplatz 11                                        |
| RecommendedActions        | {"Erweitern Sie das Volume.", "Migrieren Sie Arbeitslasten in andere Volumes."}   |

**FaultId** eindeutig innerhalb des Bereichs von einem Cluster.

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} = {"Information", "Warning" und "Fehler"}, oder entsprechende Farben wie z.B. Blau, Gelb und Rot.

**FaultingObjectDescription** Teil der Informationen zu Hardware, Software-Objekte in der Regel leer.

**FaultingObjectLocation** Standortinformationen für Hardware, in der Regel leer, für die Software-Objekte.

**RecommendedActions** Liste von empfohlenen Maßnahmen, die von unabhängig sind und in keiner bestimmten Reihenfolge. Diese Liste ist heute häufig der Länge 1.

## <a name="properties-of-fault-events"></a>Eigenschaften der Fehlerereignisse

Diese Tabelle enthält mehrere wichtige Eigenschaften das Fehlerereignis. Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageFaultEvent** -Klasse im *storagewmi.mof*.

Beachten Sie die **ChangeType**, die angibt, ob ein Fehler, entfernt oder aktualisiert erstellt wird, und die **FaultId**. Ein Ereignis enthält auch alle Eigenschaften des betreffenden Problems.

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Grund                    | "Das Volume ist nicht genügend Speicherplatz zur Verfügung ausgeführt."                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | Rack A06, RU 25, Steckplatz 11                                        |
| RecommendedActions        | {"Erweitern Sie das Volume.", "Migrieren Sie Arbeitslasten in andere Volumes."}   |

**ChangeType** ChangeType = {0, 1, 2} = {"erstellen", "Remove", "Aktualisieren"}.

## <a name="coverage"></a>Abdeckung

In Windows Server2016 bietet der Integritätsdienst die folgende Abdeckung für Fehler:  

### **<a name="physicaldisk-8"></a>Physikalischer Datenträger (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* Schweregrad: Warnung
* Grund: *"der physikalische Datenträger ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen Sie den physischen Datenträger."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* Schweregrad: Warnung
* Grund: *"Verbindung wurde auf den physischen Datenträger verloren."*
* RecommendedAction: *"Überprüfen, ob der physische Datenträger funktioniert und richtig angeschlossen ist."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* Schweregrad: Warnung
* Grund: *"der physische Datenträger weist wiederkehrenden Tonwiedergabe verzögert."*
* RecommendedAction: *"Ersetzen Sie den physischen Datenträger."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* Schweregrad: Warnung
* Grund: *"ein Fehler des physischen Datenträgers wird vorhergesagt, schnell erfolgen."*
* RecommendedAction: *"Ersetzen Sie den physischen Datenträger."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* Schweregrad: Warnung
* Grund: *"der physische Datenträger wird isoliert, da sie von Ihren Lösungsanbieter, um nicht unterstützt wird."*
* RecommendedAction: *"Ersetzen Sie den physischen Datenträger mit unterstützten Hardware".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* Schweregrad: Warnung
* Grund: *"der physikalische Datenträger ist in Quarantäne, da die Firmwareversion von Ihren Lösungsanbieter, um nicht unterstützt wird."*
* RecommendedAction: *"Aktualisieren Sie die Firmware auf dem physischen Datenträger, auf die Zielversion."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* Schweregrad: Warnung
* Grund: *"der physische Datenträger wurde nicht erkannt Metadaten."*
* RecommendedAction: *"dieser Datenträger kann Daten aus einem unbekannten Speicherpool enthalten. Stellen Sie sicher, dass sich keine sinnvolle Daten auf diesem Datenträger zunächst die Kennwortrücksetzdiskette."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* Schweregrad: Warnung
* Grund: *"Aktualisierung der Firmware auf dem physischen Datenträger Versuch fehlgeschlagen".*
* RecommendedAction: *"Versuchen Sie es mit einer anderen Firmware binäre."*

### **<a name="virtual-disk-2"></a>Virtuelle Festplatte (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* Schweregrad: Information
* Grund: *"einige Daten auf diesem Volume ist nicht vollständig ausfallsicher. Es weiterhin zugegriffen werden."*
* RecommendedAction: *"Wiederherstellen von Resilienz der Daten".*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.Detached
* Schweregrad: Kritisch
* Grund: *"das Volume kann nicht zugegriffen werden. Einige Daten möglicherweise verloren."*
* RecommendedAction: *"Überprüfen Sie die physischen bzw. Netzwerk-Konnektivität aller Speichergeräte. Sie müssen aus einer Sicherung wiederherstellen."*

### **<a name="pool-capacity-1"></a>Poolkapazität (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* Schweregrad: Warnung
* Grund: *"Speicherpool verfügt die minimale empfohlene Reservekapazität nicht. Dies kann die Möglichkeit zum Wiederherstellen von Daten Stabilität bei Laufwerkfehlern beschränken."*
* RecommendedAction: *"zusätzlichen Kapazität zum Speicherpool hinzufügen oder Speicherplatz freigegeben. Die empfohlene Mindestkonfiguration für Reserve ist ca. 2 Laufwerke ganzen Kapazität jedoch variiert je nach Bereitstellung."*

### <a name="volume-capacity-2sup1sup"></a>**Volumekapazität (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* Schweregrad: Warnung
* Grund: *"das Volume wird ausgeführt, nicht genügend Speicherplatz verfügbar."*
* RecommendedAction: *"Erweitern des Volumes oder Arbeitslasten in andere Volumes migrieren".*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* Schweregrad: Kritisch
* Grund: *"das Volume wird ausgeführt, nicht genügend Speicherplatz verfügbar."*
* RecommendedAction: *"Erweitern des Volumes oder Arbeitslasten in andere Volumes migrieren".*

### **<a name="server-3"></a>Server (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft.Health.FaultType.Server.Down
* Schweregrad: Kritisch
* Grund: *"der Server nicht erreichbar."*
* RecommendedAction: *"starten oder Server ersetzt."*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft.Health.FaultType.Server.Isolated
* Schweregrad: Kritisch
* Grund: *"der Server ist der Cluster aufgrund von Konnektivitätsproblemen isoliert."*
* RecommendedAction: *"Wenn Isolation weiterhin auftritt, überprüfen Sie die Netzwerke oder Arbeitslasten zu anderen Knoten migrieren."*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft.Health.FaultType.Server.Quarantined
* Schweregrad: Kritisch
* Grund: *"der Server wird vom Cluster aufgrund von periodischen Fehlern isoliert."*
* RecommendedAction: *"Ersetzen Sie den Server oder das Netzwerk reparieren".*

### **<a name="cluster-1"></a>Cluster (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* Schweregrad: Kritisch
* Grund: *"Cluster ist ein Serverausfall heruntergefahren."*
* RecommendedAction: *"Zeugenressource überprüfen, und starten Sie nach Bedarf neu. Starten oder ausgefallene Server zu ersetzen."*

### **<a name="network-adapterinterface-4"></a>/ Netzwerkadapter (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* Schweregrad: Warnung
* Grund: *"die Netzwerkschnittstelle wurde unterbrochen."*
* RecommendedAction: *"Schließen Sie das Netzwerkkabel."*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft.Health.FaultType.NetworkInterface.Missing
* Schweregrad: Warnung
* Grund: *"der Server {Server} hat, fehlende Netzwerkadapter mit Clusternetzwerk {Clusternetzwerk} verbunden."*
* RecommendedAction: *"Verbinden Sie den Server, auf das Clusternetzwerk fehlen."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Hardware
* Schweregrad: Warnung
* Grund: *"die Netzwerkschnittstelle wurde einen Hardwarefehler."*
* RecommendedAction: *"Ersetzen der Netzwerkschnittstellenkarte."*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disabled
* Schweregrad: Warnung
* Grund: *"die {Netzwerkschnittstelle}-Schnittstelle ist nicht aktiviert und nicht verwendet wird."*
* RecommendedAction: *"Aktivieren der Netzwerkschnittstelle."*

### **<a name="enclosure-6"></a>Gehäuse (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* Schweregrad: Warnung
* Grund: *"Kommunikation ist verloren gegangen, dem Speichergerät verbunden."*
* RecommendedAction: *"Starten oder ersetzen Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.FanError
* Schweregrad: Warnung
* Grund: *"der Lüfter an der Position {Position} des Speichergeräts ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen den Lüfter im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* Schweregrad: Warnung
* Grund: *"der aktuelle Sensor an der Position {Position} des Speichergeräts ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen einen aktuellen Sensor im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* Schweregrad: Warnung
* Grund: *"der Spannungssensor an der Position {Position} des Speichergeräts ist fehlgeschlagen."*
* RecommendedAction: *"Ersetzen ein Sensors Spannung im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* Schweregrad: Warnung
* Grund: *"der E/A-Controller an der Position {Position} des Speichergeräts ist fehlgeschlagen."*
* RecommendedAction: *"Replace einen E/A-Controller im Speichergehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* Schweregrad: Warnung
* Grund: *"der Temperatursensor an der Position {Position} des Speichergeräts ist fehlgeschlagen."*
* RecommendedAction: *"Replace Temperatursensor auf dem Speichergerät verbunden."*

### **<a name="firmware-rollout-3"></a>Firmware-Implementierung (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* Schweregrad: Warnung
* Grund: *"Derzeit nicht beim Ausführen der Firmware-Rollout."*
* RecommendedAction: *"Überprüfen Sie alle Speicherplätze fehlerfrei sind und keine Fehlerdomäne derzeit im Wartungsmodus befindet."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* Schweregrad: Warnung
* Grund: *"Firmware Rollout wurde aufgrund nicht lesbar oder unerwarteten Firmware-Versionsinformationen nach dem Anwenden einer Aktualisierung der Firmware abgebrochen."*
* RecommendedAction: *"Neustart Firmware roll-out-Wenn die Firmware-Problem behoben wurde."*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* Schweregrad: Warnung
* Grund: *"Firmware Rollout wurde abgebrochen, da zu viele physische Datenträger einen Firmware-Update-Versuch fehlschlägt."*
* RecommendedAction: *"Neustart Firmware roll-out-Wenn die Firmware-Problem behoben wurde."*

### <a name="storage-qos-3sup2sup"></a>**Speicher-QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* Schweregrad: Warnung
* Grund: *"Speicherdurchsatz ist nicht ausreichend, um die Reserven erfüllen."*
* RecommendedAction: *"Speicher-QoS-Richtlinien neu konfigurieren."*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorQos.LostCommunication
* Schweregrad: Warnung
* Grund: *"Speicher-QoS-Richtlinien-Manager ging die Kommunikation mit dem Volume."*
* RecommendedAction: *"Starten Sie neu Knoten {Knoten}"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* Schweregrad: Warnung
* Grund: *"einen oder mehrere Speicher-Consumer (in der Regel virtuelle Maschinen) verwenden eine nicht vorhandene Richtlinie mit der ID {ID}."*
* RecommendedAction: *"Erstellen Sie alle fehlenden Speicher-QoS-Richtlinien neu."*

<sup>1</sup> gibt an, auf dem Volume verfügt über 80 % voll ist (niedriger Schweregrad) oder 90 % voll ist (hoher Schweregrad) erreicht.  
<sup>2</sup> gibt an, dass einige .vhd(s) auf dem Volume nicht ihren IOPS-Mindestwert erreicht haben mehr als 10 % (niedrig), 30 % (hoch) oder 50 % (kritisch) 24-Stunden-Fensters.  

>[!NOTE]
> Die Integrität von speichergehäusekomponenten wie Lüfter, Netzteile und Sensoren wird von SCSI Enclosure Services (SES) abgeleitet. Wenn Ihr Anbieter diese Informationen nicht bereitstellt, kann der Integritätsdienst sie nicht anzeigen.  

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
