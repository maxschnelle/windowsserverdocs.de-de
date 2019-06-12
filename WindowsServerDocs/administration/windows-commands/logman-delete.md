---
title: logman delete
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e396d79dc936f56a69fac9469c020348640f1094
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437780"
---
# <a name="logman-delete"></a>logman delete

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löschen Sie die vorhandenen Sammlungen.  

## <a name="syntax"></a>Syntax  
```  
logman delete <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|        Parameter        |                                                                               Beschreibung                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    Zeigt, die kontextbezogene Hilfe an.                                                                     |
|   -s <computer name>    |                                                          Führen Sie den Befehl auf dem angegebenen Remotecomputer.                                                          |
|     -config <value>     |                                                         Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.                                                         |
|       [-n] <name>       |                                                                   Der Name des Datensammlers Ziel.                                                                    |
|          -ets           |                                              Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen.                                               |
| -[-] u < Benutzer [Kennwort] > | Gibt die Ausführung als Benutzer an. Eingeben einer \* für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben. |

## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl löscht die Data Collector Perf_log.  
```  
logman delete perf_log  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
