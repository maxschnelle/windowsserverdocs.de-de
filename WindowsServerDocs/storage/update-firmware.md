---
ms.assetid: e5945bae-4a33-487c-a019-92a69db8cf6c
title: Aktualisieren der Firmware
ms.prod: windows-server
ms.author: toklima
manager: dmoss
ms.technology: storage-spaces
ms.topic: article
author: toklima
ms.date: 10/04/2016
ms.openlocfilehash: 0e117b486fd628397bfe36aa897ff64cdd26f98b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965832"
---
# <a name="updating-drive-firmware"></a>Aktualisieren der Firmware
>Gilt für: Windows Server 2019, Windows Server 2016, Windows 10

Das Aktualisieren der Firmware für Laufwerke war bisher eine mühsame Aufgabe mit einem Ausfall Potenzial. aus diesem Grund verbessern wir die Speicherplätze, Windows Server und Windows 10, Version 1703 und neuer. Wenn Sie über Laufwerke verfügen, die den neuen, in Windows enthaltenen firmwareupdateimechanismus unterstützen, können Sie die Laufwerk Firmware von Produktions Laufwerken ohne Ausfallzeiten aktualisieren. Wenn Sie jedoch die Firmware eines Produktions Laufwerks aktualisieren möchten, lesen Sie unbedingt unsere Tipps, wie Sie das Risiko minimieren, indem Sie diese leistungsfähige neue Funktionalität nutzen.

  > [!Warning]
  > Firmwareupdates sind ein potenziell risikoreicher Wartungsvorgang, und Sie sollten sie nur nach gründlicher Überprüfung des neuen Firmwareabbilds anwenden. Es ist möglich, dass sich neue Firmware auf nicht unterstützter Hardware negativ auf die Zuverlässigkeit und Stabilität auswirken kann oder sogar zu Datenverlust führen kann. Administratoren sollten die Versionsanmerkungen zu einem gegebenen Update lesen, um dessen Auswirkungen und Anwendbarkeit zu bestimmen.

## <a name="drive-compatibility"></a>Laufwerkkompatibilität

Sie müssen über unterstützte Laufwerke verfügen, um Windows Server zum Aktualisieren von Laufwerkfirmware zu verwenden. Um häufiges Geräteverhalten zu gewährleisten, haben wir zunächst neue und-für Windows 10-und Windows Server 2016-optionale HLK-Anforderungen (Hardware Lab Kit) für SAS-, SATA-und nvme-Geräte definiert. Diese Anforderungen geben an, welche Befehle ein SATA-, SAS- oder NVMe-Gerät unterstützen muss, um mithilfe dieser neuen in Windows vorhandenen PowerShell-Cmdlets aktualisiert werden zu können. Für die Unterstützung dieser Anforderungen gibt es eine neue HLK-Prüfung, um zu überprüfen, ob Herstellerprodukte den richtigen Befehl unterstützen, und um sie in zukünftigen Revisionen zu implementieren. 

Wenden Sie sich an Ihren Lösungsanbieter, um Informationen darüber zu erhalten, ob Ihre Hardware unterstützt, dass Windows die Laufwerkfirmware aktualisiert.
Im Folgenden sind Links zu den verschiedenen Anforderungen aufgelistet:

-   SATA: [Device.Storage.Hd.Sata](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v=ws.11)#devicestoragehdsata) – im Abschnitt **[falls implementiert\] Firmware Download & Activate (Download und Aktivierung der Firmware)**
    
-   SAS: [Device.Storage.Hd.Sas](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v=ws.11)#devicestoragehdsas) – im Abschnitt **[falls implementiert\]Firmware Download & Activate (Download und Aktivierung der Firmware)**

-   NVMe: [Device.Storage.ControllerDrive.NVMe](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v=ws.11)#devicestoragecontrollerdrivenvme) – in den Abschnitten **5.7** und **5.8**

## <a name="powershell-cmdlets"></a>PowerShell-Cmdlets

Die beiden Cmdlets, die zu Windows hinzugefügt werden, sind:

-   Get-StorageFirmwareInformation
-   Update-StorageFirmware

Das erste Cmdlet bietet ausführliche Informationen zu den Funktionen des Geräts, firmwareimages und Revisionen. In diesem Fall enthält der Computer nur ein einzelnes SATA-SSD mit einem Firmwareslot. Ein Beispiel:

   ```powershell
   Get-PhysicalDisk | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E16101}
   ```

Beachten Sie, dass SAS-Geräte "supportsupdate" immer als "true" melden, da es keine Möglichkeit gibt, das Gerät explizit auf die Unterstützung dieser Befehle abzufragen.

Das zweit Cmdlet, „Update-StorageFirmware“ erlaubt den Administratoren, die Laufwerkfirmware mit einer Imagedatei zu aktualisieren, wenn das Laufwerk den neuen Firmwareupdatemechanismus unterstützt. Sie sollten diese Imagedatei direkt vom Originalgerätehersteller (OEM) oder dem Hersteller des Laufwerks anfordern.

  > [!Note]
  > Bevor Sie eine in der Produktion eingesetzte Hardware aktualisieren, testen Sie das Firmwareupdate auf einer identischen Hardware in einer Testumgebung.

Das Laufwerk lädt zunächst das neue Firmwareimage in einen internen Staging-Bereich. Währenddessen wird E/A normalerweise fortgesetzt. Das Image wird nach dem Download aktiviert. Während dieses Zeitraums kann das Laufwerk nicht auf E/A-Befehle reagieren, da eine interne Zurücksetzung erfolgt. Dies bedeutet, dass das Laufwerk keine Daten während der Aktivierung zur Verfügung stellt. Eine Anwendung, die auf diesem Laufwerk auf Daten zugreift, muss auf eine Antwort warten, bis die Aktivierung der Firmware abgeschlossen ist. Im folgenden finden Sie ein Beispiel für das Cmdlet in Aktion:

   ```powershell 
   $pd | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
   $pd | Get-StorageFirmwareInformation

   SupportsUpdate        : True
   NumberOfSlots         : 1
   ActiveSlotNumber      : 0
   SlotNumber            : {0}
   IsSlotWritable        : {True}
   FirmwareVersionInSlot : {J3E160@3}
   ```

Laufwerke schließen normalerweise keine E/A-Einforderungen ab, wenn ein neues Firmwareimage aktiviert wird. Wie lange dauert, ein Laufwerk aktivieren, hängt von dem Entwurf und der Firmware aktualisiert werden. Erfahrungsgemäß reicht der Updatezeitraum von weniger als 5 Sekunden bis über 30 Sekunden.

Dieses Laufwerk hat das Firmwareupdate innerhalb von ungefähr 5,8 Sekunden abgeschlossen, wie hier gezeigt wird:

```powershell 
Measure-Command {$pd | Update-StorageFirmware -ImagePath C:\\Firmware\\J3E16101.enc -SlotNumber 0}

 Days : 0
 Hours : 0
 Minutes : 0
 Seconds : 5
 Milliseconds : 791
 Ticks : 57913910
 TotalDays : 6.70299884259259E-05
 TotalHours : 0.00160871972222222
 TotalMinutes : 0.0965231833333333
 TotalSeconds : 5.791391
 TotalMilliseconds : 5791.391
 ```

## <a name="updating-drives-in-production"></a>Aktualisieren von Laufwerken im Produktivbetrieb

Bevor Sie einen Server in den Produktivbetrieb versetzen, wird empfohlen, dass Sie die Firmware Ihrer Laufwerke auf die Firmware aktualisieren, die vom Anbieter der Computerhardware oder dem OEM empfohlen wurde, der Ihnen Ihre Speicherlösung (Speichergehäuse, Laufwerke und Server) verkauft hat und diese unterstützt.

Sobald sich ein Server in der Produktion befindet, empfiehlt es sich, möglichst wenige Änderungen am Server vorzunehmen. Jedoch kann es vorkommen, dass der Verkäufer Ihrer Projektmappe Ihnen rät, ein wichtiges Firmwareupdate für Ihre Laufwerke zu installieren. In diesem Fall sind hier einige gute Vorgehensweisen vorgestellt, die Sie anwenden können, bevor Sie Firmwareupdates für Ihre Laufwerke installieren:

1. Lesen Sie die Anmerkungen zu dieser Version, und vergewissern Sie sich, dass das Update Probleme behandelt, die sich auf Ihre Umgebung auswirken können, und dass die Firmware keine bekannten Probleme enthält, die sich negativ auf Sie auswirken könnten.

2. Installieren Sie die Firmware auf einem Server in Ihrer Testumgebung, die über identische Laufwerke verfügt (einschließlich der Revision des Laufwerks, falls mehrere Revisionen desselben Laufwerks existieren), und testen Sie das Laufwerk unter Last mit der neuen Firmware. Informationen über die Ausführung synthetischer Auslastungstests finden Sie unter [Testen von Speicherplätzen mit synthetischen Arbeitslasten mit Windows Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn894707(v=ws.11)).

## <a name="automated-firmware-updates-with-storage-spaces-direct"></a>Automatische Firmwareupdates mit „Direkte Speicherplätze“

Windows Server 2016 enthält einen Zustandsdienst für Bereitstellungen von „Direkte Speicherplätze“ (einschließlich Microsoft Azure Stack-Lösungen). Der Hauptzweck des Zustandsdiensts ist es, die Überwachung und die Verwaltung Ihrer Hardwarebereitstellung zu erleichtern. Als Teil der Verwaltungsfunktionen bietet er die Möglichkeit, Laufwerksfirmware auf allen Knoten des Cluster zu installieren, ohne Workloads offline zu schalten oder Ausfallzeiten zu verursachen. Diese Funktion ist Richtlinien gesteuert, mit dem Steuerelement in den Händen des Administrators.

Die Verwendung des Zustandsdiensts, um Firmware auf einem Cluster zu installieren, ist sehr einfach. Sie müssen die folgenden Schritte durchführen:

-   Überlegen Sie, welche HDD- und SSD-Laufwerke Teil Ihres Clusters „Direkte Speicherplätze“ sein sollen, und ob die Laufwerke unterstützen, dass Windows Firmwareupdates ausführt.
-   Listen Sie diese Laufwerke in der XML-Datei der unterstützen Komponenten auf.
-   Identifizieren Sie die Firmwareversionen, die diese Laufwerke in der XML-Datei der unterstützten Laufwerke besitzen sollen (einschließlich den Pfad der Firmwareimages).
-   Hochladen der XML-Datei in die Clusterdatenbank

An diesem Punkt überprüft und analysiert der Zustandsdienst die XML-Datei, und identifiziert Laufwerke, die nicht die gewünschte Firmwareversion bereitgestellt haben. Anschließend werden Knoten für Knoten die E/A-Anforderungen so umgeleitet, dass sie die betroffenen Laufwerke nicht erreichen und deren Firmware aktualisiert werden kann. Ein „Direkte Speicherplätze“-Cluster erreicht Resilienz, indem er Daten auf mehrere Serverknoten aufteilt. Der Zustandsdienst kann einen gesamten Knoten mit vielen Laufwerken für Updates isolieren. Sobald ein Update für einen Knoten ausgeführt wird, wird eine Reparatur in „Speicherplätze“ ausgelöst. Alle Kopien von Daten im Cluster werden wieder miteinander synchronisiert, bevor mit dem nächsten Knoten fortgefahren wird. Für „Speicherplätze“ ist es während des Roll-out-Vorgangs normal, sich in einen „heruntergestuften“ Betriebsmodus zu versetzen, und dies wird auch erwartet.

Um eine stabile Installation und genügend Zeit für die Überprüfung des Firmwareimages zu garantieren, gibt es eine Verzögerung zwischen den Updates verschiedener Server Standardmäßig wartet der Integritätsdienst 7 Tage, bevor der 2<sup>.</sup> Server aktualisiert wird. Alle nachfolgenden Server (3<sup>.</sup>4<sup>.</sup>,...) werden mit einer Verzögerung von 1 Tag aktualisiert. Ist ein Administrator der Meinung, dass die Firmware instabil ist oder in einer anderen Weise unerwünscht, kann er/sie die weitere Installation durch den Zustandsdienst jederzeit stoppen. Wenn die Firmware zuvor überprüft wurde und eine schnellere Installation gewünscht ist, können die Standardwerte von Tagen zu Stunden oder Minuten angepasst werden.

Hier ist ein Beispiel der unterstützten Komponente XML für einen allgemeinen „Direkte Speicherplätze“-Cluster:

```xml
 <Components>
     <Disks>
        <Disk>
            <Manufacturer>Contoso</Manufacturer>
            <Model>XYZ9000</Model>
            <AllowedFirmware>
              <Version>2.0</Version>
              <Version>2.1>/Version>
              <Version>2.2</Version>
            </AllowedFirmware>
            <TargetFirmware>
              <Version>2.2</Version>
              <BinaryPath>\\path\to\image.bin</BinaryPath>
            </TargetFirmware>
        </Disk>
        ...
        ...
    </Disks>
 </Components>
```

Laden Sie einfach die XML-Datei in die Clusterdatenbank hoch, damit die Installation der neuen Firmware in diesem „Direkte Speicherplätze“-Cluster gestartet wird.

```powershell
$SpacesDirect = Get-StorageSubSystem Clus*

$CurrentDoc = $SpacesDirect | Get-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document"

$CurrentDoc.Value | Out-File <Path>
```

Bearbeiten Sie die Datei in einem beliebigen Editor, wie z.B. Visual Studio Code oder Notepad, und speichern Sie sie anschließend.

```powershell
$NewDoc = Get-Content <Path> | Out-String

$SpacesDirect | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $NewDoc
```

Wenn Sie die Integritätsdienst in Aktion sehen möchten, und weitere Informationen zum Rollout Mechanismus erhalten, sehen Sie sich dieses Video an:https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Siehe auch [Problembehandlung Laufwerks](troubleshoot-firmware-update.md)-Firmwareupdates.

### <a name="will-this-work-on-any-storage-device"></a>Arbeitet es auf jedem Speichergerät?

Es arbeitet auf Speichergeräten, die die richtigen Befehle in ihrer Firmware implementieren. Das Cmdlet "Get-storagefirmwareinformation" zeigt an, ob die Firmware eines Laufwerks die korrekten Befehle (für SATA/nvme) tatsächlich unterstützt, und der HLK-Test ermöglicht es Anbietern und OEMs, dieses Verhalten zu testen.

### <a name="after-i-update-a-sata-drive-it-reports-to-no-longer-support-the-update-mechanism-is-something-wrong-with-the-drive"></a>Nach dem Update eines SATA-Laufwerks erscheint ein Bericht, in dem angegeben ist, dass das Laufwerk den Updatemechanismus nicht länger unterstützt. Gibt es ein Problem mit dem Laufwerk?

Nein, das Laufwerk ist in Ordnung, es sei denn, die neue Firmware lässt Updates nicht mehr zu. Es wird ein bekanntes Problem auftreten, bei dem eine zwischengespeicherte Version der Laufwerk Funktionen falsch ist. Wenn Sie "Update-storageprovidercache-discoverylevel Full" ausführen, werden die Laufwerks Funktionen erneut aufgelistet und die zwischengespeicherte Kopie aktualisiert. Zur Problemumgehung wird empfohlen, den oben genannten Befehl auszuführen, bevor Sie ein Firmwareupdate oder eine komplette Installation auf einen „Direkte Speicherplätze“-Cluster initiieren.

### <a name="can-i-update-firmware-on-my-san-through-this-mechanism"></a>Kann ich Firmware auf meinen SAN mit diesem Mechanismus aktualisieren?
Nein. In der Regel verfügen SANs nicht über eigene Hilfsprogramme und Schnittstellen für Wartungsvorgänge dieser Art. Dieser neue Mechanismus ist für direkt zugeordneten Speicher konzipiert, z.B. für SATA, SAS oder NVMe-Geräte.

### <a name="from-where-do-i-get-the-firmware-image"></a>Wo erhalte ich das Firmwareabbild?

Sie sollten jede Firmware immer direkt von Ihrem OEM, Lösungsanbieter oder Hersteller des Laufwerks anfordern und sie nicht von Drittanbietern herunterladen. Windows stellt den Mechanismus bereit, um das Image für das Laufwerk zu erhalten, kann aber dessen Integrität nicht verifizieren.

### <a name="will-this-work-on-clustered-drives"></a>Funktioniert dies auf gruppierten Laufwerken?

Die Cmdlets können ihre Funktion ebenso auf gruppierten Laufwerken ausführen, bedenken Sie jedoch, dass die Orchestrierung des Zustandsdiensts die E/A-Auswirkung auf laufenden Downloads verringert. Wenn die Cmdlets direkt auf gruppierten Laufwerke verwendet werden, findet keine E/A mehr statt. Generell ist die beste Empfehlung, die Updates der Laufwerkfirmware durchzuführen, wenn keine oder nur eine minimale Workload für die zugrunde liegenden Geräte vorliegt.

### <a name="what-happens-when-i-update-firmware-on-storage-spaces"></a>Was geschieht, wenn ich die Firmware auf Speicherplätzen aktualisiere?

Sie können diesen Vorgang auf Windows Server 2016 mit auf „Direkte Speicherplätze“ bereitgestelltem Zustandsdienst durchführen, ohne dass Sie Ihre Workloads offline schalten müssen, vorausgesetzt, die Laufwerke unterstützen die Firmwareupdates durch Windows Server.

### <a name="what-happens-if-the-update-fails"></a>Was geschieht, wenn das Update fehlschlägt?

Das Update kann aus verschiedenen Gründen fehlschlagen, einige davon sind: 1) das Laufwerk unterstützt die korrekten Befehle für Windows zum Aktualisieren der Firmware nicht. In diesem Fall wird das neue Firmwareimage nie aktiviert, und das Laufwerk arbeitet weiterhin mit dem alten Image. 2) Das Image kann nicht heruntergeladen werden oder auf diesem Laufwerk angewendet werden (Versionskonflikt, beschädigtes Image,...). In diesem Fall kann das Laufwerk den Befehl zum Aktivieren nicht ausführen. In diesem Fall wird weiterhin mit dem alten Firmwareimage gearbeitet.

Wenn das Laufwerk nach einem Firmwareupdate gar nicht reagiert, weist möglicherweise die Laufwerkfirmware selbst einen Bug auf. Testen Sie alle Firmwareupdates in einer Testumgebung vor dem Einfügen in die Produktionsumgebung. Die einzige Lösung kann sein, das Laufwerk auszutauschen.

Weitere Informationen finden Sie unter [Problembehandlung bei Laufwerks Firmware-Updates](troubleshoot-firmware-update.md).

### <a name="how-do-i-stop-an-in-progress-firmware-roll-out"></a>Wie verhindere ich die Installation einer sich in Bearbeitung befindlichen Firmware?

Deaktivieren Sie die Installation in PowerShell über:
```powershell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled" -Value false
```

### <a name="i-am-seeing-an-access-denied-or-path-not-found-error-during-roll-out-how-do-i-fix-this"></a>Beim Rollout sehe ich den Fehler "Zugriff verweigert" oder "Pfad nicht gefunden". Gewusst wie beheben

Stellen Sie sicher, dass das für das Update gewünschte Firmwareimage über alle Clusterknoten zugänglich ist. Die einfachste Möglichkeit ist es, das Image auf einem freigegebenen Clustervolume zu platzieren.
