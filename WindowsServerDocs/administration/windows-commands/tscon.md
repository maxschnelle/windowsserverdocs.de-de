---
title: tscon
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8267a35aefc279ff57ce3d200415e16e431775f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883061"
---
# <a name="tscon"></a>tscon

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Eine Verbindung mit einer anderen Sitzung auf einem Server Remote Desktop Session Host (rd Session Host).  
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|\<SessionID>|Gibt die ID der Sitzung, die Sie eine Verbindung herstellen möchten. Bei Verwendung des optionalen **dest:**<*Sitzungsname*>-Parameter, dies ist die ID der Sitzung, die Sie eine Verbindung herstellen möchten.|  
|\<SessionName>|Gibt den Namen der Sitzung, die Sie eine Verbindung herstellen möchten.|  
|/dest:\<SessionName>|Gibt den Namen der aktuellen Sitzung. Diese Sitzung wird getrennt, wenn Sie mit der neuen Sitzung verbinden.|  
|/password:\<pw>|Gibt das Kennwort des Benutzers, der die Sitzung besitzt, die Sie eine Verbindung herstellen möchten. Dieses Kennwort ist erforderlich, wenn der Benutzer eine Verbindung herstellt, nicht die Sitzung besitzt.|  
|/password:*|Anweisungen für das Kennwort des Benutzers, der die Sitzung besitzt, die Sie eine Verbindung herstellen möchten.|  
|/v|Zeigt Informationen zu den Aktionen, die ausgeführt wird.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Sie müssen über die Berechtigung Vollzugriff oder spezielle Berechtigung zur Verbindung mit einer anderen Sitzung verbinden.  
-   Die **dest:**<*Sitzungsname*>-Parameter können Sie die Sitzung eines anderen Benutzers mit einer anderen Sitzung verbinden.  
-   Wenn Sie ein Kennwort nicht angeben der <*Kennwort*> Parameter, und der zielsitzung gehört zu einem anderen Benutzer als der aktuelle Knoten **Tscon** ein Fehler auftritt.  
-   Sie können nicht mit der Konsole-Sitzung verbinden.  

## <a name="BKMK_examples"></a>Beispiele für  
-   Um mit 12-Sitzung auf dem aktuellen rd Session Host-Server verbunden sind und die aktuelle Sitzung zu trennen, geben Sie Folgendes ein:  
    ```  
    tscon 12  
    ```  
-   Um eine Verbindung herstellen mit 23-Sitzung auf dem aktuellen RD-Sitzungshostserver, mit dem Kennwort Mypass und die aktuelle Sitzung zu trennen, geben Sie Folgendes ein:  
    ```  
    tscon 23 /password:mypass  
    ```  
-   Um die Sitzung TERM03 und der Sitzung TERM05 verbunden sind, und dann Sitzung TERM05 zu trennen, wenn er verbunden ist, geben Sie Folgendes ein:  
    ```  
    tscon TERM03 /v /dest:TERM05  
    ```  
#### <a name="additional-references"></a>Weitere Verweise  
[Befehlszeilensyntax](command-line-syntax-key.md)  
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)  
