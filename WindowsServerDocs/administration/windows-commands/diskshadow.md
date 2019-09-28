---
title: diskshadow
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d9f34377473608d71ce7753972e5312d9eea0f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377767"
---
# <a name="diskshadow"></a>diskshadow

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

"DiskShadow. exe" ist ein Tool, das die vom Volumeschattenkopie-Dienst angebotene Funktionalität \(vss @ no__t-1 verfügbar macht. Standardmäßig verwendet DiskShadow einen interaktiven Befehls Interpreter ähnlich dem von Diskraid oder DiskPart. DiskShadow enthält auch einen Skript fähigen Modus.  
  
> [!NOTE]  
> Sie müssen mindestens Mitglied der lokalen Gruppe Administratoren oder einer entsprechenden Gruppe sein, um DiskShadow ausführen zu können.  
  
Beispiele für die Verwendung von DiskShadow-Befehlen finden Sie unter [Beispiele](#BKMK_examples).  
  
## <a name="syntax"></a>Syntax  
Geben Sie für den interaktiven Modus Folgendes an der Eingabeaufforderung ein, um den DiskShadow-Befehls Interpreter zu starten:  
  
```  
diskshadow  
```  
  
Geben Sie im Skript Modus Folgendes ein, wobei *Skript. txt* eine Skriptdatei mit DiskShadow-Befehlen ist:  
  
```  
diskshadow -s script.txt  
```  
  
## <a name="diskshadow-commands"></a>DiskShadow-Befehle  
Sie können die folgenden Befehle im DiskShadow-Befehls Interpreter oder über eine Skriptdatei ausführen:  
  
|Parameter|Beschreibung|  
|-------|--------|  
|[set_2](set_2.md)|Legt den Kontext, die Optionen, den ausführlichen Modus und die Metadatendatei zum Erstellen von Schatten Kopien fest.|  
|[Wiederherstellung simulieren](simulate-restore.md)|Testet die Beteiligung von Writer in Wiederherstellungs Sitzungen auf dem Computer ohne Ausgabe von **vorab** -oder **postrestore** -Ereignissen an Writer.|  
|[Metadaten laden](load-metadata.md)|Lädt eine Datei "Metadata. cab" vor dem Importieren einer austauschen-Schatten Kopie oder lädt die Writer-Metadaten im Fall einer Wiederherstellung.|  
|[Maschine](writer.md)|Überprüft, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren enthält bzw. schließt.|  
|[add_1](add_1.md)|Fügt Volumes zu dem Satz von Volumes hinzu, die als Schatten kopiert werden sollen, oder fügt der Alias Umgebung Aliase hinzu.|  
|[create_1](create_1.md)|startet den Vorgang zum Erstellen von Schatten Kopien mithilfe der aktuellen Kontext-und Options Einstellungen.|  
|[Exec](exec.md)|führt eine Datei auf dem lokalen Computer aus.|  
|[Sicherung starten](begin-backup.md)|startet eine vollständige Sicherungs Sitzung.|  
|[Sicherung beenden](end-backup.md)|Beendet eine vollständige Sicherungs Sitzung und gibt ggf. ein **BackupComplete** -Ereignis mit dem entsprechenden Writer-Status aus.|  
|[Wiederherstellung starten](begin-restore.md)|startet eine Wiederherstellungs Sitzung und gibt ein **vorab** Ereignis für beteiligte Writer aus.|  
|[Wiederherstellung beenden](end-restore.md)|Beendet eine Wiederherstellungs Sitzung und gibt ein **postrestore** -Ereignis für beteiligte Writer aus.|  
|[Festlegen](reset.md)|setzt DiskShadow auf den Standardzustand zurück.|  
|[List](list.md)|Listet Writer, Schatten Kopien oder derzeit registrierte Schattenkopieanbieter auf, die sich auf dem System befinden.|  
|[Schatten löschen](delete-shadows.md)|Löscht Schatten Kopien.|  
|[import](import.md)|importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.|  
|[chel](mask.md)|entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.|  
|[sichtbar](expose.md)|macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.|  
|[Heben des](unexpose.md)|macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde.|  
|[break_2](break_2.md)|Trennt ein Schattenkopievolume von VSS.|  
|[umzukehren](revert.md)|setzt ein Volume auf eine angegebene Schatten Kopie zurück.|  
|[exit_1](exit_1.md)|beendet DiskShadow.|  
  
## <a name="remarks"></a>Hinweise  
  
-   zum Erstellen einer Schatten Kopie sind mindestens " **Add** " und " **Create** " erforderlich. Dadurch wird jedoch der Kontext und die Options Einstellungen, eine Kopiesicherung, erstellt, und es wird nur eine Schatten Kopie ohne Sicherungs Ausführungs Skript erstellt.  
  
## <a name="BKMK_examples"></a>Beispiele  
Dies ist eine Beispiel Sequenz von Befehlen, mit denen eine Schatten Kopie für die Sicherung erstellt wird. Sie kann in der Datei als Script. DSH gespeichert und mit DiskShadow \/s Skript. DSH ausgeführt werden.  
  
Nehmen Sie Folgendes an:  
  
-   Sie verfügen über ein vorhandenes Verzeichnis mit dem Namen "c: \\diskshadowdata".  
  
-   Ihr System Volume ist "C:" und das Daten Volume "d:".  
  
-   Sie verfügen über eine backupscript. cmd-Datei in c: \\diskshadowdata.  
  
-   Die Datei "backupscript. cmd" führt die Kopie der Schatten Daten p: und q: auf Ihrem Sicherungs Laufwerk aus.  
  
Sie können diese Befehle manuell eingeben oder Skripts erstellen:  
  
```  
#diskshadow script file  
set context persistent nowriters  
set metadata c:\diskshadowdata\example.cab  
set verbose on  
begin backup  
add volume c: alias Systemvolumeshadow  
add volume d: alias Datavolumeshadow  
  
create  
  
expose %Systemvolumeshadow% p:  
expose %Datavolumeshadow% q:  
exec c:\diskshadowdata\backupscript.cmd  
end backup  
#End of script  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

