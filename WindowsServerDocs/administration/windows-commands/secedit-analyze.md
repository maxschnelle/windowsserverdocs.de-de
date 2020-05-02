---
title: 'secedit: analysieren'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ae331b890d0e4201e8b621e5d84f5025934efa0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722091"
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
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch `/cfg \<configuration file name>` die Befehlszeilenoption angegeben werden.|
|cfg|Optional.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie `/db \<database file name>` mit dem-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|log|Optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll.|
|quiet|Optional.</br>Unterdrückt die Bildschirmausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Bemerkungen

Die Analyseergebnisse werden in einem separaten Bereich der-Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" der MMC angezeigt werden.

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Documents and\*Settings Useraccount<em>\My documents\security\logs\*DatabaseName</em>. log) verwendet.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt. `gpupdate` Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a>Beispiele

Führen Sie die Analyse für die Sicherheitsparameter in der Sicherheitsdatenbank "secdbtso. sdb" aus, die Sie mit dem Snap-in "Sicherheitskonfiguration und-Analyse" erstellt haben. Leiten Sie die Ausgabe an die Datei weiter SecAnalysisContosoFY11 mit Aufforderung, damit Sie überprüfen können, ob der Befehl korrekt ausgeführt wurde.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Nehmen wir an, dass die Analyse einige Unzulänglichkeiten offenbarte, damit die Sicherheits Vorlage "secmso. inf" geändert wurde. Führen Sie den Befehl erneut aus, um die Änderungen einzubeziehen, und leiten Sie die Ausgabe an die vorhandene Datei SecAnalysisContosoFY11 ohne Aufforderung.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Secedit](secedit.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)