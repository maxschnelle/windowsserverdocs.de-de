---
title: change port
description: Referenz Thema für den Befehl Port ändern, mit dem die COM-Port Zuordnungen aufgelistet oder geändert werden, die mit MS-DOS-Anwendungen kompatibel sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8dcf1097ea037aff9269edafea6e640054a697e3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716079"
---
# <a name="change-port"></a>change port

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
change port [<portX>=<portY| /d <portX | /query]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|-----------------|----------------------------------------|
| <portX>=<portY> | Ordnet com `<*portX*>` zu zu`<*portY*>` |
| /d<portX> | Löscht die Zuordnung für com.`<*portX*>` |
| /Query "aus | Zeigt die aktuellen Port Zuordnungen an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Die meisten MS-DOS-Anwendungen unterstützen nur die seriellen Anschlüsse COM1 bis COM4. Der Befehl **Port ändern** ordnet einen seriellen Anschluss einer anderen Portnummer zu, sodass apps, die High-nummerierte com-Anschlüsse nicht unterstützen, auf den seriellen Anschluss zugreifen können. Die Neuzuordnung funktioniert nur für die aktuelle Sitzung und wird nicht beibehalten, wenn Sie sich von einer Sitzung abmelden und dann wieder anmelden.

- Verwenden Sie den **änderungsport** ohne Parameter, um die verfügbaren com-Anschlüsse und ihre aktuellen Zuordnungen anzuzeigen.

## <a name="examples"></a>Beispiele

- Wenn Sie COM12 COM1 für die Verwendung durch eine MS-DOS-basierte Anwendung zuordnen möchten, geben Sie Folgendes ein:
  
  ```
  change port com12=com1
  ```

- Geben Sie Folgendes ein, um die aktuellen Port Zuordnungen anzuzeigen:
  
  ```
  change port /query
  ```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "ändern"](change.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
