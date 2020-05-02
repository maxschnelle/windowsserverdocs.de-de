---
title: FTP-Benutzer
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb4f0f47f23bec312c57266479c261c96535e8cc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725066"
---
# <a name="ftp-user"></a>FTP: Benutzer

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt einen Benutzer für den Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
user <UserName> [<Password>] [<Account>]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                                                                      BESCHREIBUNG                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          Gibt einen Benutzernamen an, mit dem sich beim Remote Computer anmelden soll.                                           |
| [<Password>] |               Gibt das Kennwort für den *Benutzernamen*an. Wenn kein Kennwort angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kennworts aufgefordert.               |
| [<Account>]  | Gibt ein Konto an, mit dem Sie sich beim Remote Computer anmelden können. Wenn kein *Konto* angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kontos aufgefordert. |

## <a name="examples"></a>Beispiele  
Geben Sie user1 mit dem Kennwort Password1 an.  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
