---
title: pubprn
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8696a372902f36f703670cf514bddf75cf4cc7e3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837103"
---
# <a name="pubprn"></a>pubprn

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Veröffentlicht einen Drucker in den Active Directory-Domänen Diensten.

## <a name="syntax"></a>Syntax
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
LDAP://CN=<Container>,DC=<Container>
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<Servername >|Gibt den Namen des Windows-Servers an, der den zu veröffentlichenden Drucker hostet. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|
|\<uncprinterpath->|Der UNC-Pfad (Universal Naming Convention) zu dem freigegebenen Drucker, den Sie veröffentlichen möchten.|
|LDAP://CN =<Container>, DC =<Container>|Gibt den Pfad zum Container in den Active Directory-Domänen Diensten an, in dem Sie den Drucker veröffentlichen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der **Pubprn** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\<language>" befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der Pubprn-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `computer Name`).

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Wenn Sie alle Drucker auf dem Computer \\\server1 im Container MyContainer in der Domäne mydomain.Company.com veröffentlichen möchten, geben Sie Folgendes ein:
```
cscript Ppubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```
Geben Sie Folgendes ein, um den Laserprinter1-Drucker auf dem \\\server1-Server im Container MyContainer in der Domäne mydomain.Company.com zu veröffentlichen:
```
cscript Ppubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
