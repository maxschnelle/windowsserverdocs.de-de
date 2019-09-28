---
title: 'Ksetup: Server'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd05fd294640c63e633b7b866307197ae6770476
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374957"
---
# <a name="ksetupserver"></a>Ksetup: Server



Hiermit können Sie einen Namen für einen Computer angeben, auf dem das Windows-Betriebssystem ausgeführt wird, damit die mit **Ksetup** vorgenommenen Änderungen den Zielcomputer aktualisieren. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /server <ServerName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<servername >|Der vollständige Computername, auf dem die Konfiguration wirksam wird, z. b. IPops897.Corp.contoso.com.</br>Wenn ein unvollständiger voll qualifizierter Domänen Computername angegeben wird, schlägt der Befehl fehl.|

## <a name="remarks"></a>Hinweise

Der Zielserver Name kann nicht entfernt werden. Sie können Sie nur auf den Namen des lokalen Computers zurücksetzen. Dies ist die Standardeinstellung.

Der Name des Zielservers wird in der Registrierung in **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos**gespeichert. Er wird nicht mit **Ksetup**gemeldet.

## <a name="BKMK_Examples"></a>Beispiele

Legen Sie die **Ksetup** -Konfigurationen auf dem IPops897-Computer, der in der Domäne "Domäne" verbunden ist, wirksam fest:
```
ksetup /server IPops897.corp.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)