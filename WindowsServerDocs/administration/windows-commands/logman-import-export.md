---
title: logman importieren | Exports
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 309274b5288bd1c17259e01cf563ae8685a2094e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374461"
---
# <a name="logman-import--export"></a>logman importieren | Exports

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importieren Sie einen Datensammler Satz aus einer XML-Datei, oder exportieren Sie einen Datensammler Satz in eine XML-Datei.  

## <a name="syntax"></a>Syntax  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|        Parameter        |                                                                        Beschreibung                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             Zeigt die kontextbezogene Hilfe an.                                                              |
|   -s <computer name>    |                                                   Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                   |
|     -config <value>     |                                                  Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                  |
|       [-n] <name>       |                                                                Der Name des Zielobjekts.                                                                 |
|       -XML-<name>       |                                                         Der Name der XML-Datei, die importiert oder exportiert werden soll.                                                         |
|          -ETS           |                                       Direktes Senden von Befehlen an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen.                                        |
| -[-] u < Benutzer [Kennwort] > | Benutzer, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|           -y            |                                                      Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                       |

## <a name="BKMK_examples"></a>Beispiele  
Der folgende Befehl importiert die XML-Datei c:\windows\perf_log.XML aus dem Computer server_1 als Datensammler Satz mit dem Namen perf_log.  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
