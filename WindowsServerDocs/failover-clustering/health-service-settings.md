---
title: Service Health-Einstellungen
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 569cf7ba30fd3f993394efd3735a56d116c067e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858331"
---
# <a name="health-service-settings"></a>Service Health-Einstellungen
> Gilt für Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, die die tägliche Überwachung verbessert und Erfahrungen für Cluster "direkte Speicherplätze".

Viele der Parameter, die steuern das Verhalten des Integritätsdiensts werden als Einstellungen verfügbar gemacht. Sie können ändern, diese an die Aggressivität der Fehler oder Aktionen zu optimieren, aktivieren Sie bestimmte Verhaltensweisen aktivieren/deaktivieren und vieles mehr.

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

Einige häufig geänderten Einstellungen sind, sowie die Standardwerte aufgeführt.

#### <a name="volume-capacity-threshold"></a>Kapazität der Replikatvolume-Schwellenwert

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>Pool reservierte Kapazität-Schwellenwert

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>Lebenszyklus physischer Datenträger

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>Unterstützte Komponenten Dokument

Finden Sie im vorherigen Abschnitt aus.

#### <a name="firmware-rollout"></a>Rollout der Firmware

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Plattform / Momentaufnahmedatenbank

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
- ["Direkte Speicherplätze" unter WindowsServer 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
