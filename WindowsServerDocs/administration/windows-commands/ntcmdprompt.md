---
title: ntcmdprompt
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5b0dcbc0735f20b63cbf441f4014411acd3a48e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723475"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt den Befehls Interpreter " **cmd. exe**" anstelle von " **Command.com**" aus, nachdem ein "beenden" und "bleiben Residenter" (Wahrheits Dienst) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung ausgeführt wurde.
## <a name="syntax"></a>Syntax
```
ntcmdprompt
```
#### <a name="parameters"></a>Parameter

| Parameter |             BESCHREIBUNG              |
|-----------|--------------------------------------|
|    /?     | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen
- Wenn **Command.com** ausgeführt wird, sind einige Features von " **cmd. exe**" (z. b. die **doskey** -Anzeige des Befehls Verlaufs) nicht verfügbar. Wenn Sie den Befehls Interpreter " **cmd. exe** " ausführen möchten, nachdem Sie einen "beenden" und "bleiben" in einer Anwendung gestartet haben oder die Eingabeaufforderung in einer Anwendung, die auf MS-DOS basiert, gestartet haben, können Sie den Befehl " **ntcmdprompt** " verwenden. Beachten Sie jedoch, dass die "ZR" möglicherweise nicht zur Verwendung verfügbar ist, wenn Sie " **cmd. exe**" ausführen. Sie können den Befehl " **ntcmdprompt** " in die Datei " **config. NT** " oder die entsprechende benutzerdefinierte Startdatei in die Programm Informationsdatei (PIF) einer Anwendung einschließen.
  ## <a name="examples"></a>Beispiele
  Geben Sie Folgendes ein, um **ntcmdprompt** in die Datei " **config. NT** " oder die in der PIF angegebene Konfigurations Startdatei einzuschließen: **ntcmdprompt**
  ## <a name="additional-references"></a>Zusätzliche Referenzen
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

