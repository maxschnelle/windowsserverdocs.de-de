---
title: FTP-Benutzer
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1c9406af0868421fa54fe757742cf2a120561b9c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438347"
---
# <a name="ftp-user"></a>FTP: Benutzer

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Gibt ein Benutzer mit dem Remotecomputer an.   
## <a name="syntax"></a>Syntax  
```  
user <UserName> [<Password>] [<Account>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                                                                      Beschreibung                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <UserName>  |                                          Gibt einen Benutzernamen mit dem Melden Sie sich an den Remotecomputer.                                           |
| [<Password>] |               Gibt das Kennwort für *Benutzername*. Wenn ein Kennwort nicht angegeben ist, jedoch erforderlich ist, **ftp** fordert das Kennwort.               |
| [<Account>]  | Gibt ein Konto mit dem Melden Sie sich an den Remotecomputer. Wenn ein *Konto* wird nicht angegeben, aber es ist erforderlich, **ftp** für das Konto aufgefordert. |

## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie mit dem Kennwort Password1 "user1" ein.  
```  
user User1 Password1  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
