---
title: FTP-Benutzer
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29081bd8c5d537e1f060e4c848b720a60b4c8aea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842853"
---
# <a name="ftp-user"></a>FTP: Benutzer

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt einen Benutzer für den Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
user <UserName> [<Password>] [<Account>]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                                                                      Beschreibung                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          Gibt einen Benutzernamen an, mit dem sich beim Remote Computer anmelden soll.                                           |
| [<Password>] |               Gibt das Kennwort für den *Benutzernamen*an. Wenn kein Kennwort angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kennworts aufgefordert.               |
| [<Account>]  | Gibt ein Konto an, mit dem Sie sich beim Remote Computer anmelden können. Wenn kein *Konto* angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kontos aufgefordert. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Geben Sie user1 mit dem Kennwort Password1 an.  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
