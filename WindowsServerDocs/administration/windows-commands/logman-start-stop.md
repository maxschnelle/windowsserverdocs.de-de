---
title: logman Start | anzuhalten
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2bd81a33779aa58e7528d0173a7a4b49489de8f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840623"
---
# <a name="logman-start--stop"></a>logman Start | anzuhalten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Starten Sie einen Datensammler, und legen Sie die Startzeit auf manuell fest, oder beenden Sie einen Datensammler Satz, und legen Sie die Endzeit auf manuell fest.  

## <a name="syntax"></a>Syntax  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|     Parameter      |                                 Beschreibung                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       Zeigt die kontextbezogene Hilfe an.                       |
| -s <computer name> |            Führen Sie den Befehl auf dem angegebenen Remote Computer aus.             |
|  -config <value>   |           Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.            |
|    [-n] <name>     |                          Der Name des Zielobjekts.                          |
|        -ETS        | Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
|        -AS         |               Führt den angeforderten Vorgang asynchron aus.                |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Der folgende Befehl startet den Datensammler perf_log auf dem Remote Computer server_1.  
```  
logman start perf_log -s server_1  
```  
## <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
