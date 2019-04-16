---
title: "Integritätsdienst-Berichte"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: bc21b9fdec5700fec23dc6af7ca15873ded34bea
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-reports"></a>Integritätsdienst-Berichte
> Gilt für WindowsServer 2016

## <a name="what-are-reports"></a>Was sind Berichte?  

Der Integritätsdienst verringert den Arbeitsaufwand zum Abrufen von Leistungs- und Kapazitätsinformationen aus Ihrem "direkte Speicherplätze"-Cluster. Ein neues Cmdlet bietet eine geordnete Liste wichtiger Metriken, die effizient gesammelt und knotenübergreifend dynamisch, mithilfe integrierter Logik zum Erkennen der Clustermitgliedschaft. Alle Werte sind nur in Echtzeit und Point-in-Time.  

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie dieses Cmdlet zum Abrufen von Metriken für den gesamten "direkte Speicherplätze"-Cluster:

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

Das optionale **Anzahl** Parameter gibt an, wie viele Gruppen mit Werten in einer zweiten Intervallen zurückgegeben.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

Sie können auch Metriken für ein bestimmtes Volume oder Server abrufen:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

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

Rufen Sie **GetReport** um Beispiele für eine Experten verwaltet Liste wichtiger Metriken, die effizient gesammelt und knotenübergreifend dynamisch, mithilfe integrierter Logik zum Erkennen der Clustermitgliedschaft streamen zu beginnen. Beispiele werden jede Sekunde danach ankommen. Alle Werte sind nur in Echtzeit und Point-in-Time.

Metriken für drei Bereiche gestreamt werden können: das Cluster, einen beliebigen Knoten oder ein Volume.

Die vollständige Liste der verfügbaren Metriken auf jeder Ebene in Windows Server2016 dokumentiert ist.

### <a name="iobserveronnext"></a>IObserver.OnNext()

Dieser Beispielcode verwendet die [Beobachterentwurfsmuster](https://msdn.microsoft.com/en-us/library/ee850490(v=vs.110).aspx) einen Beobachter implementieren, deren **OnNext()** Methode wird aufgerufen, wenn jedes neue Beispiel Metriken eingehen. Die **OnCompleted()** -Methode wird aufgerufen, wenn beim Streamen von endet. Z.B. können Sie es verwenden, um dieses Streaming, damit es auf unbestimmte Zeit fortgesetzt wird.

```
class MetricsObserver<T> : IObserver<T>
{
    public void OnNext(T Result)
    {
        // Cast
        CimMethodStreamedResult StreamedResult = Result as CimMethodStreamedResult;

        if (StreamedResult != null)
        {
            // For illustration, you could store the metrics in this dictionary
            Dictionary<string, string> Metrics = new Dictionary<string, string>();

            // Unpack
            CimInstance Report = (CimInstance)StreamedResult.ItemValue;
            IEnumerable<CimInstance> Records = (IEnumerable<CimInstance>)Report.CimInstanceProperties["Records"].Value;
            foreach (CimInstance Record in Records)
            {
                /// Each Record has "Name", "Value", and "Units"
                Metrics.Add(
                    Record.CimInstanceProperties["Name"].Value.ToString(),
                    Record.CimInstanceProperties["Value"].Value.ToString()
                    );
            }

            // TODO: Whatever you want!
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Reinvoke BeginStreamingMetrics(), defined in the next section
    }
}
```

### <a name="begin-streaming"></a>Streaming beginnen

Mit der Beobachter definiert können Sie das Streaming beginnen.

Geben Sie das Ziel **CimInstance** die Metriken beschränkt werden sollen. Der Cluster, einen beliebigen Knoten oder ein Volume möglich.

Count-Parameter ist die Anzahl der Proben Streaming endet.

```
CimInstance Target = Cluster; // From among the objects discovered in DiscoverObjects()

public void BeginStreamingMetrics(CimSession Session, CimInstance HealthService, CimInstance Target)
{
    // Set Parameters
    CimMethodParametersCollection MetricsParams = new CimMethodParametersCollection();
    MetricsParams.Add(CimMethodParameter.Create("TargetObject", Target, CimType.Instance, CimFlags.In));
    MetricsParams.Add(CimMethodParameter.Create("Count", 999, CimType.UInt32, CimFlags.In));
    // Enable WMI Streaming
    CimOperationOptions Options = new CimOperationOptions();
    Options.EnableMethodResultStreaming = true;
    // Invoke API
    CimAsyncMultipleResults<CimMethodResultBase> InvokeHandler;
    InvokeHandler = Session.InvokeMethodAsync(
        HealthService.CimSystemProperties.Namespace, HealthService, "GetReport", MetricsParams, Options
        );
    // Subscribe the Observer
    MetricsObserver<CimMethodResultBase> Observer = new MetricsObserver<CimMethodResultBase>(this);
    IDisposable Disposeable = InvokeHandler.Subscribe(Observer);
}
```

Diese Metriken können selbstverständlich in einer Datenbank gespeichert oder verwendet in der gewünschten Weise eigenem dargestellt werden.

### <a name="properties-of-reports"></a>Eigenschaften von Berichten

Jedes Sample Metriken ist eine "Bericht" enthält viele "Datensätzen", die einzelnen Metriken entsprechen.

Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageHealthReport** und **MSFT\_HealthRecord** Klassen im *storagewmi.mof*.

Jede Metrik hat nur drei Eigenschaften, gemäß der folgenden Tabelle.

| **Eigenschaft** | **Beispiel**       |
| -------------|-------------------|
| Name         | IOLatencyAverage  |
| Wert        | 0.00021           |
| Einheiten        | 3                 |

Einheiten = {0, 1, 2, 3, 4}, wobei 0 = "Bytes", 1 = "BytesPerSecond", 2 = "CountPerSecond", 3 = "Seconds", oder 4 = "Prozentsatz".

## <a name="coverage"></a>Abdeckung

Im Folgenden sind die Metriken für die einzelnen Bereiche in Windows Server2016 verfügbar.

### <a name="msftstoragesubsystem"></a>MSFT_StorageSubSystem

| **Name**                        | **Einheiten** |
|---------------------------------|-----------|
| CPUUsage                        | 4         |
| CapacityPhysicalPooledAvailable | 0         |
| CapacityPhysicalPooledTotal     | 0         |
| CapacityPhysicalTotal           | 0         |
| CapacityPhysicalUnpooled        | 0         |
| CapacityVolumesAvailable        | 0         |
| CapacityVolumesTotal            | 0         |
| IOLatencyAverage                | 3         |
| IOLatencyRead                   | 3         |
| IOLatencyWrite                  | 3         |
| IOPSRead                        | 2         |
| IOPSTotal                       | 2         |
| IOPSWrite                       | 2         |
| IOThroughputRead                | 1         |
| IOThroughputTotal               | 1         |
| IOThroughputWrite               | 1         |
| MemoryAvailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msftstoragenode"></a>MSFT_StorageNode

| **Name**            | **Einheiten** |
|---------------------|-----------|
| CPUUsage            | 4         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |
| MemoryAvailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msftvolume"></a>MSFT_Volume

| **Name**            | **Einheiten** |
|---------------------|-----------|
| CapacityAvailable   | 0         |
| CapacityTotal       | 0         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
