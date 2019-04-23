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
ms.openlocfilehash: 00473b5178eca93e9644888fbaa4c4c96c0dd683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842061"
---
# <a name="logman-delete"></a>logman delete

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löschen Sie die vorhandenen Sammlungen.  
  
## <a name="syntax"></a>Syntax  
```  
logman delete <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/?|Zeigt, die kontextbezogene Hilfe an.|  
|-s <computer name>|Führen Sie den Befehl auf dem angegebenen Remotecomputer.|  
|-config <value>|Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.|  
|[-n] <name>|Der Name des Datensammlers Ziel.|  
|-ets|Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen.|  
|-[-] u < Benutzer [Kennwort] >|Gibt die Ausführung als Benutzer an. Eingeben einer * für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben.|  
## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl löscht die Data Collector Perf_log.  
```  
logman delete perf_log  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
