---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: "Fehlerdomänenunterstützung"
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: f5c64bb8f8b7d4b8d13c76c4e94cfcf52ee32c30
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="fault-domain-awareness-in-windows-server-2016"></a>Fehlerdomänenunterstützung in Windows Server2016

> Gilt für: Windows Server 2016

Failover-Clusterunterstützung können mehrere Server zusammenarbeiten, um hohe Verfügbarkeit – oder anders ausgedrückt, um knotenfehlertoleranz zu bieten. Aber moderne Unternehmen verlangen immer höhere Verfügbarkeit ihrer Infrastruktur. Um Betriebszeit zu erreichen, müssen auch sehr unwahrscheinlichen Vorfällen wie z.B. Gehäuse-, rackausfällen oder Naturkatastrophen vor geschützt werden. Daher Failoverclustering in Windows Server2016 Gehäuse-, Rack- und Standort eine Fehlertoleranz wird auch eingeführt.

Fehlerdomänen und Fehlertoleranz sind eng miteinander verwandte Konzepte. Eine Fehlerdomäne ist eine Reihe von Hardwarekomponenten, die einen einzelnen Fehlerpunkt gemeinsam nutzen. Um auf eine gewisse Fehlertoleranz, benötigen Sie mehrere Fehlerdomänen auf dieser Ebene. Beispielsweise müssen rackfehlertoleranz fehlertolerant, Ihre Server und die Daten auf mehrere Racks verteilt werden.

Dieses kurze Video bietet einen Überblick über Fehlerdomänen in Windows Server2016:  
[![Klicken Sie auf diesem Bild um einen Überblick über Fehlerdomänen in Windows Server2016 anzusehen.](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

## <a name="benefits"></a>Vorteile
- **Von Speicherplätzen, einschließlich direkte Speicherplätze verwendet Fehlerdomänen, um die Datensicherheit zu maximieren.**  
    Die Resilienz in Storage Spaces ist konzeptionell wie verteiltes, softwaredefiniertes RAID. Mehrere Kopien aller Daten werden synchron gehalten, und wenn bei und eine Kopie verloren geht, andere sind zum Wiederherstellen der Resilienz erneut. Um die bestmögliche Resilienz zu erreichen, sollten Kopien in separaten Fehlerdomänen beibehalten werden.

- **Die [Integritätsdienst](health-service-overview.md) verwendet einen Fehler Domänen um nützlichere Warnungen auszugeben.**  
    Jeder Fehlerdomäne kann speicherortmetadaten zugeordnet werden, die automatisch in alle nachfolgenden Warnungen aufgenommen werden. Diese Deskriptoren können Vorgänge oder Wartungspersonal unterstützen und Fehler reduzieren, indem Wartungspersonal Hardware.  

- **Stretch-Clustering verwendet Fehlerdomänen für Speicher Affinität.** Stretch-Clustering ermöglicht weit entfernten Servern, einem gemeinsamen Cluster beitreten. Für optimale Leistung sollten Anwendungen oder virtuelle Computer auf Servern ausgeführt werden, die in der Nähe, die ihnen Speicherplatz bereitstellen. Fehlerdomänenunterstützung ermöglicht diese Affinität Speicher.   

## <a name="levels-of-fault-domains"></a>Ebenen der Fehlerdomänen  
Es gibt vier kanonische Ebenen von Fehlerdomänen – Standort, Rack, Gehäuse und Knoten. Knoten werden automatisch erkannt; Jede zusätzliche Ebene ist optional. Wenn beispielsweise die Bereitstellung keine Blade Server verwendet werden, kann die Gehäuseebene nicht für Sie sinnvoll.  

![Diagramm mit den verschiedenen Ebenen der Fehlerdomänen](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>Verwendung  
PowerShell oder XML-Markup können Fehlerdomänen. Beide Ansätze sind äquivalent und bieten vollständige Funktionalität.

>[!IMPORTANT]
> Geben Sie Fehlerdomänen, vor dem Aktivieren von "direkte Speicherplätze", wenn möglich. Dies ermöglicht die automatische Konfiguration, um den Pool, Ebenen und Einstellungen wie Resilienz und Anzahl der Spalten für Gehäuse- oder rackfehlertoleranz vorzubereiten. Wenn Pool und Volumes erstellt haben, werden Daten nicht nachträglich in Reaktion auf Änderungen in der fehlerdomänentopologie verschoben. Um nach dem Aktivieren von "direkte Speicherplätze" Knoten zwischen Gehäusen oder Racks zu verschieben sollten Sie zunächst den Knoten sowie seine Laufwerke aus dem Pool entfernen `Remove-ClusterNode -CleanUpDisks`.

### <a name="defining-fault-domains-with-powershell"></a>Definieren von Fehlerdomänen mit PowerShell
Windows Server2016 führt die folgenden Cmdlets Fehlerdomänen bearbeitet werden können:
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

Dieses kurze Video veranschaulicht die Verwendung dieser Cmdlets.
[![Klicken Sie auf diesem Bild um ein kurzes Video zur Verwendung der Cmdlets Cluster Fehlerdomäne anzusehen.](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

Verwendung `Get-ClusterFaultDomain`auf der aktuellen fehlerdomänentopologie. Dadurch werden alle Knoten im Cluster sowie alle Gehäuse, Racks oder Standorte, die Sie erstellt haben, aufgelistet. Sie können mit Parametern wie filtern **-Typ** oder **-Namen**, aber diese sind nicht erforderlich.

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

Verwendung `New-ClusterFaultDomain`um neue Gehäuse, Racks oder Standorte zu erstellen. Die `-Type`und `-Name`Parameter sind erforderlich. Die möglichen Werte für `-Type`sind `Chassis`, `Rack`, und `Site`. Die `-Name`kann eine beliebige Zeichenfolge sein. (Für `Node`Fehlerdomänen des Typs, der Name der tatsächliche Knotenname automatisch festgelegt werden müssen).

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server nicht möglich, und nicht überprüfen, ob alle Fehlerdomänen, die Sie erstellen in der realen, physischen Welt entsprechen. (Das klingt offensichtlich, aber es ist wichtig zu verstehen.) Wenn Sie in der physischen Welt Ihre Knoten in einem einzigen Rack befinden, klicken Sie dann das Erstellen von zwei `-Type Rack`Fehlerdomänen in der Software nicht auf magische Rack-Fehlertoleranz. Sie sind dafür verantwortlich sicherzustellen, dass die Topologie, die Sie mithilfe dieser Cmdlets erstellen die tatsächliche Anordnung der Hardware entspricht.

Verwendung `Set-ClusterFaultDomain`eine Fehlerdomäne in eine andere verschieben. Die Begriffe "Übergeordnet" und "untergeordnet" werden häufig zur Beschreibung dieser geschachtelten Beziehung verwendet. Die `-Name`und `-Parent`Parameter sind erforderlich. In `-Name`, geben Sie den Namen der Fehlerdomäne an, die verschoben wird; in `-Parent`, geben Sie den Namen des Ziels. Um mehrere Fehlerdomänen gleichzeitig zu verschieben, Listen Sie ihre Namen.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> Wenn Fehlerdomänen verschieben möchten, verschieben ihre Kinder mit ihnen. Im obigen Beispiel, wenn Rack A das übergeordnete Element des server01.contoso.com ist, die zweite Option separat muss nicht an den Standort Shanghai verschoben werden – es ist schon durch das übergeordnete Element dort, wie in der realen Welt.

Sehen Sie über- und untergeordnete Elemente in der Ausgabe des `Get-ClusterFaultDomain`in die `ParentName`und `ChildrenNames`Spalten.

Sie können auch `Set-ClusterFaultDomain`bestimmte andere Eigenschaften von Fehlerdomänen ändern. Beispielsweise können Sie optional bereitstellen `-Location`oder `-Description`Metadaten für jede Fehlerdomäne. Wenn angegeben, werden diese Informationen in hardwarewarnungen des Integritätsdiensts enthalten sein. Sie können auch mithilfe von Fehlerdomänen Umbenennen der `-NewName`Parameter. Nicht umbenennen `Node`Fehlerdomänen des Typs.

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

Verwendung `Remove-ClusterFaultDomain`entfernen Gehäuse, Racks oder Standorte, die Sie erstellt haben. Die `-Name` -Parameter ist erforderlich. Nicht entfernt eine Fehlerdomäne, die untergeordneten Elemente enthält – zunächst entweder die untergeordneten Elemente zu entfernen, oder verschieben Sie sie außerhalb mit `Set-ClusterFaultDomain`. Um eine Fehlerdomäne außerhalb von allen anderen Fehlerdomänen verschieben möchten, legen Sie seine `-Parent`auf eine leere Zeichenfolge (""). Sie können keine entfernen `Node`Fehlerdomänen des Typs. Um mehrere Fehlerdomänen gleichzeitig zu entfernen, Listen Sie ihre Namen.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>Definieren von Fehlerdomänen mit XML-markup
Fehlerdomänen können mithilfe einer XML-Design-Syntax angegeben werden. Wir empfehlen die Verwendung von Ihren bevorzugten Texteditor, wie z.B. Visual Studio Code (verfügbaren freien *[hier](https://code.visualstudio.com/)*) oder Editor, um ein XML-Dokument erstellen, die Sie speichern und wiederverwenden können.  

Dieses kurze Video veranschaulicht die Verwendung von XML-Markup Fehlerdomänen angeben.

[![CLicken Sie dieses Image um ein kurzes Video zur Verwendung von XML an Fehlerdomänen sehen Sie sich auf](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

Führen Sie das folgende Cmdlet in PowerShell:`Get-ClusterFaultDomainXML`. Dadurch wird die aktuelle fehlerdomänenspezifikation für den Cluster im XML-Format zurückgegeben. Dieser enthält jeden ermittelten `<Node>`, eingeschlossen in öffnende und schließende `<Topology>`Tags.  

Führen Sie Folgendes ein, um diese Ausgabe in einer Datei zu speichern.  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

Öffnen Sie die Datei, und fügen `<Site>`, `<Rack>`, und `<Chassis>`Tags aus, um anzugeben, wie diese Knoten auf Standorte, Racks und Gehäuse verteilt werden. Jedes Tag muss durch einen eindeutigen identifiziert werden **Namen **. Für Knoten müssen Sie den Knotennamen als standardmäßig aufgefüllt halten.  

> [!IMPORTANT]  
> Während alle zusätzlichen Tags optional sind, müssen sie die transitive Standort erfüllen &gt;Rack &gt;Gehäuse &gt;Knoten-Hierarchie und ordnungsgemäß geschlossen werden.  
Zusätzlich zum Namen können formfreie `Location="..."`und `Description="..."`beliebigen Tags hinzugefügt werden.  

#### <a name="example-two-sites-one-rack-each"></a>Beispiel: Zwei Standorte, jeweils ein Rack  

```XML
<Topology>  
  <Site Name="SEA" Location="Contoso HQ, 123 Example St, Room 4010, Seattle">  
    <Rack Name="A01" Location="Aisle A, Rack 01">  
      <Node Name="Server01" Location="Rack Unit 33" />  
      <Node Name="Server02" Location="Rack Unit 35" />  
      <Node Name="Server03" Location="Rack Unit 37" />  
    </Rack>  
  </Site>  
  <Site Name="NYC" Location="Regional Datacenter, 456 Example Ave, New York City">  
    <Rack Name="B07" Location="Aisle B, Rack 07">  
      <Node Name="Server04" Location="Rack Unit 20" />  
      <Node Name="Server05" Location="Rack Unit 22" />  
      <Node Name="Server06" Location="Rack Unit 24" />  
    </Rack>  
  </Site>  
</Topology> 
``` 

#### <a name="example-two-chassis-blade-servers"></a>Beispiel: zwei Gehäuse, Blade Server  
```XML
<Topology>  
  <Rack Name="A01" Location="Contoso HQ, Room 4010, Aisle A, Rack 01">  
    <Chassis Name="Chassis01" Location="Rack Unit 2 (Upper)" >  
      <Node Name="Server01" Location="Left" />  
      <Node Name="Server02" Location="Right" />  
    </Chassis>  
    <Chassis Name="Chassis02" Location="Rack Unit 6 (Lower)" >  
      <Node Name="Server03" Location="Left" />  
      <Node Name="Server04" Location="Right" />  
    </Chassis>  
  </Rack>  
</Topology>  
```

Klicken Sie zum Festlegen der neuen fehlerdomänenspezifikation speichern Sie den XML-Code, und führen Sie Folgendes in PowerShell.  

```PowerShell
$xml = Get-Content <Path> | Out-String  
Set-ClusterFaultDomainXML -XML $xml
```

Dieses Handbuch enthält nur zwei Beispiele, aber die `<Site>`, `<Rack>`, `<Chassis>`, und `<Node>`Tags können werden gemischt und in viele weitere Möglichkeiten, die physische Topologie Ihrer Bereitstellung widerspiegeln unabhängig sein können. Wir hoffen, dass diese Beispiele die Flexibilität dieser Tags und den Wert der freiformpositionsdeskriptoren zu ihrer Unterscheidung veranschaulichen.  

### <a name="optional-location-and-description-metadata"></a>Optional: Position und die Beschreibung Metadaten

Sie können optional bereitstellen **Speicherort** oder **Beschreibung** Metadaten für jede Fehlerdomäne. Wenn angegeben, werden diese Informationen in hardwarewarnungen des Integritätsdiensts enthalten sein. Dieses kurze Video veranschaulicht den Wert der diese Deskriptoren hinzufügen.

[![CAuf, um ein kurzes Video zur Veranschaulichung des Wert des Hinzufügens von positionsdeskriptoren zu Fehlerdomänen finden Sie unter](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>Siehe auch  
-   [Windows Server 2016](../get-started/windows-server-2016.md)  
-   [Direkte Speicherplätze in WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md) 
