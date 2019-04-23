---
title: ksetup:setcomputerpassword
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0679bb9ee429e05c7679411c5493bd21b530ef8e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831541"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup:setcomputerpassword



Legt das Kennwort für den lokalen Computer. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setcomputerpassword <Password>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Kennwort >|Mithilfe des angegebenen Kennworts das Computerkonto auf dem lokalen Computer festgelegt.</br>Das Kennwort kann nur mit einem Konto mit Administratorrechten ausführen festgelegt werden. Das Kennwort kann zwischen 1 und 156 alphanumerische oder Sonderzeichen Zeichen liegen.|

## <a name="remarks"></a>Hinweise

Dieser Befehl wirkt sich nur für das Computerkonto.

Sie müssen den Computer für die kennwortänderung wirksam neu starten.

Das Kennwort des Computerkontos wird nicht angezeigt, in der Registrierung oder als Ausgabe der **Ksetup** Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Ändern Sie das Computerkontokennwort auf dem lokalen Computer aus IPops897 zu IPop$ 897!.
```
ksetup /setcomputerpassword IPop$897!
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)