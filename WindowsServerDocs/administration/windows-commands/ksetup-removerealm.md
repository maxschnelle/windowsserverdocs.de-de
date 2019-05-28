---
title: ksetup:removerealm
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 579b0772e4642389b90aa370dad80a3eebea9d34
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564719"
---
# <a name="ksetupremoverealm"></a>ksetup:removerealm



Löscht alle Informationen für den angegebenen Bereich aus der Registrierung. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /removerealm <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com", und es wird als den Standardbereich aufgeführt beim **Ksetup** ausgeführt wird.|

## <a name="remarks"></a>Hinweise

Der Bereichsname werden an zwei Stellen in der Registrierung gespeichert: **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001** und **\CurrentControlSet\Control\Lsa\Kerberos**.

Der Standardname der Bereich kann nicht vom Domänencontroller entfernt werden, da Hiermit wird der DNS-Serverinformationen zurückgesetzt, und entfernen Sie es kann sein, des Domänencontrollers kann nicht verwendet werden dass.

## <a name="BKMK_Examples"></a>Beispiele für

Versehentlich legen Sie den Bereichsnamen von Tippfehler ".COM" auf dem lokalen Computer CORP. CONTOSO. CON
```
ksetup /setrealm CORP.CONTOSO.CON
```
Fehlerhafte Bereichsnamen aus dem lokalen Computer zu entfernen:
```
ksetup /removerealm CORP.CONTOSO.CON
```
Die Entfernung überprüfen, indem Sie Ausführung **Ksetup** und überprüfen Sie die Ausgabe.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:setrealm](ksetup-setrealm.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)