---
title: tscon
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e53ea2888b66b9e4fbf026f752acf9803270fc2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392364"
---
# <a name="tscon"></a>tscon

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) her.  
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
## <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|\<sessionid >|Gibt die ID der Sitzung an, mit der Sie eine Verbindung herstellen möchten. Wenn Sie den optionalen Parameter **/dest:** <*Sessionname*> verwenden, ist dies die ID der Sitzung, mit der Sie eine Verbindung herstellen möchten.|  
|\<sessionname >|Gibt den Namen der Sitzung an, mit der Sie eine Verbindung herstellen möchten.|  
|/dest: \<sessionname >|Gibt den Namen der aktuellen Sitzung an. Diese Sitzung wird getrennt, wenn Sie eine Verbindung mit der neuen Sitzung herstellen.|  
|/Password: \<pw >|Gibt das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten. Dieses Kennwort ist erforderlich, wenn der Benutzer, der die Verbindung herstellt, die Sitzung nicht besitzt.|  
|/Password: *|fordert das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten.|  
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Zum Herstellen einer Verbindung mit einer anderen Sitzung müssen Sie über die Berechtigung "Vollzugriff" verfügen oder eine spezielle Zugriffsberechtigung herstellen.  
-   Mit dem Parameter " **/dest:** <*Sessionname*>" können Sie die Sitzung eines anderen Benutzers mit einer anderen Sitzung verbinden.  
-   Wenn Sie im <*Password*>-Parameter kein Kennwort angeben und die Ziel Sitzung zu einem anderen Benutzer als dem aktuellen gehört, schlägt **tscon** fehl.  
-   Sie können keine Verbindung mit der Konsolen Sitzung herstellen.  

## <a name="BKMK_examples"></a>Beispiele  
- Geben Sie Folgendes ein, um eine Verbindung mit Sitzung 12 auf dem aktuellen RD-Sitzungs Host Server herzustellen und die aktuelle Sitzung zu trennen:  
  ```  
  tscon 12  
  ```  
- Geben Sie Folgendes ein, um eine Verbindung mit der Sitzung 23 auf dem aktuellen Remote Desktop-Sitzungs Host Server herzustellen, indem Sie das Kennwort mypass verwenden und die aktuelle Sitzung trennen:  
  ```  
  tscon 23 /password:mypass  
  ```  
- Wenn Sie die Sitzung mit dem Namen TERM03 mit der Sitzung namens TERM05 verbinden und dann Session TERM05 trennen möchten, geben Sie Folgendes ein, wenn eine Verbindung besteht:  
  ```  
  tscon TERM03 /v /dest:TERM05  
  ```  
  #### <a name="additional-references"></a>Weitere Verweise  
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  [Remotedesktopdienste &#40;Befehlsreferenz&#41; für terminaldienstedienste](remote-desktop-services-terminal-services-command-reference.md)  
