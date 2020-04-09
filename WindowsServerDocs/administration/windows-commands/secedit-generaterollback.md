---
title: 'secedit: generaterollback'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d2a8ec7be0292fc096c072b0f4e5806e8051408
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834933"
---
# <a name="seceditgeneraterollback"></a>secedit: generaterollback



Ermöglicht das Generieren einer Rollback-Vorlage für eine angegebene Konfigurations Vorlage. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Utility|Erforderlich</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch die `/cfg \<configuration file name>` Befehlszeilenoption angegeben werden.|
|cfg|Erforderlich</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem `/db \<database file name>`-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|RBK|Erforderlich</br>Gibt eine Sicherheits Vorlage an, in die die Roll Back Informationen geschrieben werden. Sicherheits Vorlagen werden mithilfe des Snap-Ins "Sicherheits Vorlagen" erstellt. Rollback-Dateien können mit diesem Befehl erstellt werden.|
|log|Optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|geschwiegen|Optional.</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Users \*Useraccount<em>\My documents\security\logs\*DatabaseName</em>. log) verwendet.

Ab Windows Server 2008 wurde `Secedit /refreshpolicy` durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

Mit der erfolgreichen Ausführung dieses Befehls wird festgestellt, dass der Task erfolgreich abgeschlossen wurde. und protokolliert nur die Konflikte zwischen der angegebenen Sicherheits Vorlage und der Konfiguration der Sicherheitsrichtlinie. Diese Konflikte werden in der Datei "Scesrv. log" aufgeführt.

Wenn eine vorhandene Rollback-Vorlage angegeben ist, wird Sie durch diesen Befehl überschrieben. Mit diesem Befehl können Sie eine neue Rollback-Vorlage erstellen. Für beide Bedingungen sind keine zusätzlichen Parameter erforderlich.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Nachdem Sie die Sicherheits Vorlage mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins erstellt haben, erstellen Sie die Rollback-Konfigurationsdatei, um die ursprünglichen Einstellungen zu speichern. Schreiben Sie die Aktion in die FY11-Protokolldatei.
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)