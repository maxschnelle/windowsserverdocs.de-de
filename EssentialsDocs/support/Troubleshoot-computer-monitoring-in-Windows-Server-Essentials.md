---
title: Problembehandlung für das Überwachen der Computer in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 55daffa3c1db284d3772fa39eb64e0411ad1c7a6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625090"
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Problembehandlung für das Überwachen der Computer in Windows Server Essentials

> Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält Informationen zur Problembehandlung bei Problemen, die beim Überwachen des Integritäts Status von Computern in der Meldungs Anzeige und per e-Mail in Windows Server Essentials auftreten.

> [!NOTE]
> Die aktuellsten Informationen zur Problembehandlung aus der Windows Server Essentials-Community finden Sie im [Windows Server Essentials-Forum](/answers/topics/windows-server-essentials.html). Das Windows Server Essentials-Forum eignet sich optimal, um nach Hilfe zu suchen oder um Fragen zu stellen.

## <a name="troubleshooting-email-notifications-for-alerts"></a>Problembehandlung für E-Mail-Benachrichtigungen für Warnungen

 Dieser Abschnitt enthält verschiedene Probleme, die auftreten können, wenn Sie E-Mail-Benachrichtigungen für Warnungen verwenden.

### <a name="cannot-send-the-test-email-for-the-alert"></a>Die Test-Mail für die Warnung kann nicht gesendet werden.

 **Problem** Sie erhalten eine Fehlermeldung, die besagt, dass die Test-e-Mail für die Warnung nicht senden kann.

 **Ursache** Dieser Fehler kann aufgrund eines der folgenden Probleme in den Einstellungen für Benachrichtigungen auftreten:

- Ein falscher SMTP-Server-Name oder eine falsche Portnummer.

- Es wurde fälschlicherweise angegeben, dass für den SMTP-Server eine einzelne Sockets Layer (SSL)-Verbindung erforderlich ist.

- Für den SMTP-Server ist eine Authentifizierung erforderlich und es wurden falsche Anmeldeinformationen eingegeben .

  **Lösungen** Korrigieren Sie alle Fehler in den Einstellungen der E-Mail-Benachrichtigung.

#### <a name="to-identify-issues-in-your-email-notification-settings"></a>Ermitteln von Problemen in den Einstellungen der E-Mail-Benachrichtigung

- Bitten Sie Ihren Internetdienstanbieter (ISP) um den richtigen Namen des SMTP-Servers, die Portnummer und die SSL-Verwendung.

- Überprüfen Sie die Protokolldateien für E-Mail-Benachrichtigungen für die Warnung auf dem Server, an diesem Speicherort:

    ` %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log`

    > [!TIP]
    > Um den ProgramData-Ordner anzuzeigen, müssen Sie ausgeblendeten Elemente angezeigt werden. Wenn der Ordner ProgramData nicht angezeigt wird, wählen Sie auf der Registerkarte **Ansicht** des Menübands in der Gruppe **anzeigen/ausblenden** das Textfeld ausgeblendete **Elemente** aus.

#### <a name="to-update-your-email-notification-setup-for-alerts"></a>Aktualisieren Ihres E-Mail-Benachrichtigungssetups für Warnungen

1. Klicken Sie auf dem Dashboard auf ein beliebiges Warnungssymbol in der oberen rechten Ecke, um den Alert Viewer zu öffnen.

2. Klicken Sie am unteren Ende des Alert Viewers **E-Mail-Benachrichtigungen für Warnungen einrichten**.

3. Klicken Sie im Dialogfeld **E-Mail-Benachrichtigungen für Warnungen einrichten** auf **Aktivieren**.

4. aktualisieren Sie im Dialogfeld **SMTP-Einstellungen** die SMTP-Einstellungen und klicken Sie dann auf **OK**.

5. Klicken Sie zum Testen der aktualisierten Einstellungen auf **Anwenden und E-Mail senden**.

6. Nachdem Sie sich vergewissert haben, dass die Test-e-Mail erfolgreich war, klicken Sie auf **OK** zum Speichern der aktualisierten Einstellungen.

### <a name="test-email-notification-does-not-list-any-alerts"></a>Test-E-Mail-Benachrichtigungen listet keine Warnungen auf.

**Problem** Test-E-Mail-Benachrichtigungen für Warnungen zeigt keine Warnungen an, obwohl Warnungen im Alert Viewer angezeigt werden.

**Lösung** Nicht alle Warnungen, die im Alert Viewer angezeigt werden, generieren eine E-Mail-Benachrichtigung. Nur die Warnungen, die so konfiguriert sind, dass sie als eine E-Mail-Benachrichtigung innerhalb ihrer Definitionsdateien eskaliert werden, werden als e-Mail-Nachrichten an die angegebene E-Mail-Empfänger gesendet.

Beim Klicken auf **Anwenden und E-Mails enden**, erhalten Sie in der Regel eine Beispiel-E-Mail-Benachrichtigung ohne aufgelistete Status-Warnungen. Wenn eine Zustandswarnung, für die konfiguriert ist, dass E-Mail-Benachrichtigungen gesendet werden, während dieses Test-Prozesses identifiziert wird, wird die Warnung jedoch in der Test-E-Mail enthalten sein.

### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>Für eine deinstallierte Anwendung werden aktive Warnungen angezeigt.

**Problem** Aktive Warnungen für eine Anwendung werden angezeigt, auch wenn die Anwendung und deren Integritätsdefinitionsdatei deinstalliert wurden.

**Lösung** Sie müssen die aktiven Warnungen der deinstallierten Anwendung manuell löschen. Gehen Sie wie folgt vor, um eine Warnung zu löschen.

#### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>So löschen Sie eine Warnung vom Server mithilfe des Dashboards

1. Öffnen Sie vom Server aus das Dashboard.

2. Klicken Sie im Navigationsbereich auf ein beliebiges angezeigtes Warnsymbol (Kritisch, Warnung oder Information). Dadurch wird der Alert Viewer gestartet.

3. Rechtsklicken Sie im Alert Viewer auf die Warnung, die Sie löschen möchten, und klicken Sie dann auf **Diese Warnung löschen**.