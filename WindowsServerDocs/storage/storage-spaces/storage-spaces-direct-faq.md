---
title: "\"Direkte Speicherplätze\" – häufig gestellte Fragen"
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818911"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>"Direkte Speicherplätze" – häufig gestellte Fragen (FAQ)

Dieser Artikel enthält einige häufige und häufig gestellte Fragen im Zusammenhang mit ["direkte Speicherplätze"](storage-spaces-direct-overview.md).

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>Wenn Sie "direkte Speicherplätze" mit 3 Knoten verwenden, können Sie die Leistung und Kapazität Ebenen abrufen?

Ja, können Sie sowohl eine Leistung und Kapazität in einer 2 oder 3-Knoten "direkte Speicherplätze"-Konfiguration abrufen. Sie müssen jedoch sicherstellen, dass Sie 2 kapazitätsgeräte verfügen. Das bedeutet, dass alle drei Arten von Geräten verwendet werden muss: NVME, SSD und HDD.
 
## <a name="refs-file-system-provides-real-time-tiaring-with-storage-spaces-direct-does-refs-provides-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Refs-Dateisystem bietet in Echtzeit Tiaring mit "direkte Speicherplätze". Bietet REFS dieselbe Funktionalität mit Speicherplätzen mit freigegebenen 2016?

Nein, werden Sie in Echtzeit, horizontale Skalierung mit freigegebenen Speicherplätzen mit 2016 angezeigt. Dies ist nur für "direkte Speicherplätze". 
 
## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>Kann ich ein NTFS-Dateisystem mit "direkte Speicherplätze" verwenden?
  
Ja, können Sie NTFS-Dateisystem mit "direkte Speicherplätze" verwenden. REFS wird jedoch empfohlen. NTFS bietet keine tiering in Echtzeit. 
 
## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>Ich habe es sich um "direkte Speicherplätze" Cluster mit 2 Knoten, konfiguriert, in dem der virtuelle Datenträger als 2-Wege-Spiegelung konfiguriert ist. Wenn ich eine neue Fehlerdomäne hinzufügen, wird die resilienz des vorhandenen virtuellen Datenträgers geändert?

Nachdem Sie die neue Fehlerdomäne hinzugefügt haben, werden die neuen virtuellen Datenträger, die Sie erstellen zu 3-Wege-Spiegelung springen. Die vorhandene virtuelle Datenträger bleiben jedoch einen gespiegelten 2-Wege-Datenträger. Sie können die Daten zu den neuen virtuellen Datenträgern von der vorhandenen Volumes, die Vorteile der neuen resilienz zu erhalten. kopieren.
 
## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-that-says-enable-clusters2d-again-what-should-i-do"></a>Die "direkte Speicherplätze" wurde mit erstellt die autoconfig:0 Schalter und den Pool manuell erstellt. Wenn ich versuche, Fragen den "direkte Speicherplätze" Pool, um ein neues Volume zu erstellen, erhalte ich die Nachricht, die besagt, "Enable-ClusterS2D erneut." Was soll ich tun?

In der Standardeinstellung Wenn Sie "direkte Speicherplätze" konfigurieren, mit dem Cmdlet Enable-S2D bleibt das Cmdlet alles für Sie. Erstellt den Pool und den Ebenen. Wenn Sie Autoconfig:0 verwenden zu können, muss alles manuell ausgeführt werden. Wenn Sie nur den Pool erstellt, wird die Ebene nicht notwendigerweise erstellt. Sie erhalten folgende Fehlermeldung: "Enable-ClusterS2D erneut", wenn Sie entweder nicht auf allen erstellt Ebenen oder Ebenen in einer Weise, die für die angeschlossenen Geräte nicht erstellt haben. Es wird empfohlen, dass Sie nicht die Schalter für die automatische Konfiguration in einer produktionsumgebung verwenden. 
 
## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>Ist es möglich, eine rotierenden Festplatte (HDD) in den "direkte Speicherplätze" Pool hinzufügen, nachdem Sie mit SSD-Geräten "direkte Speicherplätze" erstellt haben?

Nein. Standardmäßig können Sie, wenn Sie den Typ der einzelnen Gerät verwenden, um den Pool zu erstellen, würde es nicht Cache Datenträger konfigurieren und alle Datenträger für die Kapazität eingesetzt werden. Sie können die Konfiguration NVME-Datenträger hinzu, und NVME-Datenträger werden für den Cache konfiguriert werden.
 
## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>Ich habe eine 2-Rack-Fehlerdomäne konfiguriert: RACK 1 hat 2 Fehlerdomänen umfasst, RACK 2 1 Fehlerdomäne. Jeder Server über 4 kapazitätsgeräte 100 GB verfügt. Kann ich alle 1.200 GB Speicherplatz aus dem Pool verwenden?

Nein, können Sie nur 800 GB verwenden. Eine Fehlerdomäne Rack müssen Sie sicherstellen, dass Sie verfügen über eine 2-Wege-Spiegelung-Konfiguration, damit, die jeweils chuck und die doppelte Flächen, die in einem anderen Rack.
 
## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>Was sollten die Cachegröße sein, wenn ich "direkte Speicherplätze" konfiguriert habe?

Der Cache sollte Größe angepasst werden, um den Arbeitssatz sein (die Daten, die aktiv werden gelesen bzw. geschrieben werden zu jedem Zeitpunkt) Ihrer Anwendungen und Workloads.

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>Wie kann ich die Größe des Caches bestimmen, die von "direkte Speicherplätze" verwendet wird?

Verwenden Sie das integrierte Dienstprogramm PerfMon, um die Cachefehler zu überprüfen. Überprüfen Sie die Cachefehler Lesevorgänge/Sekunde aus dem Cluster-Speicherdatenträger für Hybrid-Zähler. Denken Sie daran, dass wenn zu viele Lesevorgänge Cache vorhanden sind, der Cache zu kleinen und empfiehlt es sich um ihn zu erweitern. 
 
## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>Gibt es ein Rechner, der die genaue Größe der Datenträger anzeigt, die reserviert für die Cache-Kapazität und resilienz, die ich besser planen kann festgelegt werden?

Sie können die Speicherrechner Leerzeichen verwenden, bei Ihrer Planung zu helfen. Sie finden Sie unter http://aka.ms/s2dcalc.
 
## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>Was ist die beste Konfiguration, die Sie beim Konfigurieren von 6-Servern und 3 Racks empfehlen würde?

Verwenden Sie 2 Server auf jedem der Racks, um die datenträgerresilienz virtueller eine 3-Wege-Spiegelung zu erhalten. Denken Sie daran, dass die Rack-Konfiguration richtig funktioniert nur, wenn Sie die Konfiguration für das Betriebssystem in die Art und Weise bereitstellen, die sie in der Regal platziert wird. 
 
## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>Kann ich den Wartungsmodus für einen bestimmten Datenträger auf einem bestimmten Server in "direkte Speicherplätze"-Cluster aktivieren?

Ja, können Sie den speicherwartungsmodus für einen bestimmten Datenträger und einer bestimmten Fehlerdomäne aktivieren. Befehls Enable-StorageMaintenanceMode wird automatisch aufgerufen, wenn Sie einen Knoten bewegen. Sie können es für einen bestimmten Datenträger aktivieren, indem Sie den folgenden Befehl ausführen:

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>Werden "direkte Speicherplätze" ist auf die Hardware unterstützt?

Es wird empfohlen, dass Sie wenden Sie sich an Ihren Hardwarehersteller, um Unterstützung zu überprüfen. Hardwarehersteller testen die Projektmappe auf ihrer Hardware und uns mitteilen, ob es oder nicht unterstützt wird. Z. B. zum Zeitpunkt der Erstellung dieses Dokuments, Server, z. B. R730 / R730xd / R630, die mehr als 8 Laufwerk Slots verfügen über SES unterstützen kann und mit "direkte Speicherplätze" kompatibel sind. Dell unterstützt nur die HBA330 mit "direkte Speicherplätze". R620 SES wird nicht unterstützt und ist nicht mit "direkte Speicherplätze" kompatibel.

Für weitere Hardware Supportinformationen Sie, wechseln Sie zu der folgenden Website: Windows Server-Katalog
 
## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>Wie verwenden "direkte Speicherplätze" von SES?

"Direkte Speicherplätze" verwendet SCSI Enclosure Services (SES)-Zuordnung, um sicherzustellen, dass die bereichszuweisungen von Daten und die Metadaten über die Fehlerdomänen auf robuste Weise verteilt. Wenn die Hardware des SES nicht unterstützt, es gibt keine Zuordnung von den Gehäusen und die Platzierung ist nicht stabil.
 
## <a name="what-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>Welcher Befehl können Sie die physikalische Erweiterung für einen virtuellen Datenträger zu überprüfen?
  
Dieses:

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
