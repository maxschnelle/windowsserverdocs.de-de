---
title: 'Ksetup: addkpasswd'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73abfff54ecfcd31ebbd7469c12228fff850fbf1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841823"
---
# <a name="ksetupaddkpasswd"></a>Ksetup: addkpasswd



Fügt ein Kerberos-Kennwort (kpasswd)-Server Adresse für einen Bereich hinzu. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

#### <a name="parameters"></a>Parameter

Wenn der Kerberos-Bereich, bei dem die Arbeitsstation authentifiziert wird, das Kerberos-Änderungs Kennwort-Protokoll unterstützt, können Sie einen Client Computer mit dem Windows-Betriebssystem für die Verwendung eines Kerberos-Kenn Wort Servers konfigurieren. Diese Einstellung wird auf der Bereichs Seite konfiguriert.

|Parameter|Beschreibung|
|---------|-----------|
|\<Realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. Bereich angezeigt, wenn **Ksetup** ausgeführt wird.|
|\<kpasswdname >|Der KDC-Name, der als Kerberos-Kenn Wort Server verwendet werden soll, wird als voll qualifizierter Domänen Name angegeben, z. b. mitkdc.Microsoft.com. Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen.|

## <a name="remarks"></a>Hinweise

Wenn der Kerberos-Bereich, bei dem die Arbeitsstation authentifiziert wird, das Kerberos-Änderungs Kennwort-Protokoll unterstützt, können Sie einen Client Computer mit dem Windows-Betriebssystem für die Verwendung eines Kerberos-Kenn Wort Servers konfigurieren.

Führen Sie den Befehl **Ksetup** aus, um den KDC-Namen zu überprüfen. Wenn **kpasswd =** nicht in der Ausgabe angezeigt wird, wurde die Zuordnung nicht konfiguriert.

Sie können weitere KDC-Namen einzeln hinzufügen.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Konfigurieren Sie den Bereich Corp. CONTOSO.com, damit der nicht-Windows-KDC-Server, mitkdc.contoso.com, als Kenn Wort Server verwendet wird:
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Dies führt zu einem nicht-Windows-Kerberos-Kenn Wort Server, der alle Kenn Wörter für die Authentifizierung zwischen ihm und dem Bereich steuert.

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)