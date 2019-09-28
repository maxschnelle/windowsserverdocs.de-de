---
title: 'Ksetup: ChangePassword'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 51be9e71c2b290e6346d23144543e0eec29f9d07
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375182"
---
# <a name="ksetupchangepassword"></a>Ksetup: ChangePassword



Verwendet das Kennwort für den Schlüsselverteilungscenter (KDC)-Kennwort (kpasswd), um das Kennwort des angemeldeten Benutzers zu ändern. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<oldpasswd >|Gibt das vorhandene Kennwort des angemeldeten Benutzers an.|
|\<newpasswd >|Gibt das neue Kennwort des angemeldeten Benutzers an.|

## <a name="remarks"></a>Hinweise

Dieser Befehl verwendet den KDC Password-Wert (kpasswd), um das Kennwort des angemeldeten Benutzers zu ändern. Wenn festgelegt, wird "kpasswd" in der Ausgabe angezeigt, indem der Befehl " **Ksetup/dumpstate** " ausgeführt wird.

Das neue Kennwort des Benutzers muss alle Kenn Wort Anforderungen erfüllen, die auf diesem Computer festgelegt sind.

Wenn das Benutzerkonto in der aktuellen Domäne nicht gefunden wird, werden Sie vom System aufgefordert, den Domänen Namen anzugeben, in dem sich das Benutzerkonto befindet.

Wenn Sie bei der nächsten Anmeldung eine Kenn Wort Änderung erzwingen möchten, kann mit diesem Befehl das Sternchen (*) verwendet werden, damit der Benutzer zur Eingabe eines neuen Kennworts aufgefordert wird.

Die Ausgabe des Befehls informiert Sie über den Status Erfolg oder Fehler.

## <a name="BKMK_Examples"></a>Beispiele

Ändern Sie das Kennwort eines Benutzers, der zurzeit in dieser Domäne an diesem Computer angemeldet ist:
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
Ändern Sie das Kennwort eines Benutzers, der zurzeit in der Domäne "Domäne" angemeldet ist:
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
Erzwingen Sie, dass der aktuell angemeldete Benutzer das Kennwort bei der nächsten Anmeldung ändert:
```
ksetup /changepassword Pas$w0rd *
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)