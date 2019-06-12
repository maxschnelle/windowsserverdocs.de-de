---
title: reset session
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5a0991c76ba890bb94b0dcf258df6207ed228e72
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441795"
---
# <a name="reset-session"></a>reset session

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ermöglicht Ihnen, zurücksetzen (löschen) eine Sitzung auf einem Server Remote Desktop Session Host (rd Session Host).  
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).  

> [!NOTE]  
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.  

## <a name="syntax"></a>Syntax  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

## <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|\<SessionName>|Gibt den Namen der Sitzung, die Sie zurücksetzen möchten. Verwenden Sie den Namen der Sitzung zu ermitteln, die **Abfragen Sitzung** Befehl.|  
|\<SessionID>|Gibt die ID der Sitzung zurücksetzen.|  
|/server:\<ServerName>|Gibt den Terminalserver mit der Sitzung, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle rd Session Host-Server verwendet.|  
|/v|Zeigt Informationen zu den Aktionen, die ausgeführt wird.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Sie können immer Ihre eigene Sitzung zurücksetzen, aber benötigen Sie Zugriff Full Control-Berechtigung zum Zurücksetzen der Sitzung eines anderen Benutzers.  
-   Denken Sie daran, die Zurücksetzen der Sitzung eines Benutzers ohne der Benutzer Warnmeldungen in der Sitzung zum Verlust von Daten führen kann.  
-   Sie sollten eine-Sitzung zurücksetzen, nur wenn ein Fehler auftritt oder reagiert.  
-   Die **/Server** Parameter ist erforderlich, nur bei Verwendung von **-Sitzung zurücksetzen** von einem Remoteserver.  

## <a name="BKMK_examples"></a>Beispiele für  
- Geben Sie zum Zurücksetzen der Sitzungs, die Rdp-TCP-Nr. 6 festgelegt:  
  ```  
  reset session rdp-tcp#6  
  ```  
- Um die Sitzung zurücksetzen, die Sitzungs-ID 3 verwendet, geben Sie Folgendes ein:  
  ```  
  reset session 3  
  ```  

#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)  
