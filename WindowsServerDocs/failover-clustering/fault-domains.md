---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: Fehlerdomänenunterstützung
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: f5c64bb8f8b7d4b8d13c76c4e94cfcf52ee32c30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821471"
---
# <a name="fault-domain-awareness-in-windows-server-2016"></a>Fehlerdomänenunterstützung in Windows Server 2016

> Gilt für: Windows Server 2016

Failoverclustering ermöglicht die Zusammenarbeit mehrerer Server, um hohe Verfügbarkeit zu bieten – oder anders ausgedrückt, um Knotenfehlertoleranz zu bieten. Aber moderne Unternehmen verlangen eine immer höhere Verfügbarkeit ihrer Infrastruktur. Um cloudähnliche Betriebszeit zu erreichen, ist auch der Schutz bei sehr unwahrscheinlichen Vorfällen wie z.B. Gehäuse- und Rackausfällen oder Naturkatastrophen erforderlich. Deshalb Failoverclustering in Windows Server 2016 führt die Gehäuse-, Rack- und Fehlertoleranz sowie Standort.

Fehlerdomänen und Fehlertoleranz sind eng miteinander verwandte Konzepte. Eine Fehlerdomäne ist eine Reihe von Hardwarekomponenten, die einen gemeinsamen Single Point of Failure haben. Um ein bestimmtes Niveau an Fehlertoleranz zu erzielen, benötigen Sie mehrere Fehlerdomänen auf dieser Ebene. Beispielsweise setzt Rackfehlertoleranz voraus, dass Ihre Server und Daten auf mehrere Racks verteilt sind.

Dieses kurze Video bietet einen Überblick über Fehlerdomänen in Windows Server 2016:  
[![Klicken Sie auf dieses Bild, um einen Überblick über Fehlerdomänen in Windows Server 2016 dabei zu sein.](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

## <a name="benefits"></a>Vorteile
- **-Speicherplätzen, einschließlich "direkte Speicherplätze", verwendet Fehlerdomänen, um die datensicherheit zu maximieren.**  
    Die Resilienz in „Speicherplätze“ ist konzeptionell wie verteiltes, softwaredefiniertes RAID. Mehrere Kopien aller Daten werden synchron beibehalten, und wenn bei einem Hardwareausfall eine Kopie verloren geht, werden andere zum Wiederherstellen der Resilienz erneut kopiert. Um die bestmögliche Resilienz zu erreichen, sollten Kopien in separaten Fehlerdomänen beibehalten werden.

- **Die [Integritätsdienst](health-service-overview.md) verwendet Fehlerdomänen, um nützlichere Warnungen auszugeben.**  
    Jeder Fehlerdomäne können Speicherortmetadaten zugeordnet werden, die automatisch in alle nachfolgenden Warnungen aufgenommen werden. Diese Deskriptoren können Vorgänge oder Wartungspersonal unterstützen und Fehler reduzieren, indem sie Hardware eindeutig machen.  

- **Stretch-clustering verwendet Fehlerdomänen für Storage-Affinität.** Stretch-Clustering ermöglicht weit entfernten Servern, einem gemeinsamen Cluster beitreten. Für optimale Leistung sollten Anwendungen oder virtuelle Computer auf Servern ausgeführt werden, die sich in der Nähe derer befinden, die ihnen Speicherplatz bereitstellen. Fehlerdomänenunterstützung ermöglicht dieser Speicher-Affinität.   

## <a name="levels-of-fault-domains"></a>Ebenen der Fehlerdomänen  
Es gibt vier kanonische Ebenen von Fehlerdomänen – Standort, Rack, Gehäuse und Knoten. Knoten werden automatisch erkannt; jede zusätzliche Ebene ist optional. Wenn Ihre Bereitstellung beispielsweise keine Blade Server enthält, ist die Gehäuseebene für Sie wahrscheinlich nicht sinnvoll.  

![Diagramm mit den verschiedenen Ebenen der Fehlerdomänen](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>Verwendung  
Sie können PowerShell oder XML-Markup verwenden, auf die Angabe von Fehlerdomänen. Beide Ansätze sind äquivalent und bieten vollständige Funktionalität.

>[!IMPORTANT]
> Geben Sie Fehlerdomänen wenn möglich an, bevor Sie „Direkte Speicherplätze“ aktivieren. Dies ermöglicht die Vorbereitung von Pool, Ebenen und Einstellungen wie Resilienz und Anzahl der Spalten für Gehäuse- oder Rackfehlertoleranz durch automatische Konfiguration. Wenn Pool und Volumes erstellt sind, werden Daten nicht nachträglich in Reaktion auf Änderungen der Fehlerdomänentopologie verschoben. Um nach dem Aktivieren von „Direkte Speicherplätze“ Knoten zwischen Gehäusen oder Racks zu verschieben, sollten Sie zuerst den Knoten sowie seine Laufwerke mit `Remove-ClusterNode -CleanUpDisks` aus dem Pool entfernen.

### <a name="defining-fault-domains-with-powershell"></a>Definieren von Fehlerdomänen mit PowerShell
Windows Server 2016 bietet die folgenden Cmdlets zum Arbeiten mit Fehlerdomänen:
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

Dieses kurze Video veranschaulicht die Verwendung dieser Cmdlets.
[![Klicken Sie auf dieses Image ein kurzes Video zur Nutzung der Fehlerdomäne für Cluster-cmdlets](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

Verwendung `Get-ClusterFaultDomain` , finden in der aktuellen fehlerdomänentopologie. Dadurch werden alle Knoten im Cluster sowie alle Gehäuse, Racks oder Standorte aufgelistet, die Sie erstellt haben. Sie können mit Parametern wie **-Type** oder **-Name** filtern, aber diese sind nicht erforderlich.

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

Verwendung `New-ClusterFaultDomain` um neue Gehäuse, Racks oder Standorte zu erstellen. Die `-Type` und `-Name` Parameter sind erforderlich. Die möglichen Werte für `-Type` sind `Chassis`, `Rack`, und `Site`. Die `-Name` kann eine beliebige Zeichenfolge sein. (Für `Node` Fehlerdomänen des Typs, der Name der tatsächliche Knotenname, automatisch festgelegt werden müssen).

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server nicht möglich, und überprüft nicht, dass alle Fehlerdomänen aus, die Sie erstellen, die alle Elemente in der realen, physischen Welt entsprechen. (Dies erscheint nahe liegend, aber es ist wichtig zu verstehen.) Wenn sich in der realen Welt alle Ihre Knoten in einem einzigen Rack befinden, dann schafft das Erstellen von zwei `-Type Rack`-Fehlerdomänen in der Software nicht auf magische Weise Rackfehlertoleranz. Sie sind dafür verantwortlich, sicherzustellen, dass die Topologie, die Sie mithilfe dieser Cmdlets erstellen, der tatsächlichen Anordnung der Hardware entspricht.

Verwendung `Set-ClusterFaultDomain` eine Fehlerdomäne in ein anderes zu verschieben. Die Begriffe „übergeordnet“ und „untergeordnet“ werden häufig zur Beschreibung dieser geschachtelten Beziehung verwendet. Die `-Name` und `-Parent` Parameter sind erforderlich. In `-Name`, geben Sie den Namen der Fehlerdomäne, die verschoben wird; in `-Parent`, geben Sie den Namen des Ziels. Um mehrere Fehlerdomänen gleichzeitig zu verschieben, listen Sie ihre Namen auf.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> Bei der Verschiebung von Fehlerdomänen werden ihre untergeordneten Objekte mit ihnen verschoben. Wenn Rack A im obigen Beispiel server01.contoso.com übergeordnet ist, muss letztere nicht separat an den Standort Shanghai verschoben werden – sie ist schon durch das übergeordnete Element dort, wie in der realen Welt.

Sehen Sie in der Ausgabe der über-/ unterordnungsbeziehung `Get-ClusterFaultDomain`in die `ParentName` und `ChildrenNames` Spalten.

Sie können auch `Set-ClusterFaultDomain` bestimmte andere Eigenschaften von Fehlerdomänen ändern. Beispielsweise können Sie optional bereitstellen `-Location` oder `-Description` Metadaten für jede Fehlerdomäne. Wenn angegeben, werden diese Informationen in Hardwarewarnungen des Integritätsdiensts einbezogen. Sie können auch mithilfe von Fehlerdomänen Umbenennen der `-NewName` Parameter. Nicht umbenennen `Node` Fehlerdomänen des Typs.

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

Verwendung `Remove-ClusterFaultDomain` entfernen, Gehäuse, Racks oder Standorte, die Sie erstellt haben. Der `-Name` -Parameter ist erforderlich. Sie können nicht entfernen eine Fehlerdomäne an, die untergeordneten Elemente enthält – zunächst entfernen Sie die untergeordneten Elemente, oder verschieben Sie sie mithilfe von `Set-ClusterFaultDomain`. Um eine Fehlerdomäne außerhalb von allen anderen Fehlerdomänen heraus zu verschieben, legen Sie dessen `-Parent` auf eine leere Zeichenfolge (""). Sie können nicht entfernt werden `Node` Fehlerdomänen des Typs. Um mehrere Fehlerdomänen gleichzeitig zu entfernen, listen Sie ihre Namen auf.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>Definieren von Fehlerdomänen mit XML-Markup
Fehlerdomänen können mithilfe einer XML-Syntax angegeben werden. Sie sollten Ihren bevorzugten Texteditor verwenden, z.B. Visual Studio Code (*[hier](https://code.visualstudio.com/)* kostenlos erhältlich) oder Editor, um ein XML-Dokument zu erstellen, das Sie speichern und wiederverwenden können.  

Dieses kurze Video veranschaulicht die Verwendung von XML-Markup zur Angabe von Fehlerdomänen.

[![Klicken Sie auf dieses Image ein kurzes Video zum XML verwenden, um die Angabe von Fehlerdomänen](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

Führen Sie in PowerShell das folgende Cmdlet: `Get-ClusterFaultDomainXML`. Dadurch wird die aktuelle Fehlerdomänenspezifikation für den Cluster im XML-Format zurückgegeben. Dies entspricht jede ermittelte `<Node>`, eingeschlossen in öffnende und schließende `<Topology>` Tags.  

Führen Sie Folgendes aus, um diese Ausgabe in einer Datei zu speichern.  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

Öffnen Sie die Datei, und fügen `<Site>`, `<Rack>`, und `<Chassis>` Tags angeben, wie diese Knoten auf Standorte, Racks und Gehäuse verteilt werden. Jedes Tag muss durch einen eindeutigen **Name** identifiziert werden. Für Knoten müssen Sie den Knotennamen als standardmäßig aufgefüllt beibehalten.  

> [!IMPORTANT]  
> Während alle zusätzlichen Tags optional sind, muss die transitive Hierarchie Standort &gt; Rack &gt; Gehäuse &gt; Knoten beibehalten und ordnungsgemäß geschlossen werden.  
Zusätzlich zum Namen können die freiformdeskriptoren `Location="..."` und `Description="..."` beliebigen Tags hinzugefügt werden.  

#### <a name="example-two-sites-one-rack-each"></a>Beispiel: Zwei Standorte, jeweils ein rack  

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

Zum Festlegen der neuen fehlerdomänenspezifikation speichern Sie Ihrer XML-Daten, und führen Sie Folgendes in PowerShell.  

```PowerShell
$xml = Get-Content <Path> | Out-String  
Set-ClusterFaultDomainXML -XML $xml
```

Dieses Handbuch enthält nur zwei Beispiele, aber die `<Site>`, `<Rack>`, `<Chassis>`, und `<Node>` Tags können gemischt und abgeglichen, die auf viele weitere Arten entsprechend die physische Topologie Ihrer Bereitstellung, was auch immer, die möglicherweise. Wir hoffen, dass diese Beispiele die Flexibilität dieser Tags und den Wert der Freiformpositionsdeskriptoren zu ihrer Unterscheidung veranschaulichen.  

### <a name="optional-location-and-description-metadata"></a>Optional: Speicherort und eine Beschreibung von Metadaten

Sie können optional angeben **Speicherort** oder **Beschreibung** Metadaten für jede Fehlerdomäne. Wenn angegeben, werden diese Informationen in Hardwarewarnungen des Integritätsdiensts einbezogen. Dieses kurze Video veranschaulicht den Vorteil des Hinzufügens von solchen Deskriptoren.

[![Klicken Sie auf, um ein kurzes Video zur Veranschaulichung des Wert des Hinzufügens von positionsdeskriptoren zu Fehlerdomänen finden Sie unter](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>Siehe auch  
-   [Windows Server 2016](../get-started/windows-server-2016.md)  
-   ["Direkte Speicherplätze" unter WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md) 
