---
title: finger
description: Referenz Thema für den Finger Befehl, mit dem Informationen zu Benutzern auf einem angegebenen Remote Computer angezeigt werden, auf dem der Fingerdienst oder-Daemon ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3403e10a1777bc117659eb052958d3a20668557
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437235"
---
# <a name="finger"></a>finger

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Benutzern auf einem angegebenen Remote Computer an (normalerweise ein Computer, auf dem UNIX ausgeführt wird), auf dem der Fingerdienst oder-Daemon ausgeführt wird. Der Remote Computer gibt das Format und die Ausgabe der Anzeige der Benutzerinformationen an. Wird ohne Parameter verwendet **und zeigt** Hilfe an.

> [!IMPORTANT]
> Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="syntax"></a>Syntax

```
finger [-l] [<user>] [@<host>] [...]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -l | Zeigt Benutzerinformationen im langen Listenformat an. |
| `<user>` | Gibt den Benutzer an, zu dem Sie Informationen benötigen. Wenn Sie den Parameter " *User* " weglassen, werden mit diesem Befehl Informationen zu allen Benutzern auf dem angegebenen Computer angezeigt. |
| `@<host>` | Gibt den Remote Computer an, auf dem der Finger Dienst ausgeführt wird, auf dem Sie nach Benutzerinformationen suchen. Sie können einen Computernamen oder eine IP-Adresse angeben. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Sie müssen **Finger** Parametern mit einem Bindestrich (-) anstelle eines Schrägstrichs (/) als Präfix versehen.

- Es `user@host` können mehrere Parameter angegeben werden.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen für *User1* auf dem Computer *users.Microsoft.com*anzuzeigen:

```
finger user1@users.microsoft.com
```

Geben Sie Folgendes ein, um Informationen für *alle Benutzer* auf dem Computer *users.Microsoft.com*anzuzeigen:

```
finger @users.microsoft.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
