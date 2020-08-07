---
title: Diskshadow
description: Referenz Artikel für den DiskShadow-Befehl, bei dem es sich um ein Tool handelt, das die vom Volumeschattenkopie-Dienst (VSS) angebotene Funktionalität verfügbar macht.
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3170cde50208eb54d1657ceee0c409d76ed3b806
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890808"
---
# <a name="diskshadow"></a>Diskshadow

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diskshadow.exe ist ein Tool, das die vom Volumeschattenkopie-Dienst (VSS) angebotene Funktionalität verfügbar macht. Standardmäßig verwendet DiskShadow einen interaktiven Befehls Interpreter ähnlich dem von Diskraid oder DiskPart. DiskShadow enthält auch einen Skript fähigen Modus.

> [!NOTE]
> Sie müssen mindestens Mitglied der lokalen Gruppe Administratoren oder einer entsprechenden Gruppe sein, um DiskShadow ausführen zu können.

## <a name="syntax"></a>Syntax

Geben Sie für den interaktiven Modus Folgendes an der Eingabeaufforderung ein, um den DiskShadow-Befehls Interpreter zu starten:

```
diskshadow
```

Geben Sie im Skript Modus Folgendes ein, wobei *script.txt* eine Skriptdatei mit DiskShadow-Befehlen ist:

```
diskshadow -s script.txt
```

### <a name="parameters"></a>Parameter

Sie können die folgenden Befehle im DiskShadow-Befehls Interpreter oder über eine Skriptdatei ausführen. Zum Erstellen einer Schatten Kopie sind mindestens " **Add** " und " **Create** " erforderlich. Hierdurch werden jedoch die Kontext-und Options Einstellungen, eine Kopiesicherung, und eine Schatten Kopie ohne Sicherungs Ausführungs Skript nicht mehr angezeigt.

| Get-Help | BESCHREIBUNG |
| --------- | ----------- |
| [SET-Befehl](set_2.md) | Legt den Kontext, die Optionen, den ausführlichen Modus und die Metadatendatei zum Erstellen von Schatten Kopien fest. |
| [Befehl "Metadaten laden"](load-metadata.md) | Lädt eine Datei "Metadata. cab" vor dem Importieren einer austauschen-Schatten Kopie oder lädt die Writer-Metadaten im Fall einer Wiederherstellung. |
| [Writer-Befehl](writer.md) | überprüft, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren enthält bzw. schließt. |
| [Befehl hinzufügen](add.md) | Fügt Volumes zu dem Satz von Volumes hinzu, die als Schatten kopiert werden sollen, oder fügt der Alias Umgebung Aliase hinzu. |
| [Create-Befehl](create.md) | Startet den Vorgang zum Erstellen von Schatten Kopien mithilfe der aktuellen Kontext-und Options Einstellungen. |
| [Befehl "exec"](exec.md) | Führt eine Datei auf dem lokalen Computer aus. |
| [Befehl zum Starten der Sicherung](begin-backup.md) | Startet eine vollständige Sicherungs Sitzung. |
| [Befehl "Sicherung beenden"](end-backup.md) | Beendet eine vollständige Sicherungs Sitzung und gibt ggf. ein **BackupComplete** -Ereignis mit dem entsprechenden Writer-Status aus. |
| [Befehl "Wiederherstellen"](begin-restore.md) | Startet eine Wiederherstellungs Sitzung und gibt ein **vorab** Ereignis für beteiligte Writer aus. |
| [Befehl "End Restore"](end-restore.md) | Beendet eine Wiederherstellungs Sitzung und gibt ein **postrestore** -Ereignis für beteiligte Writer aus. |
| [Befehl Zurücksetzen](reset.md) | Setzt DiskShadow auf den Standardzustand zurück. |
| [List-Befehl](list.md) | Listet Writer, Schatten Kopien oder derzeit registrierte Schattenkopieanbieter auf, die sich auf dem System befinden. |
| [Befehl "Shadows löschen"](delete-shadows.md) | Löscht Schatten Kopien. |
| [Import Befehl](import.md) | Importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System. |
| [Mask-Befehl](mask.md) | Entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden. |
| [Befehl verfügbar machen](expose.md) | Macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar. |
| [Befehl zum nicht verfügbar machen](unexpose.md) | Macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde. |
| [Break-Befehl](break_2.md) | Trennt ein Schattenkopievolume von VSS. |
| [revert-Befehl](revert.md) | Setzt ein Volume auf eine angegebene Schatten Kopie zurück. |
| [Exit-Befehl](exit.md) | Beendet den Befehls Interpreter oder das Skript. |

## <a name="examples"></a>Beispiele

Dies ist eine Beispiel Sequenz von Befehlen, mit denen eine Schatten Kopie für die Sicherung erstellt wird. Sie kann in der Datei als Script. DSH gespeichert und mit ausgeführt werden `diskshadow /s script.dsh` .

Nehmen Sie Folgendes an:

- Sie verfügen über ein vorhandenes Verzeichnis mit dem Namen "c: \\ diskshadowdata".

- Ihr System Volume ist "C:" und das Daten Volume "d:".

- Sie verfügen über eine backupscript. cmd-Datei in "c: \\ diskshadowdata".

- Die Datei "backupscript. cmd" führt die Kopie der Schatten Daten p: und q: auf Ihrem Sicherungs Laufwerk aus.

Sie können diese Befehle manuell eingeben oder Skripts erstellen:

```
#Diskshadow script file
set context persistent nowriters
set metadata c:\diskshadowdata\example.cab
set verbose on
begin backup
add volume c: alias systemvolumeshadow
add volume d: alias datavolumeshadow

create

expose %systemvolumeshadow% p:
expose %datavolumeshadow% q:
exec c:\diskshadowdata\backupscript.cmd
end backup
#End of script
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
