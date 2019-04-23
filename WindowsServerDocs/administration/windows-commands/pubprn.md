---
title: pubprn
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 499ff2ade7ffc6c608791ba3da0ede0c3282c13d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831701"
---
# <a name="pubprn"></a>pubprn

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Einen Drucker veröffentlicht in der active Directory-Domänendiensten.

## <a name="syntax"></a>Syntax
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
"LDAP://CN=<Container>,DC=<Container>"
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<ServerName>|Gibt den Namen des Windows-Servers, der den Drucker hostet, den Sie veröffentlichen möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|\<UNCprinterpath>|Der Pfad der Universal Naming Convention (UNC) an den freigegebenen Drucker, den Sie veröffentlichen möchten.|
|"LDAP://CN=<Container>,DC=<Container>"|Gibt den Pfad zum Container in active Directory-Domänendienste, in dem Sie den Drucker veröffentlichen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **"Pubprn"** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die "Pubprn"-Datei, oder wechseln in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele für
Veröffentlichen Sie alle Drucker auf dem \\\Server1-Computer, auf den Container "MyContainer" in der Domäne MyDomain.company.Com geben:
```
cscript Ppubprn Server1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```
Veröffentlichen Sie den Drucker Laserprinter1 auf die \\\Server1-Server, auf den Container "MyContainer" in der Domäne MyDomain.company.Com, Typ:
```
cscript Ppubprn \\Server1\Laserprinter1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
