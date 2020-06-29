---
title: Integritätsdienst Fehler
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: de2e9939302c0b9937fb54b4082feeecf6de5295
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473107"
---
# <a name="health-service-faults"></a>Integritätsdienst Fehler

> Gilt für: Windows Server 2019, Windows Server 2016

## <a name="what-are-faults"></a>Was sind Fehler?

Der Integritätsdienst überwacht ständig ihren direkte Speicherplätze Cluster, um Probleme zu erkennen und "Fehler" zu generieren. Mit einem neuen Cmdlet werden alle aktuellen Fehler angezeigt, sodass Sie die Integrität Ihrer Bereitstellung problemlos überprüfen können, ohne dass Sie die einzelnen Entitäten oder Features nacheinander betrachten müssen. Fehler sind auf Präzision, leichte Verständlichkeit und Umsetzbarkeit ausgelegt.

Jeder Fehler enthält fünf wichtige Felder:

-   severity
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
 > Die physische Stelle wird von der Konfiguration der Fehlerdomäne abgeleitet. Weitere Informationen zu Fehler Domänen finden Sie unter [Fehler Domänen in Windows Server 2016](fault-domains.md). Wenn Sie diese Informationen nicht angeben, ist das Feld mit der Stelle weniger hilfreich, sodass z. B. nur die Steckplatznummer angezeigt wird.

## <a name="root-cause-analysis"></a>Analyse der Grundursache

Der Integritätsdienst kann die potenzielle Kausalität zwischen fehlerentitäten einschätzen, um Fehler zu identifizieren und zu kombinieren, die Folgen desselben zugrunde liegenden Problems sind. Durch erkennen von Kausalketten ergeben sich kürzere Berichte. Wenn ein Server z. b. herunterfährt, wird erwartet, dass er auch keine Konnektivität hat. Daher wird nur ein Fehler für die Grundursache ausgelöst, in diesem Fall der Server.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Um aktuelle Fehler in PowerShell anzuzeigen, führen Sie dieses Cmdlet aus:

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem
```

Dadurch werden alle Fehler zurückgegeben, die sich auf den gesamten direkte Speicherplätze Cluster auswirken. In den meisten Fällen beziehen sich diese Fehler auf die Hardware oder die Konfiguration. Wenn keine Fehler vorliegen, gibt dieses Cmdlet nichts zurück.

>[!NOTE]
> In einer nicht Produktionsumgebung können Sie mit dieser Funktion experimentieren, indem Sie Fehler selbst auslösen, z. b. durch Entfernen eines physischen Datenträgers oder Herunterfahren eines Knotens. Wenn der Fehler aufgetreten ist, fügen Sie den physischen Datenträger erneut ein, oder starten Sie den Knoten neu, und der Fehler wird wieder verschwindet.

Mithilfe der folgenden Cmdlets können Sie auch Fehler anzeigen, die sich nur auf bestimmte Volumes oder Dateifreigaben auswirken:

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume

Get-FileShare -Name <Name> | Debug-FileShare
```

Dadurch werden alle Fehler zurückgegeben, die sich nur auf das jeweilige Volume oder die Dateifreigabe auswirken. In den meisten Fällen beziehen sich diese Fehler auf die Kapazitätsplanung, die datenresilienz oder Features wie Speicher Qualität oder Speicher Replikat.

## <a name="usage-in-net-and-c"></a>Verwendung in .net und C #

### <a name="connect"></a>Verbinden

Um den Integritätsdienst abzufragen, müssen Sie eine **cimsession** mit dem Cluster einrichten. Zu diesem Zweck benötigen Sie einige Dinge, die nur in der Vollversion von .net verfügbar sind, was bedeutet, dass Sie dies nicht direkt über ein Web oder Mobile App durchführen können. Diese Codebeispiele verwenden C \# , die einfachste Wahl für diese Datenzugriffs Schicht.

```
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

Der angegebene Benutzername muss ein lokaler Administrator des Bereitstellungs Ziel Computers sein.

Es wird empfohlen, dass Sie das Kennwort **SecureString** direkt aus Benutzereingaben in Echtzeit erstellen, damit Ihr Kennwort niemals im Klartext in Klartext gespeichert wird. Dies trägt dazu bei, eine Vielzahl von Sicherheitsrisiken zu verringern. In der Praxis ist es jedoch üblich, diese wie oben beschrieben zu erstellen.

### <a name="discover-objects"></a>Objekte ermitteln

Nachdem die **cimsession** eingerichtet wurde, können Sie Windows-Verwaltungsinstrumentation (WMI) im Cluster Abfragen.

Bevor Sie Fehler oder Metriken erhalten können, müssen Sie Instanzen von mehreren relevanten Objekten erhalten. Zuerst das **MSFT \_ storagesubsystem** , das direkte Speicherplätze im Cluster darstellt. Mit diesem können Sie jede **MSFT \_ storagenode** -Instanz im Cluster und alle **MSFT-Volumes \_ ,** die Datenvolumes, erhalten. Schließlich benötigen Sie auch **MSFT \_ storagehealth**, den Integritätsdienst selbst.

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

Dabei handelt es sich um dieselben Objekte, die Sie in PowerShell mithilfe von Cmdlets wie " **Get-storagesubsystem**", " **Get-storagenode**" und " **Get-Volume**" erhalten.

Sie können auf die gleichen Eigenschaften zugreifen, die unter [Klassen der Speicher Verwaltungs-API](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx)dokumentiert sind.

```
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

### <a name="query-faults"></a>Abfrage Fehler

Rufen Sie **Diagnose** auf, um alle aktuellen Fehler zu ermitteln, die auf die Ziel- **ciminstance bezogen**sind. Dies ist der Cluster oder ein beliebiges Volume.

Die komplette Liste der Fehler, die in jedem Bereich in Windows Server 2016 verfügbar sind, ist unten dokumentiert.

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

### <a name="optional-myfault-class"></a>Optional: myfault-Klasse

Möglicherweise ist es sinnvoll, eine eigene Darstellung von Fehlern zu erstellen und beizubehalten. Diese **myfault** -Klasse speichert beispielsweise verschiedene wichtige Eigenschaften von Fehlern, einschließlich der **faultid**, die später verwendet werden kann, um Aktualisierungs-oder Entfernungs Benachrichtigungen zuzuordnen, oder um eine Deduplizierung durchzuführen, wenn derselbe Fehler mehrmals erkannt wird, aus einem beliebigen Grund.

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

Die komplette Liste der Eigenschaften in den einzelnen Fehlern (**diagnoseresult**) ist unten dokumentiert.

### <a name="fault-events"></a>Fehlerereignisse

Wenn Fehler erstellt, entfernt oder aktualisiert werden, generiert der Integritätsdienst WMI-Ereignisse. Diese sind erforderlich, um den Anwendungs Status ohne häufige Abruf Vorgänge synchron zu halten, und können dabei helfen, wie z. b. das Festlegen von e-Mail-Benachrichtigungen. Um diese Ereignisse zu abonnieren, wird in diesem Beispielcode das Observer-Entwurfsmuster erneut verwendet.

Abonnieren Sie zuerst **MSFT \_ storagefaultevent** -Ereignisse.

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

Implementieren Sie als nächstes einen Beobachter, dessen **OnNext ()** -Methode aufgerufen wird, wenn ein neues Ereignis generiert wird.

Jedes Ereignis enthält den **ChangeType** , der angibt, ob ein Fehler erstellt, entfernt oder aktualisiert wird, und die relevante **faultid**.

Außerdem enthalten Sie alle Eigenschaften des Fehlers selbst.

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

### <a name="understand-fault-lifecycle"></a>Grundlegendes zum Fault Lifecycle

Fehler sind nicht als "sichtbar" oder "aufgelöst" gekennzeichnet. Sie werden erstellt, wenn die Integritätsdienst ein Problem bemerkt, und Sie werden nur dann automatisch entfernt, wenn die Integritätsdienst das Problem nicht mehr beobachten kann. Im Allgemeinen zeigt dies, dass das Problem behoben wurde.

In einigen Fällen können jedoch Fehler von der Integritätsdienst (z. b. nach einem Failover oder aufgrund von zeitweiliger Konnektivität usw.) wiedererkannt werden. Aus diesem Grund ist es möglicherweise sinnvoll, eine eigene Darstellung von Fehlern beizubehalten, damit Sie problemlos deduplizieren können. Dies ist besonders wichtig, wenn Sie e-Mail-Benachrichtigungen oder eine gleichwertige senden.

### <a name="properties-of-faults"></a>Eigenschaften von Fehlern

Diese Tabelle enthält mehrere Schlüsseleigenschaften des Fault-Objekts. Überprüfen Sie für das vollständige Schema die Klasse " **MSFT \_ storagediagnoseresult** " in der Datei " *storagewmi. MOF*".

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| Faultid                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft. Health. faultType. Volume. Capacity                      |
| `Reason`                    | "Auf dem Volume steht kein verfügbarer Speicherplatz mehr zur Verfügung."                 |
| Wahrnehmgrad         | 5                                                               |
| Faultingobjectdescription | XYZ9000 S.N. 123456789                                  |
| Faultingobjectlocation    | Rack A06, ru 25, Slot 11                                        |
| Empfehlungs Aktionen        | {"Erweitern Sie das Volume", "migrieren Sie Workloads zu anderen Volumes".   |

**Faultid** Eindeutig innerhalb des Bereichs eines Clusters.

**Wahrnehmgrad** Wahrnehmvedschwere Grad = {4, 5, 6} = {"Information", "Warning" und "Error"}, oder äquivalente Farben wie blau, gelb und rot.

**Faultingobjectdescription** Teile Informationen für Hardware, in der Regel leer für Software Objekte.

**Faultingobjectlocation** Standortinformationen für Hardware, normalerweise leer für Software Objekte.

**Empfehlungs Aktionen** Liste der empfohlenen Aktionen, die unabhängig sind und in keiner bestimmten Reihenfolge sind. Heutzutage ist diese Liste häufig von der Länge 1.

## <a name="properties-of-fault-events"></a>Eigenschaften von Fehlerereignissen

Diese Tabelle enthält mehrere Schlüsseleigenschaften des Fault-Ereignisses. Überprüfen Sie für das vollständige Schema die Klasse **MSFT \_ storagefaultevent** in *storagewmi. MOF*.

Beachten Sie den **ChangeType**, der angibt, ob ein Fehler erstellt, entfernt oder aktualisiert wird, und die **faultid**. Ein Ereignis enthält auch alle Eigenschaften des betroffenen Fehlers.

| **Eigenschaft**              | **Beispiel**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| Faultid                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft. Health. faultType. Volume. Capacity                      |
| `Reason`                    | "Auf dem Volume steht kein verfügbarer Speicherplatz mehr zur Verfügung."                 |
| Wahrnehmgrad         | 5                                                               |
| Faultingobjectdescription | XYZ9000 S.N. 123456789                                  |
| Faultingobjectlocation    | Rack A06, ru 25, Slot 11                                        |
| Empfehlungs Aktionen        | {"Erweitern Sie das Volume", "migrieren Sie Workloads zu anderen Volumes".   |

**ChangeType** ChangeType = {0, 1, 2} = {"Create", "Remove", "Update"}.

## <a name="coverage"></a>Abdeckung

In Windows Server 2016 stellt die Integritätsdienst die folgende Fehlerabdeckung bereit:

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. failedmedia
* Schweregrad: Warnung
* Grund: *"Fehler bei der physischen Festplatte."*
* Empfehlungs Aktion: *"Ersetzen des physischen Datenträgers".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. lostcommunication
* Schweregrad: Warnung
* Ursache: *"die Verbindung mit dem physischen Datenträger ist verloren gegangen".*
* Empfehlungs Aktion: *"Überprüfen Sie, ob die physische Festplatte funktioniert und ordnungsgemäß verbunden ist."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. nicht reagierend.
* Schweregrad: Warnung
* Grund: *"der physische Datenträger stellt wiederkehrende nicht Reaktionsfähigkeit dar."*
* Empfehlungs Aktion: *"Ersetzen des physischen Datenträgers".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. predictivefailure
* Schweregrad: Warnung
* Ursache: *"ein Ausfall des physischen Datenträgers ist in Kürze geplant."*
* Empfehlungs Aktion: *"Ersetzen des physischen Datenträgers".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. unsupportedhardware
* Schweregrad: Warnung
* Ursache: *"der physische Datenträger wird unter Quarantäne gestellt, weil er von Ihrem Lösungsanbieter nicht unterstützt wird."*
* Empfehlungs Aktion: *"ersetzen Sie den physischen Datenträger durch unterstützte Hardware".*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. unsupportedfirmware
* Schweregrad: Warnung
* Ursache: *"der physische Datenträger wird in Quarantäne gestellt, da seine Firmwareversion von Ihrem Lösungsanbieter nicht unterstützt wird."*
* Empfehlungs Aktion: *"Aktualisieren Sie die Firmware auf dem physischen Datenträger auf die Zielversion."*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. unerkenzedmetadata
* Schweregrad: Warnung
* Grund: *"der physische Datenträger hat nicht erkannte Meta-Daten."*
* Empfehlungs Aktion: *"dieser Datenträger kann Daten aus einem unbekannten Speicherpool enthalten. Stellen Sie zunächst sicher, dass auf diesem Datenträger keine nützlichen Daten vorhanden sind, und setzen Sie dann den Datenträger zurück.*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft. Health. faultType. PhysicalDisk. failedfirmwareupdate
* Schweregrad: Warnung
* Ursache: *"Fehler bei der Aktualisierung der Firmware auf dem physischen Datenträger."*
* Empfehlungs Aktion: *"versuchen Sie, eine andere Firmware-Binärdatei zu verwenden."*

### <a name="virtual-disk-2"></a>**Virtueller Datenträger (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft. Health. faultType. virtualdisks. needsrepair
* Schweregrad: Information
* Ursache: *"einige Daten auf diesem Volume sind nicht vollständig stabil. Der Zugriff ist weiterhin möglich. "*
* Empfehlungs Maßnahme: *"Wiederherstellen der Resilienz der Daten."*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft. Health. faultType. virtualdisks. getrennte
* Schweregrad: Kritisch
* Grund: *"der Zugriff auf das Volume ist nicht möglich. Einige Daten können verloren gehen. "*
* Empfehlungs Aktion: *"Überprüfen Sie die physische und/oder Netzwerk Konnektivität aller Speichergeräte. Möglicherweise müssen Sie eine Wiederherstellung aus einer Sicherung durch erstellen. "*

### <a name="pool-capacity-1"></a>**Pool Kapazität (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft. Health. faultType. storagepool. insuffizientreservecapacityfault
* Schweregrad: Warnung
* Ursache: *"der Speicherpool verfügt nicht über die empfohlene Mindestreserve Kapazität. Dies kann die Fähigkeit zum Wiederherstellen von datenresilienz im Fall von Laufwerk Fehlern einschränken. "*
* Empfehlungs Aktion: *"zusätzliche Kapazität zum Speicherpool hinzufügen oder Kapazität freigeben. Die empfohlene Mindestreserve ist abhängig von der Bereitstellung, aber es sind ungefähr 2 Laufwerke ausgelastet. "*

### <a name="volume-capacity-2sup1sup"></a>**Volumekapazität (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft. Health. faultType. Volume. Capacity
* Schweregrad: Warnung
* Ursache: *"der verfügbare Speicherplatz auf dem Volume steht nicht mehr zur Verfügung."*
* Empfehlungs Aktion: *"erweitern Sie das Volume, oder migrieren Sie Arbeits Auslastungen zu anderen Volumes".*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft. Health. faultType. Volume. Capacity
* Schweregrad: Kritisch
* Ursache: *"der verfügbare Speicherplatz auf dem Volume steht nicht mehr zur Verfügung."*
* Empfehlungs Aktion: *"erweitern Sie das Volume, oder migrieren Sie Arbeits Auslastungen zu anderen Volumes".*

### <a name="server-3"></a>**Server (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft. Health. faultType. Server. Down
* Schweregrad: Kritisch
* Ursache: *"der Server kann nicht erreicht werden."*
* Empfehlungs Aktion: *"Server starten oder ersetzen"*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft. Health. faultType. Server. isoliert
* Schweregrad: Kritisch
* Ursache: *"der Server ist aufgrund von Konnektivitätsproblemen vom Cluster isoliert".*
* Empfehlungs Aktion: *"Wenn die Isolation weiterhin besteht, überprüfen Sie die Netzwerk (e), oder migrieren Sie Arbeits Auslastungen zu anderen Knoten".*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft. Health. faultType. Server. Quarantäne
* Schweregrad: Kritisch
* Ursache: *"der Server wird aufgrund von wiederkehrenden Fehlern durch den Cluster unter Quarantäne gestellt."*
* Empfehlungs Aktion: *"Server ersetzen oder Netzwerk reparieren".*

### <a name="cluster-1"></a>**Cluster (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft. Health. faultType. clusterquorüberwitness. Error
* Schweregrad: Kritisch
* Ursache: *"der Cluster ist ein Server Fehler, der nicht mehr ausfällt."*
* Empfehlungs Aktion: *"Überprüfen Sie die Zeugen Ressource, und starten Sie Sie bei Bedarf neu. Starten oder ersetzen fehlerhafter Server. "*

### <a name="network-adapterinterface-4"></a>**Netzwerk Adapter/-Schnittstelle (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft. Health. faultType. NetworkAdapter. getrennte
* Schweregrad: Warnung
* Ursache: *"die Netzwerkschnittstelle wurde getrennt."*
* Empfehlungs Aktion: *"Verbindung mit dem Netzwerkkabel wiederherstellen".*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft. Health. faultType. NetworkInterface. Missing
* Schweregrad: Warnung
* Grund: *"der Server" {Server} "verfügt über fehlende Netzwerkadapter (e), die mit dem Cluster Netzwerk" {Cluster Network} "verbunden sind.*
* Empfehlungs Aktion: *"Verbinden Sie den Server mit dem fehlenden Cluster Netzwerk".*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft. Health. faultType. NetworkAdapter. Hardware
* Schweregrad: Warnung
* Ursache: *"bei der Netzwerkschnittstelle ist ein Hardwarefehler aufgetreten."*
* Empfehlungs Aktion: *"ersetzt den Netzwerkschnittstellen Adapter".*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft. Health. faultType. NetworkAdapter. deaktiviert
* Schweregrad: Warnung
* Ursache: *"die Netzwerkschnittstelle" {Network Interface} "ist nicht aktiviert und wird nicht verwendet."*
* Empfehlungs Aktion: *"Netzwerkschnittstelle aktivieren".*

### <a name="enclosure-6"></a>**Gehäuse (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft. Health. faultType. storageenclosure. lostcommunication
* Schweregrad: Warnung
* Ursache: *"die Kommunikation mit dem Speicher Gehäuse ist verloren gegangen."*
* Empfehlungs Aktion: *"das Speicher Gehäuse wird gestartet oder ersetzt."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft. Health. faultType. storageenclosure. fanerror
* Schweregrad: Warnung
* Grund: *"der Lüfter an Position {Position} des Speicher Gehäuses ist fehlgeschlagen."*
* Empfehlungs Aktion: *"ersetzen Sie den Lüfter im Speicher Gehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft. Health. faultType. storageenclosure. currentsensorerror
* Schweregrad: Warnung
* Grund: *"Fehler beim aktuellen Sensor an Position {Position} des Speicher Gehäuses."*
* Empfehlungs Aktion: *"Ersetzen eines aktuellen Sensors im Speicher Gehäuse".*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft. Health. faultType. storageenclosure. voltagesensorerror
* Schweregrad: Warnung
* Grund: *"der Spannungssensor an Position {Position} des Speicher Gehäuses ist fehlgeschlagen."*
* Empfehlungs Aktion: *"Ersetzen eines Spannungs Sensors im Speicher Gehäuse".*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft. Health. faultType. storageenclosure. iocontrollererror
* Schweregrad: Warnung
* Ursache: "Fehler beim e/a- *Controller an Position {Position} des Speicher Gehäuses."*
* Empfehlungs Aktion: *"ersetzt einen IO-Controller im Speicher Gehäuse."*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft. Health. faultType. storageenclosure. temperaturesensorerror
* Schweregrad: Warnung
* Grund: *"Fehler beim Temperatursensor an Position {Position} des Speicher Gehäuses."*
* Empfehlungs Aktion: *"Ersetzen eines Temperatursensors im Speicher Gehäuse".*

### <a name="firmware-rollout-3"></a>**Firmware-Rollout (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft. Health. faultType. fauldomain. failedmaintenancemode
* Schweregrad: Warnung
* Ursache: *"der Fortschritt während der firmwarerollout kann zurzeit nicht fortgesetzt werden."*
* Empfehlungs Aktion: *"Überprüfen Sie, ob alle Speicherplätze fehlerfrei sind und derzeit keine Fehler Domäne im Wartungsmodus ist".*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft. Health. faultType. fauldomain. firmwareverifyversionfaile
* Schweregrad: Warnung
* Grund: *"der firmwarerollout wurde aufgrund von unlesbaren oder unerwarteten Firmwareversion-Informationen nach dem Anwenden eines* Firmwareupdates abgebrochen"
* Empfehlungs Aktion: *"firmwarerollout neu starten, sobald das firmwareproblem behoben wurde".*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft. Health. faultType. fauldomain. deomanyfailedupdates
* Schweregrad: Warnung
* Grund: *"der firmwarerollout wurde abgebrochen, weil zu viele physische* Datenträger fehlgeschlagen sind."
* Empfehlungs Aktion: *"firmwarerollout neu starten, sobald das firmwareproblem behoben wurde".*

### <a name="storage-qos-3sup2sup"></a>**Speicher-QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft. Health. faultType. storqos. insuffizientdurchsatz
* Schweregrad: Warnung
* Ursache: *"der Speicher Durchsatz reicht nicht aus, um Reserven zu erfüllen".*
* Empfehlungs Aktion: *"Speicher-QoS-Richtlinien neu konfigurieren".*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft. Health. faultType. storqos. lostcommunication
* Schweregrad: Warnung
* Ursache: *"der Speicher-QoS-Richtlinien-Manager hat die Kommunikation mit dem Volume verloren."*
* Empfehlungs Aktion: *"Neustart der Knoten {Nodes}"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft. Health. faultType. storqos. miskonfiguriredflow
* Schweregrad: Warnung
* Ursache: *"mindestens ein speicherconsumer (in der Regel Virtual Machines) verwendet eine nicht vorhandene Richtlinie mit der ID {ID}".*
* Empfehlungs Aktion: *"alle fehlenden Speicher-QoS-Richtlinien neu erstellen".*

<sup>1</sup> gibt an, dass das Volume 80% vollständig (neben Schweregrad) oder 90% voll (Schweregrad) erreicht hat.
<sup>2</sup> gibt an, dass einige VHDs auf dem Volume nicht ihren minimalen IOPS-Aufwand für über 10% (neben Version), 30% (Hauptversion) oder 50% (kritisch) des parallelen 24-Stunden-Fensters erreicht haben.

>[!NOTE]
> Die Integrität von Speichergehäusekomponenten wie Lüfter, Netzteile und Sensoren wird von SES (SCSI Enclosure Services) abgeleitet. Wenn Ihr Anbieter diese Informationen nicht bereitstellt, kann der Integritätsdienst sie nicht anzeigen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Der Integritätsdienst in Windows Server 2016](health-service-overview.md)
