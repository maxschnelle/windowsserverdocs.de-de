---
title: WSUS-Nachrichten und Tipps zur Problembehandlung
description: 'Windows Server Update Service (WSUS)-Thema: Problembehandlung bei Verwendung von WSUS-Nachrichten'
ms.prod: windows-server
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
ms.openlocfilehash: 1e432a962662995cf570b28d0b9496594f3e10e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369859"
---
# <a name="wsus-messages-and-troubleshooting-tips"></a>WSUS-Nachrichten und Tipps zur Problembehandlung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Informationen zu den folgenden WSUS-Meldungen:

-   "Der Computer hat den Status nicht gemeldet"

-   "Nachrichten-ID 6703-Fehler bei der WSUS-Synchronisierung"

-   "Fehler 0x80070643: Schwerwiegender Fehler bei der Installation "

-   "Einige Dienste werden nicht ausgeführt. Überprüfen Sie die folgenden Dienste [...] ".

## <a name="computer-has-not-reported-status"></a>Der Computer hat den Status nicht gemeldet.
Diese Meldung wird in der WSUS-Konsole generiert, wenn ein WSUS-Client Computer keine Informationen an den WSUS-Server sendet, um den aktuellen Aktualisierungs Status anzugeben. Dieses Problem tritt normalerweise durch den WSUS-Client Computer und nicht durch den WSUS-Server auf.

Die häufigsten Gründe sind:

-   Die Konnektivität des Computers mit dem Netzwerk wurde unterbrochen:
    -   Das Netzwerkkabel ist nicht verbunden.
    -   Ein dazwischenliegende Netzwerkkabel ist fehlerhaft.
    -   Der Computer verfügt über einen fehlerhaften Netzwerkadapter.
    -   Der Netzwerkport, mit dem der Computer verbunden ist, wurde deaktiviert.
    -   Der drahtlose Adapter kann keine Verbindung mit dem drahtlosen Zugriffspunkt des Unternehmens herstellen und eine Verbindung mit ihm herstellen.
-   Der Computer ist ausgeschaltet. (Es wurde heruntergefahren oder befindet sich im Standbymodus oder im Ruhezustand.)

## <a name="message-id-6703---wsus-synchronization-failed"></a>Meldungs-ID 6703-Fehler beim Synchronisieren der WSUS
> Meldung: Fehler bei der Anforderung mit HTTP-Status 503: Dienst nicht verfügbar.
> 
> Quelle: Microsoft. updateservices. Administration. AdminProxy. kreateupdateserver.

Wenn Sie versuchen, Update Services auf dem WSUS-Server zu öffnen, erhalten Sie die folgende Fehlermeldung:

> Fehler: Verbindungsfehler
> 
> Fehler beim Herstellen einer Verbindung mit dem WSUS-Server. Dieser Fehler kann aus verschiedenen Gründen auftreten. Wenden Sie sich an Ihren Netzwerkadministrator, falls das Problem weiterhin besteht. Klicken Sie auf den Server Knoten zurücksetzen, um erneut eine Verbindung mit dem Server herzustellen.

Zusätzlich zu den obigen Schritten schlägt der Zugriff auf die URL für die WSUS-Verwaltungs Website (d. h. `http://CM12CAS:8530`) mit dem folgenden Fehler fehl:

> HTTP-Fehler 503. Der Dienst ist nicht verfügbar.

In dieser Situation ist die wahrscheinlichste Ursache, dass sich der WsusPool-Anwendungs Pool in IIS im beendeten Zustand befindet.

Außerdem wird der Standardwert für das Limit für den privaten Speicher (KB) für den Anwendungs Pool wahrscheinlich auf den Standardwert von 1843200 KB festgelegt. Wenn dieses Problem auftritt, erhöhen Sie das Limit für den privaten Speicher auf 4 GB (4 Millionen KB), und starten Sie den Anwendungs Pool neu. Um das Limit für den privaten Speicher zu erhöhen, wählen Sie den Anwendungs Pool WsusPool aus, und klicken Sie unter Anwendungs Pool bearbeiten auf Erweiterte Einstellungen. Legen Sie dann das Limit für den privaten Speicher auf 4 GB (4 Millionen KB) fest. Nachdem der Anwendungs Pool neu gestartet wurde, überwachen Sie den Status der SMS_WSUS_SYNC_Manager-Komponente, "WCM. log" und "wsyncmgr. log" auf Fehler. Beachten Sie, dass es möglicherweise erforderlich ist, den Grenzwert für den privaten Arbeitsspeicher je nach Umgebung auf 8 GB (8 Millionen KB) oder höher zu erhöhen.

Weitere Informationen finden Sie unter: [Die WSUS-Synchronisierung in ConfigMgr 2012 schlägt mit HTTP 503-Fehlern fehl.](http://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx)

## <a name="error-0x80070643-fatal-error-during-installation"></a>Fehler 0x80070643: Schwerwiegender Fehler bei der Installation
Das WSUS-Setup verwendet Microsoft SQL Server, um die Installation auszuführen. Dieses Problem tritt auf, weil der Benutzer, der das WSUS-Setup ausgeführt hat, nicht über System Administrator Berechtigungen in SQL Server verfügt.

Um dieses Problem zu beheben, erteilen Sie System Administrator Berechtigungen für ein Benutzerkonto oder ein Gruppenkonto in SQL Server, und führen Sie dann das WSUS-Setup erneut aus.

## <a name="some-services-are-not-running-check-the-following-services"></a>Einige Dienste werden nicht ausgeführt. Überprüfen Sie die folgenden Dienste:

- **Selbst Aktualisierungs** Weitere Informationen zur Problembehandlung beim SelfUpdate-Dienst finden Sie unter [Automatische Updates muss aktualisiert werden](https://technet.microsoft.com/library/cc708554(v=ws.10).aspx) .

- **Wssuservice. exe:** Dieser Dienst vereinfacht die Synchronisierung. Wenn bei der Synchronisierung Probleme auftreten, greifen Sie auf "wsusservice. exe" zu, indem Sie auf **Start**, zeigen Sie auf **Verwaltung**, klicken Sie auf **Dienste**, und suchen Sie dann in der Liste der Dienste nach **Windows Server Update Service** . Gehen Sie wie folgt vor:
    
    -   Überprüfen Sie, ob dieser Dienst ausgeführt wird. Klicken Sie auf **starten** , wenn es beendet oder **neu gestartet** wird, um den Dienst zu aktualisieren.
    
    -   Verwenden Sie Ereignisanzeige, um die **Anwendungs**-, **SECURIT**-und **System** Ereignisprotokolle zu überprüfen, um festzustellen, ob Ereignisse vorhanden sind, die möglicherweise auf ein Problem hinweisen.
    
    -   Sie können auch die Datei "SoftwareDistribution. log" überprüfen, um festzustellen, ob Ereignisse vorhanden sind, die auf ein Problem hinweisen können.

- **Webservicessql-Dienst:** Webdienste werden in IIS gehostet. Wenn Sie nicht ausgeführt werden, stellen Sie sicher, dass IIS ausgeführt wird (oder gestartet). Sie können auch versuchen, den Webdienst zurückzusetzen, indem Sie an einer Eingabeaufforderung **iisreset** eingeben.

- **SQL-Dienst:** Jeder Dienst mit Ausnahme des selbst Aktualisierungs-Dienstanbieter erfordert, dass der SQL-Dienst ausgeführt wird. Wenn eine der Protokolldateien SQL-Verbindungsprobleme anzeigt, überprüfen Sie zuerst den SQL-Dienst. Um auf den SQL-Dienst zuzugreifen, klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, klicken Sie auf **Dienste**, und suchen Sie dann nach einem der folgenden Informationen:
    
  - **MSSQLSERVER** (wenn Sie WMSDE oder MSDE verwenden, oder wenn Sie SQL Server verwenden und den Standardinstanznamen für den Instanznamen verwenden)
    
  - **MSSQL $ WSUS** (wenn Sie eine SQL Server Datenbank verwenden und die Daten Bank Instanz "WSUS" benannt haben)
    
    Klicken Sie mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten** , wenn der Dienst nicht ausgeführt wird, oder **neu starten** , um den Dienst zu aktualisieren, falls er ausgeführt wird
