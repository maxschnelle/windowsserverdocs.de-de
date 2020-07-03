---
title: ntcmdprompt
description: Referenz Artikel für den Befehl "ntcmdprompt", von dem der Befehls Interpreter **Cmd.exe**anstelle von " **Command.com**" ausgeführt wird, nachdem eine Beendigungs-und Ruhezustand (After) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung ausgeführt wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a70a8cfdbe6e37bfb8d90bed23e961d100843506
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925345"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt den Befehls Interpreter **Cmd.exe**anstelle von **Command.com**nach dem Ausführen eines Beendigungs-und Aufenthalts Residenten (After) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung aus.

## <a name="syntax"></a>Syntax

```
ntcmdprompt
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn **Command.com** ausgeführt wird, sind einige Features von **Cmd.exe**, z. b. die **doskey** -Anzeige von Befehlsverlauf, nicht verfügbar. Wenn Sie lieber den **Cmd.exe** Befehls Interpreter ausführen möchten, nachdem Sie einen "beenden" und "bleiben" in der Anwendung gestartet haben, oder die Eingabeaufforderung in einer Anwendung, die auf MS-DOS basiert, gestartet haben, können Sie den Befehl " **ntcmdprompt** " verwenden. Beachten Sie jedoch, dass die Wahrheits-r möglicherweise nicht zur Verwendung verfügbar ist, wenn Sie **Cmd.exe**ausführen. Sie können den Befehl " **ntcmdprompt** " in die Datei " **config. NT** " oder die entsprechende benutzerdefinierte Startdatei in die Programm Informationsdatei (PIF) einer Anwendung einschließen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
