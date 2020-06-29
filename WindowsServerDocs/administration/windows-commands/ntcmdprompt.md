---
title: ntcmdprompt
description: Referenz Thema für den Befehl "ntcmdprompt", bei dem der Befehls Interpreter **Cmd.exe**anstelle von " **Command.com**" ausgeführt wird, nachdem eine Beendigungs-und Ruhezustand (After) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung ausgeführt wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08d5ee1af4c019724a77eda6370e63541e16a72a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472775"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt den Befehls Interpreter **Cmd.exe**anstelle von **Command.com**nach dem Ausführen eines Beendigungs-und Aufenthalts Residenten (After) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung aus.

## <a name="syntax"></a>Syntax

```
ntcmdprompt
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn **Command.com** ausgeführt wird, sind einige Features von **Cmd.exe**, z. b. die **doskey** -Anzeige von Befehlsverlauf, nicht verfügbar. Wenn Sie lieber den **Cmd.exe** Befehls Interpreter ausführen möchten, nachdem Sie einen "beenden" und "bleiben" in der Anwendung gestartet haben, oder die Eingabeaufforderung in einer Anwendung, die auf MS-DOS basiert, gestartet haben, können Sie den Befehl " **ntcmdprompt** " verwenden. Beachten Sie jedoch, dass die Wahrheits-r möglicherweise nicht zur Verwendung verfügbar ist, wenn Sie **Cmd.exe**ausführen. Sie können den Befehl " **ntcmdprompt** " in die Datei " **config. NT** " oder die entsprechende benutzerdefinierte Startdatei in die Programm Informationsdatei (PIF) einer Anwendung einschließen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
