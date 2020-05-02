---
title: reset session
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: df7b953e02c7339b7ed66a831955f802dd21e624
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722361"
---
# <a name="reset-session"></a>reset session

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Zurücksetzen (Löschen) einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).  
  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

### <a name="parameters"></a>Parameter  

|Parameter|BESCHREIBUNG|  
|-------|--------|  
|\<Sessionname->|Gibt den Namen der Sitzung an, die Sie zurücksetzen möchten. Um den Namen der Sitzung zu ermitteln, verwenden Sie den Befehl **Abfrage Sitzung** .|  
|\<SessionID->|Gibt die ID der zurück zusetzenden Sitzung an.|  
|/Server:\<Servername>|Gibt den Terminal Server mit der Sitzung an, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|  
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Bemerkungen  
-   Sie können jederzeit eigene Sitzungen zurücksetzen, aber Sie müssen über die Berechtigung "Vollzugriff" verfügen, um die Sitzung eines anderen Benutzers zurückzusetzen.  
-   Beachten Sie, dass das Zurücksetzen der Sitzung eines Benutzers ohne Warnung den Benutzer zum Verlust von Daten in der Sitzung führen kann.  
-   Sie sollten eine Sitzung nur dann zurücksetzen, wenn Sie nicht mehr reagiert oder anscheinend nicht mehr reagiert.  
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie die **Reset-Sitzung** von einem Remote Server aus verwenden.  

## <a name="examples"></a>Beispiele  
- Geben Sie Folgendes ein, um die für RDP-TCP # 6 vorgesehene Sitzung zurückzusetzen:  
  ```  
  reset session rdp-tcp#6  
  ```  
- Um die Sitzung zurückzusetzen, die Sitzungs-ID 3 verwendet, geben Sie Folgendes ein:  
  ```  
  reset session 3  
  ```  

## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)  
