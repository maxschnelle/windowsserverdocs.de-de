---
title: logman delete
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b30fd6eb7915d3d0296988a98968dcde58bdbc2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724375"
---
# <a name="logman-delete"></a>logman delete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löschen eines vorhandenen Daten Sammlers.  

## <a name="syntax"></a>Syntax  
```  
logman delete <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                               BESCHREIBUNG                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|   -s<computer name>    |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|     -config <value>     |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|       [-n]<name>       |                                                                   Der Name des Ziel Daten Sammlers.                                                                    |
|          -ETS           |                                              Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                               |
| -[-] u <Benutzer [Kennwort] > | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie \* einen als Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |

## <a name="examples"></a>Beispiele  
Der folgende Befehl löscht den perf_log des Daten Sammlers.  
```  
logman delete perf_log  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
