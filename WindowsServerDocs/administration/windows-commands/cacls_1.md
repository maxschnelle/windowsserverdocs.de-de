---
title: cacls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04b60bd852abdb55059efb96aec4c290361d6a74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379953"
---
# <a name="cacls"></a>cacls

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden freigegebene Zugriffs Steuerungs Listen (DACL) für angegebene Dateien angezeigt oder geändert.  
## <a name="syntax"></a>Syntax  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                                            Beschreibung                                                                                             |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      \<filename\>       |                                                                            Erforderlich. Zeigt ACLs der angegebenen Dateien an.                                                                             |
|           /t            |                                                          ändert ACLs der angegebenen Dateien im aktuellen Verzeichnis und allen Unterverzeichnissen.                                                          |
|           /m            |                                                                          ändert ACLs von Volumes, die in ein Verzeichnis eingebunden sind.                                                                           |
|           /l            |                                                                        Arbeiten Sie mit dem symbolischen Link selbst im Vergleich zum Ziel.                                                                         |
|         /s: SDDL         |                                       ersetzt die ACLs durch die in der SDDL-Zeichenfolge angegebenen (ungültig durch **/e**, **/g**, **/r**, **/p**oder **/d**).                                        |
|           /e            |                                                                                 Bearbeiten Sie die ACL, anstatt Sie zu ersetzen.                                                                                  |
|           /c            |                                                                                 Fortfahren bei Fehlern beim Zugriff verweigert.                                                                                  |
|    /g Benutzer: \<perm @ no__t-1     |   Erteilen Sie angegebene Benutzer Zugriffsrechte.<br /><br />Gültige Werte für die Berechtigung:<br /><br />-n-None<br />-r-lesen<br />-w-schreiben<br />-c-ändern (schreiben)<br />-f-Vollzugriff   |
|      /r Benutzer [...]      |                                                                  Widerrufen Sie die Zugriffsrechte des angegebenen Benutzers (nur gültig mit **/e**).                                                                   |
| [/p User: \<perm @ no__t-1 [...] | ersetzt die Zugriffsrechte für den angegebenen Benutzer.<br /><br />Gültige Werte für die Berechtigung:<br /><br />-n-None<br />-r-lesen<br />-w-schreiben<br />-c-ändern (schreiben)<br />-f-Vollzugriff |
|     [/d User [...]      |                                                                                    Der angegebene Benutzer Zugriff wird verweigert.                                                                                     |
|           /?            |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                |

## <a name="remarks"></a>Hinweise  
- Dieser Befehl ist veraltet. Verwenden Sie stattdessen [icacls](icacls.md) .  
- Verwenden Sie die folgende Tabelle, um die Ergebnisse zu interpretieren:  


  |      Ausgabe       |                Zugriffs Steuerungs Eintrag (ACE) gilt für                |
  |-------------------|---------------------------------------------------------------------|
  |        ZÄHLEN         |               Objekt erben. Dieser Ordner und die Dateien.                |
  |        CI         |           Der Container erbt. Dieser Ordner und Unterordner.            |
  |        IO         | Nur erben. Der ACE gilt nicht für die aktuelle Datei bzw. das aktuelle Verzeichnis. |
  | Keine Ausgabe Meldung |                          Nur dieser Ordner.                          |
  |     ZÄHLEN RKI      |                 Dieser Ordner, die Unterordner und die Dateien.                 |
  |   ZÄHLEN RKI BRASILIANER    |                     Nur Unterordner und Dateien.                      |
  |     RKI BRASILIANER      |                          Nur Unterordner.                           |
  |     ZÄHLEN BRASILIANER      |                             Nur Dateien.                             |


- Sie können Platzhalter verwenden ( **?** und **\\ @ no__t-2**), um mehrere Dateien anzugeben.  
- Sie können mehr als einen Benutzer angeben.  

#### <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
