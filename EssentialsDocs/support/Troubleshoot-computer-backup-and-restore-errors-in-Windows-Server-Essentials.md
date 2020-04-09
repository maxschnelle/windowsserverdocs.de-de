---
title: Problembehebung bei Computersicherungs- und Wiederherstellungsfehlern in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 06/25/2013
ms.prod: windows-server
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 542c0a583aca56ce72ef0e2e55f2b1543558dfa8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852183"
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>Problembehebung bei Computersicherungs- und Wiederherstellungsfehlern in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Verwenden Sie diese Verfahren für die Problembehandlung von Computersicherungen in Windows Server Essentials, einschließlich Sicherungskonfigurationsproblemen, unvollständige oder nicht erfolgreiche Sicherungen, Sicherungsstatuswarnungen und Probleme mit Datei-, Ordner- oder vollständigen Systemwiederherstellungen.  
  
> [!NOTE]
>  Die neuesten Informationen zur Problembehandlung aus der Windows Server Essentials-Community finden Sie im [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums//winserveressentials/threads).  
  
##  <a name="troubleshoot-backup-configuration-issues-for-a-connected-computer"></a><a name="BKMK_TroubleshootBackupConfigurationIssues"></a>Beheben von Problemen mit der Sicherungs Konfiguration für einen verbundenen Computer  
 Verwenden Sie diese Verfahren zum Beheben von Problemen mit Sicherungskonfigurationen für Computer, die auf dem Windows Server Essentials-Server gesichert werden.  
  
### <a name="errors"></a>Fehler  
  
-   Sicherungskonfiguration wurde nicht erfolgreich abgeschlossen  
  
-   Fehler beim Erfassen von Informationen für Computer  
  
-   Fehler beim Entfernen des Computers aus der Sicherung  
  
### <a name="resolutions"></a>Lösungen  
  
##### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>So beheben Sie Fehler, die beim Konfigurieren von Sicherungen für einen verbundenen Computer auftreten  
  
1.  Stellen Sie sicher, dass der Computer über ein Netzwerkgerät mit dem Netzwerk verbunden ist.  
  
2.  Stellen Sie sicher, dass das Netzwerkgerät, mit dem der Computer verbunden ist, auch mit dem Netzwerk verbunden und eingeschaltet ist sowie einwandfrei funktioniert.  
  
3.  Stellen Sie sicher, dass "Windows Server Client Backup Service" und "Windows Server Client Computer Backup Provider Service" auf dem Server ausgeführt werden.  
  
    ###### <a name="to-start-computer-backup-services-on-the-server"></a>So starten Sie Computersicherungsdienste auf dem Server  
  
    1.  Klicken Sie auf dem Server, auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
    2.  Führen Sie einen Bildlauf nach unten aus, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **Gestartet** lautet, klicken Sie mit der rechten Maustaste auf den Dienst. Klicken Sie dann auf **Starten**.  
  
    3.  Klicken Sie auf **Windows Server Client Computer Backup Service**. Wenn der Status des Diensts nicht **Gestartet** lautet, klicken Sie mit der rechten Maustaste auf den Dienst. Klicken Sie dann auf **Starten**.  
  
    4.  Schließen Sie **Dienste**.  
  
4.  Stellen Sie sicher, dass "Windows Server Client Computer Backup Provider Service" auf dem Clientcomputer ausgeführt wird.  
  
    ###### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>So starten Sie den Computersicherungsdienst auf dem Clientcomputer  
  
    1.  Klicken Sie auf dem Clientcomputer auf **Start**, geben Sie **Dienste** in das Textfeld **Programme und Dateien suchen** ein, und drücken Sie dann die EINGABETASTE.  
  
    2.  Führen Sie einen Bildlauf nach unten aus, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **Gestartet** lautet, klicken Sie mit der rechten Maustaste auf den Dienst. Klicken Sie dann auf **Starten**.  
  
    3.  Schließen Sie **Dienste**.  
  
5.  Überprüfen Sie die Warnungen, um festzustellen, ob Fehler in der Sicherungsdatenbank vorliegen. Wenn Fehler vorhanden sind, folgen Sie den Anweisungen in der Warnung, um die Sicherungsdatenbank zu reparieren.  
  
6.  Deinstallieren Sie die Windows Server Essentials Connector-Software von dem Computer und installieren Sie sie neu. Weitere Informationen finden Sie in den Themen [Deinstallieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [Installieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11).  
  
##  <a name="troubleshoot-a-backup-that-did-not-complete-properly"></a><a name="BKMK_TroubleshootaBackupThatDidNotCompleteProperly"></a>Behandeln von Problemen mit einer Sicherung, die nicht ordnungsgemäß ausgeführt wurde  
 Wenn eine Sicherung nicht erfolgreich war, war kein Teil der Sicherung erfolgreich und es sind keine Daten für die Wiederherstellung verfügbar. Wenn eine Sicherung unvollständig ist, wurden nicht alle in der Sicherungskonfiguration angegebenen Elemente gesichert. Einige Daten können aber wiederherstellbar sein.  
  
### <a name="errors"></a>Fehler  
  
-   Sicherung ist unvollständig  
  
-   Sicherung nicht erfolgreich  
  
### <a name="resolutions"></a>Lösungen  
  
##### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>So identifizieren Sie Volumes, die nicht ordnungsgemäß gesichert wurden  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard, und klicken Sie dann auf **Computer und Sicherung**.  
  
2.  Klicken Sie auf den Namen des Computers, auf dem die Sicherung nicht erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Computereigenschaften anzeigen** im Bereich **Aufgaben**.  
  
3.  Klicken Sie auf die Sicherung, die nicht erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Details anzeigen**.  
  
4.  Im Dialogfeld **Sicherungsdetails** wird ein grünes Häkchen für den Status jedes Volumes angezeigt, das gesichert wurde.  
  
##### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>So beheben Sie ein Problem mit einer nicht erfolgreichen Sicherung eines Volumes  
  
1.  Stellen Sie sicher, dass die Festplatte mit dem Computer verbunden und eingeschaltet ist sowie einwandfrei funktioniert.  
  
2.  Führen Sie **chkdsk /f /r** aus, um alle Fehler auf der Festplatte zu beheben ( **/f**) und lesbare Informationen in fehlerhaften Sektoren wiederherzustellen ( **/r**). Weitere Informationen zum Ausführen von **chkdsk**finden Sie unter [CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562).  
  
3.  Stellen Sie sicher, dass der Computer nicht heruntergefahren oder vom Netzwerk getrennt wurde, während die Sicherung ausgeführt wurde.  
  
4.  Stellen Sie sicher, dass ausreichend freier Speicherplatz auf jedem Volume zum Ausführen der Sicherung vorhanden ist. Die Sicherung erfordert zusätzlichen Speicherplatz auf dem Clientcomputer, um einen VSS-Snapshot zu erstellen. Auf Volumes, die nicht für das System reserviert ist, muss mindestens 10 Prozent verfügbarer Speicherplatz frei sein. Wenn die Größe des Volumes auf einem für das System reservierten Volume kleiner als 500 MB ist, erfordert VSS 32 MB freien Speicherplatz zum Erstellen eines Snapshots. Ist das Volume 500 MB oder größer, erfordert VSS 320 MB freien Speicherplatz.  
  
     Wenn nicht genügend freier Speicherplatz auf einem Volume verfügbar ist, führen Sie eine dieser Lösungen durch:  
  
    -   Erweitern Sie das Volume. Sie können grundlegende oder dynamische Volumes mit Ausnahme des für das System reservierten Volumes erweitern.  
  
        ###### <a name="to-extend-a-volume"></a>So erweitern Sie in Volume  
  
        1.  Klicken Sie in der Systemsteuerung auf **System und Sicherheit**.  
  
        2.  Klicken Sie unter **Verwaltung** auf **Festplattenpartitionen erstellen und formatieren**.  
  
        3.  Klicken Sie mit der rechten Maustaste auf das Volume, das Sie erweitern möchten. Wenn **Volume erweitern** aktiviert ist, wählen Sie diese Option aus. Wenn die Option nicht aktiviert ist, können Sie das Volume nicht erweitern.  
  
        4.  Führen Sie die Schritte im Assistenten zum Erweitern von Volumes aus, um den Datenträger zu erweitern.  
  
    -   Löschen Sie Inhalte vom Volume, um mehr Speicherplatz verfügbar zu machen.  
  
        > [!NOTE]
        >  Wenn Sie auf dem für das System reservierten Volume Speicherplatz freigeben müssen, können Sie das Systemwiederherstellungsabbild auf ein anderes Volume verschieben. Anweisungen finden Sie unter [Bereitstellen eines Abbilds für die Systemwiederherstellung](https://technet.microsoft.com/library/dd744280\(v=ws.10\).aspx).  
  
    -   Schließen Sie das Volume aus der Clientsicherung aus. Führen Sie diesen Schritt nur durch, wenn es wichtig ist, eine Sicherungskopie der Daten auf dem Volume zu behalten.  
  
        > [!WARNING]
        >  Wenn Sie das für das System reservierte Volume aus einer Clientsicherung ausschließen, wird das Clientsystem nicht gesichert, und Sie sind nicht in der Lage, eine vollständige Systemwiederherstellung auf dem Computer auszuführen.  
  
5.  Überprüfen Sie andere Warnungen auf dem Server, die u. U. darauf hindeuten, dass nicht genügend freier Speicherplatz auf dem Server für den erfolgreichen Abschluss der Sicherung vorhanden ist. Folgen Sie den Anweisungen in der Warnung, um das Problem zu beheben.  
  
6.  Führen Sie **vssadmin** an einer Eingabeaufforderung aus, um Probleme mit VSS (Volume Shadow Copy Service) zu beheben. Informationen zu **vssadmin**finden Sie unter [VSSADMIN](https://go.microsoft.com/fwlink/?LinkID=94332).  
  
##  <a name="troubleshoot-backup-health-alert-issues"></a><a name="BKMK_TroubleshootBackupHealthAlertIssues"></a>Beheben von Problemen mit der Sicherungs Integritäts Warnung  
  
### <a name="errors"></a>Fehler  
  
-   Der Windows Server Solutions Computer Backup Provider-Dienst funktioniert nicht mehr  
  
-   Der Windows Server Solutions Client Computer Backup Provider-Dienst funktioniert nicht mehr  
  
### <a name="resolutions"></a>Lösungen  
  
##### <a name="to-troubleshoot-a-backup-health-alert"></a>So beheben Sie ein Problem mit einer Sicherungsstatuswarnung  
  
1.  Wenn eine Warnung besagt, dass die Sicherungsdatenbank Probleme aufweist, folgen Sie die Anweisungen in der Warnung, um das Problem zu beheben.  
  
2.  Wenn eine Warnung besagt, dass ein Sicherungsdienst nicht ausgeführt wird, versuchen Sie, den Dienst auf dem Server- oder Clientcomputer zu starten, auf dem Sie die Fehlermeldung erhalten haben.  
  
    ###### <a name="to-start-backup-services-on-the-server"></a>So starten Sie Sicherungsdienste auf dem Server  
  
    1.  Klicken Sie auf dem Server auf **Start**, klicken Sie auf **Verwaltung** und dann auf **Dienste**.  
  
        > [!NOTE]
        >  Wenn Sie den Server remote verwalten, müssen Sie die Remotedesktopverbindung verwenden, um auf den Serverdesktop zuzugreifen. Informationen zum Verwenden der Remotedesktopverbindung finden Sie unter [Herstellen einer Verbindung mit einem anderen Computer mithilfe der Remotedesktopverbindung](https://windows.microsoft.com/windows-vista/Connect-to-another-computer-using-Remote-Desktop-Connection).  
  
    2.  Führen Sie einen Bildlauf nach unten aus, und klicken Sie auf **Windows Server Client Computer Backup Provider Service**. Wenn der Status des Diensts nicht **Gestartet** lautet, klicken Sie mit der rechten Maustaste auf den Dienst. Klicken Sie dann auf **Starten**.  
  
    3.  Klicken Sie auf **Windows Server Client Computer Backup Service**. Wenn der Status des Diensts nicht **Gestartet** lautet, klicken Sie mit der rechten Maustaste auf den Dienst. Klicken Sie dann auf **Starten**.  
  
    4.  Schließen Sie **Dienste**.  
  
    ###### <a name="to-start-backup-services-on-a-client-computer"></a>So starten Sie Sicherungsdienste auf einem Clientcomputer  
  
    1.  Klicken Sie auf dem Clientcomputer auf **Start**, geben Sie **Dienste** in das Textfeld **Programme und Dateien suchen** ein, und drücken Sie dann die EINGABETASTE.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Windows Server Client Computer Backup Provider Service**. Klicken Sie dann auf **Starten**.  
  
    3.  Schließen Sie **Dienste**.  
  
3.  Überprüfen Sie die Ereignisprotokolle auf dem Clientcomputer oder Server auf Probleme im Zusammenhang mit Sicherungsdiensten oder Treibern.  
  
4.  Starten Sie den Server- oder Clientcomputer neu, auf dem Sie die Fehlermeldung erhalten haben.  
  
5.  Überprüfen Sie Statuswarnungen für andere Probleme, die sich auf die Clientsicherung auswirken können.  
  
##  <a name="troubleshoot-a-file-or-folder-restore"></a><a name="BKMK_FileAndFolder"></a>Problembehandlung bei einer Datei-oder Ordner Wiederherstellung  
  
### <a name="errors"></a>Fehler  
  
-   Datei- oder Ordnerwiederherstellung wurde nicht erfolgreich abgeschlossen.  
  
### <a name="resolutions"></a>Lösungen  
  
##### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>So beheben Sie ein Problem mit einer nicht erfolgreichen Datei- oder Ordnerwiederherstellung  
  
1.  Stellen Sie sicher, dass der Computer über ein Netzwerkgerät mit dem Netzwerk verbunden ist.  
  
2.  Stellen Sie sicher, dass das Netzwerkgerät, mit dem der Computer verbunden ist, auch mit dem Netzwerk verbunden und eingeschaltet ist sowie einwandfrei funktioniert.  
  
3.  Überprüfen Sie die Warnungen, um festzustellen, ob Fehler in der Sicherungsdatenbank vorliegen. Wenn Fehler vorhanden sind, folgen Sie den Anweisungen in der Warnung, um die Sicherungsdatenbank zu reparieren.  
  
4.  Versuchen Sie, die Dateien oder Ordner aus einer anderen Sicherung wiederherzustellen.  
  
5.  Stellen Sie sicher, dass der **Windows Server Solution-Computerwiederherstellungstreiber** installiert ist und ordnungsgemäß funktioniert.  
  
    ###### <a name="to-check-the-status-of-the-windows-server-solution-computer-restore-driver"></a>So überprüfen Sie den Status des Windows Server Solution-Computerwiederherstellungstreibers  
  
    1.  Klicken Sie auf **Start**, geben Sie **Geräte-Manager** in das Textfeld **Programme und Dateien suchen** ein, und drücken Sie dann die EINGABETASTE.  
  
    2.  Klicken Sie im Geräte-Manager auf **Systemgeräte**, führen Sie einen Bildlauf zu **Windows Server Solution-Computerwiederherstellungstreiber** durch.  
  
    3.  Wenn der Treiber nicht angezeigt wird:  
  
        1.  Öffnen Sie eine Eingabeaufforderung mit Administratorrechten, und führen Sie den folgenden Befehl aus:  
  
             **%ProgramFiles%\Windows server\bin\backupdriverinstaller.exe? -i**  
  
        2.  Aktualisieren Sie den Geräte-Manager. Der Treiber sollte angezeigt werden.  
  
    4.  Falls das Symbol, das angezeigt wird, einem Computermonitor entspricht, ist der Treiber installiert und funktioniert ordnungsgemäß. Schließen Sie den Geräte-Manager.  
  
    5.  Wenn das Symbol, das angezeigt wird, keinem Computermonitor entspricht  
  
        1.  Klicken Sie mit der rechten Maustaste  auf **Windows Server Solution-Computerwiederherstellungstreiber**, und klicken Sie dann auf **Eigenschaften**.  
  
        2.  Klicken Sie auf die Registerkarte **Treiber** und dann auf **Treiber aktualisieren**.  
  
        3.  Klicken Sie auf **Automatisch nach aktueller Treibersoftware suchen**, und folgen Sie dann die Anweisungen, um den Treiber zu aktualisieren.  
  
    6.  Schließen Sie den Geräte-Manager.  
  
6.  Deinstallieren Sie die Windows Server Essentials Connector-Software von dem Computer und installieren Sie sie neu. Weitere Informationen finden Sie in den Themen [Deinstallieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) und [Installieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11).  
  
##  <a name="troubleshoot-a-full-system-restore"></a><a name="BKMK_Troubleshootfullsystemrestoreissues"></a>Problembehandlung bei einer vollständigen Systemwiederherstellung  
  
### <a name="errors"></a>Fehler  
  
-   Nach einer vollständigen Systemwiederherstellung ist die Anmeldung am Clientcomputer nicht möglich.  
  
### <a name="resolutions"></a>Lösungen  
 Wenn Sie den Namen eines Computers ändern und später eine Sicherung wiederherstellen müssen, die vor dem Ändern des Computernamens gespeichert wurde, und dann nach der Wiederherstellung versuchen, sich mit Ihrem Domänenkonto anzumelden, erhalten Sie einen Fehler wie diesen: "Die Sicherheitsdatenbank auf dem Server hat kein Computerkonto für diese Arbeitsstations-Vertrauensstellung." Um erneut Netzwerkzugriff auf den Computer zu erhalten, entfernen Sie die Connector-Software, entfernen Sie den Computer aus der Windows-Domäne, und stellen Sie dann erneut eine Verbindung zum Server her.  
  
##### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>So erhalten Sie wieder Netzwerkzugriff auf einen wiederhergestellten Computer nach einer Computernamensänderung  
  
1.  Melden Sie sich als lokaler Administrator an dem Computer an.  
  
2.  Deinstallieren Sie die Connector-Software. Weitere Informationen finden Sie unter [Deinstallieren der Connector-Software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).  
  
3.  Entfernen Sie den Computer aus der Domäne. Weitere Informationen finden Sie unter [Entfernen eines Computers aus einer Windows-Domäne](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8).  
  
4.  Verbinden Sie den Computer erneut mit dem Server. Weitere Informationen finden Sie unter [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Unterstützung von Windows Server Essentials](Support-Windows-Server-Essentials.md)