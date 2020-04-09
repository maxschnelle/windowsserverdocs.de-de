---
title: logman delete
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0ab38eab988770de4fbcef8af2c7be6a6137b16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840753"
---
# <a name="logman-delete"></a>logman delete

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löschen eines vorhandenen Daten Sammlers.  

## <a name="syntax"></a>Syntax  
```  
logman delete <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                               Beschreibung                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|   -s <computer name>    |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|     -config <value>     |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|       [-n] <name>       |                                                                   Der Name des Ziel Daten Sammlers.                                                                    |
|          -ETS           |                                              Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                               |
| -[-] u < Benutzer [Kennwort] > | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung angezeigt. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Der folgende Befehl löscht den perf_log des Daten Sammlers.  
```  
logman delete perf_log  
```  
## <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
