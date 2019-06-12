---
title: evntcmd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e2a4a7f9e6bdf6f200b86e028617cae924571455
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439455"
---
# <a name="evntcmd"></a>evntcmd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Konfiguriert die Übersetzung von Ereignissen in Traps, Ziele oder beides basierend auf Informationen in einer Konfigurationsdatei.   
## <a name="syntax"></a>Syntax  
```  
evntcmd [/s <computerName>] [/v <verbosityLevel>] [/n] <FileName>  
```  
### <a name="parameters"></a>Parameter  

|      Parameter      |                                                                                                                                                            Beschreibung                                                                                                                                                             |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /s <computerName>  |                                                         Gibt den Namen, den Computer, auf dem Sie die Übersetzung von Ereignissen in Traps, Ziele oder beides zu konfigurieren möchten. Wenn Sie einen Computer nicht angeben, tritt ein, die Konfiguration, auf dem lokalen Computer.                                                          |
| /v <verbosityLevel> | Gibt an, welche Typen von Status, die Nachrichten werden als Traps und Trapziele konfiguriert sind. Dieser Parameter muss eine ganze Zahl zwischen 0 und 10 sein. Bei Angabe von 10 werden alle Typen von Nachrichten angezeigt, einschließlich der Verfolgung von Nachrichten und Warnungen zu, ob der Trap-Konfiguration erfolgreich war. Wenn Sie 0 angeben, werden keine Meldungen angezeigt. |
|         /n          |                                                                                                           Gibt an, dass der SNMP-Dienst nicht neu gestartet werden soll, wenn dieser Computer konfigurationsänderungen Trap empfangen.                                                                                                            |
|     <FileName>      |                                                                                     Gibt den Namen der Konfigurationsdatei mit Informationen zu der Übersetzung von Ereignissen in Traps und Ziele, die Sie konfigurieren möchten.                                                                                     |
|         /?          |                                                                                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                |

## <a name="remarks"></a>Hinweise  
- Wenn Sie Traps konfiguriert werden, jedoch nicht Trapziele möchten, können Sie eine gültige Konfigurationsdatei an erstellen, mithilfe von Ereignis, um die Trap-Konvertierung, dies ist ein grafisches Hilfsprogramm. Wenn Sie den SNMP-Dienst installiert haben, können Sie Ereignis Trap-Konvertierung starten, indem Sie die Eingabe **Evntwin** an einer Eingabeaufforderung. Nachdem Sie die Traps definiert haben, Sie möchten, klicken Sie auf exportieren, um eine Datei zu erstellen, die geeignet ist, für die Verwendung mit **Evntcmd**. Können Sie Ereignis Trap-Konvertierung ganz einfach eine Konfigurationsdatei erstellen, und klicken Sie dann mithilfe der Konfigurationsdatei mit **Evntcmd** an der Eingabeaufforderung aus, um Traps schnell auf mehreren Computern zu konfigurieren.  
- Die Syntax für die Konfiguration einer Traps lautet wie folgt aus:  
  **#pragma add**<em><EventLogFile> <EventSource> <EventID> [<Count> [<Period>]]</em>  
  -   Der Text **#pragma** müssen am Anfang jeder Eintrag in der Datei angezeigt werden.  
  -   Der Parameter **hinzufügen** gibt an, dass eine Ereignis, um das Abfangen der Konfiguration hinzugefügt werden soll.  
  -   Die Parameter *Ereignisprotokolldatei*, *EventSource*, und *EventID* erforderlich sind. Der Parameter *Ereignisprotokolldatei* gibt die Datei, in dem das Ereignis wird aufgezeichnet. Der Parameter *EventSource* gibt an, die Anwendung, die das Ereignis generiert. Die *EventID* Parameter gibt die eindeutige Nummer, die jedes Ereignis identifiziert. Starten, um herauszufinden, welche Werte bestimmten Ereignissen entsprechen, Ereignis, um die Trap-Konvertierung geben **Evntwin** an einer Eingabeaufforderung. Klicken Sie auf **benutzerdefinierte**, und klicken Sie dann auf **bearbeiten**. Klicken Sie unter **Ereignisquellen**, Durchsuchen Sie die Ordner aus, bis Sie das Ereignis Sie verwenden möchten finden, konfigurieren, klicken darauf, und klicken Sie dann auf **hinzufügen**. Informationen über die Ereignisquelle, die Ereignis-Protokolldatei und die Ereignis-ID angezeigt wird, klicken Sie unter **Quell-, melden Sie sich**, und **abfangen spezifische ID**bzw.  
  -   Die *Anzahl* Parameter ist optional, und gibt an, wie oft das Ereignis auftreten muss, bevor eine Trap-Nachricht gesendet wird. Wenn Sie nicht verwenden, die *Anzahl* -Parameter der Trap-Nachricht wird gesendet, nachdem das Ereignis tritt einmal auf.  
  -   Die *Zeitraum* Parameter ist optional, aber es müssen Sie verwenden die *Anzahl* Parameter. Die *Zeitraum* Parameter gibt die eine Zeitdauer (in Sekunden) während der muss das Ereignis auftritt, die Anzahl der Male, die mit der Count-Parameter angegeben wird, bevor eine Trap-Nachricht gesendet wird. Wenn Sie nicht verwenden, die *Zeitraum* Parameter eine Trap-Nachricht wird gesendet, nachdem das Ereignis tritt auf, wie oft mit angegeben wird, der *Anzahl* Parameter, unabhängig davon, wie viel Zeit zwischen den Ausführungen verstreicht.  
- Die Syntax für das Entfernen eines Traps lautet wie folgt:  
  **#pragma delete**<em><EventLogFile> <EventSource> <EventID></em>  
  -   Der Text **#pragma** müssen am Anfang jeder Eintrag in der Datei angezeigt werden.  
  -   Der Parameter *löschen* gibt an, dass eine Ereignis, um die Konfiguration abfangen entfernt werden soll.  
  -   Die Parameter *Ereignisprotokolldatei*, *EventSource*, und *EventID* erforderlich sind. Der Parameter *Ereignisprotokolldatei* gibt das Protokoll an, in dem das Ereignis aufgezeichnet wird. Der Parameter *EventSource* gibt an, die Anwendung, die das Ereignis generiert. Die *EventID* Parameter gibt die eindeutige Nummer, die jedes Ereignis identifiziert.  
- Die Syntax für die Konfiguration der Trap-Ziel lautet wie folgt aus:  
  **#pragma add_TRAP_DEST**<em><CommunityName> <HostID></em>  
  -   Der Text **#pragma** müssen am Anfang jeder Eintrag in der Datei angezeigt werden.  
  -   Der Parameter **Add_TRAP_DEST** gibt an, dass Sie die Trap-Nachrichten an einem bestimmten Host in einer Community gesendet werden soll.  
  -   Der Parameter *CommunityName* gibt an, den Namen der Community, die in die Trap-Nachrichten gesendet werden.  
  -   Der Parameter *"HostID"* gibt den Namen oder die IP-Adresse des Hosts an, die Trap-Nachrichten gesendet werden sollen.  
- Die Syntax für das Entfernen der Trap-Ziel lautet wie folgt aus:  
  **#pragma delete_TRAP_DEST**<em><CommunityName> <HostID></em>  
  - Der Text **#pragma** müssen am Anfang jeder Eintrag in der Datei angezeigt werden.  
  - Der Parameter *Delete_TRAP_DEST* gibt an, dass Sie nicht möchten, dass Trap-Nachrichten an einem bestimmten Host in einer Community gesendet werden.  
  - Der Parameter *CommunityName* gibt an, den Namen der Community, die in die Trap-Nachrichten gesendet werden.  
  - Der Parameter *"HostID"* gibt den Namen oder die IP-Adresse des Hosts, Sie möchten nicht Trap-Nachrichten gesendet werden.  
    ## <a name="BKMK_Examples"></a>Beispiele für  
    Die folgenden Beispiele veranschaulichen die Einträge in der Konfigurationsdatei für die **Evntcmd** Befehl. Sie dienen nicht an einer Eingabeaufforderung eingegeben werden.  
    Wenn der Ereignisprotokolldienst neu gestartet wird, geben Sie eine Trap-Nachricht zu senden:  
    ```  
    #pragma add System "Eventlog" 2147489653  
    ```  
    Zum Senden, geben Sie eine Trap-Nachricht, wenn der Ereignisprotokolldienst zweimal in drei Minuten neu gestartet wird:  
    ```  
    #pragma add System "Eventlog" 2147489653 2 180  
    ```  
    Um zu beenden, senden eine Trap-Nachricht ein, wenn die Ereignisprotokoll-Dienst neu gestartet wird, geben Sie Folgendes ein:  
    ```  
    #pragma delete System "Eventlog" 2147489653  
    ```  
    Um in der Community, die mit dem Namen Public an den Host mit der IP-Adresse 192.168.100.100 Trap-Nachrichten zu senden, geben Sie Folgendes ein:  
    ```  
    #pragma add_TRAP_DEST public 192.168.100.100  
    ```  
    Um in der Community, die mit dem Namen Private an den Host mit dem Namen "host1" Trap-Nachrichten zu senden, geben Sie Folgendes ein:  
    ```  
    #pragma add_TRAP_DEST private Host1  
    ```  
    Zum Beenden, sendet der Trap-Nachrichten in der Community, die mit dem Namen Private auf dem gleichen Computer, auf dem Sie Ziele konfigurieren, geben Sie Folgendes ein:  
    ```  
    #pragma delete_TRAP_DEST private localhost  
    ```  
    ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
