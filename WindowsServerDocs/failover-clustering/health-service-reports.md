---
title: Integritätsdienst-Berichte
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: e018c0270a0bf410dada9c05d2c25e51fdfac1d8
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280153"
---
# <a name="health-service-reports"></a>Integritätsdienst-Berichte
> Gilt für: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>Was sind Berichte  

Der Integritätsdienst verringert den Arbeitsaufwand beim aktueller Leistungs- und Kapazitätsinformationen aus Ihrem "direkte Speicherplätze"-Cluster zu erhalten. Ein neues Cmdlet bietet es sich um eine geordnete Liste wichtiger Metriken, die effizient gesammelt und aggregiert dynamisch für einen Knoten, die mithilfe integrierter Logik zum Erkennen der Clustermitgliedschaft. Alle Werte sind in Echtzeit und ausschließlich zeitpunktbezogen.  

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie dieses Cmdlet aus, um Metriken für den gesamten "direkte Speicherplätze"-Cluster zu erhalten:

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

Der optionale **Anzahl** Parameter gibt an, wie viele Gruppen mit Werten in einem-Sekunden-Intervallen zurückgegeben.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

Sie können auch Metriken für ein bestimmtes Volume oder Server abrufen:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

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

Rufen Sie **GetReport** um Beispiele für eine Experten kuratierten Liste wichtiger Metriken, die effizient gesammelt und aggregiert dynamisch für einen Knoten, die mithilfe integrierter Logik zum Erkennen der Clustermitgliedschaft streaming zu starten. Beispiele werden danach pro Sekunde eingehen. Alle Werte sind in Echtzeit und ausschließlich zeitpunktbezogen.

Metriken können gestreamt werden, für die drei Bereiche: den Cluster, einen beliebigen Knoten oder ein Volume.

Die vollständige Liste der Metriken, die in jeder Bereich in Windows Server 2016 verfügbar sind, wird im folgenden dokumentiert.

### <a name="iobserveronnext"></a>IObserver.OnNext()

Dieser Beispielcode verwendet die [Entwurfsmuster "Beobachter"](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx) zum Implementieren eines observers, deren **OnNext()** Methode wird aufgerufen werden, wenn jedes neues Beispiel von Metriken empfangen. Die **OnCompleted()** Methode wird aufgerufen, wenn/wenn streaming endet. Beispielsweise könnte es können Sie erneut initiieren, streaming, damit es auf unbestimmte Zeit fortgesetzt.

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

### <a name="begin-streaming"></a>Streaming von

Mit den Beobachter, der definiert wird können Sie das streaming beginnen.

Geben Sie das Ziel **CimInstance** , für die Metriken beschränkt werden soll. Sie können den Cluster, einen beliebigen Knoten oder ein Volume sein.

Der Count-Parameter ist die Anzahl der abtastungen vor dem streaming endet.

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

Diese Metriken können natürlich in einer Datenbank gespeichert oder ganz nach Bedarf verwendeten visualisiert werden.

### <a name="properties-of-reports"></a>Eigenschaften von Berichten

Jedes Beispiels Metriken ist eine "Bericht" viele "Datensätze" für einzelne Metriken enthält.

Überprüfen Sie für das vollständige Schema, das **MSFT\_StorageHealthReport** und **MSFT\_HealthRecord** Klassen im *storagewmi.mof*.

Jede Metrik verfügt über nur drei Eigenschaften, die gemäß der folgenden Tabelle.

| **Eigenschaft** | **Beispiel**       |
| -------------|-------------------|
| Name         | IOLatencyAverage  |
| Wert        | 0.00021           |
| Einheiten        | 3                 |

Einheiten = {0, 1, 2, 3, 4}, wobei 0 = "Bytes", 1 = "BytesPerSecond", 2 = "CountPerSecond", 3 = "Seconds", oder 4 = "Prozent".

## <a name="coverage"></a>Abdeckung

Im folgenden sind die Metriken für jeden Bereich in Windows Server 2016 verfügbar.

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
