---
title: logman importieren | Exports
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffc2e42f353352f69cf61dfb1f108a7d53cb7c4b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724361"
---
# <a name="logman-import--export"></a>logman importieren | Exports

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importieren Sie einen Datensammler Satz aus einer XML-Datei, oder exportieren Sie einen Datensammler Satz in eine XML-Datei.  

## <a name="syntax"></a>Syntax  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                        BESCHREIBUNG                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             Zeigt die kontextbezogene Hilfe an.                                                              |
|   -s<computer name>    |                                                   Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                   |
|     -config <value>     |                                                  Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                  |
|       [-n]<name>       |                                                                Name des Zielobjekts                                                                 |
|       -XML<name>       |                                                         Der Name der XML-Datei, die importiert oder exportiert werden soll.                                                         |
|          -ETS           |                                       Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                        |
| -[-] u <Benutzer [Kennwort] > | Benutzer, der als ausgeführt werden soll. Wenn Sie \* einen als Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|           -y            |                                                      Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                       |

## <a name="examples"></a>Beispiele  
Der folgende Befehl importiert die XML-Datei "c:\windows\ perf_log. xml" aus dem Computer server_1 als Datensammler Satz mit dem Namen perf_log.  
```  
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
