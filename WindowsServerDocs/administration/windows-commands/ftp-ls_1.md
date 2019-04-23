---
title: ftp ls_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c45e26f6578510837f190ae20e3140e619dc59cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841761"
---
# <a name="ftp-ls1"></a>ftp: ls_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012


>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine verkürzte Liste der Dateien und Unterverzeichnisse des Remotecomputers an.   
## <a name="syntax"></a>Syntax  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<remotedirectory>]|Gibt das Verzeichnis für das eine Liste angezeigt werden sollen. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remotecomputer verwendet.|  
|[<LocalFile>]|Gibt eine lokale Datei in dem die Auflistung gespeichert. Wenn eine lokale Datei nicht angegeben ist, werden die Ergebnisse auf dem Bildschirm angezeigt.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Anzeigen einer verkürzten Liste der Dateien und Unterverzeichnisse des Remotecomputers an.  
```  
ls  
```  
Erhalten Sie eine abgekürzte Verzeichnisliste mit **dir1** wird aufgerufen, auf dem Remotecomputer, und speichern Sie sie in einer lokalen Datei **Verliste.txt**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
