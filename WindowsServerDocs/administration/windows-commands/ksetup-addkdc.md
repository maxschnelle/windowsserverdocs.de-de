---
title: 'Ksetup: addkdc'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bb31cbc8ba7920c4ba609f86202e2e62a705078
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841833"
---
# <a name="ksetupaddkdc"></a>Ksetup: addkdc



Fügt eine Schlüsselverteilungscenter (KDC)-Adresse für den angegebenen Kerberos-Bereich hinzu. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird. In diesem Bereich versuchen Sie, den anderen KDC hinzuzufügen.|
|\<kdcname >|Der KDC-Name wird als voll qualifizierter Domänen Name angegeben, z. b. mitkdc.Microsoft.com. Wenn der KDC-Name ausgelassen wird, sucht DNS nach KDCs.|

## <a name="remarks"></a>Hinweise

Diese Zuordnungen werden in der Registrierung unter **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**gespeichert. Um Kerberos-Bereichs Konfigurationsdaten auf mehreren Computern bereitzustellen, verwenden Sie das Snap-in "Sicherheits Konfigurations Vorlage" und die Richtlinien Verteilung anstelle der expliziten Verwendung von **Ksetup** auf einzelnen Computern.

Der Computer muss neu gestartet werden, bevor die neue Bereichseinstellung verwendet wird.

Um den Standard Bereichs Namen für den Computer zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** an der Eingabeaufforderung aus, und überprüfen Sie die Ausgabe für den hinzugefügten KDC.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Konfigurieren Sie einen nicht-Windows-KDC-Server und den Bereich, der von der Arbeitsstation verwendet werden soll:
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
Führen Sie das Ksetup-Tool in der Befehlszeile desselben Computers wie im vorherigen Befehl aus, um das Kennwort für das lokale Computer Konto auf p@sswrd1% festzulegen. Starten Sie dann den Computer neu.
```
Ksetup /setcomputerpassword p@sswrd1%
```

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)