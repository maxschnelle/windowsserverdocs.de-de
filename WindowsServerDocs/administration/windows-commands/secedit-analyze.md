---
title: secedit analyze
description: Referenz Artikel für den Befehl "Analyse analysieren", mit dem Sie die aktuellen Systemeinstellungen anhand der in einer Datenbank gespeicherten Baseline-Einstellungen analysieren können.
ms.topic: reference
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 783f9d1042b860adefc49f58f38f66e0571468e3
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388556"
---
# <a name="secedit-analyze"></a>secedit/analyze

Ermöglicht es Ihnen, die aktuellen Systemeinstellungen anhand von baselineeinstellungen zu analysieren, die in einer Datenbank gespeichert sind.

## <a name="syntax"></a>Syntax

```
secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /db | Erforderlich. Gibt den Pfad und den Dateinamen der Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird. Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss die `/cfg <configuration file name>` Option ebenfalls angegeben werden. |
| /cfg | Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden. Diese Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db <database file name>` . Wenn dieser Parameter nicht auch angegeben wird, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist. |
| /overwrite | Gibt an, ob die Sicherheits Vorlage im **/cfg** -Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen. Diese Option ist nur gültig, wenn der- `/cfg <configuration file name>` Parameter ebenfalls verwendet wird. Wenn dieser Parameter nicht auch angegeben wird, wird die Vorlage im **/cfg** -Parameter an die gespeicherte Vorlage angehängt. |
| /Log | Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll. Wenn Sie keinen Speicherort für die Datei angeben, wird die Standardprotokoll Datei `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` verwendet. |
| /quiet | Unterdrückt die Bildschirmausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden. |

## <a name="examples"></a>Beispiele

Zum Durchführen der Analyse für die Sicherheitsparameter in der Sicherheitsdatenbank, *secdbconfiguration. SDB*, und Weiterleiten der Ausgabe an die Datei *SecAnalysisContosoFY11*, einschließlich der Eingabe Aufforderungen zum Überprüfen, ob der Befehl ordnungsgemäß ausgeführt wurde, geben Sie Folgendes ein:

```
secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

Wenn Sie Änderungen, die für den Analyseprozess in der Datei " *secmso. inf* " erforderlich sind, einschließen und dann die Ausgabe an die vorhandene Datei weiterleiten möchten, geben Sie *SecAnalysisContosoFY11*ohne Eingabeaufforderung Folgendes ein:

```
secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [secedit/configure](secedit-configure.md)

- [secedit/Export](secedit-export.md)

- [secedit/generaterollback](secedit-generaterollback.md)

- [secedit/Import](secedit-import.md)

- [secedit/Validate](secedit-validate.md)