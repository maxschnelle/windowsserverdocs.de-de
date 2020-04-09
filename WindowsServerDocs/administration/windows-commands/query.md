---
title: Abfrage
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d89ae8c7c526bce396b2583abc1728456f7bcc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836823"
---
# <a name="query"></a>Abfrage

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen, Sitzungen und Remotedesktop-Sitzungshost (RD-Sitzungshost)-Servern an.

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[Abfrageprozess](query-process.md)|Zeigt Informationen zu Prozessen an, die auf einem Remote Desktop-Sitzungs Host Server ausgeführt werden.|
|[Abfrage Sitzung](query-session.md)|Zeigt Informationen zu Sitzungen auf einem Remote Desktop-Sitzungs Host Server an.|
|[termserver Abfragen](query-termserver.md)|Zeigt eine Liste aller RD-Sitzungs Host Server im Netzwerk an.|
|[Benutzer Abfragen](query-user.md)|Zeigt Informationen zu Benutzersitzungen auf einem Remote Desktop-Sitzungs Host Server an.|

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Remotedesktopdienste Befehlsreferenz (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
