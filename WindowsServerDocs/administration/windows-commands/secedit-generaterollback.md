---
title: secedit generaterollback
description: Referenz Artikel zum Befehl "generaterollback" mit secedit, mit dem Sie eine Rollback-Vorlage für eine angegebene Konfigurations Vorlage generieren können.
ms.topic: reference
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ae2e368ef387ea84095fcbcc51ad1e622225a2cc
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388816"
---
# <a name="secedit-generaterollback"></a>secedit/generaterollback

Ermöglicht das Generieren einer Rollback-Vorlage für eine angegebene Konfigurations Vorlage. Wenn eine vorhandene Rollback-Vorlage vorhanden ist, werden die vorhandenen Informationen durch das erneute Ausführen dieses Befehls überschrieben.

Wenn Sie diesen Befehl erfolgreich ausführen, werden die Konflikte zwischen der angegebenen Sicherheits Vorlage und der Konfiguration der Sicherheitsrichtlinie in der Datei "Scesrv. log" protokolliert.

## <a name="syntax"></a>Syntax

```
secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /db | Erforderlich. Gibt den Pfad und den Dateinamen der Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird. Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss die `/cfg <configuration file name>` Option ebenfalls angegeben werden. |
| /cfg | Erforderlich. Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden. Diese Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db <database file name>` . Wenn dieser Parameter nicht auch angegeben wird, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist. |
| /rbk | Erforderlich. Gibt eine Sicherheits Vorlage an, in die die Roll Back Informationen geschrieben werden. Sicherheits Vorlagen werden mithilfe des Snap-Ins "Sicherheits Vorlagen" erstellt. Rollback-Dateien können mit diesem Befehl erstellt werden. |
| /Log | Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll. Wenn Sie keinen Speicherort für die Datei angeben, wird die Standardprotokoll Datei `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` verwendet. |
| /quiet | Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden. |

## <a name="examples"></a>Beispiele

Um die Roll Back Konfigurationsdatei zu erstellen, geben Sie für die zuvor erstellte Datei " *sectmpltentoso. inf* ", während Sie die ursprünglichen Einstellungen speichern und dann die Aktion in die *SecAnalysisContosoFY11* -Protokolldatei schreiben, Folgendes ein:

```
secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [secedit/analyze](secedit-analyze.md)

- [secedit/configure](secedit-configure.md)

- [secedit/Export](secedit-export.md)

- [secedit/Import](secedit-import.md)

- [secedit/Validate](secedit-validate.md)