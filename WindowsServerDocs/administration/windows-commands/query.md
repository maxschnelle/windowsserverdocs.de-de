---
title: Abfrage
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dcea0fa4ea91de56e81c51bf9fe87ec7e3a49fa
ms.sourcegitcommit: 4894649cc47dfa535306cc334871f81155198f76
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2020
ms.locfileid: "84254713"
---
# <a name="query"></a>Abfrage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen, Sitzungen und Remotedesktop-Sitzungshost (RD-Sitzungshost)-Servern an.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)) in the Microsoft-Dokumentation Windows Server Library.

## <a name="syntax"></a>Syntax

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|[query process](query-process.md)|Zeigt Informationen zu Prozessen an, die auf einem Remote Desktop-Sitzungs Host Server ausgeführt werden.|
|[Abfrage Sitzung](query-session.md)|Zeigt Informationen zu Sitzungen auf einem Remote Desktop-Sitzungs Host Server an.|
|[termserver Abfragen](query-termserver.md)|Zeigt eine Liste aller RD-Sitzungs Host Server im Netzwerk an.|
|[Benutzer Abfragen](query-user.md)|Zeigt Informationen zu Benutzersitzungen auf einem Remote Desktop-Sitzungs Host Server an.|

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
