---
title: mqbkup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66783e0bbfe5c82971e14fd05e913d485485dc6f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373510"
---
# <a name="mqbkup"></a>mqbkup

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert MSMQ-Nachrichten Dateien und Registrierungs Einstellungen auf einem Speichergerät und stellt zuvor gespeicherte Nachrichten und Einstellungen wieder her.   
Der lokale MSMQ-Dienst wird durch die Sicherung und den Wiederherstellungs Vorgang beendet. Wenn der MSMQ-Dienst zuvor gestartet wurde, versucht das Hilfsprogramm, den MSMQ-Dienst am Ende der Sicherung oder des Wiederherstellungs Vorgangs neu zu starten. Wenn der Dienst vor der Ausführung des Hilfsprogramms bereits beendet wurde, wird nicht versucht, den Dienst neu zu starten.  
Vor der Verwendung des Dienstprogramms MSMQ-Nachrichten Sicherung/Wiederherstellung müssen Sie alle lokalen Anwendungen schließen, die MSMQ verwenden.  
## <a name="syntax"></a>Syntax  
```  
mqbkup {/b | /r} <folder path_to_storage_device>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/b|Gibt den Sicherungs Vorgang an|  
|/r|Gibt Wiederherstellungs Vorgang an|  
|< Ordner path_to_storage @ no__t-0device >|Gibt den Pfad an, in dem die MSMQ-Nachrichten Dateien und Registrierungs Einstellungen gespeichert werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="BKMK_Examples"></a>Beispiele  
So sichern Sie alle MSMQ-Nachrichten Dateien und-Registrierungs Einstellungen und speichern Sie im Ordner " *msmqbkup* " auf Laufwerk "C:".  
```  
mqbkup /b c:\msmqbkup  
```  
Wenn der angegebene Ordner nicht vorhanden ist, wird er von dem Hilfsprogramm automatisch erstellt. Wenn Sie einen vorhandenen Ordner angeben, muss dieser Ordner leer sein. Wenn Sie einen nicht leeren Ordner angeben, löscht das Hilfsprogramm alle darin enthaltenen Dateien und Unterordner. In diesem Fall werden Sie aufgefordert, die Berechtigung zum Löschen vorhandener Dateien und Unterordner anzugeben. Sie können den **/y** -Parameter verwenden, um anzugeben, dass Sie im Voraus den Löschvorgang für alle vorhandenen Dateien und Unterordner im angegebenen Ordner zustimmen.  
So löschen Sie alle Dateien und Unterordner im Ordner " *oldbkup* " auf dem Laufwerk "C:" und speichern MSMQ-Nachrichten Dateien und Registrierungs Einstellungen in diesem Ordner.  
```  
mqbkup /b /y c:\oldbkup  
```  
So stellen Sie MSMQ-Nachrichten und Registrierungs Einstellungen wieder her:  
```  
mqbkup /r c:\msmqbkup  
```  
Die Speicherorte von Ordnern, die zum Speichern von MSMQ-Nachrichten Dateien verwendet werden, werden in der Registrierung gespeichert. Folglich stellt das Hilfsprogramm MSMQ-Nachrichten Dateien in den Ordnern wieder her, die in der Registrierung angegeben sind, und nicht für die Speicherordner, die vor dem Wiederherstellungs Vorgang verwendet werden. Wenn die in der Registrierung angegebenen Ordner nicht vorhanden sind, werden Sie durch den Wiederherstellungs Vorgang automatisch erstellt. Wenn Ordner Verzeichnisse vorhanden sind und nicht leer sind, werden Sie vom Hilfsprogramm aufgefordert, die Berechtigung zum Löschen des aktuellen Inhalts dieser Ordner zu löschen.  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
