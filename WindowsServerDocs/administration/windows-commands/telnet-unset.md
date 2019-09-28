---
title: Telnet nicht festgelegt
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6f0eb98c4168d2f664780dad42ca1aea5463d24
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383484"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert zuvor festgelegte Optionen.   
## <a name="syntax"></a>Syntax  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|bsasdel|Sendet **Rückraum** als **RÜCKTASTE**.|  
|CRLF|Sendet die **Eingabe** Taste als CR. Wird auch als Zeilenvorschub Modus bezeichnet.|  
|Delta-|Sendet **Delete** als **Delete**.|  
|Weg|entfernt die Einstellung für das Escapezeichen.|  
|LOCALECHO|Deaktiviert LOCALECHO.|  
|logging|Deaktiviert die Protokollierung.|  
|NTLM|Deaktiviert die NTLM-Authentifizierung.|  
|?|Zeigt die Hilfe für diesen Befehl an.|  
## <a name="BKMK_Examples"></a>Beispiele  
Deaktivieren Sie die Protokollierung.  
```  
u logging  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
