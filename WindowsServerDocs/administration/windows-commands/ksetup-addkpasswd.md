---
title: 'Ksetup: addkpasswd'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c260c711ae87f88be8b9466e73afaf3fe1c83a1e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724734"
---
# <a name="ksetupaddkpasswd"></a>Ksetup: addkpasswd



Fügt ein Kerberos-Kennwort (kpasswd)-Server Adresse für einen Bereich hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

#### <a name="parameters"></a>Parameter

Wenn der Kerberos-Bereich, bei dem die Arbeitsstation authentifiziert wird, das Kerberos-Änderungs Kennwort-Protokoll unterstützt, können Sie einen Client Computer mit dem Windows-Betriebssystem für die Verwendung eines Kerberos-Kenn Wort Servers konfigurieren. Diese Einstellung wird auf der Bereichs Seite konfiguriert.

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. Bereich angezeigt, wenn **Ksetup** ausgeführt wird.|
|\<Kpasswdname->|Der KDC-Name, der als Kerberos-Kenn Wort Server verwendet werden soll, wird als voll qualifizierter Domänen Name angegeben, z. b. mitkdc.Microsoft.com. Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen.|

## <a name="remarks"></a>Bemerkungen

Wenn der Kerberos-Bereich, bei dem die Arbeitsstation authentifiziert wird, das Kerberos-Änderungs Kennwort-Protokoll unterstützt, können Sie einen Client Computer mit dem Windows-Betriebssystem für die Verwendung eines Kerberos-Kenn Wort Servers konfigurieren.

Führen Sie den Befehl **Ksetup** aus, um den KDC-Namen zu überprüfen. Wenn **kpasswd =** nicht in der Ausgabe angezeigt wird, wurde die Zuordnung nicht konfiguriert.

Sie können weitere KDC-Namen einzeln hinzufügen.

## <a name="examples"></a>Beispiele

Konfigurieren Sie den Bereich Corp. CONTOSO.com, damit der nicht-Windows-KDC-Server, mitkdc.contoso.com, als Kenn Wort Server verwendet wird:
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Dies führt zu einem nicht-Windows-Kerberos-Kenn Wort Server, der alle Kenn Wörter für die Authentifizierung zwischen ihm und dem Bereich steuert.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)