---
title: logman query
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05448a4f129a59145813dd0da7199d4adf845c5c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724353"
---
# <a name="logman-query"></a>logman query

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eigenschaften des Daten Sammlers oder des Datensammler Satzes Abfragen.  

## <a name="syntax"></a>Syntax  
```  
logman query [providers|Data Collector Set name] [options]  
```  
### <a name="parameters"></a>Parameter  

|     Parameter      |                                 BESCHREIBUNG                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       Zeigt die kontextbezogene Hilfe an.                       |
| -s<computer name> |            Führen Sie den Befehl auf dem angegebenen Remote Computer aus.             |
|  -config <value>   |           Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.            |
|    [-n]<name>     |                          Name des Zielobjekts                          |
|        -ETS        | Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |

## <a name="examples"></a>Beispiele  
Der folgende Befehl listet alle Datensammler Sätze auf, die auf dem Zielsystem konfiguriert sind.  
```  
logman query  
```  
Mit dem folgenden Befehl werden die Datensammler aufgelistet, die im Datensammler Satz mit dem Namen perf_log enthalten sind.  
```  
logman query perf_log  
```  
Der folgende Befehl listet alle verfügbaren Anbieter von Datensammlern auf dem Zielsystem auf.  
```  
logman query providers  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
