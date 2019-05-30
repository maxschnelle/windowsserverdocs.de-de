---
title: WSUS-Nachrichten und Tipps zur Problembehandlung
description: Windows Server Update Service (WSUS)-Thema – Problembehandlung bei der Verwendung von WSUS-Nachrichten
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f6317f7-bfe0-42d9-87ce-d8f038c728ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 77a4702ddab987cb3adda7627badb790e3102952
ms.sourcegitcommit: 8eea7aadbe94f5d4635c4ffedc6a831558733cc0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308546"
---
# <a name="wsus-messages-and-troubleshooting-tips"></a>WSUS-Nachrichten und Tipps zur Problembehandlung

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema enthält Informationen über die folgenden WSUS-Nachrichten:

-   "Der Computer hat keinen Status erstellt"

-   "Statusmeldung 6703 - Fehler bei der WSUS-Synchronisierung"

-   "Fehler 0 x 80070643: Schwerwiegender Fehler während der Installation"

-   "Einige Dienste werden nicht ausgeführt. Überprüfen Sie die folgenden Dienste [...]"

## <a name="computer-has-not-reported-status"></a>Computer hat Status nicht gemeldet.
Diese Meldung wird in der WSUS-Konsole generiert, wenn es sich bei ein WSUS-Clientcomputer auf den WSUS-Server an ihrem aktuellen Zustand des Updates keine Informationen sendet. Dieses Problem wird in der Regel durch die WSUS-Clientcomputer nicht auf dem WSUS-Server verursacht.

Die häufigsten Gründe sind:

-   Der Computer hat die Verbindung mit dem Netzwerk verloren:
    -   Es ist das Netzwerkkabel abgezogen.
    -   Ein Beteiligte Netzwerkkabel ist fehlerhaft.
    -   Der Computer hat einen fehlerhaften Netzwerkadapter.
    -   Der Netzwerkport mit dem der Computer verbunden wurde deaktiviert.
    -   Der drahtlose Adapter kann nicht zugeordnet werden und eine Verbindung herstellen, mit dem Unternehmensnetzwerk drahtlosen Zugriffspunkt.
-   Der Computer ist ausgeschaltet. (Es heruntergefahren wurde oder befindet sich im Standbymodus oder Ruhezustand-Modus).

## <a name="message-id-6703---wsus-synchronization-failed"></a>Statusmeldung 6703 - WSUS-Synchronisierung fehlgeschlagen
> Meldung: Die Anforderung ist mit HTTP-Status 503 fehlgeschlagen: Der Dienst ist nicht verfügbar.

> Quelle: Microsoft.UpdateServices.Administration.AdminProxy.createUpdateServer.

Wenn Sie versuchen, die Update Services auf dem WSUS-Server öffnen Fehlermeldung Sie die folgende:

> Fehler: Verbindungsfehler

> Verbindung mit dem WSUS-Server ist ein Fehler aufgetreten. Dieser Fehler kann eine Reihe von Gründen auftreten. Wenden Sie sich an Ihren Netzwerkadministrator, wenn das Problem weiterhin besteht. Klicken Sie auf das Zurücksetzen des Server-Knoten, um erneut eine Verbindung mit dem Server herzustellen.

Zusätzlich zu den oben genannten versucht, auf die URL für die WSUS-Verwaltungswebsite zugreifen (z. B. `http://CM12CAS:8530`) mit folgendem Fehler fehl:

> HTTP-Fehler 503. Der Dienst ist nicht verfügbar

In diesem Fall ist die wahrscheinlichste Ursache, dass die Wsuspool-Anwendung in IIS in einem beendeten Zustand.

Darüber hinaus wird der Private Arbeitsspeicher Grenzwert (KB) für den Anwendungspool wahrscheinlich auf den Standardwert von 1843200 KB festgelegt. Wenn Sie dieses Problem auftritt, erhöhen Sie das Limit für den privaten Speicher auf 4GB (4000000 KB), und starten Sie den Anwendungspool neu. Um das Limit für den privaten Speicher zu erhöhen, wählen Sie die Wsuspool-Anwendung aus, und klicken Sie auf Erweiterte Einstellungen unter "Anwendungspool bearbeiten". Legen Sie das Limit für den privaten Speicher auf 4GB (4000000 KB). Nach der Anwendungspool neu gestartet wurde, überwachen Sie die SMS_WSUS_SYNC_MANAGER-Komponentenstatus, die "WCM.log" und die Datei "WSyncMgr.log" auf Fehler aus. Beachten Sie, dass es möglicherweise erforderlich, um das Arbeitsspeicherlimit Private auf 8 GB (8000000 KB) oder höher abhängig von der Umgebung zu erhöhen.

Weitere Informationen finden Sie unter: [Fehler bei der WSUS-Synchronisierung in Configuration Manager 2012 mit HTTP 503-Fehler](http://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx)

## <a name="error-0x80070643-fatal-error-during-installation"></a>Fehler 0 x 80070643: Schwerwiegender Fehler bei der installation
WSUS-Setup verwendet Microsoft SQL Server, um die Installation durchzuführen. Dieses Problem tritt auf, da der Benutzer, der WSUS-Setup ausgeführt wird, nicht über Systemadministratorberechtigungen in SQL Server verfügt.

Um dieses Problem zu beheben, Gewähren von Berechtigungen vom Systemadministrator, um ein Benutzerkonto oder ein Gruppenkonto in SQL Server, und führen Sie das WSUS-Setup erneut aus.

## <a name="some-services-are-not-running-check-the-following-services"></a>Einige Dienste werden nicht ausgeführt. Überprüfen Sie die folgenden Dienste:

- **SelfUpdate:** Finden Sie unter [automatischer Updates muss aktualisiert werden](https://technet.microsoft.com/library/cc708554(v=ws.10).aspx) Informationen zur Problembehandlung bei selbstaktualisierungsdiensts.

- **WSSUService.exe:** Dieser Dienst ermöglicht die Synchronisierung. Wenn Sie Probleme bei der Synchronisierung haben, WSUSService.exe zugreifen, indem Sie auf **starten**, zeigen Sie auf **Verwaltung**, klicken Sie auf **Services**, und suchen dann nach **Windows Server Update Service** in der Liste der Dienste. Gehen Sie wie folgt vor:
    
    -   Stellen Sie sicher, dass dieser Dienst ausgeführt wird. Klicken Sie auf **starten** beendet oder **Neustart** auf den Dienst zu aktualisieren.
    
    -   Mithilfe der Ereignisanzeige zum Überprüfen der **Anwendung**, **Securit**"y" und **System** Ereignisprotokolle, um festzustellen, ob die Ereignisse, die ein Problem hinweisen vorhanden sind.
    
    -   Sie können auch überprüfen, dass die Datei "SoftwareDistribution.log", um festzustellen, ob die Ereignisse, die ein Problem hinweisen.

- **Web-ServicesSQL Dienst:** Webdienste werden in IIS gehostet. Wenn sie nicht ausgeführt werden, stellen Sie sicher, dass IIS ausgeführt wird (oder gestartet) ist. Sie können auch versuchen, das Zurücksetzen des Webdiensts durch Eingabe **"iisreset"** an einer Eingabeaufforderung.

- **SQL Service:** Jeder Dienst, mit Ausnahme von selbstaktualisierungsdiensts erfordert, dass der SQL-Dienst ausgeführt wird. Wenn eine der Protokolldateien für SQL-Verbindungsprobleme anzugeben, überprüfen Sie zunächst den SQL-Dienst. Um die SQL-Dienst zuzugreifen, klicken Sie auf **starten**, zeigen Sie auf **Verwaltung**, klicken Sie auf **Services**, und suchen Sie nach einer der folgenden:
    
    -   **MSSQLSERver** (bei Verwendung WMSDE oder MSDE, oder wenn Sie SQL Server verwenden und der Name der Standardinstanz für den Instanznamen verwenden)
    
    -   **MSSQL$ WSUS** (Wenn Sie SQL Server-Datenbank verwenden und müssen mit dem Namen Ihrer Datenbankinstanz "WSUS")
    
    Mit der rechten Maustaste in des Diensts, und klicken Sie dann auf **starten** , wenn der Dienst nicht ausgeführt wird, oder **Neustart** auf den Dienst zu aktualisieren, wenn er ausgeführt wird.
