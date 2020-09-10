---
title: Abfrage
description: Referenz Artikel für den Abfragebefehl, der Informationen über Prozesse, Sitzungen und Remotedesktop-Sitzungshost Server anzeigt.
ms.topic: reference
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 62719f6ace4f27e46701958180811118886929a8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637427"
---
# <a name="query"></a>Abfrage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen, Sitzungen und Remotedesktop-Sitzungshost Servern an. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [query process](query-process.md) | Zeigt Informationen zu Prozessen an, die auf einem Remotedesktop-Sitzungshost Server ausgeführt werden. |
| [query session](query-session.md) | Zeigt Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server an. |
| [query termserver](query-termserver.md) | Zeigt eine Liste aller Remotedesktop-Sitzungshost Server im Netzwerk an. |
| [query user](query-user.md) | Zeigt Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
