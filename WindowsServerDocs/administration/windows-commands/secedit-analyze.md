---
title: 'secedit: analysieren'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dca476237af48ef4222a47aefb8291571a5d66eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835013"
---
# <a name="seceditanalyze"></a>secedit: analysieren



Ermöglicht es Ihnen, die aktuellen Systemeinstellungen anhand von baselineeinstellungen zu analysieren, die in einer Datenbank gespeichert sind. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Utility|Erforderlich</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch die `/cfg \<configuration file name>` Befehlszeilenoption angegeben werden.|
|cfg|Optional.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem `/db \<database file name>`-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der `/cfg \<configuration file name>`-Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|log|Optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll.|
|geschwiegen|Optional.</br>Unterdrückt die Bildschirmausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Die Analyseergebnisse werden in einem separaten Bereich der-Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" der MMC angezeigt werden.

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Documents und Settings\*Useraccount<em>\My documents\security\logs\*DatabaseName</em>. log) verwendet.

In Windows Server 2008 wurde `Secedit /refreshpolicy` durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

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
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)