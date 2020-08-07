---
title: query termserver
description: Referenz Artikel für den Abfrage-termserver-Befehl, der eine Liste aller Remotedesktop-Sitzungshost Server im Netzwerk anzeigt.
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 755220fc5c105b97ae7d210857b662095fd306da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884412"
---
# <a name="query-termserver"></a>query termserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste aller Remotedesktop-Sitzungshost Server im Netzwerk an. Mit diesem Befehl wird das Netzwerk nach allen angefügten Remotedesktop-Sitzungshost Servern durchsucht und die folgenden Informationen zurückgegeben:

- Name des Servers

- Netzwerk (und Knotenadresse, wenn die/Address-Option verwendet wird)

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
query termserver [<servername>] [/domain:<domain>] [/address] [/continue]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<servername>` | Gibt den Namen an, der den Remotedesktop-Sitzungshost Server identifiziert. |
| /Domain`<domain>` | Gibt die Domäne an, die für Terminal Server abgefragt werden soll. Sie müssen keine Domäne angeben, wenn Sie die Domäne Abfragen, in der Sie gerade arbeiten. |
| /address | Zeigt die Netzwerk-und Knoten Adressen für jeden Server an. |
| /Continue | Verhindert, dass angehalten wird, nachdem jeder Bildschirm mit Informationen angezeigt wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Um Informationen zu allen Remotedesktop-Sitzungshost Servern im Netzwerk anzuzeigen, geben Sie Folgendes ein:

```
query termserver
```

Geben Sie Folgendes ein, um Informationen zum Remotedesktop-Sitzungshost Server mit dem Namen *Server3*anzuzeigen:

```
query termserver Server3
```

Geben Sie Folgendes ein, um Informationen zu allen Remotedesktop-Sitzungshost Servern in *der Domäne "* Configuration Manager" anzuzeigen:

```
query termserver /domain:CONTOSO
```

Geben Sie Folgendes ein, um die Netzwerk-und Knotenadresse für den Remotedesktop-Sitzungshost Server mit dem Namen *Server3*anzuzeigen:

```
query termserver Server3 /address
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Abfragebefehl](query.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
