---
title: query
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebe10bb78a6a901871a75e8533b3389c38060666
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863151"
---
# <a name="query"></a>query

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen über Prozesse, Sitzungen und Remotedesktop-Sitzungshost (RD Session Host)-Server.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
query process
query session
query termserver
query user
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[Abfrageprozess](query-process.md)|Zeigt Informationen zu Prozessen, die auf einen Remotedesktop-Sitzungshostserver ausgeführt werden.|
|[abfragesitzung](query-session.md)|Zeigt Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshostserver.|
|[Abfrage termserver](query-termserver.md)|Zeigt eine Liste aller RD-Sitzungshost-Server im Netzwerk.|
|[Benutzer, der Abfragen](query-user.md)|Informationen über die Sitzung des Benutzers auf einen Remotedesktop-Sitzungshostserver angezeigt.|

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
