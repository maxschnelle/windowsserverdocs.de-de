---
title: diskshadow
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b2c5648235a1c856c6aef09621e2381e74d08d70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869181"
---
# <a name="diskshadow"></a>diskshadow

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

DiskShadow.exe ist ein Tool, das die Funktionen der Volumeschattenkopie-Dienst verfügbar macht \(VSS\). Standardmäßig wird von Diskshadow einen interaktiver Interpreter vergleichbar mit dem von Diskraid oder DiskPart verwendet. DiskShadow umfasst auch einen skriptfähigen Modus.  
  
> [!NOTE]  
> Mitgliedschaft in der lokalen Gruppe "Administratoren" oder einer gleichwertigen, ist die mindestvoraussetzung, um Diskshadow auszuführen.  
  
Beispiele für Diskshadow-Befehle verwenden, finden Sie unter [Beispiele](#BKMK_examples).  
  
## <a name="syntax"></a>Syntax  
Geben Sie Folgendes an der Eingabeaufforderung, starten Sie den Befehlsinterpreter Diskshadow, für den interaktiven Modus:  
  
```  
diskshadow  
```  
  
Geben Sie Folgendes ein, für den Skriptmodus, in denen *script.txt* ist eine Skriptdatei mit Diskshadow-Befehlen:  
  
```  
diskshadow -s script.txt  
```  
  
## <a name="diskshadow-commands"></a>DiskShadow-Befehle  
Sie können die folgenden Befehle in der Befehlsinterpreter Diskshadow oder über eine Skriptdatei ausführen:  
  
|Parameter|Beschreibung|  
|-------|--------|  
|[set_2](set_2.md)|Legt fest, der Kontext, Optionen, ausführlichen Modus und Metadatendatei für die Erstellung von Schattenkopien.|  
|[Simulieren der Wiederherstellung](simulate-restore.md)|Testet Writer Beteiligung in der Restore-Sitzungen auf dem Computer nur durch Ausstellung **PreRestore** oder **PostRestore** Ereignisse auf Writer.|  
|[Laden von Metadaten](load-metadata.md)|Lädt eine Metadaten-CAB-Datei vor dem Importieren der übertragbarer Schattenkopien oder lädt die Metadaten im Fall einer Wiederherstellung.|  
|[writer](writer.md)|Überprüft, ob ein Writer oder eine Komponente enthalten ist oder ein Writer oder eine Komponente aus der Sicherung oder Wiederherstellung Prozedur schließt.|  
|[add_1](add_1.md)|Hinzufügen von Volumes auf den Satz von Volumes, die zu spiegelnde sind, oder fügt Aliase auf die Alias-Umgebung.|  
|[create_1](create_1.md)|Startet die Erstellung Schattenkopie, mit den aktuellen Kontext und die Option Einstellungen an.|  
|[exec](exec.md)|führt eine Datei auf dem lokalen Computer.|  
|[Starten der Sicherung](begin-backup.md)|Eine vollständige Sicherung Sitzung startet.|  
|[Ende der Sicherung](end-backup.md)|Beendet eine vollständige Sicherung Sitzung und Probleme eine **Backupcomplete** -Ereignis mit der entsprechenden Writerzustand, falls erforderlich.|  
|[Start der Wiederherstellung](begin-restore.md)|Startet eine Wiederherstellung der Sitzung und Probleme eine **PreRestore** Ereignis beteiligten Writer.|  
|[Ende der Wiederherstellung](end-restore.md)|Beendet eine Wiederherstellung der Sitzung und die Probleme einer **PostRestore** Ereignis beteiligten Writer.|  
|[reset](reset.md)|Diskshadow zurückgesetzt auf den Standardzustand.|  
|[list](list.md)|Listen-Writer, Schattenkopien und gegenwärtig registrierten Volumeschattenkopie-Anbieter, die auf dem System sind.|  
|[Löschen Sie Schatten](delete-shadows.md)|Löscht die Schattenkopien.|  
|[import](import.md)|importiert eine übertragbarer Schattenkopien aus einer geladenen Metadaten-Datei in das System an.|  
|[mask](mask.md)|Hardwareschattenkopien, die mithilfe von importiert wurden entfernt die **importieren** Befehl.|  
|[verfügbar machen](expose.md)|Stellt eine permanente Schattenkopie als Laufwerkbuchstaben, Freigabe oder Bereitstellungspunkt an.|  
|[unexpose](unexpose.md)|Unexposes eine Schattenkopie, die verfügbar gemacht wurde die **verfügbar zu machen** Befehl.|  
|[break_2](break_2.md)|Hebt die Zuordnung einer Schattenkopievolume von VSS.|  
|[revert](revert.md)|wird ein Volume an einer angegebenen Schattenkopie zurückgesetzt.|  
|[exit_1](exit_1.md)|Diskshadow wird beendet.|  
  
## <a name="remarks"></a>Hinweise  
  
-   mindestens ein nur **hinzufügen** und **erstellen** sind erforderlich, um eine Schattenkopie zu erstellen. Aber dies wird der Kontext und optionseinstellungen in Anspruch genommenen, einer kopiesicherung werden und erstellt nur dann eine Schattenkopie ohne Ausführung der backup-Script.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Dies ist eine Beispiel-Sequenz von Befehlen, die eine Schattenkopie für die Sicherung erstellt. Diese Datei als script.dsh gespeichert, und ausgeführt werden kann mit Diskshadow \/s script.dsh  
  
Nehmen Sie an Folgendes:  
  
-   Sie haben ein vorhandenes Verzeichnis namens "c:"\\Diskshadowdata.  
  
-   Das Systemvolume ist "c:", und Ihr Datenvolumen ist "d:".  
  
-   Sie haben eine backupscript.cmd-Datei in "c:"\\Diskshadowdata.  
  
-   Die Datei backupscript.cmd wird die Kopie der Schattenkopie Daten p: und f:, auf das Sicherungslaufwerk ausgeführt.  
  
Sie können diese Befehle manuell eingeben oder ein Skript:  
  
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
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

