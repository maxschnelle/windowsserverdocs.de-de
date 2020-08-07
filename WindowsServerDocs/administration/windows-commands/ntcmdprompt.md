---
title: ntcmdprompt
description: Referenz Artikel für den Befehl "ntcmdprompt", von dem der Befehls Interpreter **Cmd.exe**anstelle von " **Command.com**" ausgeführt wird, nachdem eine Beendigungs-und Ruhezustand (After) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung ausgeführt wurde.
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53ed39f0fd455314dc5ccd90f0286f6dfd35ea72
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885302"
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

#### <a name="remarks"></a>Bemerkungen

- Wenn **Command.com** ausgeführt wird, sind einige Features von **Cmd.exe**, z. b. die **doskey** -Anzeige von Befehlsverlauf, nicht verfügbar. Wenn Sie lieber den **Cmd.exe** Befehls Interpreter ausführen möchten, nachdem Sie einen "beenden" und "bleiben" in der Anwendung gestartet haben, oder die Eingabeaufforderung in einer Anwendung, die auf MS-DOS basiert, gestartet haben, können Sie den Befehl " **ntcmdprompt** " verwenden. Beachten Sie jedoch, dass die Wahrheits-r möglicherweise nicht zur Verwendung verfügbar ist, wenn Sie **Cmd.exe**ausführen. Sie können den Befehl " **ntcmdprompt** " in die Datei " **config. NT** " oder die entsprechende benutzerdefinierte Startdatei in die Programm Informationsdatei (PIF) einer Anwendung einschließen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
