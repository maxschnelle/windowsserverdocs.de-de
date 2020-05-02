---
title: 'Ksetup: setcomputerpassword'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9cb0c2ee36ed85ddfb015a80e86198fe788f8474
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724584"
---
# <a name="ksetupsetcomputerpassword"></a>Ksetup: setcomputerpassword



Legt das Kennwort für den lokalen Computer fest.

## <a name="syntax"></a>Syntax

```
ksetup /setcomputerpassword <Password>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Kennwort>|Verwendet das angegebene Kennwort, um das Computer Konto auf dem lokalen Computer festzulegen.</br>Das Kennwort kann nur mit einem Konto mit Administrator Berechtigungen festgelegt werden. Das Kennwort kann zwischen 1 und 156 alphanumerische Zeichen oder Sonderzeichen enthalten.|

## <a name="remarks"></a>Bemerkungen

Dieser Befehl wirkt sich nur auf das Computer Konto aus.

Sie müssen den Computer neu starten, damit die Kenn Wort Änderung wirksam wird.

Das Kennwort des Computer Kontos wird nicht in der Registrierung oder als Ausgabe des **Ksetup** -Befehls angezeigt.

## <a name="examples"></a>Beispiele

Ändern Sie das Kennwort des Computer Kontos auf dem lokalen Computer von IPops897 auf IPOP $897!.
```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)