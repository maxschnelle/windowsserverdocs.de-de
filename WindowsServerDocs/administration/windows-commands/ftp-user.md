---
title: FTP-Benutzer
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63281a0ffdd646d3652eb3a442a8edd9acec9cce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375869"
---
# <a name="ftp-user"></a>FTP: Benutzer

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt einen Benutzer für den Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
user <UserName> [<Password>] [<Account>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                                                                      Beschreibung                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          Gibt einen Benutzernamen an, mit dem sich beim Remote Computer anmelden soll.                                           |
| [<Password>] |               Gibt das Kennwort für den *Benutzernamen*an. Wenn kein Kennwort angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kennworts aufgefordert.               |
| [<Account>]  | Gibt ein Konto an, mit dem Sie sich beim Remote Computer anmelden können. Wenn kein *Konto* angegeben ist, aber erforderlich ist, werden Sie von **FTP** zur Eingabe des Kontos aufgefordert. |

## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie user1 mit dem Kennwort Password1 an.  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
