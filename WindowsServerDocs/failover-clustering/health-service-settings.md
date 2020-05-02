---
title: Integritätsdienst Einstellungen
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: a8262567abdd18847e99026c43d722351a00d3f2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720540"
---
# <a name="health-service-settings"></a>Integritätsdienst Einstellungen

> Gilt für: Windows Server 2019, Windows Server 2016

Der Integritätsdienst ist ein neues Feature in Windows Server 2016, das die tägliche Überwachung und Betriebsbereitschaft für Cluster mit direkte Speicherplätze verbessert.

Viele der Parameter, die das Verhalten der Integritätsdienst steuern, werden als Einstellungen verfügbar gemacht. Sie können diese ändern, um die Aggressivität von Fehlern oder Aktionen zu optimieren, bestimmte Verhalten ein-/ausschalten und vieles mehr.

Verwenden Sie das folgende PowerShell-Cmdlet, um Einstellungen festzulegen oder zu ändern.

### <a name="usage"></a>Verwendung

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>Beispiel

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>Allgemeine Einstellungen

Einige häufig geänderte Einstellungen sind im folgenden aufgeführt, zusammen mit ihren Standardwerten.

#### <a name="volume-capacity-threshold"></a>Schwellenwert für Volumenkapazität

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>Schwellenwert für Pool Reserve Kapazität

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

#### <a name="supported-components-document"></a>Dokument zu unterstützten Komponenten

Weitere Informationen finden Sie im vorherigen Abschnitt.

#### <a name="firmware-rollout"></a>Firmware-Rollout

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Plattform/ineszenz

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

## <a name="see-also"></a>Weitere Informationen

- [Der Integritätsdienst in Windows Server 2016](health-service-overview.md)
- [Direkte Speicherplätze in Windows Server 2016](../storage/storage-spaces/storage-spaces-direct-overview.md)
