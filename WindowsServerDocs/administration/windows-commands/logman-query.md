---
title: logman query
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6e00e1ca7e6e090fd618af5b0ca2307bb573ab8c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437720"
---
# <a name="logman-query"></a>logman query

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Abfrage-Datensammler oder Datensammler legen Eigenschaften fest.  

## <a name="syntax"></a>Syntax  
```  
logman query [providers|"Data Collector Set name"] [options]  
```  
## <a name="parameters"></a>Parameter  

|     Parameter      |                                 Beschreibung                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       Zeigt, die kontextbezogene Hilfe an.                       |
| -s <computer name> |            Führen Sie den Befehl auf dem angegebenen Remotecomputer.             |
|  -config <value>   |           Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.            |
|    [-n] <name>     |                          Der Name des Zielobjekts.                          |
|        -ets        | Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen. |

## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl listet alle Data Collector Sets, die auf dem Zielsystem konfiguriert.  
```  
logman query  
```  
Der folgende Befehl listet die Datensammler in den Datensammlersatz mit dem Namen Perf_log enthalten sind.  
```  
logman query "perf_log"  
```  
Der folgende Befehl listet alle verfügbaren Anbieter der Datensammler auf dem Zielsystem.  
```  
logman query providers  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
