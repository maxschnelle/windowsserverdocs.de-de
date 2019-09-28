---
title: logman delete
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8360a4955a5ebed3eb25fda77acf587c56fbf5d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374428"
---
# <a name="logman-delete"></a>logman delete

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löschen eines vorhandenen Daten Sammlers.  

## <a name="syntax"></a>Syntax  
```  
logman delete <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|        Parameter        |                                                                               Beschreibung                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|   -s <computer name>    |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|     -config <value>     |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|       [-n] <name>       |                                                                   Der Name des Ziel Daten Sammlers.                                                                    |
|          -ETS           |                                              Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                               |
| -[-] u < Benutzer [Kennwort] > | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |

## <a name="BKMK_examples"></a>Beispiele  
Der folgende Befehl löscht den perf_log des Daten Sammlers.  
```  
logman delete perf_log  
```  
#### <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
