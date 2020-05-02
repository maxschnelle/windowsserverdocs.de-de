---
title: 'Ksetup: removerealm'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb7bf4663594a6c164d6495a9ba4cd81942afb79
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724607"
---
# <a name="ksetupremoverealm"></a>Ksetup: removerealm



Löscht alle Informationen für den angegebenen Bereich aus der Registrierung.

## <a name="syntax"></a>Syntax

```
ksetup /removerealm <RealmName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird.|

## <a name="remarks"></a>Bemerkungen

Der Bereichs Name wird an zwei Stellen in der Registrierung gespeichert: **HKEY_LOCAL_MACHINE \system\controlset001** und **\currentcontrolset\control\lsa\kerberos**.

Der Standard Bereichs Name kann nicht vom Domänen Controller entfernt werden, da dadurch seine DNS-Informationen zurückgesetzt werden, und durch das Entfernen kann der Domänen Controller unbrauchbar werden.

## <a name="examples"></a>Beispiele

Legen Sie den Bereichs Namen versehentlich auf dem lokalen Computer auf dem lokalen Computer auf Corp fest. CONTOSO. Lexikon
```
ksetup /setrealm CORP.CONTOSO.CON
```
Entfernen Sie den fehlerhaften Bereichs Namen auf dem lokalen Computer:
```
ksetup /removerealm CORP.CONTOSO.CON
```
Überprüfen Sie das Entfernen, indem Sie **Ksetup** ausführen und die Ausgabe überprüfen.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)