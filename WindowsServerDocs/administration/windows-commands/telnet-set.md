---
title: Telnet-Satz
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e39e2812edc9cd5f169a046def26beebda1d007e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383620"
---
# <a name="telnet-set"></a>Telnet: Set

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt Optionen fest.   
## <a name="syntax"></a>Syntax  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
### <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                                                                                              Beschreibung                                                                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     bsasdel                      |                                                                                                                                 Sendet **Rückraum** als **Lösch**Vorgang.                                                                                                                                  |
|                       CRLF                       |                                                                                                        Sendet CR & LF (0x0D, 0x 0A), wenn die **Eingabe** Taste gedrückt wird. Wird als neuer Zeilen Modus bezeichnet.                                                                                                        |
|                     Delta-                      |                                                                                                                                 Sendet **Delete** als **RÜCKTASTE**.                                                                                                                                  |
|                Escape-<Character>                | Legt das Escapezeichen fest, mit dem die Telnet-Client Eingabeaufforderung eingegeben wird. Das Escapezeichen kann ein einzelnes Zeichen oder eine Kombination aus der **STRG** -Taste und einem Zeichen sein. Halten Sie zum Festlegen einer Tastenkombination die **STRG** -Taste gedrückt, während Sie das Zeichen eingeben, das Sie zuweisen möchten. |
|                    LOCALECHO                     |                                                                                                                                         Schaltet das lokale Echo ein.                                                                                                                                          |
|                Protokolldatei-<FileName>                |                                                                                               Protokolliert die aktuelle Telnet-Sitzung in der lokalen Datei. Die Protokollierung beginnt automatisch, wenn Sie diese Option festlegen.                                                                                               |
|                     logging                      |                                                                                                                  Schaltet die Protokollierung ein. Wenn keine Protokolldatei festgelegt ist, wird eine Fehlermeldung angezeigt.                                                                                                                   |
|           Modus {Konsolen &#124; Bildschirm}           |                                                                                                                                       Legt den Betriebsmodus fest.                                                                                                                                        |
|                       NTLM                       |                                                                                                                                     Schaltet die NTLM-Authentifizierung ein.                                                                                                                                     |
| Begriff {ANSI &#124; VT100 &#124; VT52 &#124; VTNT} |                                                                                                                                        Legt den Terminaltyp fest.                                                                                                                                        |
|                        ?                         |                                                                                                                                    Zeigt die Hilfe für diesen Befehl an.                                                                                                                                    |

## <a name="remarks"></a>Hinweise  
1. Sie können den **Festlegung** -Befehl verwenden, um eine Option zu deaktivieren, die zuvor festgelegt wurde.  
2. In nicht englischsprachigen Versionen von Telnet ist das **Codeset** <option> verfügbar. **Codeset** <option> legt den aktuellen Code fest, der auf eine Option festgelegt ist. dabei kann es sich um einen der folgenden handeln: **Shift JIS**, **Japanese EUC**, **JIS Kanji**, **JIS Kanji (78)** , **Dec Kanji**, **NEC Kanji**. Sie sollten den gleichen Code festlegen, der auf dem Remote Computer festgelegt ist.  
   ## <a name="BKMK_Examples"></a>Beispiele  
   Festlegen der Protokolldatei und Starten der Protokollierung in der lokalen Datei "tnlog. txt"  
   ```  
   set logfile tnlog.txt  
   ```  
   ## <a name="additional-references"></a>Weitere Verweise  
3. [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
