---
title: cacls
description: Windows-Befehle Thema für cacls, die freigegebene Zugriffs Steuerungs Listen (DACL) für angegebene Dateien anzeigen oder ändern.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8cc6300563880a587b6544ec8cb61e9010ad6c2c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848243"
---
# <a name="cacls"></a>cacls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden freigegebene Zugriffs Steuerungs Listen (DACL) für angegebene Dateien angezeigt oder geändert.  

## <a name="syntax"></a>Syntax  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
#### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                                            Beschreibung                                                                                             |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      \<filename\>       |                                                                            Erforderlich Zeigt ACLs der angegebenen Dateien an.                                                                             |
|           /t            |                                                          ändert ACLs der angegebenen Dateien im aktuellen Verzeichnis und allen Unterverzeichnissen.                                                          |
|           /m            |                                                                          ändert ACLs von Volumes, die in ein Verzeichnis eingebunden sind.                                                                           |
|           /l            |                                                                        Arbeiten Sie mit dem symbolischen Link selbst im Vergleich zum Ziel.                                                                         |
|         /s: SDDL         |                                       ersetzt die ACLs durch die in der SDDL-Zeichenfolge angegebenen (ungültig durch **/e**, **/g**, **/r**, **/p**oder **/d**).                                        |
|           /e            |                                                                                 Bearbeiten Sie die ACL, anstatt Sie zu ersetzen.                                                                                  |
|           /c            |                                                                                 Fortfahren bei Fehlern beim Zugriff verweigert.                                                                                  |
|    /g User:\<Perm\>     |   Erteilen Sie angegebene Benutzer Zugriffsrechte.<p>Gültige Werte für die Berechtigung:<p>-n-None<br />-r-lesen<br />-w-schreiben<br />-c-ändern (schreiben)<br />-f-Vollzugriff   |
|      /r Benutzer [...]      |                                                                  Widerrufen Sie die Zugriffsrechte des angegebenen Benutzers (nur gültig mit **/e**).                                                                   |
| [/p User:\<Perm\> [...] | ersetzt die Zugriffsrechte für den angegebenen Benutzer.<p>Gültige Werte für die Berechtigung:<p>-n-None<br />-r-lesen<br />-w-schreiben<br />-c-ändern (schreiben)<br />-f-Vollzugriff |
|     [/d User [...]      |                                                                                    Der angegebene Benutzer Zugriff wird verweigert.                                                                                     |
|           /?            |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                |

## <a name="remarks"></a>Hinweise  
- Dieser Befehl ist veraltet. Verwenden Sie stattdessen [icacls](icacls.md) .  
- Verwenden Sie die folgende Tabelle, um die Ergebnisse zu interpretieren:  


  |      Ausgabe       |                Zugriffs Steuerungs Eintrag (ACE) gilt für                |
  |-------------------|---------------------------------------------------------------------|
  |        Zählen         |               Objekt erben. Dieser Ordner und die Dateien.                |
  |        Konfigurationselement         |           Der Container erbt. Dieser Ordner und Unterordner.            |
  |        EA         | Nur erben. Der ACE gilt nicht für die aktuelle Datei bzw. das aktuelle Verzeichnis. |
  | Keine Ausgabe Meldung |                          Nur dieser Ordner.                          |
  |     Zählen RKI      |                 Dieser Ordner, die Unterordner und die Dateien.                 |
  |   Zählen RKI Brasilianer    |                     Nur Unterordner und Dateien.                      |
  |     RKI Brasilianer      |                          Nur Unterordner.                           |
  |     Zählen Brasilianer      |                             Nur Dateien.                             |


- Sie können Platzhalter verwenden ( **?** und **\\\*** ), um mehrere Dateien anzugeben.  
- Sie können mehr als einen Benutzer angeben.  

## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
