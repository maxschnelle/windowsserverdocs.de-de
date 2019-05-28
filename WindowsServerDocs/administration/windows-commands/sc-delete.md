---
title: SC delete
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68af5f118b2cc9d7941abddccd2a1bc7fde4c6d0
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222934"
---
# <a name="sc-delete"></a>SC delete



Löscht einen Unterschlüssel Service aus der Registrierung. Wenn der Dienst ausgeführt wird, oder wenn ein anderer Prozess ein geöffnetes Handle an den Dienst verfügt, wird der Dienst zum Löschen markiert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] delete [<ServiceName>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remoteservers auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format verwenden (z. B. \\ \\"myserver"). Um SC.exe lokal ausführen zu können, müssen lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen, die zurückgegeben werden, indem die **Getkeyname** Vorgang.|
|?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Verwendung **Software** auf **Systemsteuerung** DHCP, DNS oder andere Dienste integriertes Betriebssystem zu löschen. Beachten Sie, dass **Software** nicht nur der Unterschlüssel der Registrierung für den Dienst entfernt, aber es außerdem deinstallieren Sie den Dienst und löschen Sie alle Verknüpfungen.

## <a name="examples"></a>Beispiele

So löschen Sie den Dienstunterschlüssel **NewServ** Geben Sie an der Registrierung auf dem lokalen Computer:
```
sc delete newserv
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)