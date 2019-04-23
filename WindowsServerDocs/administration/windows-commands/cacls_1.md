---
title: cacls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 289015ff580d7e2fba5ff911878028f5302cab8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838081"
---
# <a name="cacls"></a>cacls

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, oder ändert Zugriffssteuerungslisten (DACL) für bestimmte Dateien.  
## <a name="syntax"></a>Syntax  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|\<filename\>|Erforderlich. Zeigt die Acls der angegebenen Dateien.|  
|/t|Ändert die Acls der angegebenen Dateien in das aktuelle Verzeichnis und alle Unterverzeichnisse.|  
|/m|Änderungen werden Acls der Volumes in ein Verzeichnis eingebunden.|  
|/l|Die symbolische Verknüpfung selbst im Vergleich zu dem Ziel arbeiten.|  
|/s:sddl|ersetzt die Acls, mit denen in der SDDL-Zeichenfolge angegebene (ungültig mit **/e**, **/g**, **/r**, **/p**, oder   **/d**).|  
|/ e|Bearbeiten Sie ACL, anstatt ihn zu ersetzen.|  
|/c|Bei Zugriffsverweigerungsfehler fortsetzen.|  
|/ g-Benutzer:\<permanent festlegen\>|Die angegebenen Benutzerzugriffsrechte auf.<br /><br />Gültige Werte für die Berechtigung:<br /><br />-n - keine<br />-R - lesen<br />-w - Schreibvorgänge<br />-C - Änderung (Schreiben)<br />-f - Vollzugriff|  
|/ r-Benutzer [...]|Widerrufen des angegebenen Benutzers (nur gültig mit **/e**).|  
|[/ p-Benutzer:\<Perm\> [...]|Ersetzen Sie die Zugriffsrechte des angegebenen Benutzers.<br /><br />Gültige Werte für die Berechtigung:<br /><br />-n - keine<br />-R - lesen<br />-w - Schreibvorgänge<br />-C - Änderung (Schreiben)<br />-f - Vollzugriff|  
|[/ d-Benutzer [...]|Angegebene Benutzer der Zugriff verweigert.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="remarks"></a>Hinweise  
-   Mit diesem Befehl ist veraltet. Verwenden Sie [Icacls](icacls.md) stattdessen.  
-   Verwenden Sie in der folgende Tabelle, zum Interpretieren der Ergebnisse:  

    |Ausgabe|Der Zugriffssteuerungseintrag (ACE) gilt für|  
    |-----|----------------------|  
    |OI|Erbt. Dieser Ordner und Dateien.|  
    |CI|Container erben. Dieser Ordner und Unterordner.|  
    |IO|Nur erben. Der ACE gilt nicht für die aktuelle Datei/Verzeichnis.|  
    |Keine Ausgabenachricht|Nur für diesen Ordner.|  
    |(OI) (CI)|Dieser Ordner, Unterordner und Dateien.|  
    |(OI) (CI) (E/A)|Nur Unterordner und Dateien.|  
    |(CI)(IO)|Nur Unterordner.|  
    |(OI)(IO)|Nur Dateien.|  

-   Sie können Platzhalter verwenden (**?** und **\***) auf mehrere Dateien anzugeben.  
-   Sie können mehr als einen Benutzer angeben.  

#### <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
