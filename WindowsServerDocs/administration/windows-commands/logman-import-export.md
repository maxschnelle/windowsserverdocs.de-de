---
title: logman importieren | Exports
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81147f9e2e2da69c8e59969f3c176264a7fa353a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840673"
---
# <a name="logman-import--export"></a>logman importieren | Exports

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importieren Sie einen Datensammler Satz aus einer XML-Datei, oder exportieren Sie einen Datensammler Satz in eine XML-Datei.  

## <a name="syntax"></a>Syntax  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|        Parameter        |                                                                        Beschreibung                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             Zeigt die kontextbezogene Hilfe an.                                                              |
|   -s <computer name>    |                                                   Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                   |
|     -config <value>     |                                                  Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                  |
|       [-n] <name>       |                                                                Der Name des Zielobjekts.                                                                 |
|       -XML-<name>       |                                                         Der Name der XML-Datei, die importiert oder exportiert werden soll.                                                         |
|          -ETS           |                                       Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                        |
| -[-] u < Benutzer [Kennwort] > | Benutzer, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung angezeigt. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|           -y            |                                                      Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                       |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Der folgende Befehl importiert die XML-Datei "c:\windows\ perf_log. xml" aus dem Computer server_1 als Datensammler Satz mit dem Namen perf_log.  
```  
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml  
```  
## <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
