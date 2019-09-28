---
title: Integritätsdienst in Windows Server
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 02/09/2018
ms.openlocfilehash: df455dfb0d2936192a3c2d7825e2d6d031cfe892
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361070"
---
# <a name="health-service-in-windows-server"></a>Integritätsdienst in Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung und Betriebsbereitschaft für Cluster mit direkte Speicherplätze verbessert.

## <a name="prerequisites"></a>Erforderliche Komponenten  

Für „Direkte Speicherplätze“ ist der Integritätsdienst standardmäßig aktiviert. Für seine Einrichtung und seinen Start sind keine weiteren Aktionen erforderlich. Weitere Informationen zu direkte Speicherplätze finden Sie unter [direkte Speicherplätze in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md).  

## <a name="reports"></a>Berichte

Siehe [Integritätsdienst Berichte](health-service-reports.md).

## <a name="faults"></a>Fehler

Siehe [Integritätsdienst Fehler](health-service-faults.md).

## <a name="actions"></a>Aktionen

Siehe [Integritätsdienst Aktionen](health-service-actions.md).

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

Nach Möglichkeit sollten Sie den deaktivierten physischen Datenträger austauschen. In den meisten Fällen besteht dies aus einem Hot-Swap-Vorgang, d. h., das Ausschalten des Knotens oder des Speicher Gehäuses ist nicht erforderlich. In den Informationen zum Fehler finden Sie hilfreiche Angaben zu Stelle und Teil.  

#### <a name="verification"></a>Überprüfung

Wenn der Ersetzungs Datenträger eingefügt wird, wird er anhand des Dokuments "Unterstützte Komponenten" überprüft (Weitere Informationen finden Sie im nächsten Abschnitt).

#### <a name="pooling"></a>Erstellen von Pools  

Falls zulässig, wird der Austauschdatenträger automatisch dem Pool seines Vorgängers hinzugefügt, um den Betrieb aufzunehmen. Sobald der Fehler verschwunden ist, wird das System in seinen Ausgangszustand mit perfekter Integrität zurückgesetzt.  

## <a name="supported-components-document"></a>Dokument zu unterstützten Komponenten  

Der Integritätsdienst stellt einen Erzwingungs Mechanismus bereit, mit dem die von direkte Speicherplätze verwendeten Komponenten auf die von dem Administrator oder dem Lösungs Hersteller bereitgestellten Komponenten beschränkt werden. Diese kann verwendet werden, um eine versehentliche Nutzung nicht unterstützter Hardware durch Sie oder andere zu verhindern, sodass Garantie- und Supportvertragsbedingungen besser eingehalten werden. Diese Funktion ist zurzeit auf physische Festplattengeräte beschränkt, einschließlich SSDs, HDDs und nvme-Laufwerke. Das Dokument "Unterstützte Komponenten" kann für das Modell, den Hersteller (optional) und die Firmwareversion (optional) eingeschränkt werden.

### <a name="usage"></a>Verwendung  

Im Dokument "Unterstützte Komponenten" wird eine XML-inspirierte Syntax verwendet. Es wird empfohlen, Ihren bevorzugten Text-Editor, z. b. die kostenlose [Visual Studio Code](http://code.visualstudio.com/) oder den Editor, zum Erstellen eines XML-Dokuments zu verwenden, das Sie speichern und wieder verwenden können.

#### <a name="sections"></a>Strecken

Das Dokument weist zwei unabhängige Abschnitte auf: `Disks` und `Cache`.

Wenn der `Disks`-Abschnitt angegeben ist, können nur die aufgeführten Laufwerke (als `Disk`) Pools beitreten. Nicht aufgelistete Laufwerke werden daran gehindert, Pools beizutreten, was die Verwendung in der Produktion praktisch ausschließt. Wenn dieser Abschnitt leer bleibt, wird jedem Laufwerk das beitreten zu Pools gestattet.

Wenn der Abschnitt "`Cache`" angegeben wird, werden nur die aufgeführten Laufwerke (wie `CacheDisk`) für die Zwischenspeicherung verwendet. Wenn dieser Abschnitt leer bleibt, versucht direkte Speicherplätze, [basierend auf Medientyp und Bustyp zu erraten](../storage/storage-spaces/understand-the-cache.md#cache-drives-are-selected-automatically). Die hier aufgeführten Laufwerke sollten auch in `Disks` aufgeführt werden.

>[!IMPORTANT]
> Das Dokument "Unterstützte Komponenten" gilt nicht rückwirkend für bereits in einem Pool zusammengefasste und verwendete Laufwerke.  

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

Fügen Sie zum Auflisten mehrerer Laufwerke einfach zusätzliche `<Disk>`-oder `<CacheDisk>`-Tags hinzu.

Um diese XML-Datei beim Bereitstellen von direkte Speicherplätze einzufügen, verwenden Sie den Parameter "`-XML`":

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String  
Enable-ClusterS2D -XML $MyXML
```

So können Sie das Dokument "Unterstützte Komponenten" nach der Bereitstellung direkte Speicherplätze festlegen oder ändern:

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

Siehe [Integritätsdienst Einstellungen](health-service-settings.md).

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst Berichte](health-service-reports.md)
- [Integritätsdienst Fehler](health-service-faults.md)
- [Integritätsdienst Aktionen](health-service-actions.md)
- [Integritätsdienst Einstellungen](health-service-settings.md)
- [Direkte Speicherplätze in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
