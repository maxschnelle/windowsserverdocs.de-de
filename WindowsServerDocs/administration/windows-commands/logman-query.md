---
title: logman query
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6acf6cf5240dd59357f4c788577190699a354744
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374417"
---
# <a name="logman-query"></a>logman query

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eigenschaften des Daten Sammlers oder des Datensammler Satzes Abfragen.  

## <a name="syntax"></a>Syntax  
```  
logman query [providers|"Data Collector Set name"] [options]  
```  
## <a name="parameters"></a>Parameter  

|     Parameter      |                                 Beschreibung                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       Zeigt die kontextbezogene Hilfe an.                       |
| -s <computer name> |            Führen Sie den Befehl auf dem angegebenen Remote Computer aus.             |
|  -config <value>   |           Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.            |
|    [-n] <name>     |                          Der Name des Zielobjekts.                          |
|        -ETS        | Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |

## <a name="BKMK_examples"></a>Beispiele  
Der folgende Befehl listet alle Datensammler Sätze auf, die auf dem Zielsystem konfiguriert sind.  
```  
logman query  
```  
Mit dem folgenden Befehl werden die Datensammler aufgelistet, die im Datensammler Satz mit dem Namen perf_log enthalten sind.  
```  
logman query "perf_log"  
```  
Der folgende Befehl listet alle verfügbaren Anbieter von Datensammlern auf dem Zielsystem auf.  
```  
logman query providers  
```  
#### <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
