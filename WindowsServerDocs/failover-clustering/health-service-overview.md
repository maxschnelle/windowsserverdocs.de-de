---
title: "Integritätsdienst in WindowsServer 2016"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 834fcfb749e89e4768dce3f229564feea550a432
ms.sourcegitcommit: 30fcae929ce7b611f5d3a5f8fee64b0299272110
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2017
---
# <a name="health-service-in-windows-server-2016"></a>Integritätsdienst in WindowsServer 2016
> Gilt für WindowsServer 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung verbessert und betriebliche Erfahrung für Cluster mit "direkte Speicherplätze".

## <a name="prerequisites"></a>Erforderliche Komponenten  

Der Integritätsdienst ist standardmäßig mit "direkte Speicherplätze" aktiviert. Keine weitere Aktion ist erforderlich, richten sie ein oder starten. Weitere Informationen zu "direkte Speicherplätze" finden Sie unter ["direkte Speicherplätze" in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md).  

## <a name="reports"></a>Berichte

Weitere Informationen finden Sie unter [Integritätsdienst meldet](health-service-reports.md).

## <a name="faults"></a>Seitenfehler

Weitere Informationen finden Sie unter [Integritätsdienst Fehler](health-service-faults.md).

## <a name="actions"></a>Aktionen

Weitere Informationen finden Sie unter [Integritätsdienst Aktionen](health-service-actions.md).

## <a name="automation"></a>Automatisierung  

Dieser Abschnitt enthält Workflows, die vom Integritätsdienst im Lebenszyklus von Datenträgern automatisiert werden.  

### <a name="disk-lifecycle"></a>Lebenszyklus von Datenträgern   

Der Integritätsdienst automatisiert die meisten Phasen des Lebenszyklus physischer Datenträger. Nehmen wir an, dass der ursprüngliche Zustand der Bereitstellung perfekte Integrität -, d. h. ist, alle physischen Datenträger ordnungsgemäß funktionieren.  

#### <a name="retirement"></a>Zurückziehen  

Physische Datenträger werden automatisch gelöscht, wenn Sie nicht mehr verwendet werden, und ein entsprechender Fehler ausgelöst wird. Es gibt mehrere Fälle:  

-   Medienfehler: der physische Datenträger ist definitiv konnte oder beschädigt ist, und muss ersetzt werden.  

-   Kommunikationsverlust: der physische Datenträger verfügt über Konnektivität für mehr als 15 Minuten lang verloren.  

-   Keine Reaktion: der physische Datenträger Latenz von 5,0 Sekunden drei oder mehrmals innerhalb einer Stunde ausgestellt hat.  

>[!NOTE]
> Wenn die Verbindung verloren geht auf viele physische Datenträger auf einmal oder auf einen gesamten Knoten oder Speichergehäuse, wird der Integritätsdienst *nicht* diese Datenträger abkoppeln, da sie wahrscheinlich die Ursache sind.  

Wenn der deaktivierte Datenträger als Cache für viele andere physische Datenträger fungiert hat, werden diese automatisch zu einem anderen Cachedatenträger zugewiesen werden, wenn einer verfügbar ist. Es ist keine spezielle Benutzeraktion erforderlich.  

#### <a name="restoring-resiliency"></a>Wiederherstellen der ausfallsicherheit  

Nachdem Sie ein physischer Datenträger außer Betrieb genommen wurde, beginnt der Integritätsdienst sofort kopieren seiner Daten auf den verbleibenden physischen Datenträgern, um die vollständige ausfallsicherheit wiederherzustellen. Sobald dies abgeschlossen ist, werden die Daten vollständig sicher und fehlertolerant.  

>[!NOTE]
> Die sofortige Wiederherstellung erfordert ausreichend verfügbare Kapazität auf den verbleibenden physischen Datenträgern.  

#### <a name="blinking-the-indicator-light"></a>Blinken der Leuchte  

Wenn möglich, beginnt der Integritätsdienst das Blinken der Leuchte auf dem deaktivierten physischen Datenträger oder an seinem Steckplatz. Dies wird dauerhaft fortgesetzt, bis der deaktivierte Datenträger ausgetauscht wird.  

>[!NOTE]
> In einigen Fällen der Datenträger möglicherweise nicht auf eine Weise, die auch die Statusanzeige nicht funktionieren - zusammengelegt z. B. einem Totalausfall des Stroms.  

#### <a name="physical-replacement"></a>Physische Ersatz  

Ersetzen Sie den deaktivierten physischen Datenträger, wenn möglich. In den meisten Fällen besteht aus einem hot-Swap – d. h. Das Ausschalten der Knotens oder Speichergehäuses ist nicht erforderlich. Finden Sie unter den Fehler finden Sie hilfreiche Angaben zu Stelle und Teileinformationen.  

#### <a name="verification"></a>Überprüfung

Bei der austauschdatenträger eingebaut wurde, wird er anhand dieses Dokuments für unterstützte Komponenten überprüft werden (siehe nächsten Abschnitt).

#### <a name="pooling"></a>Pooling  

Falls zulässig, wird der austauschdatenträger automatisch in seinem Vorläufer Pool verwenden eingeben ersetzt. An diesem Punkt wird das System in seinen Ausgangszustand mit perfekter Integrität zurückgegeben, und klicken Sie dann der Fehler nicht mehr.  

## <a name="supported-components-document"></a>Unterstützte Komponenten Dokument  

Der Integritätsdienst bietet einen Erzwingungsmechanismus zum Beschränken der Komponenten von "direkte Speicherplätze" verwendet, um auf ein Dokument Komponenten unterstützt durch den Administrator oder Lösungsanbieter bereitgestellt. Dies kann verwendet werden zu verhindern, dass Garantie-Nutzung nicht unterstützter Hardware durch Sie oder andere, welches mit Garantie supportvertragsbedingungen. Diese Funktionalität ist derzeit auf physische Datenträger, z. B. SSDs HDDs, beschränkt, und NVMe-Laufwerke. Das Dokument für unterstützte Komponenten können auf Modell, Hersteller (optional) und Firmware-Version (optional) beschränken.

### <a name="usage"></a>Verwendung  

Das unterstützte Komponenten Dokument verwendet eine XML-Design-Syntax. Wir empfehlen die Verwendung von Ihren bevorzugten Texteditor, wie z. B. Visual Studio Code (verfügbaren freien [hier](http://code.visualstudio.com/)) oder Editor, um ein XML-Dokument erstellen, die Sie speichern und wiederverwenden können.

#### <a name="sections"></a>Abschnitte

Das Dokument hat zwei unabhängige Abschnitte: **Datenträger** und **Cache**.

Wenn die **Datenträger** Abschnitt bereitgestellt wird, dürfen nur die aufgeführten Laufwerke Pools beitreten. Nicht aufgelistete Laufwerke können nicht beitreten zu Speicherpools, die Sie nicht in der Produktion. Wenn in diesem Abschnitt leer ist, wird jedem Laufwerk beitreten Pools ausgeführt werden.

Wenn die **Cache** Abschnitt bereitgestellt wird, nur die aufgeführten Laufwerke zum Zwischenspeichern verwendet werden. Wenn in diesem Abschnitt leer ist, "direkte Speicherplätze" versucht, zu erraten basierend auf den Medientyp und Bustyp. Z. B. wenn die Bereitstellung Solid State Drives (SSDS) und Festplattenlaufwerken (HDDS) verwendet, wird die erste automatisch ausgewählt zum Zwischenspeichern von; Wenn Ihre Bereitstellung reine Flash verwendet, müssen Sie jedoch die höhere Belastungen Geräte angeben, die Sie zum Zwischenspeichern von hier verwenden möchten.

>[!IMPORTANT]
> Das unterstützte Komponenten Dokument wird nicht rückwirkend für Laufwerke, die bereits in einem Pool zusammengefasste und bei Verwendung angewendet.  

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
        <BinaryPath>\\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
  </Disks>

  <Cache>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Cache>

</Components>

```

Um mehrere Laufwerke aufzulisten, fügen Sie einfach zusätzliche ** &lt;Datenträger&gt; ** Tags in einem dieser Abschnitte.

Verwenden Sie diese XML-Datei eingefügt, wenn Sie "direkte Speicherplätze" bereitstellen, die **- XML-** Kennzeichen:

```PowerShell
Enable-ClusterS2D -XML <MyXML>
```

Um festzulegen, oder ändern Sie das Dokument für die unterstützte Komponenten, nachdem direkte Speicherplätze bereitgestellt wurde (d. h., wenn der Integritätsdienst bereits ausgeführt wird), verwenden Sie das folgende PowerShell-Cmdlet:

```PowerShell
$MyXML = Get-Content <\\path\to\file.xml> | Out-String  
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML  
```

>[!NOTE]
>Das Modell, Hersteller und die Firmware-Version-Eigenschaften sollten exakt die Werte, die Sie mit der **Get-PhysicalDisk** Cmdlet. Dies kann von der "vernünftigen" Erwartung, abhängig von Ihrem Anbieter unterscheiden. Beispielsweise anstatt "Contoso", möglicherweise "CONTOSO-Ltd" HEIßEN, oder kann leer sein, während das Modell "Contoso-XZY9000" ist.  

Sie können überprüfen, mit dem folgenden PowerShell-Cmdlet:  

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion  
```

## <a name="settings"></a>Einstellungen

Weitere Informationen finden Sie unter [Integritätsdienst Einstellungen](health-service-settings.md).

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst-Berichte](health-service-reports.md)
- [Health-Dienst Fehler](health-service-faults.md)
- [Health Service-Aktionen](health-service-actions.md)
- [Health-Dienst-Einstellungen](health-service-settings.md)
- [Direkte Speicherplätze in WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
