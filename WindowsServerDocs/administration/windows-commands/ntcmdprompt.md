---
title: ntcmdprompt
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25afab00ced3cb14771c18aa38c7fd8c98aecc0c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838043"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt den Befehls Interpreter " **cmd. exe**" anstelle von " **Command.com**" aus, nachdem ein "beenden" und "bleiben Residenter" (Wahrheits Dienst) oder nach dem Starten der Eingabeaufforderung in einer MS-DOS-Anwendung ausgeführt wurde.
## <a name="syntax"></a>Syntax
```
ntcmdprompt
```
#### <a name="parameters"></a>Parameter

| Parameter |             Beschreibung              |
|-----------|--------------------------------------|
|    /?     | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise
- Wenn **Command.com** ausgeführt wird, sind einige Features von " **cmd. exe**" (z. b. die **doskey** -Anzeige des Befehls Verlaufs) nicht verfügbar. Wenn Sie den Befehls Interpreter " **cmd. exe** " ausführen möchten, nachdem Sie einen "beenden" und "bleiben" in einer Anwendung gestartet haben oder die Eingabeaufforderung in einer Anwendung, die auf MS-DOS basiert, gestartet haben, können Sie den Befehl " **ntcmdprompt** " verwenden. Beachten Sie jedoch, dass die "ZR" möglicherweise nicht zur Verwendung verfügbar ist, wenn Sie " **cmd. exe**" ausführen. Sie können den Befehl " **ntcmdprompt** " in die Datei " **config. NT** " oder die entsprechende benutzerdefinierte Startdatei in die Programm Informationsdatei (PIF) einer Anwendung einschließen.
  ## <a name="examples"></a>Beispiele
  Geben Sie Folgendes ein, um **ntcmdprompt** in die Datei " **config. NT** " oder die in der PIF angegebene Konfigurations Startdatei einzuschließen: **ntcmdprompt**
  ## <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

