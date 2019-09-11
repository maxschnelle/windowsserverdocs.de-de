---
title: 'Direkte Speicherplätze: häufig gestellte Fragen'
description: Weitere Informationen zu direkte Speicherplätze
keywords: Speicherplätze
ms.prod: windows-server-threshold
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1aafac9a994e907e8b8ee3b556618d630cdf8418
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872066"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>Direkte Speicherplätze: häufig gestellte Fragen (FAQ)

In diesem Artikel werden einige häufige und häufig gestellte Fragen im Zusammenhang mit [direkte Speicherplätze](storage-spaces-direct-overview.md)aufgeführt.

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>Wenn Sie direkte Speicherplätze mit drei Knoten verwenden, können Sie sowohl Leistungs-als auch Kapazitäts Ebenen erhalten?

Ja, Sie können eine Leistungs-und Kapazitäts Ebene in einer direkte Speicherplätze Konfiguration mit zwei oder drei Knoten erhalten. Sie müssen jedoch sicherstellen, dass Sie über zwei Kapazitäts Geräte verfügen. Dies bedeutet, dass Sie alle drei Arten von Geräten verwenden müssen: Nvme, SSD und HDD.
 
## <a name="refs-file-system-provides-real-time-tiaring-with-storage-spaces-direct-does-refs-provides-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Das Refs-Dateisystem ermöglicht das tiaring in Echtzeit mit direkte Speicherplätze. Bietet Refs die gleiche Funktionalität wie für freigegebene Speicherplätze in 2016?

Nein, Sie erhalten keine Echt Zeit Tiering mit freigegebenen Speicherplätzen mit 2016. Dies gilt nur für direkte Speicherplätze. 
 
## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>Kann ich ein NTFS-Dateisystem mit direkte Speicherplätze verwenden?
  
Ja, Sie können das NTFS-Dateisystem mit direkte Speicherplätze verwenden. Refs wird jedoch empfohlen. NTFS bietet kein Echt Zeit Tiering. 
 
## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>Ich habe zwei Knoten direkte Speicherplätze Cluster konfiguriert, wobei der virtuelle Datenträger als bidirektionale Spiegelung konfiguriert ist. Wird die Resilienz der vorhandenen virtuellen Datenträger geändert, wenn ich eine neue Fehler Domäne hinzufüge?

Nachdem Sie die neue Fehler Domäne hinzugefügt haben, werden die neuen virtuellen Datenträger, die Sie erstellen, in die 3-Wege-Spiegelung springen. Allerdings bleibt die vorhandene virtuelle Festplatte ein Datenträger mit 2-Wege-Spiegelung. Sie können die Daten aus den vorhandenen Volumes auf die neuen virtuellen Datenträger kopieren, um die Vorteile der neuen Resilienz zu erhalten.
 
## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-that-says-enable-clusters2d-again-what-should-i-do"></a>Der direkte Speicherplätze wurde mithilfe von AutoConfig: 0 erstellt. und der Pool manuell erstellt. Wenn ich versuche, den direkte Speicherplätze Pool abzufragen, um ein neues Volume zu erstellen, erhalte ich eine Meldung, die besagt, dass "Enable-ClusterS2D Again" lautet. Was soll ich tun?

Wenn Sie direkte Speicherplätze mithilfe des Cmdlets "Enable-S2D" konfigurieren, führt das Cmdlet standardmäßig alles für Sie aus. Der Pool und die Ebenen werden erstellt. Bei Verwendung von AutoConfig: 0 muss alles manuell erfolgen. Wenn Sie nur den Pool erstellt haben, wird die Ebene nicht notwendigerweise erstellt. Sie erhalten die Fehlermeldung "Enable-ClusterS2D Again", wenn Sie keine Ebenen auf allen oder nicht erstellten Ebenen auf eine Weise erstellt haben, die den angefügten Geräten entspricht. Es wird empfohlen, den AutoConfig-Switch nicht in einer Produktionsumgebung zu verwenden. 
 
## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>Ist es möglich, einen spindatenträger (HDD) zum direkte Speicherplätze Pool hinzuzufügen, nachdem Sie direkte Speicherplätze mit SSD-Geräten erstellt haben?

Nein. Wenn Sie zum Erstellen des Pools den einzelnen Gerätetyp verwenden, werden standardmäßig keine Cache Datenträger konfiguriert, und alle Datenträger werden für die Kapazität verwendet. Sie können nvme-Datenträger zur Konfiguration hinzufügen, und nvme-Datenträger werden für den Cache konfiguriert.
 
## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>Ich habe eine 2-Rack-Fehler Domäne konfiguriert: Rack 1 hat zwei Fehler Domänen, Rack 2 hat eine Fehler Domäne. Jeder Server verfügt über vier Kapazität 100 GB-Geräte. Kann ich alle 1.200 GB Speicherplatz aus dem Pool verwenden?

Nein, Sie können nur 800 GB verwenden. In einer rackfehlerdomäne müssen Sie sicherstellen, dass Sie über eine Konfiguration mit zwei-Wege-Spiegelung verfügen, damit jeder Chuck und seine doppelten Flächen in einem anderen Gestell werden.
 
## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>Was sollte die Cache Größe sein, wenn ich direkte Speicherplätze konfiguriere?

Der Cache sollte Größe aufweisen, um das Workingset (die Daten, die zu einem beliebigen Zeitpunkt aktiv gelesen oder geschrieben werden) Ihrer Anwendungen und Arbeits Auslastungen zu berücksichtigen.

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>Wie kann ich die Größe des Caches ermitteln, die von direkte Speicherplätze verwendet wird?

Verwenden Sie das integrierte Hilfsprogramm Perfmon, um die Cache Fehler zu überprüfen. Überprüfen Sie die Cache-fehllese Vorgänge/Sek. im Cluster Speicher-Hybrid Datenträger. Beachten Sie Folgendes: Wenn der Cache zu viele Lesevorgänge fehlt, ist der Cache unter skaliert, und Sie können ihn erweitern. 
 
## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>Gibt es einen Rechner, der die genaue Größe der Datenträger anzeigt, die für den Cache, die Kapazität und die Resilienz reserviert werden, sodass ich besser planen kann?

Sie können den Speicherplatz Rechner verwenden, um Sie bei der Planung zu unterstützen. Es ist unter http://aka.ms/s2dcalc verfügbar.
 
## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>Was ist die beste Konfiguration, die Sie beim Konfigurieren von 6 Servern und 3 Racks empfehlen sollten?

Verwenden Sie für jeden der Racks 2 Server, um die Resilienz virtueller Datenträger für eine 3-Wege-Spiegelung zu erzielen. Beachten Sie, dass die Rack-Konfiguration nur dann ordnungsgemäß funktioniert, wenn Sie die Konfiguration dem Betriebssystem in der Art und Weise bereitstellen, in der Sie auf dem Rack platziert ist. 
 
## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>Kann ich den Wartungsmodus für einen bestimmten Datenträger auf einem bestimmten Server in direkte Speicherplätze Cluster aktivieren?

Ja, Sie können den Speicher Wartungsmodus für einen bestimmten Datenträger und eine bestimmte Fehler Domäne aktivieren. Der Befehl enable-storagemaintenancemode wird automatisch aufgerufen, wenn Sie einen Knoten anhalten. Sie können Sie für einen bestimmten Datenträger aktivieren, indem Sie den folgenden Befehl ausführen:

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>Wird direkte Speicherplätze auf meiner Hardware unterstützt?

Wir empfehlen, dass Sie sich an Ihren Hardwarehersteller wenden, um den Support zu überprüfen Hardware Anbieter testen die Lösung auf Ihrer Hardware und kommentieren, ob Sie unterstützt wird. Zum Zeitpunkt der Erstellung dieses Dokuments können z. b. Server wie R730/R730xd/R630, die über mehr als 8 Laufwerk Slots verfügen, SES unterstützen und mit direkte Speicherplätze kompatibel sein. Dell unterstützt nur die HBA330 mit direkte Speicherplätze. R620 unterstützt keine SES und ist nicht mit direkte Speicherplätze kompatibel.

Weitere Informationen zur Hardwareunterstützung finden Sie auf der folgenden Website: Windows Server-Katalog
 
## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>Wie nutzt direkte Speicherplätze die Verwendung von SES?

Direkte Speicherplätze verwendet die SCSI-Gehäuse Dienste (SES), um sicherzustellen, dass Daten-und Metadatenbereiche auf robuste Weise auf die Fehler Domänen verteilt werden. Wenn die Hardware keine SES unterstützt, gibt es keine Zuordnung der Gehäuse, und die Daten Platzierung ist nicht stabil.
 
## <a name="what-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>Welchen Befehl können Sie verwenden, um den physischen Umfang eines virtuellen Datenträgers zu überprüfen?
  
Dieses:

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
