---
title: reset session
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 67a4e910ba87209c9700f2242f7859a6cc9e725f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384528"
---
# <a name="reset-session"></a>reset session

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Zurücksetzen (Löschen) einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).  
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

## <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|\<sessionname >|Gibt den Namen der Sitzung an, die Sie zurücksetzen möchten. Um den Namen der Sitzung zu ermitteln, verwenden Sie den Befehl **Abfrage Sitzung** .|  
|\<sessionid >|Gibt die ID der zurück zusetzenden Sitzung an.|  
|/Server: \<servername >|Gibt den Terminal Server mit der Sitzung an, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|  
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Sie können jederzeit eigene Sitzungen zurücksetzen, aber Sie müssen über die Berechtigung "Vollzugriff" verfügen, um die Sitzung eines anderen Benutzers zurückzusetzen.  
-   Beachten Sie, dass das Zurücksetzen der Sitzung eines Benutzers ohne Warnung den Benutzer zum Verlust von Daten in der Sitzung führen kann.  
-   Sie sollten eine Sitzung nur dann zurücksetzen, wenn Sie nicht mehr reagiert oder anscheinend nicht mehr reagiert.  
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie die **Reset-Sitzung** von einem Remote Server aus verwenden.  

## <a name="BKMK_examples"></a>Beispiele  
- Geben Sie Folgendes ein, um die für RDP-TCP # 6 vorgesehene Sitzung zurückzusetzen:  
  ```  
  reset session rdp-tcp#6  
  ```  
- Um die Sitzung zurückzusetzen, die Sitzungs-ID 3 verwendet, geben Sie Folgendes ein:  
  ```  
  reset session 3  
  ```  

#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Remotedesktopdienste &#40;Befehlsreferenz&#41; für terminaldienstedienste](remote-desktop-services-terminal-services-command-reference.md)  
