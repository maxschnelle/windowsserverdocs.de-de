---
title: pubprn
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17ca9e98ef9e3423521b03c5c21be4b3f1538b62
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722776"
---
# <a name="pubprn"></a>pubprn

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Veröffentlicht einen Drucker in den Active Directory-Domänen Diensten.

## <a name="syntax"></a>Syntax
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
LDAP://CN=<Container>,DC=<Container>
```

### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|\<Servername>|Gibt den Namen des Windows-Servers an, der den zu veröffentlichenden Drucker hostet. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|
|\<Uncprinterpath->|Der UNC-Pfad (Universal Naming Convention) zu dem freigegebenen Drucker, den Sie veröffentlichen möchten.|
|LDAP://CN =<Container>, DC =<Container>|Gibt den Pfad zum Container in den Active Directory-Domänen Diensten an, in dem Sie den Drucker veröffentlichen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
-   Der **Pubprn** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\ <language> " befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der Pubprn-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen `computer Name`(z. b.).

## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um \\alle Drucker auf dem Computer "\server1" im Container MyContainer in der Domäne mydomain.Company.com zu veröffentlichen:
```
cscript Ppubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```
Zum Veröffentlichen des Laserprinter1-Druckers \\auf dem Server "\server1" im Container "MyContainer" in der Domäne "mydomain.Company.com" geben Sie Folgendes ein:
```
cscript Ppubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
