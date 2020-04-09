---
title: 'Ksetup: setcomputerpassword'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e65ea6e935d9fde9c23842755c36e418928dec7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841373"
---
# <a name="ksetupsetcomputerpassword"></a>Ksetup: setcomputerpassword



Legt das Kennwort für den lokalen Computer fest. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setcomputerpassword <Password>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Kennwort \<>|Verwendet das angegebene Kennwort, um das Computer Konto auf dem lokalen Computer festzulegen.</br>Das Kennwort kann nur mit einem Konto mit Administrator Berechtigungen festgelegt werden. Das Kennwort kann zwischen 1 und 156 alphanumerische Zeichen oder Sonderzeichen enthalten.|

## <a name="remarks"></a>Hinweise

Dieser Befehl wirkt sich nur auf das Computer Konto aus.

Sie müssen den Computer neu starten, damit die Kenn Wort Änderung wirksam wird.

Das Kennwort des Computer Kontos wird nicht in der Registrierung oder als Ausgabe des **Ksetup** -Befehls angezeigt.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Ändern Sie das Kennwort des Computer Kontos auf dem lokalen Computer von IPops897 auf IPOP $897!.
```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)