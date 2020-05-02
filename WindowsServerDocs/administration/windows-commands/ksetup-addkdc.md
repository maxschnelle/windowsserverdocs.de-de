---
title: 'Ksetup: addkdc'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76d592e4f1c32305d6f939a66a6ad42cd582b032
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724765"
---
# <a name="ksetupaddkdc"></a>Ksetup: addkdc



Fügt eine Schlüsselverteilungscenter (KDC)-Adresse für den angegebenen Kerberos-Bereich hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird. In diesem Bereich versuchen Sie, den anderen KDC hinzuzufügen.|
|\<Kdcname->|Der KDC-Name wird als voll qualifizierter Domänen Name angegeben, z. b. mitkdc.Microsoft.com. Wenn der KDC-Name ausgelassen wird, sucht DNS nach KDCs.|

## <a name="remarks"></a>Bemerkungen

Diese Zuordnungen werden in der Registrierung unter **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**gespeichert. Um Kerberos-Bereichs Konfigurationsdaten auf mehreren Computern bereitzustellen, verwenden Sie das Snap-in "Sicherheits Konfigurations Vorlage" und die Richtlinien Verteilung anstelle der expliziten Verwendung von **Ksetup** auf einzelnen Computern.

Der Computer muss neu gestartet werden, bevor die neue Bereichseinstellung verwendet wird.

Um den Standard Bereichs Namen für den Computer zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** an der Eingabeaufforderung aus, und überprüfen Sie die Ausgabe für den hinzugefügten KDC.

## <a name="examples"></a>Beispiele

Konfigurieren Sie einen nicht-Windows-KDC-Server und den Bereich, der von der Arbeitsstation verwendet werden soll:
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
Führen Sie das Ksetup-Tool in der Befehlszeile desselben Computers wie im vorherigen Befehl aus, um das Kennwort für das lokale p@sswrd1Computer Konto auf% festzulegen. Starten Sie den Computer anschließend neu.
```
Ksetup /setcomputerpassword p@sswrd1%
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)