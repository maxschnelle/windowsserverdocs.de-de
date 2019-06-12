---
title: Telnet-Satz
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b68ce0ee87d80b25cf13db5bebc6c407a9fe091f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441019"
---
# <a name="telnet-set"></a>Telnet: festgelegt

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Legt Optionen fest.   
## <a name="syntax"></a>Syntax  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
### <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                                                                                              Beschreibung                                                                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     bsasdel                      |                                                                                                                                 Sendet **RÜCKTASTE** als eine **löschen**.                                                                                                                                  |
|                       crlf                       |                                                                                                        Sendet CR & LF (0x0D, 0 x 0A) Wenn die **EINGABETASTE** gedrückt wird. Als neue Zeilenmodus bezeichnet.                                                                                                        |
|                     delasbs                      |                                                                                                                                 Sendet **löschen** als eine **RÜCKTASTE**.                                                                                                                                  |
|                Escapezeichen <Character>                | Legt fest, das Escapezeichen verwendet, um die Telnet-Client-Eingabeaufforderung einzugeben. Das Escape-Zeichen kann ein einzelnes Zeichen, oder es kann sein, eine Kombination aus den **STRG** Schlüssel sowie ein Zeichen. Um eine Kombination von Steuerelement-Schlüssel festzulegen, halten Sie die **STRG** gedrückt, während Sie das Zeichen eingeben, die Sie zuweisen möchten. |
|                    localecho                     |                                                                                                                                         Aktiviert die lokale Echo.                                                                                                                                          |
|                Protokolldatei <FileName>                |                                                                                               Die Telnet-Sitzung in der lokalen Datei protokolliert. Protokollierung wird automatisch gestartet, wenn Sie diese Option festgelegt.                                                                                               |
|                     logging                      |                                                                                                                  Aktiviert die Protokollierung. Wenn keine Protokolldatei festgelegt ist, wird eine Fehlermeldung angezeigt.                                                                                                                   |
|           Modus {Konsole &#124; Bildschirm}           |                                                                                                                                       Legt den Betriebsmodus fest.                                                                                                                                        |
|                       ntlm                       |                                                                                                                                     Aktiviert die NTLM-Authentifizierung.                                                                                                                                     |
| term {ansi &#124; vt100 &#124; vt52 &#124; vtnt} |                                                                                                                                        Legt den Terminalserver fest.                                                                                                                                        |
|                        ?                         |                                                                                                                                    Zeigt die Hilfe für diesen Befehl.                                                                                                                                    |

## <a name="remarks"></a>Hinweise  
1. Können Sie die **Festlegung** Befehl aus, um eine Option zu deaktivieren, die zuvor festgelegt wurde.  
2. In nicht englischsprachigen Versionen von Telnet die **Codesatz** <option> verfügbar ist. **Codesatz** <option> legt den aktuellen Code eine Option, die möglicherweise eine der folgenden festgelegt: **shift-JIS**, **japanische EUC**, **JIS Kanji**, **JIS Kanji (78)** , **DEC Kanji**, **NEC Kanji**. Sie sollten den gleichen Code, der festgelegt wird, auf dem Remotecomputer festlegen.  
   ## <a name="BKMK_Examples"></a>Beispiele für  
   Legen Sie die Protokolldatei, und beginnen Sie die Protokollierung in der lokalen Datei tnlog.txt  
   ```  
   set logfile tnlog.txt  
   ```  
   ## <a name="additional-references"></a>Zusätzliche Referenzen  
3. [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
