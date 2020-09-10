---
title: 'secedit: analysieren'
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 272a05b36ce998aaed9a3ee8bd8b9c273296c030
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636860"
---
# <a name="seceditanalyze"></a>secedit: analysieren



Ermöglicht es Ihnen, die aktuellen Systemeinstellungen anhand von baselineeinstellungen zu analysieren, die in einer Datenbank gespeichert sind.

## <a name="syntax"></a>Syntax

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, `/cfg \<configuration file name>` muss auch die Befehlszeilenoption angegeben werden.|
|cfg|(Optional)</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db \<database file name>` . Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|overwrite|(Optional)</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der- `/cfg \<configuration file name>` Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|log|(Optional)</br>Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll.|
|quiet|(Optional)</br>Unterdrückt die Bildschirmausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Die Analyseergebnisse werden in einem separaten Bereich der-Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" der MMC angezeigt werden.

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Documents and Settings \* Useraccount<em>\My documents\security\logs \* DatabaseName</em>. log) verwendet.

In Windows Server 2008 wurde durch `Secedit /refreshpolicy` ersetzt `gpupdate` . Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a>Beispiele

Führen Sie die Analyse für die Sicherheitsparameter in der Sicherheitsdatenbank "secdbtso. sdb" aus, die Sie mit dem Snap-in "Sicherheitskonfiguration und-Analyse" erstellt haben. Leiten Sie die Ausgabe an die Datei weiter SecAnalysisContosoFY11 mit Aufforderung, damit Sie überprüfen können, ob der Befehl korrekt ausgeführt wurde.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Nehmen wir an, dass die Analyse einige Unzulänglichkeiten offenbarte, damit die Sicherheits Vorlage "secmso. inf" geändert wurde. Führen Sie den Befehl erneut aus, um die Änderungen einzubeziehen, und leiten Sie die Ausgabe an die vorhandene Datei SecAnalysisContosoFY11 ohne Aufforderung.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)