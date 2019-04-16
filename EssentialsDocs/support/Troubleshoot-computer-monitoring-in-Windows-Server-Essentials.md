---
title: "Problembehandlung beim Überwachen der Computer in Windows Server Essentials"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 72fe309e0e7ce6d7227cce8b7f2c5dbf018eb4a1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Problembehandlung beim Überwachen der Computer in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Thema enthält Informationen zur Problembehandlung von Problemen, die während der Überwachung des Integritätsstatus von Computern in der Meldungsanzeige und über E-Mail-Benachrichtigungen in Windows Server Essentials.  
  
> [!NOTE]
>  Aktuelle Informationen zur Problembehandlung aus der Windows Server Essentials-Community, empfehlen wir, Sie besuchen die [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums/winserveressentials/threads). Die Windows Server Essentials-Forum ist ein idealer Ausgangspunkt, um nach Hilfe suchen oder eine Frage stellen.  
  
##  <a name="BKMK_TS"></a>Problembehandlung für E-Mail-Benachrichtigungen für Warnungen  
 Dieser Abschnittenthält verschiedene Probleme, die auftreten können, wenn E-Mail-Benachrichtigungen für Warnungen verwenden.  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>Der-e-Testmail für die Warnung kann nicht gesendet werden.  
 **Problem** erhalten Sie eine Fehlermeldung angezeigt, die besagt, kann nicht für Warnung die Test-Mail senden.  
  
 **Ursache** dieser Fehler kann aufgrund eines der folgenden Probleme in den Einstellungen für Benachrichtigungen auftreten:  
  
-   Ein falscher SMTP-Servername oder die Portnummer an.  
  
-   Es wurde fälschlicherweise angegeben, dass der SMTP-Server eine einzelne Sockets Layer (SSL)-Verbindung erforderlich ist.  
  
-   Der SMTP-Server erfordert Authentifizierung und wurden falsche Anmeldeinformationen eingegeben.  
  
 **Lösungen** korrigieren Sie Fehler in den Einstellungen der E-Mail-Benachrichtigung.  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>Identifizieren von Problemen in den Einstellungen der E-Mail-Benachrichtigung  
  
-   Bitten Sie Ihr Internetdienstanbieter (ISP) für die richtige SMTP-Servername, Portnummer und SSL-Verwendung.  
  
-   Überprüfen Sie die Protokolldateien für E-Mail-Benachrichtigungen für die Warnung auf dem Server an diesem Speicherort:  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  Um den ProgramData-Ordner angezeigt wird, müssen Sie ausgeblendeten Elemente angezeigt werden. Wenn vergessen finden Sie unter der ProgramData-Ordner auf dem Menüband s **Ansicht** Registerkarte die **einblenden/ausblenden** Gruppe, und wählen die **ausgeblendete Elemente** Textfeld.  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>Aktualisieren Sie Ihre E-Mail-benachrichtigungssetups für Warnungen  
  
1.  Klicken Sie auf dem Dashboard auf beliebiges Warnungssymbol in der oberen rechten Ecke, um die Meldungsanzeige zu öffnen.  
  
2.  Klicken Sie am Ende des Alert Viewers auf **E-Mail-Benachrichtigungen für Warnungen einrichten**.  
  
3.  In der **E-Mail-Benachrichtigungen für Warnungen einrichten** Dialogfeld, klicken Sie auf **aktivieren**.  
  
4.  In der **SMTP-Einstellungen** Dialogfeld aktualisieren Sie die SMTP-Einstellungen, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie zum Testen der aktualisierten Einstellungen **anwenden und E-Mail senden**.  
  
6.  Vergewissern Sie sich, dass die-e-Testmail erfolgreich war, klicken Sie auf **OK** zum Speichern der aktualisierten Einstellungen.  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>Test-E-Mail-Benachrichtigung wird keine Warnungen aufgeführt.  
 **Problem** Test-E-Mail-Benachrichtigungen für Warnungen zeigt keine Warnungen, auch wenn es in der Meldungsanzeige aufgeführten Warnungen.  
  
 **Lösung** nicht alle Warnungen, die in der Meldungsanzeige gemeldet werden, generieren eine E-Mail-Benachrichtigung. Nur die Warnungen, die als eine E-Mail-Benachrichtigung innerhalb ihrer Definitionsdateien eskaliert werden konfiguriert sind, werden als E-Mail-Nachrichten an die angegebene E-Mail-Empfänger gesendet.  
  
 Beim Klicken auf **anwenden und e-Mail senden**, in der Regel eine Beispiel für die e-Mail-Benachrichtigung mit ohne aufgelisteten Status-Warnungen erhalten. Wenn eine integritätswarnung auftritt, die zum Senden von E-Mail-Benachrichtigungen konfiguriert ist, während dieses Test-Prozesses identifiziert wird, wird die Warnung jedoch in der-e-Testmail enthalten.  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>Für eine deinstallierte Anwendung werden aktive Warnungen angezeigt.  
 **Problem** aktive Warnungen für eine Anwendung werden angezeigt, auch wenn die Anwendung und deren integritätsdefinitionsdatei deinstalliert wurden.  
  
 **Lösung** müssen Sie die aktiven Warnungen der deinstallierten Anwendung manuell löschen. Führen Sie folgende Schritteaus, um eine Warnung zu löschen.  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>So löschen Sie eine Warnung vom Server mithilfe des Dashboards  
  
1.  Öffnen Sie das Dashboard vom Server.  
  
2.  Klicken Sie im Navigationsbereich auf beliebiges angezeigtes Warnsymbol (kritisch, Warnung oder Information). Dadurch wird der Alert Viewer gestartet.  
  
3.  In der Meldungsanzeige mit der Maustaste der Warnung, die Sie löschen möchten, und klicken Sie dann auf **diese Warnung löschen**.
