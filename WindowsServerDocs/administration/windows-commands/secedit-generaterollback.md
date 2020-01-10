---
title: 'secedit: generaterollback'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797f93f010a903d6ec21f568d8d665cb2e42e692
ms.sourcegitcommit: 5ed817fff1262e390403a4f4f6c38fdc12300c29
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/07/2020
ms.locfileid: "75702741"
---
# <a name="seceditgeneraterollback"></a>secedit: generaterollback



Ermöglicht das Generieren einer Rollback-Vorlage für eine angegebene Konfigurations Vorlage. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch die `/cfg \<configuration file name>` Befehlszeilenoption angegeben werden.|
|cfg|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem `/db \<database file name>`-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|RBK|Erforderlich.</br>Gibt eine Sicherheits Vorlage an, in die die Roll Back Informationen geschrieben werden. Sicherheits Vorlagen werden mithilfe des Snap-Ins "Sicherheits Vorlagen" erstellt. Rollback-Dateien können mit diesem Befehl erstellt werden.|
|log|(Optional)</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|quiet|(Optional)</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Users \*Useraccount<em>\My documents\security\logs\*DatabaseName</em>. log) verwendet.

Ab Windows Server 2008 wurde `Secedit /refreshpolicy` durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

Bei erfolgreicher Ausführung dieses Befehls wird der Status "der Task wurde erfolgreich abgeschlossen" angezeigt. und protokolliert nur die Konflikte zwischen der angegebenen Sicherheits Vorlage und der Konfiguration der Sicherheitsrichtlinie. Diese Konflikte werden in der Datei "Scesrv. log" aufgeführt.

Wenn eine vorhandene Rollback-Vorlage angegeben ist, wird Sie durch diesen Befehl überschrieben. Mit diesem Befehl können Sie eine neue Rollback-Vorlage erstellen. Für beide Bedingungen sind keine zusätzlichen Parameter erforderlich.

## <a name="BKMK_Examples"></a>Beispiele

Nachdem Sie die Sicherheits Vorlage mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins erstellt haben, erstellen Sie die Rollback-Konfigurationsdatei, um die ursprünglichen Einstellungen zu speichern. Schreiben Sie die Aktion in die FY11-Protokolldatei.
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)