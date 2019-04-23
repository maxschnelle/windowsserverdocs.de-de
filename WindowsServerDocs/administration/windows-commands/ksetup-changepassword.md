---
title: ksetup:changepassword
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f629c6c7930777583df38f5af900ed380ec60f9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878531"
---
# <a name="ksetupchangepassword"></a>ksetup:changepassword



Verwendet die Wert für das Schlüsselverteilungscenter (Key Distribution Center, KDC)-Kennwort (Kpasswd) zum Ändern des Kennworts des angemeldeten Benutzers. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<OldPasswd>|Gibt die vorhandenen Kennwort des angemeldeten Benutzers.|
|\<NewPasswd>|Gibt die protokollierten auf das neue Kennwort des Benutzers an.|

## <a name="remarks"></a>Hinweise

Dieser Befehl verwendet den KDC-Kennwortwert (Kpasswd), um das Kennwort des angemeldeten Benutzers zu ändern. Die Kpasswd, wenn festgelegt ist, wird in der Ausgabe angezeigt, mit der **Ksetup /dumpstate** Befehl.

Neues Kennwort des Benutzers muss es sich um die kennwortanforderungen erfüllen, die auf diesem Computer festgelegt sind.

Wenn das Benutzerkonto, das nicht in der aktuellen Domäne gefunden wird, fragt das System Sie den Domänennamen angeben, in dem sich das Benutzerkonto befindet.

Wenn Sie eine kennwortänderung bei der nächsten Anmeldung erzwingen möchten, kann mit diesem Befehl das Sternchen (*), damit der Benutzer ein neues Kennwort aufgefordert werden.

Die Ausgabe des Befehls informiert Sie über den Erfolg oder Fehler Status.

## <a name="BKMK_Examples"></a>Beispiele für

Ändern Sie das Kennwort eines Benutzers, der für diesen Computer in dieser Domäne angemeldet ist:
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
Ändern Sie das Kennwort eines Benutzers, die derzeit in der Contoso-Domäne angemeldet ist:
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
Erzwingen des derzeit angemeldeten Benutzers das Kennwort bei der nächsten Anmeldung ändern:
```
ksetup /changepassword Pas$w0rd *
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)