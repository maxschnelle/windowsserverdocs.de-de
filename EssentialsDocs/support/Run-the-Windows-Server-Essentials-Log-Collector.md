---
title: "Führen Sie die Windows Server Essentials Log Collector"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6b49fee7ca4a19d5a501cf96c1ce356f8242c81f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Führen Sie die Windows Server Essentials Log Collector
Sie können die Windows Server Essentials Log Collector vom Server oder einem Computer im Netzwerk ausführen. Wenn Sie den Log Collector vom Server ausführen, können Sie nur Protokolle vom Server sammeln. Wenn Sie den Log Collector von einem Computer im Netzwerk ausführen, können Sie Protokolle vom Server, zusätzlich zu den Protokollen für diesen Computer erfasst.  
  
 Sie benötigen die entsprechenden Administratorrechte zum Ausführen des Log Collectors. Wenn Sie Protokolldateien für einen Server erfassen, müssen Sie ein Serveradministrator sein; Wenn Sie Protokolldateien auf einem Computer im Netzwerk erfassen, müssen Sie eine Client-Administrator für diesen Computer sein.  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>Der Log Collector auf dem Server ausgeführt wird, mithilfe des Assistenten  
  
1.  Auf der **starten** Seite des Servers, klicken Sie auf **Windows Server Essentials Log Collector**.  
  
    > [!NOTE]
    >  -   Wenn das Log Collector-Programm nicht angezeigt wird die **starten** Seite, wechseln Sie zu **%System%\Program Files (x86) \Windows Server Essentials Log Collector**, und doppelklicken Sie dann auf **LogCollector**.  
    > -   Wenn Sie nicht mit dem Server mit Administratorrechten angemeldet sind, werden Sie von den Log Collector aufgefordert, Ihre Anmeldeinformationen einzugeben.  
  
2.  Wenn Sie einen Speicherort für die erfassten Protokolldateien speichern aufgefordert werden, können Sie den Standardspeicherort **\\\ < ServerName\ > \logs**, oder einen anderen Speicherort angeben. Um den Standardspeicherort zu übernehmen, klicken Sie auf **Weiter**. Klicken Sie zum Ändern des Speicherorts auf **Durchsuchen**, navigieren Sie zu dem Ordner, in dem die Protokolldateien gespeichert werden sollen, und klicken Sie dann auf **speichern**.  
  
    > [!NOTE]
    >  Sie müssen nicht für die Protokolldateien Dateinamen angeben. Der Log Collector benennt die Sammlung der ZIP-Datei durch Verkettung der Computername und der Zeitstempel der Datei.  
  
3.  Eine Statusleiste wird angezeigt, während die Protokolle gesammelt werden.  
  
4.  Um den Inhalt der Protokolldatei für die Sammlung anzuzeigen, wählen Sie die **öffnen Sie den Speicherort, in dem die Protokolle gespeichert wurden**, und klicken Sie auf **schließen** den Assistenten zu schließen und öffnen die Protokolldatei für die Sammlung.  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>Der Log Collector auf einem Computer im Netzwerk ausgeführt wird, mithilfe des Assistenten  
  
1.  Navigieren Sie zu **%System%\Program Files (x86) \Windows Server Essentials Log Collector**, und klicken Sie dann auf die Datei **LogCollector.exe**.  
  
    > [!NOTE]
    >  Wenn Sie nicht auf dem Netzwerkcomputer mit Administratorrechten angemeldet sind, geben Sie Ihren Benutzernamen und Kennwort ein, und klicken Sie dann auf **Weiter**.  
  
2.  Wählen Sie die Protokolle, die Sie wie folgt erfassen möchten:  
  
    1.  Wählen Sie die **Protokolldateien** Kontrollkästchen, um die Protokolldateien auf dem Server zu erfassen.  
  
    2.  Die **Clientcomputer-Protokolldateien (dieser Computer)** Kontrollkästchen ist standardmäßig aktiviert und gibt an, dass der Log Collector die Protokolle vom Netzwerkcomputer gesammelt werden, die ausgeführt wird der. Wenn Sie nur Serverprotokolle erfassen möchten, deaktivieren Sie die **Clientcomputer-Protokolldateien (dieser Computer)** Kontrollkästchen.  
  
    3.  Klicken Sie auf **Weiter**.  
  
3.  Wenn Sie aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für ein Server-Administrator, und klicken Sie dann auf **Weiter**.  
  
4.  Geben Sie ein, oder navigieren Sie zu dem Speicherort der Protokolldateien zu speichern, und klicken Sie auf **Weiter**.  
  
    > [!NOTE]
    >  Sie müssen nicht für die Protokolldateien Dateinamen angeben. Der Log Collector benennt die Sammlung der ZIP-Datei durch Verkettung der Computername und der Zeitstempel der Datei.  
  
5.  Eine Statusleiste wird angezeigt, während die Protokolle gesammelt werden.  
  
6.  Um den Inhalt der Protokolldatei für die Sammlung anzuzeigen, wählen Sie die **öffnen Sie den Speicherort, in dem die Protokolle gespeichert wurden**, und klicken Sie auf **schließen** den Assistenten zu schließen und öffnen die Protokolldatei für die Sammlung.  
  
### <a name="running-the-log-collector-manually"></a>Ausführen von Log Collector manuell  
 Nachdem der Log Collector installiert ist, wird eine geplante Aufgabe zum Ausführen des Tools erstellt. Anschließend können Sie den Log Collector aus Ausführen der **geplanten Task-Manager** ohne den Assistenten, wenn Probleme beim Starten des Assistenten.  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>Der Log Collector manuell auf dem Server ausführen  
  
1.  Melden Sie sich direkt oder Remote mit dem Server.  
  
2.  Öffnen der **Taskplaner**.  
  
3.  Im Stammverzeichnis der **Aufgabenplanungsbibliothek**, navigieren Sie zu dem geplanten Task **LogCollector**.  
  
4.  Mit der rechten Maustaste **LogCollector**, und klicken Sie dann auf **ausführen**. Der Log Collector legt die Protokolle im Standardordner auf dem Server **\\\ < ServerName\ > \Logs**. Wenn Sie keine Schreibberechtigung für den Ordner haben, oder der Ordner ist nicht vorhanden, werden Protokolle platziert, der **< Temp\ >** Unterverzeichnis.  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>Um den Log Collector manuell auf einem Computer im Netzwerk ausführen  
  
1.  Melden Sie sich direkt oder Remote auf dem Netzwerkcomputer.  
  
2.  Öffnen der **Taskplaner**.  
  
3.  Im Stammverzeichnis der **Aufgabenplanungsbibliothek**, navigieren Sie zu dem geplanten Task **LogCollector**.  
  
4.  Mit der rechten Maustaste **LogCollector**, und klicken Sie dann auf **ausführen**. Der Log Collector legt die Protokolle in der **< Temp\ >** Ordner auf dem Computer im Netzwerk.
