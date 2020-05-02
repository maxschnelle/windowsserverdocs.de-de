---
title: logman Start | anzuhalten
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68f570d99d4b3eaa818c9fbdcce76c42d1cb12d4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724345"
---
# <a name="logman-start--stop"></a>logman Start | anzuhalten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Starten Sie einen Datensammler, und legen Sie die Startzeit auf manuell fest, oder beenden Sie einen Datensammler Satz, und legen Sie die Endzeit auf manuell fest.  

## <a name="syntax"></a>Syntax  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|     Parameter      |                                 BESCHREIBUNG                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       Zeigt die kontextbezogene Hilfe an.                       |
| -s<computer name> |            Führen Sie den Befehl auf dem angegebenen Remote Computer aus.             |
|  -config <value>   |           Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.            |
|    [-n]<name>     |                          Name des Zielobjekts                          |
|        -ETS        | Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
|        -AS         |               Führt den angeforderten Vorgang asynchron aus.                |

## <a name="examples"></a>Beispiele  
Der folgende Befehl startet den Datensammler perf_log auf dem Remote Computer server_1.  
```  
logman start perf_log -s server_1  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
