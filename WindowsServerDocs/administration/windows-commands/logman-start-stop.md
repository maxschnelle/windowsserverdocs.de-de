---
title: Logman Start | Beenden
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c6027c4c9a99e45bb1c2e95cdfd4a7687a5c43b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437678"
---
# <a name="logman-start--stop"></a>Logman Start | Beenden

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Starten Sie einen Datensammler und die Startzeit auf manuell festgelegt, oder beenden Sie einen Datensammler festgelegt und die Endzeit auf manuell festgelegt.  

## <a name="syntax"></a>Syntax  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|     Parameter      |                                 Beschreibung                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       Zeigt, die kontextbezogene Hilfe an.                       |
| -s <computer name> |            Führen Sie den Befehl auf dem angegebenen Remotecomputer.             |
|  -config <value>   |           Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.            |
|    [-n] <name>     |                          Der Name des Zielobjekts.                          |
|        -ets        | Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen. |
|        -as         |               Den angeforderten Vorgang asynchron ausführen.                |

## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl startet den Data Collector Perf_log auf dem Remotecomputer server_1.  
```  
logman start perf_log -s server_1  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
