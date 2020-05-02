---
title: Telnet nicht festgelegt
description: Referenz Thema für die Unmenge von Telnet, die zuvor festgelegte Optionen deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d88f5e479564cad8e2ec7e82dbb4f4cef35cd012
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721465"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert zuvor festgelegte Optionen.   

## <a name="syntax"></a>Syntax  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|bsasdel|Sendet **Rückraum** als **RÜCKTASTE**.|  
|CRLF|Sendet die **Eingabe** Taste als CR. Wird auch als Zeilenvorschub Modus bezeichnet.|  
|Delta-|Sendet **Delete** als **Delete**.|  
|Escape|entfernt die Einstellung für das Escapezeichen.|  
|LOCALECHO|Deaktiviert LOCALECHO.|  
|logging|Schaltet die Protokollierung aus.|  
|ntlm|Deaktiviert die NTLM-Authentifizierung.|  
|?|Zeigt die Hilfe für diesen Befehl an.|  
## <a name="examples"></a>Beispiele  
Deaktivieren Sie die Protokollierung.  
```  
u logging  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
