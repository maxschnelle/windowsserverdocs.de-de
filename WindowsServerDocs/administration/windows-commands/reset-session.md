---
title: reset session
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b83aa67e0d90be9ddc679b32c8ffa4270efec41f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835793"
---
# <a name="reset-session"></a>reset session

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Zurücksetzen (Löschen) einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).  
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).  

> [!NOTE]  
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

### <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|\<Sessionname >|Gibt den Namen der Sitzung an, die Sie zurücksetzen möchten. Um den Namen der Sitzung zu ermitteln, verwenden Sie den Befehl **Abfrage Sitzung** .|  
|\<SessionID >|Gibt die ID der zurück zusetzenden Sitzung an.|  
|/Server:\<Servername >|Gibt den Terminal Server mit der Sitzung an, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|  
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Sie können jederzeit eigene Sitzungen zurücksetzen, aber Sie müssen über die Berechtigung "Vollzugriff" verfügen, um die Sitzung eines anderen Benutzers zurückzusetzen.  
-   Beachten Sie, dass das Zurücksetzen der Sitzung eines Benutzers ohne Warnung den Benutzer zum Verlust von Daten in der Sitzung führen kann.  
-   Sie sollten eine Sitzung nur dann zurücksetzen, wenn Sie nicht mehr reagiert oder anscheinend nicht mehr reagiert.  
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie die **Reset-Sitzung** von einem Remote Server aus verwenden.  

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
- Geben Sie Folgendes ein, um die für RDP-TCP # 6 vorgesehene Sitzung zurückzusetzen:  
  ```  
  reset session rdp-tcp#6  
  ```  
- Um die Sitzung zurückzusetzen, die Sitzungs-ID 3 verwendet, geben Sie Folgendes ein:  
  ```  
  reset session 3  
  ```  

## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)  
