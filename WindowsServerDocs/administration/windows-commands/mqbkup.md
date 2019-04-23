---
title: mqbkup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a809bfc788ba25afab280e80e5c6f0dc9c70dc86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842901"
---
# <a name="mqbkup"></a>mqbkup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sichert Dateien der MSMQ-Nachricht und der Registrierung Einstellungen an ein Speichergerät und stellt zuvor gespeicherte Nachrichten und die Einstellungen wieder her.   
Sowohl die Sicherung und der Restore-Vorgang werden die lokalen MSMQ-Dienst beendet. Wenn der MSMQ-Dienst vorab gestartet wurde, versucht das Hilfsprogramm am Ende der Sicherung oder Wiederherstellung den MSMQ-Dienst neu starten. Wenn der Dienst bereits vor dem Ausführen des Dienstprogramms beendet wurde, ist nicht zum Neustart des Diensts versucht.  
Bevor Sie mit dem Hilfsprogramm für die MSMQ-Nachricht sichern/wiederherstellen müssen Sie alle lokale Anwendungen schließen, die Verwendung von MSMQ.  
## <a name="syntax"></a>Syntax  
```  
mqbkup {/b | /r} <folder path_to_storage_device>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/b|Gibt an, Sicherungsvorgang|  
|/r|Gibt die Restore-Vorgang an|  
|< Ordner Path_to_storage\_Gerät >|Gibt den Pfad, in denen der MSMQ-Nachricht-Dateien und registrierungseinstellungen gespeichert sind|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Zum Sichern, alle MSMQ-Nachricht-Dateien und registrierungseinstellungen, und speichern sie in der *Msmqbkup* Ordner auf dem Laufwerk "c:".  
```  
mqbkup /b c:\msmqbkup  
```  
Wenn der angegebene Ordner nicht vorhanden ist, wird das Hilfsprogramm automatisch eine erstellt. Wenn Sie einen vorhandenen Ordner angeben möchten, muss dieser Ordner leer sein. Wenn Sie einen nicht leerer Ordner angeben, werden das Hilfsprogramm alle Dateien und die darin enthaltenen Unterordner gelöscht. In diesem Fall werden Sie aufgefordert, die die Berechtigung zum Löschen von vorhandenen Dateien und Unterordner erteilen. Sie können die **/y** Parameter, um anzugeben, dass Sie vorab das Löschen aller vorhandenen Dateien und Unterverzeichnisse im angegebenen Ordner zustimmen.  
So löschen Sie alle Dateien und Unterordner in der *Oldbkup* Ordner auf Ihrem Laufwerk "c:" und Store MSMQ-Nachricht-Dateien und registrierungseinstellungen für das in diesem Ordner.  
```  
mqbkup /b /y c:\oldbkup  
```  
Um MSMQ-Nachrichten und registrierungseinstellungen wiederherzustellen:  
```  
mqbkup /r c:\msmqbkup  
```  
Die Speicherorte von Ordnern zum Speichern von Dateien für MSMQ-Nachricht werden in der Registrierung gespeichert. Daher wird das Dienstprogramm MSMQ-Nachricht-Dateien für die Ordner, in der Registrierung angegeben und nicht für die vor dem Wiederherstellungsvorgang verwendeten Speicherordner wiederhergestellt. Wenn die in der Registrierung angegebene Ordner nicht vorhanden sind, wird Sie von der Restore-Vorgang automatisch erstellt. Wenn Ordner Verzeichnisse vorhanden sind und nicht leer sind, fordert das Hilfsprogramm Sie für die Berechtigung, die den aktuellen Inhalt dieser Ordner löschen.  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
