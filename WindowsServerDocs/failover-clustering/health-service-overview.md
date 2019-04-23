---
title: Integritätsdienst in WindowsServer
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 02/09/2018
ms.openlocfilehash: 5afb64dcf0c59697ed55d7cf51ef1bc36e7e0e36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863811"
---
# <a name="health-service-in-windows-server"></a>Integritätsdienst in WindowsServer

> Gilt für Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, die die tägliche Überwachung verbessert und Erfahrungen für Cluster "direkte Speicherplätze".

## <a name="prerequisites"></a>Vorraussetzungen  

Für „Direkte Speicherplätze“ ist der Integritätsdienst standardmäßig aktiviert. Für seine Einrichtung und seinen Start sind keine weiteren Aktionen erforderlich. Weitere Informationen zu "direkte Speicherplätze" finden Sie unter ["direkte Speicherplätze" in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md).  

## <a name="reports"></a>Berichte

Finden Sie unter [Integritätsdienst meldet](health-service-reports.md).

## <a name="faults"></a>Fehler

Finden Sie unter [Integritätsdienst Fehler](health-service-faults.md).

## <a name="actions"></a>Aktionen

Finden Sie unter [Integritätsdienst Aktionen](health-service-actions.md).

## <a name="automation"></a>Automatisierung  

Im nächsten Abschnitt werden Workflows beschrieben, die vom Integritätsdienst im Lebenszyklus von Datenträgern automatisiert werden.  

### <a name="disk-lifecycle"></a>Lebenszyklus von Datenträgern   

Der Integritätsdienst automatisiert die meisten Phasen des Lebenszyklus physischer Datenträger. Angenommen, der Ausgangsstatus Ihrer Bereitstellung ist eine perfekte Integrität, was heißt, dass alle physischen Datenträger ordnungsgemäß funktionieren.  

#### <a name="retirement"></a>Deaktivierung  

Physische Datenträger werden automatisch deaktiviert, wenn sie nicht mehr verwendet werden können, woraufhin ein entsprechender Fehler ausgelöst wird. Es gibt mehrere Fälle:  

-   Medienfehler: Der physische Datenträger ist definitiv ausgefallen oder beschädigt und muss ausgetauscht werden.  

-   Kommunikationsverlust: Der physische Datenträger hatte 15 Minuten lang keine Verbindung.  

-   Keine Reaktion: Der physische Datenträger hatte binnen einer Stunde dreimal oder öfter eine Latenz von 5,0 Sekunden zu verzeichnen.  

>[!NOTE]
> Wenn die Verbindung mit zahlreichen physischen Datenträgern gleichzeitig bzw. mit einem gesamten Knoten oder Speichergehäuse verloren geht, werden diese Datenträger vom Integritätsdienst *nicht* deaktiviert, weil sie wahrscheinlich nicht die Ursache sind.  

Wenn der deaktivierte Datenträger als Cache für viele andere physische Datenträger fungiert hat, werden diese, sofern verfügbar, automatisch einem anderen Cachedatenträger neu zugewiesen. Es ist keine spezielle Benutzeraktion erforderlich.  

#### <a name="restoring-resiliency"></a>Wiederherstellen der Ausfallsicherheit  

Nachdem ein physischer Datenträger deaktiviert wurde, beginnt der Integritätsdienst sofort mit dem Kopieren seiner Daten auf die restlichen physischen Datenträger, um die vollständige Ausfallsicherheit wiederherzustellen. Sobald dies abgeschlossen ist, sind die Daten vollständig sicher und wieder fehlertolerant.  

>[!NOTE]
> Die sofortige Wiederherstellung erfordert ausreichend verfügbare Kapazität auf den verbleibenden physischen Datenträgern.  

#### <a name="blinking-the-indicator-light"></a>Blinken der Leuchte  

Falls möglich, aktiviert der Integritätsdienst das Blinken der Leuchte auf dem deaktivierten physischen Datenträger oder an seinem Steckplatz. Dies wird dauerhaft fortgesetzt, bis der deaktivierte Datenträger ausgetauscht wird.  

>[!NOTE]
> Mitunter kann der Datenträger ggf. auf eine Weise ausfallen, die selbst das Funktionieren der Leuchte verhindert, z. B. beim Totalausfall des Stroms.  

#### <a name="physical-replacement"></a>Physischer Austausch  

Nach Möglichkeit sollten Sie den deaktivierten physischen Datenträger austauschen. In den meisten Fällen diese besteht aus einer hot-Swap – d. h. das Ausschalten der Knotens oder Speichergehäuses ist nicht erforderlich. In den Informationen zum Fehler finden Sie hilfreiche Angaben zu Stelle und Teil.  

#### <a name="verification"></a>Überprüfung

Wenn der austauschdatenträger eingebaut wurde, wird es für das Dokument für die unterstützten Komponenten überprüft werden (siehe nächster Abschnitt).

#### <a name="pooling"></a>Erstellen von Pools  

Falls zulässig, wird der Austauschdatenträger automatisch dem Pool seines Vorgängers hinzugefügt, um den Betrieb aufzunehmen. Sobald der Fehler verschwunden ist, wird das System in seinen Ausgangszustand mit perfekter Integrität zurückgesetzt.  

## <a name="supported-components-document"></a>Unterstützte Komponenten Dokument  

Der Integritätsdienst bietet einen Erzwingungsmechanismus zum Beschränken der Komponenten, die von "direkte Speicherplätze" verwendet werden, mit denen in einem Dokument Komponenten unterstützt durch den Administrator oder Lösungsanbieter bereitgestellt. Diese kann verwendet werden, um eine versehentliche Nutzung nicht unterstützter Hardware durch Sie oder andere zu verhindern, sodass Garantie- und Supportvertragsbedingungen besser eingehalten werden. Diese Funktion ist derzeit begrenzt auf physische Datenträger, einschließlich SSDs zu HDDs und NVMe-Laufwerke. Das Dokument für die unterstützten Komponenten können auf das Modell, Hersteller (optional) und -Firmware-Version (optional) einschränken.

### <a name="usage"></a>Verwendung  

Das Dokument für die unterstützten Komponenten wird eine XML-inspiriert Syntax verwendet. Es wird empfohlen, Ihren bevorzugten Texteditor, beispielsweise die kostenlose [Visual Studio Code](http://code.visualstudio.com/) oder Editor, um ein XML-Dokument erstellen, das Sie speichern und wiederverwenden können.

#### <a name="sections"></a>Abschnitte

Das Dokument besteht aus zwei unabhängige Abschnitten: `Disks` und `Cache`.

Wenn die `Disks` Abschnitt bereitgestellt wird, werden nur die Laufwerke aufgeführt (als `Disk`) sind zulässig, um Pools zu verknüpfen. Alle nicht aufgeführten Laufwerke werden daran gehindert Verknüpfen von Pools, die eingesetzt werden können in der Produktion. Wenn in diesem Abschnitt leer gelassen wird, wird jedes Laufwerk Verknüpfen des Pools zulässig.

Wenn die `Cache` Abschnitt bereitgestellt wird, werden nur die Laufwerke aufgeführt (als `CacheDisk`) werden für die Zwischenspeicherung verwendet. Wenn in diesem Abschnitt leer gelassen wird, "direkte Speicherplätze" versucht, [Raten basierend auf den Medientyp und Bustyp](../storage/storage-spaces/understand-the-cache.md#cache-drives-are-selected-automatically). Laufwerke, die hier aufgeführten sollte auch aufgeführt werden `Disks`.

>[!IMPORTANT]
> Das Dokument für die unterstützten Komponenten wird nicht rückwirkend für Laufwerke, die bereits in einem Pool zusammengefasst und angewendet.  

#### <a name="example"></a>Beispiel

```XML
<Components>

  <Disks>
    <Disk>
      <Manufacturer>Contoso</Manufacturer>
      <Model>XYZ9000</Model>
      <AllowedFirmware>
        <Version>2.0</Version>
        <Version>2.1</Version>
        <Version>2.2</Version>
      </AllowedFirmware>
      <TargetFirmware>
        <Version>2.1</Version>
        <BinaryPath>C:\ClusterStorage\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Disks>

  <Cache>
    <CacheDisk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </CacheDisk>
  </Cache>

</Components>

```

Um mehrere Laufwerke aufzulisten, fügen Sie einfach zusätzliche `<Disk>` oder `<CacheDisk>` Tags.

Um diesen XML-Code einzufügen, wenn Sie "direkte Speicherplätze" bereitstellen, verwenden Sie die `-XML` Parameter:

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String  
Enable-ClusterS2D -XML $MyXML
```

Festlegen oder ändern Sie das Dokument für die unterstützten Komponenten aus, sobald "direkte Speicherplätze" bereitgestellt wurde:

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String  
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML  
```

>[!NOTE]
>Die Eigenschaften „Model“, „Manufacturer“ und „FirmwareVersion“ müssen exakt mit den Werten übereinstimmen, die Sie mit dem Cmdlet **Get-PhysicalDisk** abrufen. Je nach Implementierung des Herstellers weichen diese von Ihren Erwartungen ab. Anstatt „Contoso“ kann der Hersteller (Manufacturer) „CONTOSO-LTD“ heißen, oder dieser Eintrag ist leer, während das Modell „Contoso-XZY9000“ ist.  

Sie können dies mit dem folgenden PowerShell-Cmdlet überprüfen:  

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion  
```

## <a name="settings"></a>Einstellungen

Finden Sie unter [Integritätsdienst Einstellungen](health-service-settings.md).

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst-Berichte](health-service-reports.md)
- [Integritätsdienst-Dienstfehler](health-service-faults.md)
- [Integrität von Dienstaktionen](health-service-actions.md)
- [Service Health-Einstellungen](health-service-settings.md)
- ["Direkte Speicherplätze" unter WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
