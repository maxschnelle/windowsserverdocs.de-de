---
title: 'Ksetup: ChangePassword'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68b14388ff3c33458873b494c8d5a770b44f7545
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841783"
---
# <a name="ksetupchangepassword"></a>Ksetup: ChangePassword



Verwendet das Kennwort für den Schlüsselverteilungscenter (KDC)-Kennwort (kpasswd), um das Kennwort des angemeldeten Benutzers zu ändern. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

#### <a name="parameters"></a>Parameter

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

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)