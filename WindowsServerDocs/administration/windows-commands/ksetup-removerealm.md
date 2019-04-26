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
ms.openlocfilehash: 3f62208d6576890529be80b1c6cb3cc073a2b4e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853361"
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

Legen Sie den Bereichsnamen versehentlich durch den Namen ". COM? Klicken Sie auf dem lokalen Computer CORP. CONTOSO. CON
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
-   [Befehlszeilensyntax](command-line-syntax-key.md)