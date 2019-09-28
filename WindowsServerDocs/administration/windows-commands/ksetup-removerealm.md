---
title: 'Ksetup: removerealm'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11858d8a24d4f125c83b3e4092ac48f336a9ef0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374953"
---
# <a name="ksetupremoverealm"></a>Ksetup: removerealm



Löscht alle Informationen für den angegebenen Bereich aus der Registrierung. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird.|

## <a name="remarks"></a>Hinweise

Der Bereichs Name wird an zwei Stellen in der Registrierung gespeichert: **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001** und **\currentcontrolset\control\lsa\kerberos**.

Der Standard Bereichs Name kann nicht vom Domänen Controller entfernt werden, da dadurch seine DNS-Informationen zurückgesetzt werden, und durch das Entfernen kann der Domänen Controller unbrauchbar werden.

## <a name="BKMK_Examples"></a>Beispiele

Legen Sie den Bereichs Namen versehentlich fest, indem Sie ". com" auf dem lokalen Computer auf Corp festlegen. CONTOSO. Lexikon
```
ksetup /setrealm CORP.CONTOSO.CON
```
Entfernen Sie den fehlerhaften Bereichs Namen auf dem lokalen Computer:
```
ksetup /removerealm CORP.CONTOSO.CON
```
Überprüfen Sie das Entfernen, indem Sie **Ksetup** ausführen und die Ausgabe überprüfen.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)