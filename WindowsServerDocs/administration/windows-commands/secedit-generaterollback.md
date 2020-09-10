---
title: 'secedit: generaterollback'
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 28b8fedf952bfa5466bc0a893a46f2e7f69165f6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636798"
---
# <a name="seceditgeneraterollback"></a>secedit: generaterollback



Ermöglicht das Generieren einer Rollback-Vorlage für eine angegebene Konfigurations Vorlage.

## <a name="syntax"></a>Syntax

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, `/cfg \<configuration file name>` muss auch die Befehlszeilenoption angegeben werden.|
|cfg|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db \<database file name>` . Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|RBK|Erforderlich.</br>Gibt eine Sicherheits Vorlage an, in die die Roll Back Informationen geschrieben werden. Sicherheits Vorlagen werden mithilfe des Snap-Ins "Sicherheits Vorlagen" erstellt. Rollback-Dateien können mit diesem Befehl erstellt werden.|
|log|(Optional)</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|quiet|(Optional)</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Users \* Useraccount<em>\My documents\security\logs \* DatabaseName</em>. log) verwendet.

Ab Windows Server 2008 wurde durch `Secedit /refreshpolicy` ersetzt `gpupdate` . Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

Mit der erfolgreichen Ausführung dieses Befehls wird festgestellt, dass der Task erfolgreich abgeschlossen wurde. und protokolliert nur die Konflikte zwischen der angegebenen Sicherheits Vorlage und der Konfiguration der Sicherheitsrichtlinie. Diese Konflikte werden in der Datei "Scesrv. log" aufgeführt.

Wenn eine vorhandene Rollback-Vorlage angegeben ist, wird Sie durch diesen Befehl überschrieben. Mit diesem Befehl können Sie eine neue Rollback-Vorlage erstellen. Für beide Bedingungen sind keine zusätzlichen Parameter erforderlich.

## <a name="examples"></a>Beispiele

Nachdem Sie die Sicherheits Vorlage mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins erstellt haben, erstellen Sie die Rollback-Konfigurationsdatei, um die ursprünglichen Einstellungen zu speichern. Schreiben Sie die Aktion in die FY11-Protokolldatei.
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)