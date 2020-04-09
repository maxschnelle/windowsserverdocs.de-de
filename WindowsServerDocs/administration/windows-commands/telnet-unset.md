---
title: Telnet nicht festgelegt
description: Windows-Befehls Thema für Telnet unset, das zuvor festgelegte Optionen deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34d52eedb2a5547ad0e3f2912dbe2a250eaf8fc5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833143"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert zuvor festgelegte Optionen.   

## <a name="syntax"></a>Syntax  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|bsasdel|Sendet **Rückraum** als **RÜCKTASTE**.|  
|CRLF|Sendet die **Eingabe** Taste als CR. Wird auch als Zeilenvorschub Modus bezeichnet.|  
|Delta-|Sendet **Delete** als **Delete**.|  
|Escape|entfernt die Einstellung für das Escapezeichen.|  
|LOCALECHO|Deaktiviert LOCALECHO.|  
|Protokollieren|Deaktiviert die Protokollierung.|  
|ntlm|Deaktiviert die NTLM-Authentifizierung.|  
|?|Zeigt die Hilfe für diesen Befehl an.|  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Deaktivieren Sie die Protokollierung.  
```  
u logging  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
