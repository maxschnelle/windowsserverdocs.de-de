---
title: Logman Import | Exportieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 67621b109c379cc2758b4036460b6bb82df3e3d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848301"
---
# <a name="logman-import--export"></a>Logman Import | Exportieren

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Importieren Sie einer Datensammlergruppe aus einer XML-Datei oder in eine XML-Datei exportieren Sie Data Collector Set.  
  
## <a name="syntax"></a>Syntax  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|-?|Zeigt, die kontextbezogene Hilfe an.|  
|-s <computer name>|Führen Sie den Befehl auf dem angegebenen Remotecomputer.|  
|-config <value>|Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.|  
|[-n] <name>|Der Name des Zielobjekts.|  
|-xml <name>|Der Name der XML-Datei zum Importieren oder exportieren.|  
|-ets|Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen.|  
|-[-] u < Benutzer [Kennwort] >|Benutzer, der als ausführen. Eingeben einer * für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben.|  
|-y|Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.|  
## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl importiert die XML-Datei c:\windows\perf_log.xml aus der Computer server_1, wie ein Datensammler aufgerufene Perf_log festgelegt.  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
