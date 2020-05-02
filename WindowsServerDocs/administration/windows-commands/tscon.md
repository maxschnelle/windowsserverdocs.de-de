---
title: tscon
description: Referenz Thema für tscon, das eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) herstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a95b7b63f91e7450d949ded294a48c2596e385db
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721273"
---
# <a name="tscon"></a>tscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server her.  

  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
### <a name="parameters"></a>Parameter  

|Parameter|BESCHREIBUNG|  
|-------|--------|  
|\<SessionID->|Gibt die ID der Sitzung an, mit der Sie eine Verbindung herstellen möchten. Wenn Sie den optionalen Parameter **/dest:**<*Sessionname*> verwenden, ist dies die ID der Sitzung, mit der Sie eine Verbindung herstellen möchten.|  
|\<Sessionname->|Gibt den Namen der Sitzung an, mit der Sie eine Verbindung herstellen möchten.|  
|/dest:\<Sessionname>|Gibt den Namen der aktuellen Sitzung an. Diese Sitzung wird getrennt, wenn Sie eine Verbindung mit der neuen Sitzung herstellen.|  
|/Password:\<PW->|Gibt das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten. Dieses Kennwort ist erforderlich, wenn der Benutzer, der die Verbindung herstellt, die Sitzung nicht besitzt.|  
|/Password: *|fordert das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten.|  
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Bemerkungen  
-   Zum Herstellen einer Verbindung mit einer anderen Sitzung müssen Sie über die Berechtigung "Vollzugriff" verfügen oder eine spezielle Zugriffsberechtigung herstellen.  
-   Mit dem Parameter " **/dest:**<*Sessionname*>" können Sie die Sitzung eines anderen Benutzers mit einer anderen Sitzung verbinden.  
-   Wenn Sie im <*Password*>-Parameter kein Kennwort angeben und die Ziel Sitzung zu einem anderen Benutzer als dem aktuellen gehört, schlägt **tscon** fehl.  
-   Sie können keine Verbindung mit der Konsolen Sitzung herstellen.  

## <a name="examples"></a>Beispiele  
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
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
  - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)  
