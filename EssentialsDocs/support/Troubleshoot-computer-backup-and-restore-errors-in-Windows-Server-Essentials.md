---
title: Problembehebung bei computersicherungs- und Wiederherstellungsfehlern in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 06/25/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37e79661442ba9f66a564b6c6c8fb57db1978454
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>Problembehebung bei computersicherungs- und Wiederherstellungsfehlern in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Verwenden Sie diese Verfahren, um die Problembehandlung von computersicherungen in Windows Server Essentials, einschließlich sicherungskonfigurationsproblemen, unvollständige oder nicht erfolgreiche Sicherungen, sicherungsstatuswarnungen und Probleme mit Datei-, Ordner- oder vollständigen systemwiederherstellungen.  
  
> [!NOTE]
>  Die neuesten Informationen zur Problembehandlung aus der Windows Server Essentials-Community finden Sie auf der [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums//winserveressentials/threads).  
  
##  <a name="BKMK_TroubleshootBackupConfigurationIssues"></a>Behandeln von sicherungskonfigurationsproblemen für einen verbundenen Computer  
 Verwenden Sie diese Verfahren behandeln von Problemen mit Sicherungskonfigurationen für Computer, die auf dem Windows Server Essentials-Server gesichert werden.  
  
### <a name="errors"></a>Fehler  
  
-   Sicherungskonfiguration wurde nicht erfolgreich abgeschlossen.  
  
-   Fehler beim Sammeln von Informationen für Computer  
  
-   Fehler beim Entfernen des Computers aus einer Sicherung  
  
### <a name="resolutions"></a>Auflösungen  
  
##### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>Problembehandlung bei Fehlern, die beim Konfigurieren von Sicherungen für einen verbundenen Computer auftreten  
  
1.  Stellen Sie sicher, dass Ihr Computer über ein Netzwerkgerät mit dem Netzwerk verbunden ist.  
  
2.  Stellen Sie sicher, dass das Netzwerkgerät, dem mit der Computer verbunden ist auch mit dem Netzwerk, eingeschaltet ist, verbunden ist und einwandfrei funktioniert.  
  
3.  Stellen Sie sicher, dass Windows Server Client Backup Service und Windows Server Client Computer Backup Provider Service auf dem Server ausgeführt werden.  
  
    ###### <a name="to-start-computer-backup-services-on-the-server"></a>Starten Sie computersicherungsdienste auf dem Server  
  
    1.  Klicken Sie auf dem Server, auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
    2.  Führen Sie einen Bildlauf nach unten, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **gestartet**mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten**.  
  
    3.  Klicken Sie auf **Windows Server Client Computer Backup Service**. Wenn der Status des Diensts nicht **gestartet**mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten**.  
  
    4.  Schließen **Dienste**.  
  
4.  Stellen Sie sicher, dass Windows Server Client Computer Backup Provider Service auf dem Clientcomputer ausgeführt wird.  
  
    ###### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>Starten Sie den computersicherungsdienst auf dem Clientcomputer  
  
    1.  Klicken Sie auf dem Clientcomputer auf **starten**, Typ **Dienste** in der **Programme und Dateien suchen** Textfeld, und drücken Sie dann die EINGABETASTE.  
  
    2.  Führen Sie einen Bildlauf nach unten, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **gestartet**mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten**.  
  
    3.  Schließen **Dienste**.  
  
5.  Überprüfen Sie Warnungen, um zu bestimmen, ob der Fehler in der Sicherungsdatenbank vorliegen. Wenn Fehler vorhanden sind, führen Sie die Anweisungen in der Warnung, um die Sicherungsdatenbank reparieren.  
  
6.  Deinstallieren Sie die Windows Server Essentials Connector-Software auf dem Computer, und installieren Sie es erneut. Weitere Informationen finden Sie unter den Themen [deinstallieren die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [installieren Sie die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11).  
  
##  <a name="BKMK_TroubleshootaBackupThatDidNotCompleteProperly"></a>Problembehandlung bei einer Sicherung, die nicht ordnungsgemäß abgeschlossen wurde  
 Wenn eine Sicherung nicht erfolgreich war, ist kein Teil der Sicherung erfolgreich ist und keine Daten für die Wiederherstellung verfügbar. Jedoch, wenn eine Sicherung unvollständig ist, angegeben nicht alle Elemente in der Sicherung Konfiguration gesichert wurden, aber einige Daten möglicherweise für die Wiederherstellung verfügbar sein.  
  
### <a name="errors"></a>Fehler  
  
-   Sicherung ist unvollständig  
  
-   Sicherung nicht erfolgreich  
  
### <a name="resolutions"></a>Auflösungen  
  
##### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>So identifizieren Sie Volumes, die nicht erfolgreich gesichert wurden  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf **Computer und Sicherung**.  
  
2.  Klicken Sie auf den Namen des Computers, in denen Sicherung nicht erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Computereigenschaften anzeigen** in der **Aufgaben** Bereich.  
  
3.  Klicken Sie auf die Sicherung, die nicht erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Details anzeigen**.  
  
4.  In der **Sicherungsdetails**, ein grünes Häkchen angezeigt wird der Status jedes Volumes, die erfolgreich gesichert wurde.  
  
##### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>Problembehandlung bei einer nicht erfolgreichen Sicherung eines Volumes  
  
1.  Stellen Sie sicher, dass die Festplatte mit dem Computer aktiviert ist, verbunden ist und einwandfrei funktioniert.  
  
2.  Führen Sie **Chkdsk /f r** zum Beheben von Fehler auf der Festplatte (**/f**) und lesbare Informationen über fehlerhaften Sektoren wiederherzustellen (**/r**). Weitere Informationen zum Ausführen **Chkdsk**, finden Sie unter [CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562).  
  
3.  Stellen Sie sicher, dass der Computer nicht heruntergefahren oder vom Netzwerk getrennt wird, während die Sicherung ausgeführt wurde.  
  
4.  Stellen Sie sicher, dass genügend freier Speicherplatz vorhanden ist, auf jedem Volume für die Sicherung ausgeführt. Sicherung erfordert zusätzlichen Speicherplatz auf dem Clientcomputer einen VSS-Snapshot zu erstellen. Auf Volumes, die nicht das System reserviert ist, muss mindestens 10Prozent verfügbarer Speicherplatz frei sein. Auf einem System reservierte Volume das Volume kleiner als 500MB ist, erfordert VSS 32MB freien Speicherplatz zum Erstellen eines Snapshots. ist das Volume 500MB oder größer, erfordert VSS 320MB freien Speicherplatz.  
  
     Wenn nicht genügend freier Speicherplatz auf einem Volume verfügbar ist, führen Sie eine der folgenden Lösungen:  
  
    -   Erweitern Sie das Volume. Sie können alle dynamischen Volumes mit Ausnahme von der das System reservierten Volume erweitern.  
  
        ###### <a name="to-extend-a-volume"></a>Erweitern eines Volumes  
  
        1.  Klicken Sie in der Systemsteuerung auf **System und Sicherheit**.  
  
        2.  Klicken Sie unter **Verwaltung**, klicken Sie auf **erstellen und Formatieren von Festplattenpartitionen**.  
  
        3.  Klicken Sie auf das Volume, das Sie erweitern möchten. Wenn **Volume erweitern** ist aktiviert, wählen Sie diese Option. Wenn die Option nicht aktiviert ist, können Sie das Volume nicht erweitern.  
  
        4.  Führen Sie die Schritteim Assistenten zum Erweitern von Volumes auf den Datenträger zu erweitern.  
  
    -   Löschen Sie Inhalte vom Volume, um mehr Speicherplatz verfügbar zu machen.  
  
        > [!NOTE]
        >  Wenn Sie auf das System reservierten Volume Speicherplatz freigeben müssen, können Sie das Systemwiederherstellungsabbild auf ein anderes Volume verschieben. Anweisungen finden Sie unter [bereitstellen ein Systemabbild-Wiederherstellung](https://technet.microsoft.com/library/dd744280\(v=ws.10\).aspx).  
  
    -   Schließen Sie das Volume aus der Clientsicherung aus. Vorgehensweise, wenn es nicht wichtig, dass Sie eine Sicherungskopie der Daten auf dem Volume zu verwalten.  
  
        > [!WARNING]
        >  Wenn Sie das System reservierte Volume aus einer Clientsicherung ausschließen, das Clientsystem nicht gesichert, und Sie werden nicht in der Lage, eine vollständige Systemwiederherstellung auf dem Computer durchführen.  
  
5.  Suchen Sie nach anderen Warnungen auf dem Server, der darauf hinweisen, dass es ist nicht genügend freier Speicherplatz auf dem Server für die Sicherung erfolgreich abgeschlossen. Führen Sie die Anweisungen in der Warnung, um das Problem zu beheben.  
  
6.  Führen Sie **Vssadmin** Probleme in einem Eingabeaufforderungsfenster Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) zu beheben. Informationen zu **Vssadmin**, finden Sie unter [VSSADMIN](https://go.microsoft.com/fwlink/?LinkID=94332).  
  
##  <a name="BKMK_TroubleshootBackupHealthAlertIssues"></a>Problembehandlung für sicherungsstatuswarnungen  
  
### <a name="errors"></a>Fehler  
  
-   Windows Server Solutions Computer Backup Provider Service funktioniert nicht  
  
-   Windows Server Solutions Client Computer Backup Provider Service funktioniert nicht  
  
### <a name="resolutions"></a>Auflösungen  
  
##### <a name="to-troubleshoot-a-backup-health-alert"></a>Um einer sicherungsstatuswarnung  
  
1.  Wenn eine Warnung besagt, dass die Sicherungsdatenbank Probleme aufweist, führen Sie die Anweisungen in der Warnung, um das Problem zu beheben.  
  
2.  Wenn eine Warnung besagt, dass ein Sicherungsdienst nicht ausgeführt wird, versuchen Sie, starten Sie den Dienst auf dem Server oder dem Clientcomputer, in dem Sie die Fehlermeldung erhalten haben.  
  
    ###### <a name="to-start-backup-services-on-the-server"></a>Starten Sie Sicherungsdienste auf dem Server  
  
    1.  Klicken Sie auf dem Server, auf **starten**, und klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
        > [!NOTE]
        >  Wenn Sie den Server remote verwalten, müssen Sie Remotedesktopverbindung verwenden, auf den Server-Desktop zugreifen. Informationen zum Verwenden der Remotedesktopverbindung finden Sie unter [Verbinden mit einem anderen Computer mithilfe der Remotedesktopverbindung](https://windows.microsoft.com/windows-vista/Connect-to-another-computer-using-Remote-Desktop-Connection).  
  
    2.  Führen Sie einen Bildlauf nach unten, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **gestartet**mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten**.  
  
    3.  Klicken Sie auf **Windows Server Client Computer Backup Service**. Wenn der Status des Diensts nicht **gestartet**mit der rechten Maustaste auf den Dienst, und klicken Sie dann auf **starten**.  
  
    4.  Schließen **Dienste**.  
  
    ###### <a name="to-start-backup-services-on-a-client-computer"></a>Starten Sie Sicherungsdienste auf einem Clientcomputer  
  
    1.  Klicken Sie auf dem Clientcomputer auf **starten**, Typ **Dienste** in der **Programme und Dateien suchen** Geben Sie im Textfeld, und klicken Sie dann auf.  
  
    2.  Mit der rechten Maustaste **Windows Server Client Computer Backup Provider Service**, und klicken Sie dann auf **starten**.  
  
    3.  Schließen der **Dienste**.  
  
3.  Überprüfen Sie die Ereignisprotokolle auf dem Clientcomputer oder Server auf Probleme im Zusammenhang, um Dienste oder Treiber zu sichern.  
  
4.  Neustart der Server oder Clientcomputer, in dem Sie die Fehlermeldung erhalten haben.  
  
5.  Überprüfen Sie Warnungen für andere Probleme, die sich auf die Clientsicherung können.  
  
##  <a name="BKMK_FileAndFolder"></a>Problembehandlung bei der Wiederherstellung einer Datei oder eines Ordners  
  
### <a name="errors"></a>Fehler  
  
-   Datei- oder ordnerwiederherstellung wurde nicht erfolgreich abgeschlossen.  
  
### <a name="resolutions"></a>Auflösungen  
  
##### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>Problembehandlung bei einer nicht erfolgreichen Datei- oder ordnerwiederherstellung  
  
1.  Stellen Sie sicher, dass Ihr Computer über ein Netzwerkgerät mit dem Netzwerk verbunden ist.  
  
2.  Stellen Sie sicher, dass das Netzwerkgerät, dem mit der Computer verbunden ist auch mit dem Netzwerk, eingeschaltet ist, verbunden ist und einwandfrei funktioniert.  
  
3.  Überprüfen Sie Warnungen, um zu bestimmen, ob der Fehler in der Sicherungsdatenbank vorliegen. Wenn Fehler vorhanden sind, führen Sie die Anweisungen in der Warnung, um die Sicherungsdatenbank reparieren.  
  
4.  Versuchen Sie, die Dateien oder Ordner aus einer anderen Sicherung wiederherzustellen.  
  
5.  Stellen Sie sicher, dass die **Windows Server Solution-Computerwiederherstellungstreiber** installiert ist und ordnungsgemäß funktioniert.  
  
    ###### <a name="to-check-the-status-of-the-windows-server-solution-computer-restore-driver"></a>So überprüfen Sie den Status der Windows Server Solution-Computerwiederherstellungstreiber  
  
    1.  Klicken Sie auf **starten**, Typ **Geräte-Manager** in der **Programme und Dateien suchen** Geben Sie im Textfeld, und klicken Sie dann auf.  
  
    2.  Klicken Sie im Geräte-Manager auf **Systemgeräte**, führen Sie einen Bildlauf **Windows Server Computerwiederherstellungstreiber**.  
  
    3.  Wenn der Treiber nicht angezeigt wird:  
  
        1.  Öffnen Sie eine Eingabeaufforderung mit Administratorrechten, und führen Sie den folgenden Befehl:  
  
             **%ProgramFiles%\Windows Server\Bin\BackupDriverInstaller.exe?  Ich**  
  
        2.  Aktualisieren Sie die Geräte-Manager. Der Treiber sollte angezeigt werden.  
  
    4.  Wenn das Symbol, das angezeigt wird, einem Computermonitor entspricht, ist der Treiber installiert ist und ausgeführt ordnungsgemäß. Geräte-Manager zu schließen.  
  
    5.  Wenn das angezeigte Symbol keinem Computermonitor entspricht  
  
        1.  Mit der rechten Maustaste **Windows Server Computerwiederherstellungstreiber**, und klicken Sie dann auf **Eigenschaften**.  
  
        2.  Klicken Sie auf die **Treiber** Registerkarte, und klicken Sie dann auf **Aktualisierungstreiber**.  
  
        3.  Klicken Sie auf **automatisch nach aktueller Treibersoftware suchen**, und folgen Sie dann die Anweisungen, um den Treiber zu aktualisieren.  
  
    6.  Geräte-Manager zu schließen.  
  
6.  Deinstallieren Sie die Windows Server Essentials Connector-Software auf dem Computer, und installieren Sie es erneut. Weitere Informationen finden Sie unter den Themen [deinstallieren die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [installieren Sie die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11).  
  
##  <a name="BKMK_Troubleshootfullsystemrestoreissues"></a>Problembehandlung bei einer vollständigen Systemwiederherstellung  
  
### <a name="errors"></a>Fehler  
  
-   Kann nicht nach einer vollständigen Systemwiederherstellung auf dem Clientcomputer melden.  
  
### <a name="resolutions"></a>Auflösungen  
 Wenn Sie den Namen eines Computers ändern, und Sie später eine Sicherung wiederherstellen, die gespeichert wurde, bevor Sie den Namen des Computers nach der Wiederherstellung geändert, wenn Sie versuchen, melden Sie sich bei Ihrem Domänenkonto anzumelden müssen, Sie dieser Fehler werden angezeigt: "die Sicherheitsdatenbank auf dem Server verfügt nicht über ein Computerkonto für diese Arbeitsstations-Vertrauensstellung." Um erneut Netzwerkzugriff auf den Computer zu erhalten, entfernen Sie die Connector-Software, entfernen Sie den Computer aus der Windows-Domäne und erneut mit dem Server verbinden.  
  
##### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>Erhalten Sie Zugriff auf das Netzwerk auf einen wiederhergestellten Computer nach einer Änderung der Computer namens  
  
1.  Melden Sie sich als lokaler Administrator auf dem Computer an.  
  
2.  Deinstallieren Sie die Connector-Software. Weitere Informationen finden Sie unter [deinstallieren die Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).  
  
3.  Entfernen Sie den Computer aus der Domäne. Weitere Informationen finden Sie unter [Entfernen eines Computers aus einer Windows-Domäne](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8).  
  
4.  Verbinden Sie den Computer erneut mit dem Server. Weitere Informationen finden Sie unter [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Unterstützung für Windows Server Essentials](Support-Windows-Server-Essentials.md)