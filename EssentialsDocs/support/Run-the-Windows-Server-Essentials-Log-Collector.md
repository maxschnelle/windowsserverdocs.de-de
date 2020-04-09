---
title: Ausführen des Windows Server Essentials-Protokollsammlers
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6aac2ed382321349d39874c7db7617f6da845919
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852273"
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Ausführen des Windows Server Essentials-Protokollsammlers
Sie können den Windows Server Essentials Log Collector auf dem Server oder einem Computer im Netzwerk ausführen. Wenn Sie den Log Collector vom Server ausführen, können nur Protokolle vom Server erfasst werden. Wenn Sie den Log Collector von einem Computer im Netzwerk ausführen, können Sie auswählen, ob Protokolle von dem Server, zusätzlich zu den Protokollen für diesen Computer, erfasst werden sollen.  
  
 Sie müssen über die entsprechenden Administratorrechte zum Ausführen des Log Collector verfügen. Wenn Sie Protokolldateien für einen Server erfassen, müssen Sie ein Serveradministrator sein; Wenn Sie Protokolldateien auf einem Computer im Netzwerk erfassen, müssen Sie ein Clientadministrator für diesen Computer sein.  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>So führen Sie den Log Collector auf dem Server mithilfe des Assistenten aus  
  
1. Klicken Sie auf der **Start** Seite des Servers auf **Windows Server Essentials Log Collector**.  
  
   > [!NOTE]
   > - Wenn das Programm "Log Collector" nicht auf der **Start** Seite angezeigt wird, navigieren Sie zu **%System%\Program Files (x86) \Windows Server Essentials Log Collector**, und doppelklicken Sie dann auf **logcollector**.  
   >   -   Wenn Sie nicht auf dem Server mit Administratorrechten angemeldet sind, werden Sie vom Log Collector zur Eingabe Ihrer Anmeldeinformationen aufgefordert.  
  
2. Wenn Sie aufgefordert werden, einen Speicherort zum Speichern der gesammelten Protokolldateien anzugeben, können Sie den Standard Speicherort **\\\\< Servername\>\Logs**auswählen oder einen anderen Speicherort angeben. Um den Standardspeicherort zu übernehmen, klicken Sie auf **Weiter**. Zum Ändern des Speicherorts klicken Sie auf **Durchsuchen**, navigieren Sie zu dem Ordner, in dem Protokolldateien gespeichert werden sollen, und klicken Sie dann auf **Speichern**.  
  
   > [!NOTE]
   >  Sie brauchen keine Dateinamen für die Protokolldateien anzugeben. Der Log Collector benennt die Sammlung der ZIP-Dateien, indem er den Computernamen und den Zeitstempel der Datei verkettet.  
  
3. Eine Statusleiste wird angezeigt, während die Protokolle erfasst werden.  
  
4. Um den Inhalt der Protokollerfassungsdatei anzuzeigen, wählen Sie das Kontrollkästchen **Speicherort der Protokolldateien öffnen** aus, und klicken Sie auf **Schließen**, um den Assistenten zu schließen und die Protokollerfassungsdatei zu öffnen.  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>So führen Sie den Log Collector auf einem Netzwerkcomputer mithilfe des Assistenten aus  
  
1.  Navigieren Sie zu **%System%\Program Files (x86) \Windows Server Essentials Log Collector**, und doppelklicken Sie dann auf die Datei **logcollector. exe**.  
  
    > [!NOTE]
    >  Wenn Sie nicht auf dem Netzwerkcomputer mit Administratorrechten angemeldet sind, geben Sie Ihren Benutzernamen und das Kennwort ein, wenn Sie dazu aufgefordert werden, und klicken Sie dann auf **Weiter**.  
  
2.  Wählen Sie die Protokolle, die Sie erfassen möchten, wie folgt aus:  
  
    1.  Wählen Sie das Kontrollkästchen**Serverprotokolldateien** aus, um Protokolldateien auf dem Server zu sammeln.  
  
    2.  Das Kontrollkästchen **Clientcomputer-Protokolldateien (dieser Computer)** ist standardmäßig aktiviert und gibt an, dass der Log Collector die Protokolle vom Netzwerkcomputer, der ausgeführt wird, erfasst. Wenn Sie nur Serverprotokolle erfassen möchten, deaktivieren Sie das Kontrollkästchen **Clientcomputer-Protokolldateien (dieser Computer)** .  
  
    3.  Klicken Sie auf **Weiter**.  
  
3.  Wenn Sie dazu aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für einen Serveradministrator ein, und klicken Sie dann auf **Weiter**.  
  
4.  Navigieren Sie zu dem Speicherort für die Protokolldateien oder geben Sie den Speicherort ein, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Sie brauchen keine Dateinamen für die Protokolldateien anzugeben. Der Log Collector benennt die Sammlung der ZIP-Dateien, indem er den Computernamen und den Zeitstempel der Datei verkettet.  
  
5.  Eine Statusleiste wird angezeigt, während die Protokolle erfasst werden.  
  
6.  Um den Inhalt der Protokollerfassungsdatei anzuzeigen, wählen Sie das Kontrollkästchen **Speicherort der Protokolldateien öffnen** aus, und klicken Sie auf **Schließen**, um den Assistenten zu schließen und die Protokollerfassungsdatei zu öffnen.  
  
### <a name="running-the-log-collector-manually"></a>Manuelles Ausführen von Log Collector  
 Nachdem der Log Collector installiert ist, wird eine geplante Aufgabe zum Ausführen des Tools erstellt. Anschließend können Sie den Log Collector aus dem **Manager für geplante Aufgaben** heraus ausführen, ohne den Assistenten zu verwenden, wenn Probleme beim Starten des Assistenten auftreten.  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>So führen Sie den Log Collector manuell auf dem Server aus  
  
1.  Melden Sie sich direkt oder remote auf dem Server an.  
  
2.  Öffnen Sie den **Taskplaner**.  
  
3.  Navigieren Sie im Stamm der **Aufgabenplanungsbibliothek** zur geplanten Aufgabe mit dem Namen **LogCollector**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **LogCollector**, und klicken Sie dann auf **Ausführen**. Der Log Collector platziert die Protokolle im Standardordner auf dem Server, **\\\\< Servername\>\Logs**. Wenn Sie nicht über Schreibberechtigungen für den Ordner verfügen oder der Ordner nicht vorhanden ist, werden die Protokolle im < temporären **\>** Unterverzeichnis abgelegt.  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>So führen Sie den Log Collector manuell auf dem Netzwerkcomputer aus  
  
1.  Melden Sie sich direkt oder remote auf dem Netzwerkcomputer an.  
  
2.  Öffnen Sie den **Taskplaner**.  
  
3.  Navigieren Sie im Stamm der **Aufgabenplanungsbibliothek** zur geplanten Aufgabe mit dem Namen **LogCollector**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **LogCollector**, und klicken Sie dann auf **Ausführen**. Der Log Collector platziert die Protokolle im Ordner **< Temp\>** auf dem Netzwerk Computer.
