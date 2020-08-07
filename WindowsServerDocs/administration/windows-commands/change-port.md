---
title: change port
description: Referenz Artikel für den Befehl Port ändern, mit dem die COM-Port Zuordnungen aufgelistet oder geändert werden, die mit MS-DOS-Anwendungen kompatibel sind.
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64c0d012d8106d99f1d7a167dd8f2d1d9107150b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880259"
---
# <a name="change-port"></a>change port

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "ändern"](change.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
