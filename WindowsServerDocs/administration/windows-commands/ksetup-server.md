---
title: 'Ksetup: Server'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7889e1a03d3c0eec1958bf1d6356c67e9371a80f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841443"
---
# <a name="ksetupserver"></a>Ksetup: Server



Hiermit können Sie einen Namen für einen Computer angeben, auf dem das Windows-Betriebssystem ausgeführt wird, damit die mit **Ksetup** vorgenommenen Änderungen den Zielcomputer aktualisieren. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /server <ServerName>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Servername >|Der vollständige Computername, auf dem die Konfiguration wirksam wird, z. b. IPops897.Corp.contoso.com.</br>Wenn ein unvollständiger voll qualifizierter Domänen Computername angegeben wird, schlägt der Befehl fehl.|

## <a name="remarks"></a>Hinweise

Der Zielserver Name kann nicht entfernt werden. Sie können Sie nur auf den Namen des lokalen Computers zurücksetzen. Dies ist die Standardeinstellung.

Der Name des Zielservers wird in der Registrierung unter **HKEY_LOCAL_MACHINE \system\controlset001\control\lsa\kerberos**gespeichert. Er wird nicht mit **Ksetup**gemeldet.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Legen Sie die **Ksetup** -Konfigurationen auf dem IPops897-Computer, der in der Domäne "Domäne" verbunden ist, wirksam fest:
```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)