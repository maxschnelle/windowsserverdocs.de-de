---
title: Health-Dienst-Einstellungen
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 569cf7ba30fd3f993394efd3735a56d116c067e0
ms.sourcegitcommit: 30fcae929ce7b611f5d3a5f8fee64b0299272110
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2017
---
# <a name="health-service-settings"></a>Health-Dienst-Einstellungen
> Gilt für WindowsServer 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung verbessert und betriebliche Erfahrung für Cluster mit "direkte Speicherplätze".

Viele der Parameter auf, die das Verhalten des Integritätsdiensts werden als Einstellungen verfügbar gemacht. Sie können diese zum Optimieren der Aggressivität von Fehlern oder Aktionen, aktivieren Sie die ein-/Ausschalten des Verhaltens und vieles mehr ändern.

Verwenden Sie das folgende PowerShell-Cmdlet zum Festlegen oder Ändern von Einstellungen.

### <a name="usage"></a>Verwendung

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>Beispiel

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>Allgemeine Einstellungen

Einige häufig geänderten Einstellungen werden zusammen mit ihren Standardwerten unten aufgeführt.

#### <a name="volume-capacity-threshold"></a>Kapazität-Schwellenwert

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>Pool reservieren Kapazität-Schwellenwert

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>Lebenszyklus von physischen Datenträgern

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>Unterstützte Komponenten Dokument

Finden Sie im vorherigen Abschnitt.

#### <a name="firmware-rollout"></a>Firmware-Einführung

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Plattform / Ruhe

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>Metriken

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>Debuggen

```
"System.LogLevel" = 4
```

## <a name="see-also"></a>Siehe auch

- [Integritätsdienst in WindowsServer 2016](health-service-overview.md)
- [Direkte Speicherplätze in WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
