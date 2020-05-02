---
title: Integritätsdienst Berichte
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 0a03dc5d646d24c9f24f979df36fb3fe1eafe631
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720553"
---
# <a name="health-service-reports"></a>Integritätsdienst Berichte

> Gilt für: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>Was sind Berichte?  

Der-Integritätsdienst reduziert den Aufwand, der erforderlich ist, um Informationen über die Leistung und die Kapazität Ihres direkte Speicherplätze Clusters zu erhalten. Ein neues Cmdlet bietet eine Liste mit wichtigen Metriken, die effizient gesammelt und dynamisch über Knoten aggregiert werden, mit integrierter Logik zum Erkennen der Cluster Mitgliedschaft. Alle Werte sind in Echtzeit und ausschließlich zeitpunktbezogen.  

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie dieses Cmdlet, um Metriken für den gesamten direkte Speicherplätze Cluster zu erhalten:

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

Der optionale **count** -Parameter gibt an, wie viele Sätze von Werten in Intervallen von einer Sekunde zurückgegeben werden.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

Sie können auch Metriken für ein bestimmtes Volume oder einen bestimmten Server erhalten:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>Verwendung in .net und C #

### <a name="connect"></a>Verbinden

Um den Integritätsdienst abzufragen, müssen Sie eine **cimsession** mit dem Cluster einrichten. Zu diesem Zweck benötigen Sie einige Dinge, die nur in der Vollversion von .net verfügbar sind, was bedeutet, dass Sie dies nicht direkt über ein Web oder Mobile App durchführen können. Diese Codebeispiele verwenden C\#, die einfachste Wahl für diese Datenzugriffs Schicht.

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

Bevor Sie Fehler oder Metriken erhalten können, müssen Sie Instanzen von mehreren relevanten Objekten erhalten. Zuerst das **MSFT\_storagesubsystem** , das direkte Speicherplätze im Cluster darstellt. Mit diesem können Sie jede **\_MSFT storagenode** -Instanz im Cluster und alle **MSFT\_**-Volumes, die Datenvolumes, erhalten. Schließlich benötigen Sie auch **MSFT\_storagehealth**, den Integritätsdienst selbst.

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

Rufen Sie **GetReport** auf, um mit dem Streamen von Beispielen für eine vom Experten zusammengestellte Liste mit wichtigen Metriken zu beginnen, die effizient gesammelt und dynamisch über Knoten aggregiert werden, mit integrierter Logik zum Erkennen der Cluster Mitgliedschaft. Die Beispiele werden anschließend jede Sekunde empfangen. Alle Werte sind in Echtzeit und ausschließlich zeitpunktbezogen.

Metriken können für drei Bereiche gestreamt werden: Cluster, Knoten oder beliebiges Volume.

Die komplette Liste der Metriken, die in jedem Bereich in Windows Server 2016 verfügbar sind, ist unten dokumentiert.

### <a name="iobserveronnext"></a>IObserver. OnNext ()

In diesem Beispielcode wird das [Observer-Entwurfsmuster](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx) zum Implementieren eines Beobachters verwendet, dessen **OnNext ()** -Methode aufgerufen wird, wenn jedes neue metrikbeispiel erreicht wird. Die zugehörige **onabgeschlossene ()** -Methode wird beim Beenden des Streamings aufgerufen. Beispielsweise können Sie es verwenden, um das Streaming erneut zu initiieren, sodass es unbegrenzt fortgesetzt wird.

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

### <a name="begin-streaming"></a>Streaming starten

Wenn der Observer definiert ist, können Sie mit dem Streaming beginnen.

Geben Sie die Ziel- **ciminstance** an, für die Sie die Metriken festlegen möchten. Dabei kann es sich um den Cluster, einen beliebigen Knoten oder ein beliebiges Volume handeln.

Der count-Parameter entspricht der Anzahl von Samplings, bevor das Streaming beendet wird.

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

Natürlich können diese Metriken visualisiert, in einer Datenbank gespeichert oder in der gewünschten Weise verwendet werden.

### <a name="properties-of-reports"></a>Eigenschaften von Berichten

Jede Stichprobe von Metriken ist ein "Bericht", der viele "Datensätze" enthält, die einzelnen Metriken entsprechen.

Überprüfen Sie für das vollständige Schema die Klassen **\_MSFT storagehealthreport** und **MSFT\_healthrecord** in *storagewmi. MOF*.

Jede Metrik hat pro dieser Tabelle nur drei Eigenschaften.

| **Eigenschaft** | **Beispiel**       |
| -------------|-------------------|
| Name         | Iolatencyaverage  |
| Wert        | 0,00021           |
| Units        | 3                 |

Einheiten = {0, 1, 2, 3, 4}, wobei 0 = "Bytes", 1 = "bytespersecond", 2 = "count-persecond", 3 = "seconds" oder 4 = "Prozentsatz".

## <a name="coverage"></a>Abdeckung

Im folgenden finden Sie die verfügbaren Metriken für jeden Bereich in Windows Server 2016.

### <a name="msft_storagesubsystem"></a>MSFT_StorageSubSystem

| **Name**                        | **Units** |
|---------------------------------|-----------|
| CPUUsage                        | 4         |
| Capacityphysicalpooledavailable | 0         |
| Capacityphysicalpooledtotal     | 0         |
| Capacityphysicaltotal           | 0         |
| Capacityphysicalunpooled        | 0         |
| Capacityvolumesavailable        | 0         |
| Capacityvolumestotal            | 0         |
| Iolatencyaverage                | 3         |
| Iolatencyread                   | 3         |
| Iolatencywrite                  | 3         |
| Iopsread                        | 2         |
| Iopstotal                       | 2         |
| Iopswrite                       | 2         |
| Iodurchputread                | 1         |
| Iodurchlauf puttotal               | 1         |
| Iothrough putwrite               | 1         |
| Memoryavailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msft_storagenode"></a>MSFT_StorageNode

| **Name**            | **Units** |
|---------------------|-----------|
| CPUUsage            | 4         |
| Iolatencyaverage    | 3         |
| Iolatencyread       | 3         |
| Iolatencywrite      | 3         |
| Iopsread            | 2         |
| Iopstotal           | 2         |
| Iopswrite           | 2         |
| Iodurchputread    | 1         |
| Iodurchlauf puttotal   | 1         |
| Iothrough putwrite   | 1         |
| Memoryavailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msft_volume"></a>MSFT_Volume

| **Name**            | **Units** |
|---------------------|-----------|
| Verfügbare Kapazität   | 0         |
| Capacitytotal       | 0         |
| Iolatencyaverage    | 3         |
| Iolatencyread       | 3         |
| Iolatencywrite      | 3         |
| Iopsread            | 2         |
| Iopstotal           | 2         |
| Iopswrite           | 2         |
| Iodurchputread    | 1         |
| Iodurchlauf puttotal   | 1         |
| Iothrough putwrite   | 1         |

## <a name="see-also"></a>Weitere Informationen

- [Der Integritätsdienst in Windows Server 2016](health-service-overview.md)
