---
title: mqbkup
description: Referenz Artikel zum Mqbkup-Befehl, der MSMQ-Nachrichten Dateien und Registrierungs Einstellungen auf einem Speichergerät sichert und zuvor gespeicherte Nachrichten und Einstellungen wiederherstellt.
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7eecb016efd039d87774c3fd869e746df1e60178
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886299"
---
# <a name="mqbkup"></a>mqbkup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert MSMQ-Nachrichten Dateien und Registrierungs Einstellungen auf einem Speichergerät und stellt zuvor gespeicherte Nachrichten und Einstellungen wieder her.

Der lokale MSMQ-Dienst wird durch die Sicherungs-und Wiederherstellungs Vorgänge angehalten. Wenn der MSMQ-Dienst zuvor gestartet wurde, versucht das Hilfsprogramm, den MSMQ-Dienst am Ende der Sicherung oder des Wiederherstellungs Vorgangs neu zu starten. Wenn der Dienst vor der Ausführung des Hilfsprogramms bereits beendet wurde, wird nicht versucht, den Dienst neu zu starten.

Vor der Verwendung des Dienstprogramms MSMQ-Nachrichten Sicherung/Wiederherstellung müssen Sie alle lokalen Anwendungen schließen, die MSMQ verwenden.

## <a name="syntax"></a>Syntax

```
mqbkup {/b | /r} <folder path_to_storage_device>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| /b | Gibt den Sicherungs Vorgang an. |
| /r | Gibt den Wiederherstellungs Vorgang an. |
| `<folder path_to_storage_device>` | Gibt den Pfad an, in dem die MSMQ-Nachrichten Dateien und Registrierungs Einstellungen gespeichert werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn ein angegebener Ordner nicht vorhanden ist, während der Sicherungs-oder Wiederherstellungs Vorgang durchgeführt wird, wird der Ordner automatisch vom Hilfsprogramm erstellt.

- Wenn Sie einen vorhandenen Ordner angeben, muss er leer sein. Wenn Sie einen nicht leeren Ordner angeben, löscht das Hilfsprogramm alle darin enthaltenen Dateien und Unterordner. In diesem Fall werden Sie aufgefordert, die Berechtigung zum Löschen vorhandener Dateien und Unterordner anzugeben. Sie können den **/y** -Parameter verwenden, um anzugeben, dass Sie im Voraus den Löschvorgang für alle vorhandenen Dateien und Unterordner im angegebenen Ordner zustimmen.

- Die Speicherorte von Ordnern, die zum Speichern von MSMQ-Nachrichten Dateien verwendet werden, werden in der Registrierung gespeichert. Daher stellt das Hilfsprogramm MSMQ-Nachrichten Dateien in den Ordnern wieder her, die in der Registrierung angegeben sind, und nicht für die Speicherordner, die vor dem Wiederherstellungs Vorgang verwendet werden

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle MSMQ-Nachrichten Dateien und-Registrierungs Einstellungen zu sichern und im Ordner " *msmqbkup* " auf Laufwerk C: zu speichern:

```
mqbkup /b c:\msmqbkup
```

Geben Sie Folgendes ein, um alle vorhandenen Dateien und Unterordner im Ordner *oldbkup* auf Laufwerk C: zu löschen und dann MSMQ-Nachrichten Dateien und Registrierungs Einstellungen im Ordner zu speichern:

```
mqbkup /b /y c:\oldbkup
```

Geben Sie Folgendes ein, um MSMQ-Nachrichten und Registrierungs Einstellungen wiederherzustellen:

```
mqbkup /r c:\msmqbkup
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [MSMQ PowerShell-Referenz](/powershell/module/msmq/?view=win10-ps)
