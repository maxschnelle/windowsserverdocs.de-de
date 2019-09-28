---
title: tskill
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 697363c91837ff675a14099fd212f4f0753b739b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392332"
---
# <a name="tskill"></a>tskill

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet einen Prozess, der in einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) ausgeführt wird.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|\<processid >|Gibt die ID des Prozesses an, den Sie beenden möchten.|
|\<processname >|Gibt den Namen des Prozesses an, den Sie beenden möchten. Dieser Parameter kann Platzhalter Zeichen enthalten.|
|/Server: \<servername >|Gibt den Terminal Server an, der den Prozess enthält, den Sie beenden möchten. Wenn **/Server** nicht angegeben ist, wird der aktuelle RD-Sitzungshost Server verwendet.|
|/ID: \<sessionid >|Beendet den Prozess, der in der angegebenen Sitzung ausgeführt wird.|
|/a|Beendet den Prozess, der in allen Sitzungen ausgeführt wird.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
- Sie können **tskills** verwenden, um nur die Prozesse zu beenden, die Ihnen angehören, es sei denn, Sie sind ein Administrator. Administratoren haben Vollzugriff auf alle **tskills** -Funktionen und können Prozesse beenden, die in anderen Benutzersitzungen ausgeführt werden.
- Wenn alle Prozesse, die in einer Sitzung ausgeführt werden, beendet werden, wird die Sitzung ebenfalls beendet.
- Wenn Sie die Parameter " *ProcessName* " und " **/Server:** <em>Servername</em> " verwenden, müssen Sie auch den Parameter " **/ID:** <em>SessionID</em> " oder " **/a** " angeben.

## <a name="BKMK_examples"></a>Beispiele
- Um den Prozess 6543 zu beenden, geben Sie Folgendes ein:
  ```
  tskill 6543
  ```
- Zum Beenden des Prozesses "Explorer", der in Sitzung 5 ausgeführt wird, geben Sie Folgendes ein:
  ```
  tskill explorer /id:5
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
