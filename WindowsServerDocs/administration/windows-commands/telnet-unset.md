---
title: Telnet ist nicht festgelegt
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 37c4d84d1664fdc13ea7ffec60bf981b264dba00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853891"
---
# <a name="telnet-unset"></a>Telnet: nicht festgelegt

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Deaktiviert die zuvor die Set-Optionen.   
## <a name="syntax"></a>Syntax  
```  
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|bsasdel|Sendet **RÜCKTASTE** als eine **RÜCKTASTE**.|  
|crlf|Sendet die **EINGABETASTE** Schlüssel wird als ein CR. Auch bekannt als feed Zeile Modus.|  
|delasbs|Sendet **löschen** als **löschen**.|  
|Escapezeichen|Entfernt die Einstellung der Escape-Zeichen.|  
|localecho|BACKSPACE aktiviert.|  
|logging|Deaktiviert die Protokollierung.|  
|ntlm|Deaktiviert die NTLM-Authentifizierung.|  
|?|Zeigt die Hilfe für diesen Befehl.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Deaktivieren der Protokollierung.  
```  
u logging  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
