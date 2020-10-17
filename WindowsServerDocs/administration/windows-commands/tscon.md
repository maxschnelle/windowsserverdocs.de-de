---
title: tscon
description: Referenz Artikel zu tscon, der eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server herstellt.
ms.topic: reference
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 17b18aea265ff7c703c2ef6c9c3d0021a9d9ea00
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156390"
---
# <a name="tscon"></a>tscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server her.

> [!IMPORTANT]
> Zum Herstellen einer Verbindung mit einer anderen Sitzung müssen Sie über die Berechtigung " **Vollzugriff** " verfügen oder eine **spezielle Zugriffsberechtigung herstellen** .

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
tscon {<sessionID> | <sessionname>} [/dest:<sessionname>] [/password:<pw> | /password:*] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<sessionID>` | Gibt die ID der Sitzung an, mit der Sie eine Verbindung herstellen möchten. Wenn Sie den optionalen- `/dest:<sessionname>` Parameter verwenden, können Sie auch den Namen der aktuellen Sitzung angeben. |
| `<sessionname>` | Gibt den Namen der Sitzung an, mit der Sie eine Verbindung herstellen möchten. |
| /dest`<sessionname>` | Gibt den Namen der aktuellen Sitzung an. Diese Sitzung wird getrennt, wenn Sie eine Verbindung mit der neuen Sitzung herstellen. Sie können diesen Parameter auch verwenden, um die Sitzung eines anderen Benutzers mit einer anderen Sitzung zu verbinden. |
| /Password`<pw>` | Gibt das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten. Dieses Kennwort ist erforderlich, wenn der Benutzer, der die Verbindung herstellt, die Sitzung nicht besitzt. |
| /Password`*` | Fordert das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Dieser Befehl schlägt fehl, wenn Sie kein Kennwort im **/Password** -Parameter angeben und die Ziel Sitzung zu einem anderen Benutzer als dem aktuellen gehört.

- Sie können keine Verbindung mit der Konsolen Sitzung herstellen.

## <a name="examples"></a>Beispiele

Zum Herstellen einer Verbindung mit *Sitzung 12* auf dem aktuellen Remotedesktopdienste-Sitzungs Host Server und zum Trennen der aktuellen Sitzung geben Sie Folgendes ein:

```
tscon 12
```

Geben Sie Folgendes ein, um eine Verbindung mit *Sitzung 23* auf dem aktuellen Remotedesktopdienste Sitzungs Host Server mithilfe des Kennworts *mypass*herzustellen und die Verbindung mit der aktuellen Sitzung zu trennen:

```
tscon 23 /password:mypass
```

Geben Sie Folgendes *ein, um*die Sitzung mit dem Namen " *TERM03* " und der Sitzung mit dem Namen " *TERM05*" zu verbinden.

```
tscon TERM03 /v /dest:TERM05
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
