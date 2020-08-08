---
ms.assetid: 13210461-1e92-48a1-91a2-c251957ba256
title: Problembehandlung für Firmwareupdates
ms.author: toklima
manager: masriniv
ms.topic: article
author: toklima
ms.date: 04/18/2017
ms.openlocfilehash: b63df280585c4e1d5de88bc8a2ab08cce74c06d7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946223"
---
# <a name="troubleshooting-drive-firmware-updates"></a>Problembehandlung für Firmwareupdates

>Gilt für: Windows 10, Windows Server (halbjährlicher Kanal),

Windows 10, Version 1703 und höher und Windows Server (halbjährlicher Kanal) beinhalten die Möglichkeit, die Firmware von HDDs und SSDs zu aktualisieren, die mit der Firmwareupdate-Erweiterung (zusätzlicher Qualifizierer) über PowerShell zertifiziert wurden.

Weitere Informationen zu diesem Feature finden Sie hier:

- [Aktualisieren der Laufwerkfirmware für in Windows Server 2016](update-firmware.md)
- [Aktualisieren der Laufwerk Firmware ohne Ausfallzeit in direkte Speicherplätze](https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct)

Firmwareupdates können aus verschiedenen Gründen fehlschlagen. Der Zweck dieses Artikels ist die erweiterte Problembehandlung.

  > [!Note]
  > Die Informationen in diesem Artikel sind je nach Problem möglicherweise nicht ausreichend, um alle möglichen Fehlerfälle vollständig zu debuggen.

## <a name="common-issues"></a>Häufige Probleme
In der Architektur basiert diese neue Funktion auf APIs, die im Windows-Speicher Stapel implementiert sind und von PowerShell aufgerufen werden. Der Speicher Stapel stützt sich auf Treiber und Hardware, um in der Branche definierte Befehle ordnungsgemäß zu implementieren. Dies ergibt mehrere Punkte, an denen Fehler auftreten können. Die am häufigsten beobachteten Probleme sind:

1.  Ein bestimmtes Laufwerk implementiert die Industriestandard Befehle nicht ordnungsgemäß (ohne den AQ).
2.  Die APIs, die zum Ausführen des Updates erforderlich sind, sind nicht implementiert oder fehlerhaft (wenn Treiber von Drittanbietern verwendet werden).
3.  Die APIs funktionieren, aber es liegt ein Problem mit der Firmware vor (ungültiges/beschädigtes Image,...).

In den folgenden Abschnitten finden Sie Informationen zur Problembehandlung, abhängig davon, ob Treiber von Microsoft oder Drittanbietern verwendet werden.

## <a name="identifying-inappropriate-hardware"></a>Identifizieren nicht geeigneter Hardware
Die schnellste Methode, um zu ermitteln, ob ein Gerät den richtigen Befehlssatz unterstützt, ist das Starten von PowerShell und das Übergeben eines Datenträgers, der das PhysicalDisk-Objekt darstellt, an das Cmdlet "Get-storagefirmwareinfo". Beispiel:

```powershell
Get-PhysicalDisk -SerialNumber 15140F55976D | Get-StorageFirmwareInformation
```
Und hier ist eine Beispielausgabe:

```
PhysicalDisk          : MSFT_PhysicalDisk (ObjectId = "{1}\\TOKLIMA-DL380\root/Microsoft/Windo...)
SupportsUpdate        : True
NumberOfSlots         : 1
ActiveSlotNumber      : 0
SlotNumber            : {0}
IsSlotWritable        : {True}
FirmwareVersionInSlot : {0013}
```

Das Feld supportsupdate, zumindest für SATA-und nvme-Geräte, gibt an, ob die integrierte PowerShell-Funktionalität zum Aktualisieren der Firmware verwendet werden kann.

Das Feld supportsupdate meldet für SAS-angeschlossene Geräte immer den Wert "true", da die Abfrage der entsprechenden Befehls Unterstützung mit Industriestandard Befehlen nicht möglich ist.

Um zu überprüfen, ob ein SAS-Gerät den erforderlichen Befehlssatz unterstützt, gibt es zwei Optionen:
1.  Probieren Sie es über das Cmdlet "Update-storagefirmware" mit einem geeigneten Firmwareabbild aus, oder
2.  Sehen Sie sich den Windows Server-Katalog an, um zu ermitteln, welche SAS-Geräte erfolgreich das FW-Updatehttps://www.windowsservercatalog.com/)

### <a name="remediation-options"></a>Wiederherstellungsoptionen
Wenn ein bestimmtes Gerät, das Sie testen, den entsprechenden Befehlssatz nicht unterstützt, Fragen Sie entweder den Anbieter ab, um festzustellen, ob eine aktualisierte Firmware verfügbar ist, die den erforderlichen Befehlssatz bereitstellt, oder lesen Sie den Windows Server-Katalog, um Geräte für die Beschaffung zu identifizieren, die den entsprechenden Befehlssatz implementieren

## <a name="troubleshooting-with-3rd-party-drivers-sas"></a>Problembehandlung bei Drittanbieter Treibern (SAS)
Die Softwarekomponenten, die am ehesten mit Hardware interagieren, sind Mini Port Treiber im Windows-Speicher Stapel. Bei einigen Speicher Protokollen, wie z. b. SATA und nvme, stellt Microsoft Native Windows-Treiber bereit. Diese Treiber ermöglichen zusätzliche Debuginformationen. Hardware-und Softwarehersteller von Drittanbietern können allerdings ihre eigenen Mini Port-Treiber für Ihre Geräte schreiben und deren Support Ebene für Debuginformationen variieren.

Um zu ermitteln, was mit dem Firmwaredownload geschehen ist, und APIs zu aktivieren, die über den Speicher Stapel hinaus gesendet werden, überprüfen Sie den folgenden Ereignisprotokoll Kanal:

Ereignisanzeige-Anwendungs-und Dienst Protokolle-Microsoft-Windows-stordiag- **Microsoft-Windows-Storage-Classpnp/Operational**

Dieser Kanal zeichnet Informationen zu den Windows-APIs auf, die an die Mini Port-Treiber gesendet werden, und zu deren Antworten. Beispielsweise wird die unten gezeigte Fehlerbedingung angezeigt, wenn versucht wird, ein Firmwareabbild auf ein SATA-Gerät herunterzuladen, das über einen SAS-HBA verbunden ist, der die erforderliche Übersetzung von SAS in SATA nicht ordnungsgemäß implementiert:

```powershell
Get-PhysicalDisk -SerialNumber 44GS103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
```
Beispiel für die Ausgabe:

```
Update-StorageFirmware : Failed

Extended information:
A warning or error has been encountered during storage firmware update.
Incorrect function.

Activity ID: {1224482b-2315-4a38-81eb-27bb7de19c00}
At line:1 char:47
+ ... S103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.en ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : NotSpecified: (:) [Update-StorageFirmware], CimException
+ FullyQualifiedErrorId : StorageWMI 4,Microsoft.Management.Infrastructure.CimCmdlets.InvokeCimMethodCommand,Update-StorageFirmware
```

PowerShell löst einen Fehler aus und hat die Informationen erhalten, dass die aufgerufene Funktion (d.h. Kernel-API) falsch war. Dies kann bedeuten, dass entweder die API nicht vom Drittanbieter-SAS-Mini Port Treiber (in diesem Fall "true") implementiert wurde oder dass die API aus einem anderen Grund fehlgeschlagen ist, z. b. eine falsche Ausrichtung der Download Segmente.

```
EventData
DeviceGUID  {132EDB55-6BAC-A3A0-C2D5-203C7551D700}
DeviceNumber    1
Vendor  ATA
Model   TOSHIBA THNSNJ12
FirmwareVersion 6101
SerialNumber    44GS103UT5EW
DownLevelIrpStatus  0xc0000185
SrbStatus   132
ScsiStatus  2
SenseKey    5
AdditionalSenseCode 36
AdditionalSenseCodeQualifier    0
CdbByteCount    10
CdbBytes    3B0E0000000001000000
NumberOfRetriesDone 0
```

Das ETW-Ereignis 507 aus dem Kanal zeigt, dass bei einer SCSI-SRB-Anforderung ein Fehler aufgetreten ist, und gibt die zusätzlichen Informationen an, dass senserkey den Wert ' 5 ' (unzulässige Anforderung) aufweist und dass zusätzliche Informationen ' 36 ' (Ungültiges Feld in CDB) waren.

   > [!Note]
   > Diese Informationen werden direkt durch den fraglichen Mini Port bereitgestellt, und die Genauigkeit dieser Informationen hängt von der Implementierung und der Komplexität des Mini Port-Treibers ab.

Es ist möglich, dass unterschiedliche Fehlerzustände dieselben Fehlercodes aufweisen, wenn der Mini Port-Treiber zwischen diesen nicht eindeutig ist. Wenn Sie z. b. versuchen, ein ungültiges Firmwareabbild über einen SAS-HBA auf ein SATA-Gerät herunterzuladen (auf das das Gerät fehlschlägt), werden Sie möglicherweise in denselben Fehlercode übersetzt.

In Fällen, in denen Protokolle gemischt sind und Übersetzungen auftreten, d. h. SATA hinter SAS, empfiehlt es sich, das SATA-Gerät direkt mit einem SATA-Controller zu testen, um es als potenzielles Problem auszuschließen.

### <a name="remediation-options"></a>Wiederherstellungsoptionen
Wenn der Drittanbieter Treiber nicht die erforderlichen APIs oder Übersetzungen implementiert, ist es möglich, entweder an die von Microsoft bereitgestellten Alternativen für SATA (StorAHCI.sys) und nvme (StorNVMe.sys) zu wechseln oder sich an den OEM-oder HBA-Anbieter zu wenden, der den SAS-Treiber bereitgestellt hat, und abzufragen, ob eine neuere Version mit der richtigen Unterstützung vorhanden ist.

## <a name="additional-troubleshooting-with-microsoft-drivers-satanvme"></a>Zusätzliche Problembehandlung bei Microsoft-Treibern (SATA/nvme)
Wenn Windows Native-Treiber, wie z. b. StorAHCI.sys oder StorNVMe.sys, für die Speicherung von Geräten verwendet werden, ist es möglich, während der Firmwareupdates zusätzliche Informationen zu möglichen Fehlern zu erhalten.

Neben dem Classpnp-Betriebskanal protokollieren storahci und stornvme die Protokoll spezifischen Rückgabecodes des Geräts im folgenden etw-Kanal:

Ereignisanzeige-Anwendungs-und Dienst Protokolle-Microsoft-Windows-stordiag- **Microsoft-Windows-Storage-Storport/Diagnose**

Die Diagnoseprotokolle werden standardmäßig nicht angezeigt und können aktiviert/angezeigt werden, indem Sie in EventViewer auf "Ansicht" klicken und im Dropdown Menü "Analyse-und Debugprotokolle anzeigen" auswählen.

Aktivieren Sie zum Erfassen dieser erweiterten Protokolleinträge das Protokoll, reproduzieren Sie den Fehler bei der Firmwareupdate, und speichern Sie das Diagnoseprotokoll.

Im folgenden finden Sie ein Beispiel für ein Firmwareupdate auf einem SATA-Gerät, da das herunter zuladende Image ungültig war (Ereignis-ID: 258):

```
EventData
MiniportName    storahci
MiniportEventId 19
MiniportEventDescription    Firmware Activate Completion
PortNumber  0
Bus 2
Target  0
LUN 0
Irp 0xffff8c84cd45aca0
Srb 0xffffab0024030bc0
Parameter1Name  SrbStatus
Parameter1Value 130
Parameter2Name  ReturnCode
Parameter2Value 0
Parameter3Name  FeaturesReg
Parameter3Value 15
Parameter4Name  SectorCountReg
Parameter4Value 0
Parameter5Name  DriveHeadReg
Parameter5Value 160
Parameter6Name  CommandReg
Parameter6Value 146
Parameter7Name  NULL
Parameter7Value 0
Parameter8Name  NULL
Parameter8Value 0
```

Das obige Ereignis enthält detaillierte Geräteinformationen in den Parameterwerten 2 bis 6. Hier sehen wir verschiedene ATA-Registerwerte. Die ATA-ACS-Spezifikation kann verwendet werden, um die folgenden Werte für den Fehler eines herunterladbaren mikrocodebefehls zu decodieren:
- Rückgabe Code: 0 (0000 0000) (N/v-bedeutungslos, weil keine Nutzlast übertragen wurde)
- Features: 15 (0000 1111) (Bit 1 ist auf "1" festgelegt und gibt "Abort" an)
- Sector count: 0 (0000 0000) (N/v)
- Drivehead: 160 (1010 0000) (N/v – nur veraltete Bits sind festgelegt)
- Befehl: 146 (1001 0010) (Bit 1 ist auf "1" festgelegt, um die Verfügbarkeit von Sense-Daten anzugeben)

Dies weist darauf hin, dass der Firmwareupdate-Vorgang vom Gerät abgebrochen wurde.

Ein ähnliches Maß an Debuginformationen ist in diesem Kanal verfügbar, wenn nvme-Geräte mit dem Windows-systemeigenen nvme-Treiber (StorNVMe.sys) verwendet werden.
