---
title: 'Ksetup: Server'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91549eb78f825264016ec0e03b7035f79132f260
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724592"
---
# <a name="ksetupserver"></a>Ksetup: Server



Hiermit können Sie einen Namen für einen Computer angeben, auf dem das Windows-Betriebssystem ausgeführt wird, damit die mit **Ksetup** vorgenommenen Änderungen den Zielcomputer aktualisieren.

## <a name="syntax"></a>Syntax

```
ksetup /server <ServerName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Servername>|Der vollständige Computername, auf dem die Konfiguration wirksam wird, z. b. IPops897.Corp.contoso.com.</br>Wenn ein unvollständiger voll qualifizierter Domänen Computername angegeben wird, schlägt der Befehl fehl.|

## <a name="remarks"></a>Bemerkungen

Der Zielserver Name kann nicht entfernt werden. Sie können Sie nur auf den Namen des lokalen Computers zurücksetzen. Dies ist die Standardeinstellung.

Der Name des Zielservers wird in der Registrierung unter **HKEY_LOCAL_MACHINE \system\controlset001\control\lsa\kerberos**gespeichert. Er wird nicht mit **Ksetup**gemeldet.

## <a name="examples"></a>Beispiele

Legen Sie die **Ksetup** -Konfigurationen auf dem IPops897-Computer, der in der Domäne "Domäne" verbunden ist, wirksam fest:
```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)