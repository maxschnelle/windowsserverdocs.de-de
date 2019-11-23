---
title: evntcmd
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1aabb74-76e7-4304-95a6-50ad87e92fd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4496df6df1a40b383505627d58389c098493f59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377436"
---
# <a name="evntcmd"></a>evntcmd

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert die Übersetzung von Ereignissen in Traps, Trap Ziele oder beides basierend auf Informationen in einer Konfigurationsdatei.   
## <a name="syntax"></a>Syntax  
```  
evntcmd [/s <computerName>] [/v <verbosityLevel>] [/n] <FileName>  
```  
### <a name="parameters"></a>Parameter  

|      Parameter      |                                                                                                                                                            Beschreibung                                                                                                                                                             |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /s <computerName>  |                                                         Gibt anhand des Namens den Computer an, auf dem Sie die Übersetzung von Ereignissen in Traps, Trap Ziele oder beides konfigurieren möchten. Wenn Sie keinen Computer angeben, erfolgt die Konfiguration auf dem lokalen Computer.                                                          |
| /v <verbosityLevel> | Gibt an, welche Arten von Statusmeldungen als Traps angezeigt werden und welche Trap Ziele konfiguriert werden. Dieser Parameter muss eine ganze Zahl zwischen 0 und 10 sein. Wenn Sie 10 angeben, werden alle Arten von Meldungen angezeigt, einschließlich der Ablauf Verfolgung von Nachrichten und Warnungen darüber, ob die Trap-Konfiguration erfolgreich war. Wenn Sie 0 angeben, werden keine Meldungen angezeigt. |
|         /n          |                                                                                                           Gibt an, dass der SNMP-Dienst nicht neu gestartet werden soll, wenn dieser Computer Trap-Konfigurationsänderungen empfängt.                                                                                                            |
|     <FileName>      |                                                                                     Gibt nach Name die Konfigurationsdatei an, die Informationen über die Übersetzung von Ereignissen in Traps und Trap Ziele enthält, die Sie konfigurieren möchten.                                                                                     |
|         /?          |                                                                                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                |

## <a name="remarks"></a>Hinweise  
- Wenn Sie Traps, aber keine Trap Ziele konfigurieren möchten, können Sie eine gültige Konfigurationsdatei erstellen, indem Sie das-Ereignis verwenden, um den Konvertierer zu verwenden, der ein grafisches Hilfsprogramm ist. Wenn Sie den SNMP-Dienst installiert haben, können Sie das Ereignis starten, um den Konvertierer abzufangen, indem Sie an einer Eingabeaufforderung **evntwin** eingeben. Nachdem Sie die gewünschten Traps definiert haben, klicken Sie auf exportieren, um eine Datei zu erstellen, die für die Verwendung mit **evntcmd**geeignet ist. Sie können das Ereignis verwenden, um den Konvertierer zu verwenden, um problemlos eine Konfigurationsdatei zu erstellen, und dann die Konfigurationsdatei mit **evntcmd** an der Eingabeaufforderung verwenden, um auf mehreren Computern schnell Traps zu konfigurieren.  
- Die Syntax für die Konfiguration eines Trap lautet wie folgt:  
  #pragma<em><EventLogFile> <EventSource> <EventID> [<Count> [<Period>]] **Hinzufügen**</em>  
  -   Der Text **#pragma** muss am Anfang jedes Eintrags in der Datei angezeigt werden.  
  -   Der Parameter **Add** gibt an, dass Sie der Trap-Konfiguration ein Ereignis hinzufügen möchten.  
  -   Die Parameter " *EventLogFile*", " *eventSource*" und " *EventID* " sind erforderlich. Der *EventLogFile* -Parameter gibt die Datei an, in der das Ereignis aufgezeichnet wird. Der *eventSource* -Parameter gibt die Anwendung an, die das Ereignis generiert. Der *EventID-* Parameter gibt die eindeutige Zahl an, durch die die einzelnen Ereignisse identifiziert werden. Um herauszufinden, welche Werte bestimmten Ereignissen entsprechen, starten Sie das Ereignis, um den Konvertierer zu starten, indem Sie an einer Eingabeaufforderung **evntwin** eingeben. Klicken Sie auf **Benutzer**definiert und dann auf **Bearbeiten**. Durchsuchen Sie unter **Ereignis Quellen**die Ordner, bis Sie das Ereignis finden, das Sie konfigurieren möchten, klicken Sie auf das Ereignis, und klicken Sie dann auf **Hinzufügen**. Informationen zur Ereignis Quelle, der Ereignisprotokoll Datei und der Ereignis-ID werden unter **Quell-, Protokoll**-bzw. **Trap spezifische ID**angezeigt.  
  -   Der *count* -Parameter ist optional und gibt an, wie oft das Ereignis auftreten muss, bevor eine Trap-Nachricht gesendet wird. Wenn Sie den *count* -Parameter nicht verwenden, wird die Trap-Nachricht gesendet, nachdem das Ereignis einmal auftritt.  
  -   Der *Period* -Parameter ist optional, erfordert jedoch die Verwendung des *count* -Parameters. Der *Period* -Parameter gibt eine Zeitspanne (in Sekunden) an, während der das Ereignis mit dem count-Parameter angegeben werden muss, bevor eine Trap-Nachricht gesendet wird. Wenn Sie den *Period* -Parameter nicht verwenden, wird eine Trap-Nachricht gesendet, nachdem das Ereignis so oft wie angegeben mit dem *count* -Parameter auftritt, unabhängig davon, wie viel Zeit zwischen den vorkommen abläuft.  
- Die Syntax zum Entfernen eines Trap lautet wie folgt:  
  **#pragma löschen**<em><EventLogFile> <EventSource> <EventID></em>  
  -   Der Text **#pragma** muss am Anfang jedes Eintrags in der Datei angezeigt werden.  
  -   Der Parameter *Delete* gibt an, dass Sie ein Ereignis zur Trap-Konfiguration entfernen möchten.  
  -   Die Parameter " *EventLogFile*", " *eventSource*" und " *EventID* " sind erforderlich. Der Parameter *EventLogFile* gibt das Protokoll an, in dem das Ereignis aufgezeichnet wird. Der *eventSource* -Parameter gibt die Anwendung an, die das Ereignis generiert. Der *EventID-* Parameter gibt die eindeutige Zahl an, durch die die einzelnen Ereignisse identifiziert werden.  
- Die Syntax zum Konfigurieren eines Trap-Ziels lautet wie folgt:  
  **#pragma add_TRAP_DEST**<em><CommunityName> <HostID></em>  
  -   Der Text **#pragma** muss am Anfang jedes Eintrags in der Datei angezeigt werden.  
  -   Der Parameter **add_TRAP_DEST** gibt an, dass Trap-Nachrichten an einen angegebenen Host innerhalb einer Community gesendet werden sollen.  
  -   Der *Communityname* -Parameter gibt die Community, in der Trap-Nachrichten gesendet werden, anhand des Namens an.  
  -   Der *-Parameter Hostid* gibt den Host, an den Trap-Nachrichten gesendet werden sollen, anhand des Namens oder der IP-Adresse an.  
- Die Syntax zum Entfernen eines Trap-Ziels lautet wie folgt:  
  **#pragma delete_TRAP_DEST**<em><CommunityName> <HostID></em>  
  - Der Text **#pragma** muss am Anfang jedes Eintrags in der Datei angezeigt werden.  
  - Der-Parameter *delete_TRAP_DEST* gibt an, dass Trap-Nachrichten nicht an einen angegebenen Host innerhalb einer Community gesendet werden sollen.  
  - Der *Communityname* -Parameter gibt die Community, in der Trap-Nachrichten gesendet werden, anhand des Namens an.  
  - Der *-Parameter Hostid* gibt anhand des Namens oder der IP-Adresse den Host an, an den keine Trap-Nachrichten gesendet werden sollen.  
    ## <a name="BKMK_Examples"></a>Beispiele  
    In den folgenden Beispielen werden Einträge in der Konfigurationsdatei für den Befehl " **evntcmd** " veranschaulicht. Sie sind nicht darauf ausgelegt, an einer Eingabeaufforderung eingegeben zu werden.  
    Um eine Trap-Nachricht zu senden, wenn der Ereignisprotokoll Dienst neu gestartet wird, geben Sie Folgendes ein:  
    ```  
    #pragma add System "Eventlog" 2147489653  
    ```  
    Geben Sie Folgendes ein, um eine Trap-Nachricht zu senden, wenn der Ereignisprotokoll Dienst zweimal innerhalb von drei Minuten neu gestartet wird:  
    ```  
    #pragma add System "Eventlog" 2147489653 2 180  
    ```  
    Geben Sie Folgendes ein, um das Senden einer Trap-Nachricht zu erhalten, wenn der Ereignisprotokoll Dienst neu gestartet wird  
    ```  
    #pragma delete System "Eventlog" 2147489653  
    ```  
    Zum Senden von Trap-Nachrichten innerhalb der Community mit dem Namen Public an den Host mit der IP-Adresse 192.168.100.100 geben Sie Folgendes ein:  
    ```  
    #pragma add_TRAP_DEST public 192.168.100.100  
    ```  
    Geben Sie Folgendes ein, um Trap-Nachrichten innerhalb der Community namens "private" an den Host mit dem Namen host1  
    ```  
    #pragma add_TRAP_DEST private Host1  
    ```  
    Geben Sie Folgendes ein, um das Senden von Trap-Nachrichten innerhalb der Community mit dem Namen "private" an denselben Computer zu übertragen, auf dem Sie die  
    ```  
    #pragma delete_TRAP_DEST private localhost  
    ```  
    ## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
