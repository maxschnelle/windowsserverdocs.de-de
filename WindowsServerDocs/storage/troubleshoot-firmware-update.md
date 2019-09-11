---
ms.assetid: 13210461-1e92-48a1-91a2-c251957ba256
title: Problembehandlung für Updates der Laufwerkfirmware
ms.prod: windows-server-threshold
ms.author: toklima
ms.manager: masriniv
ms.technology: storage
ms.topic: article
author: toklima
ms.date: 04/18/2017
ms.openlocfilehash: 8283b87e9505b1d3f47ddc823016fbcc7c0c29e6
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867047"
---
# <a name="troubleshooting-drive-firmware-updates"></a>Problembehandlung für Updates der Laufwerkfirmware

>Gilt für: Windows 10, Windows Server (halbjährlicher Kanal),

Version 1703 von Windows 10 und höher sowie Windows Server (Semi-Annual Channel) verfügt über eine Funktion zum Aktualisieren der Firmware von HDDs und SSDs, die mit dem Firmware Upgradeable AQ (Additional Qualifier) per PowerShell zertifiziert wurden.

Weitere Informationen zu diesem Feature finden Sie hier:

- [Aktualisieren der Laufwerks Firmware in Windows Server 2016](update-firmware.md)
- [Aktualisieren der Laufwerk Firmware ohne Ausfallzeit in direkte Speicherplätze](https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct)

Firmwareupdates können aus verschiedenen Gründen fehlschlagen. Dieser Artikel soll Ihnen als Hilfe bei der erweiterten Problembehandlung dienen.

  > [!Note]
  > Je nach Problem kann es sein, dass die Informationen in diesem Artikel nicht ausreichen, um alle möglichen Fehlerfälle zu debuggen.

## <a name="common-issues"></a>Allgemeine Probleme
In Bezug auf die Architektur basiert diese neue Funktion auf APIs, die im Windows-Speicherstapel implementiert sind, der von PowerShell aufgerufen wird. Der Speicherstapel nutzt Treiber und Hardware, um die branchenüblichen Befehle richtig zu implementieren. Dies führt zu mehreren Punkten, an denen Fehler auftreten können. Die am häufigsten beobachteten Probleme sind:

1.  Ein bestimmtes Laufwerk implementiert die branchenüblichen Befehle nicht richtig (AQ nicht vorhanden).
2.  Die APIs, die zum Durchführen des Updates erforderlich sind, werden nicht implementiert oder sind fehlerhaft (bei Verwendung von Treibern von Drittanbietern).
3.  Die APIs funktionieren, aber es liegt ein Problem mit der Firmware selbst vor (ungültig/beschädigtes Image usw.).

Die folgenden Abschnitte enthalten Informationen zur Problembehandlung (unterteilt danach, ob Treiber von Microsoft oder von Drittanbietern verwendet werden).

## <a name="identifying-inappropriate-hardware"></a>Identifizieren falscher Hardware
Die schnellste und einfachste Möglichkeit zur Ermittlung, ob ein Gerät den richtigen Befehlssatz unterstützt, ist das Starten von PowerShell und das Übergeben eines Datenträgers, der das PhysicalDisk-Objekt darstellt, an das Get-StorageFirmwareInfo-Cmdlet. Beispiel:

```powershell
Get-PhysicalDisk -SerialNumber 15140F55976D | Get-StorageFirmwareInformation
```
Dies ist ein Beispiel für eine Ausgabe:

```
PhysicalDisk          : MSFT_PhysicalDisk (ObjectId = "{1}\\TOKLIMA-DL380\root/Microsoft/Windo...)
SupportsUpdate        : True
NumberOfSlots         : 1
ActiveSlotNumber      : 0
SlotNumber            : {0}
IsSlotWritable        : {True}
FirmwareVersionInSlot : {0013}
```

Im Feld „SupportsUpdate“ wird – für SATA- und NVMe-Geräte – angegeben, ob die integrierte PowerShell-Funktionalität zum Aktualisieren der Firmware verwendet werden kann.

Im Feld „SupportsUpdate“ wird für mit SAS verbundene Geräte immer „True“ gemeldet, da das Abfragen der richtigen Befehlsunterstützung mit branchenüblichen Befehlen nicht möglich ist.

Es gibt zwei Optionen, um zu überprüfen, ob ein SAS-Gerät den erforderlichen Befehlssatz unterstützt:
1.  Ausprobieren per Update-StorageFirmware-Cmdlet mit einem passenden Firmwareimage
2.  Sehen Sie sich den Windows Server-Katalog an, um zu ermitteln, welche SAS-Geräte erfolgreich das FW-Update https://www.windowsservercatalog.com/)

### <a name="remediation-options"></a>Lösungsoptionen
Wenn ein bestimmtes zu testendes Gerät den richtigen Befehlssatz nicht unterstützt, können Sie entweder bei Ihrem Anbieter anfragen, ob eine aktualisierte Firmware mit dem erforderlichen Befehlssatz verfügbar ist, oder Sie können mit dem Windows Server-Katalog Geräte ermitteln, die den richtigen Befehlssatz implementieren.

## <a name="troubleshooting-with-3rd-party-drivers-sas"></a>Problembehandlung mit Drittanbietertreibern (SAS)
Die Softwarekomponenten, die am stärksten mit Hardware interagieren, sind Miniport-Treiber im Windows-Speicherstapel. Für einige Speicherprotokolle, z. B. SATA und NVMe, stellt Microsoft native Windows-Treiber bereit. Diese Treiber ermöglichen die Nutzung zusätzlicher Debuginformationen. Drittanbieter von Hardware und Software können für ihre Geräte dagegen eigene Miniport-Treiber schreiben, und die Supportstufe kann für Debuginformationen jeweils variieren.

Nutzen Sie den folgenden Ereignisprotokollkanal, um zu ermitteln, was mit dem Firmwaredownload passiert ist, und unabhängig vom Miniport-Treiber APIs zu aktivieren, die an den Speicherstapel gesendet wurden:

Ereignisanzeige > Anwendungs- und Dienstprotokolle > Microsoft > Windows > StorDiag > **Microsoft-Windows-Storage-ClassPnP/Operational**

Dieser Kanal zeichnet Informationen zu den Windows-APIs, die an die Miniport-Treiber gesendet werden, und deren Antworten auf. Die folgende Fehlerbedingung tritt beispielsweise bei dem Versuch auf, ein Firmwareimage auf ein SATA-Gerät herunterzuladen, das über eine SAS-HBA-Einheit angeschlossen ist, für die die erforderliche Übersetzung von SAS in SATA nicht richtig implementiert wurde:

```powershell
Get-PhysicalDisk -SerialNumber 44GS103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
```
Hier ist ein Beispiel für die Ausgabe angegeben:

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
    
PowerShell löst einen Fehler aus und hat Informationen dazu empfangen, dass die aufgerufene Funktion (Kernel-API) fehlerhaft war. Dies kann bedeuten, dass entweder die API vom SAS-Miniport-Treiber nicht implementiert wurde (hier der Fall), oder für die API aus einem anderen Grund ein Fehler aufgetreten ist, z. B. eine Fehlausrichtung der Downloadsegmente.

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
   > Diese Informationen werden direkt vom betreffenden Miniport bereitgestellt, und die Genauigkeit dieser Informationen hängt von der Implementierung und vom technischen Stand des Miniport-Treibers ab.

Es ist möglich, dass andere Fehlerbedingungen die gleichen Fehlercodes aufweisen, wenn der Miniport-Treiber nicht dazwischen unterscheidet. Beispielsweise kann der Versuch, ein ungültiges Firmwareimage über eine SAS-HBA-Einheit auf ein SATA-Gerät herunterzuladen (wobei der Vorgang für das Gerät voraussichtlich fehlschlägt), ggf. in die gleichen Fehlercodes übersetzt werden.

In Fällen, in denen gemischte Protokolle verwendet und Übersetzungen durchgeführt werden, also bei SATA hinter SAS, ist es am besten, das SATA-Gerät mit einer direkten Verbindung mit einem SATA-Controller zu testen. So kann ausgeschlossen werden, dass dies ein potenzielles Problem darstellt.

### <a name="remediation-options"></a>Lösungsoptionen
Wenn für den Treiber des Drittanbieters ermittelt wird, dass die erforderlichen APIs oder Übersetzungen nicht implementiert werden, kann entweder zu den von Microsoft bereitgestellten Alternativen für SATA (StorAHCI.sys) und NVMe (StorNVMe.sys) gewechselt werden, oder Sie können beim OEM- oder HBA-Anbieter des SAS-Treibers nachfragen, ob eine neuere Version mit der richtigen Unterstützung vorhanden ist.

## <a name="additional-troubleshooting-with-microsoft-drivers-satanvme"></a>Weitere Problembehandlung mit Microsoft-Treiber (SATA/NVMe)
Wenn native Windows-Treiber, z. B. „StorAHCI.sys“ oder „StorNVMe.sys“, für den Betrieb von Speichergeräten verwendet werden, können zusätzliche Informationen zu möglichen Fehlerfällen bei den Aktualisierungsvorgängen für die Firmware abgerufen werden.

Neben dem Classpnp-Betriebskanal protokollieren storahci und stornvme die Protokoll spezifischen Rückgabecodes des Geräts im folgenden etw-Kanal:

Ereignisanzeige > Anwendungs- und Dienstprotokolle > Microsoft > Windows > StorDiag > **Microsoft-Windows-Storage-StorPort/Diagnose**

Die Diagnoseprotokolle werden nicht standardmäßig angezeigt und können aktiviert bzw. angezeigt werden, indem Sie unter EventViewer auf „Ansicht“ klicken und im Dropdownmenü die Option „Analytische und Debugprotokolle einblenden“ wählen.

Um diese erweiterten Protokolleinträge zu sammeln, aktivieren Sie das Protokoll, reproduzieren den Fehler beim Firmwareupdate und speichern das Diagnoseprotokoll.

Im folgenden finden Sie ein Beispiel für ein Firmwareupdate auf einem SATA-Gerät, da das herunter zuladende Image ungültig ist (Ereignis-ID: 258):

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

Das obige Ereignis enthält in den Parameterwerten 2 bis 6 ausführliche Geräteinformationen. Hier sind verschiedene ATA-Registerwerte aufgeführt. Die ATA-ACS-Spezifikation kann zum Decodieren der unten angegebenen Werte in Bezug auf das Fehlschlagen eines Befehls zum Herunterladen von Microcode (Download Microcode) verwendet werden:
- Rückgabe Code: 0 (0000 0000) (N/v-bedeutungslos, weil keine Nutzlast übertragen wurde)
- Features: 15 (0000 1111) (Bit 1 ist auf "1" festgelegt und gibt "Abort" an)
- Sector count: 0 (0000 0000) (N/V)
- Drivehead: 160 (1010 0000) (N/v – nur veraltete Bits sind festgelegt)
- S 146 (1001 0010) (Bit 1 ist auf ' 1 ' festgelegt, um die Verfügbarkeit von Sense-Daten anzugeben)

Hier erfahren wir, dass der Vorgang zur Aktualisierung der Firmware vom Gerät abgebrochen wurde.

In diesem Kanal ist eine ähnliche Menge von Debuginformationen verfügbar, wenn NVMe-Geräte mit dem nativen Windows-NVMe-Treiber (StorNVMe.sys) verwendet werden.
