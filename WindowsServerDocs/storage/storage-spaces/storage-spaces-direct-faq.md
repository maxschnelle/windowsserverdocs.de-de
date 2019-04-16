---
title: Speicherplätze – häufig gestellte Fragen
description: Erfahren Sie, wie etwa Storage Spaces Direct
keywords: Speicherplätze
ms.prod: windows-server-threshold
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: b17aa7ddc783e95fbcc19fe3913192d245133c7f
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066884"
---
# Speicherplätze – häufig gestellte Fragen (FAQ)

Dieser Artikel enthält einige allgemeinen und häufig gestellten Fragen im Zusammenhang mit ["Direkte Speicherplätze"](storage-spaces-direct-overview.md).

## Wenn Sie "direkte Speicherplätze" mit 3 Knoten verwenden, können Sie die Leistung und Kapazität Ebenen erhalten?

Ja, erhalten Sie eine Leistung und die Kapazitätsebene in einer Konfiguration mit 2 oder 3-Knoten "direkte Speicherplätze". Sie müssen allerdings sicherstellen, dass Sie über 2 kapazitätsgeräte verfügen. Das bedeutet, dass Sie alle drei Arten von Geräten verwenden müssen: NVME, SSD und HDD.
 
## Dateisystem (Refs) bietet in Echtzeit Tiaring mit "direkte Speicherplätze". Bietet REFS die gleiche Funktionalität mit freigegebenen "Speicherplätze" in 2016?

Nein, werden Sie in Echtzeit mit freigegebenen "Speicherplätze" mit 2016 Stufen angezeigt. Dies ist nur für "direkte Speicherplätze". 
 
## Kann ich mit "direkte Speicherplätze" ein NTFS-Dateisystem verwenden?
  
Ja, können Sie das NTFS-Dateisystem mit "direkte Speicherplätze" verwenden. REFS wird jedoch empfohlen. NTFS bietet keine in Echtzeit Stufen. 
 
## Ich habe "direkte Speicherplätze" Cluster mit 2 Knoten, konfiguriert, in denen der virtuelle Datenträger als 2-Wege-spiegelungsresilienz konfiguriert ist. Wenn ich eine neue Fehlerdomäne hinzufügen, wird die resilienz des vorhandenen virtuellen Laufwerks geändert?

Nachdem Sie die neue Fehlerdomäne hinzugefügt haben, werden der neue virtuelle Datenträger, die Sie erstellen 3-Wege-Spiegelung eingefügt. Der vorhandene virtuelle Datenträger bleibt jedoch einer gespiegelten 2-Wege-Festplatte. Sie können die Daten in den neuen virtuellen Datenträger von den vorhandenen Volumes auf die Vorteile der neuen Stabilität zu erhalten kopieren.
 
## "Direkte Speicherplätze" erstellt mit der Befehlszeilenoption Autoconfig:0 und dem Pool manuell erstellt wurde. Beim Versuch, den "direkte Speicherplätze" Pool zum Erstellen eines neuen Datenträgers abzufragen, erhalte ich eine Meldung mit der Bezeichnung "Enable-ClusterS2D erneut." Was soll ich tun?

Standardmäßig Wenn Sie "direkte Speicherplätze" konfigurieren, mit dem Cmdlet Enable-S2D führt das Cmdlet alles, was für Sie. Es schafft des Pools und die Ebenen. Wenn Sie Autoconfig:0 verwenden, muss alles manuell ausgeführt werden. Wenn Sie nur den Pool erstellt haben, wird die Ebene nicht notwendigerweise erstellt. Sie erhalten eine Fehlermeldung "Enable-ClusterS2D erneut", wenn Sie entweder nicht erstellt auf allen Ebenen oder Ebenen in einer Weise, die Geräte angeschlossen entspricht nicht erstellt haben. Es wird empfohlen, dass Sie nicht den Schalter für die automatische Konfiguration in einer produktiven Umgebung verwenden. 
 
## Ist es möglich, einen sich drehenden Datenträger (HDDS) an den "direkte Speicherplätze" Pool hinzufügen, nachdem Sie "direkte Speicherplätze" mit SSD-Geräten erstellt haben?

Nein. Standardmäßig Wenn Sie den einzelnen Gerätetyp zum Erstellen des Pools verwenden, wäre es nicht Cache Festplatten konfigurieren und alle Laufwerke für Kapazität verwendet werden würden. Sie können die Konfiguration NVME-Laufwerke hinzufügen, und NVME-Laufwerke würde für Cache konfiguriert werden.
 
## Ich habe eine 2-Rack Fehlerdomäne konfiguriert: RACK 1 hat 2 Fehlerdomänen, RACK 2 1 Fehlerdomäne. Jeder Server verfügt über 4 kapazitätsgeräte 100 GB. Kann alle 1.200 GB Speicherplatz aus dem Pool werden verwenden?

Nein, können Sie nur 800 GB. In einer Rack-Fehlertoleranz Domäne müssen Sie sicherstellen, dass Sie über eine Konfiguration 2-Wege-Spiegelung, damit, von denen jedes chuck und seine doppelte Flächen, die in einem anderen Rack verfügen.
 
## Was sollte die Cachegröße sein, wenn ich erhalte die Meldung "direkte Speicherplätze" Konfigurieren?

Der Cache sollte angepasst werden, um den Arbeitssatz aufzunehmen (die Daten, aktiv gelesen oder geschrieben werden zu einem bestimmten Zeitpunkt) Ihrer Anwendungen und Workloads.

## Wie kann ich die Größe des Caches ermitteln, die von "direkte Speicherplätze" verwendet wird?

Verwenden Sie das integrierte Hilfsprogramm Systemmonitor, um die Cachefehlerrate zu überprüfen. Überprüfen Sie den Cache Miss Reads/sec aus dem Cluster Storage Hybrid Disk Zähler. Denken Sie daran, dass zu viele Lesevorgänge Cache nicht vorhanden sind, im Cache nicht groß genug ist und Sie es zu erweitern möchten. 
 
## Gibt es ein Rechner, der die genaue Größe der Datenträger angezeigt, die für Cache, Kapazität und Stabilität, die besser planen kann würde reservieren festgelegt werden?

Die Storage Spaces Rechner können Sie Ihre Planung erleichtern. Es steht unter http://aka.ms/s2dcalc.
 
## Was ist die beste Konfiguration, die Sie beim Konfigurieren von 6 Servern und 3 Racks empfehlen möchten?

Verwenden Sie 2 Server für jede der Racks, um den virtuellen Datenträger resilienz einer 3-Wege-Spiegelung abzurufen. Denken Sie daran, dass die Rack-Konfiguration ordnungsgemäß funktionieren, würden nur dann, wenn Sie die Konfiguration des Betriebssystems auf die Art und Weise bereitstellen, die sie auf das Rack abgelegt wird. 
 
## Kann ich Wartungsmodus für ein bestimmtes Laufwerk auf einem bestimmten Server in "direkte Speicherplätze"-Cluster aktivieren?

Ja, können Sie Speicher Wartungsmodus auf ein bestimmtes Laufwerk und eine bestimmte Fehlerdomäne aktivieren. Der Befehl Enable-StorageMaintenanceMode wird automatisch aufgerufen, wenn Sie einen Knoten anhalten. Sie können es für ein bestimmtes Laufwerk aktivieren, indem Sie den folgenden Befehl ausführen:

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## Werden "direkte Speicherplätze" ist auf Meine Hardware unterstützt?

Es wird empfohlen, dass Sie sich an Ihren Hardwareanbieter, um festzustellen, ob wenden. Hardwareanbietern testen Sie die Lösung auf ihre Hardware und einen Kommentar oder nicht unterstützt wird. Z. B. zum Zeitpunkt der Erstellung dieses Dokuments, Server, z. B. R730 / R730xd / R630, die mehr als 8 Laufwerk Steckplätze verfügen kann SES unterstützen und mit "direkte Speicherplätze" kompatibel sind. Dell unterstützt nur die HBA330 mit "direkte Speicherplätze". R620 SES nicht unterstützt und ist nicht kompatibel mit "direkte Speicherplätze".

Für mehr Hardware Supportinformationen, rufen Sie die folgende Website: Windows Server-Katalog
 
## Wie wird "direkte Speicherplätze" machen SES verwenden?

"Direkte Speicherplätze" verwendet SCSI Enclosure Services (SES) Zuordnung, um Stellen Sie sicher, dass Tafeln von Daten und die Metadaten auf die Fehlerdomänen robustes Weise verteilt wird. Wenn die Hardware SES nicht unterstützt, ist keine Zuordnung von den Gehäusen und die Platzierung von Daten ist nicht robustes.
 
## Welcher Befehl können Sie überprüfen, die physikalische Erweiterung für einen virtuellen Datenträger?
  
Dieses:

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
