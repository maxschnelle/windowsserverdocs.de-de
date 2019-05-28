---
title: Problembehandlung bei Benutzerprofilen mit Ereignissen
description: So beheben Sie Probleme beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablaufverfolgungsprotokolle.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f30bfcd531731e3a0d14350536ddf418c50f3ea0
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475949"
---
# <a name="troubleshoot-user-profiles-with-events"></a>Problembehandlung bei Benutzerprofilen mit Ereignissen

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012 und WindowsServer (halbjährlicher Kanal).

Dieses Thema beschreibt die Behandlung von Problemen beim Laden und Entladen von Benutzerprofilen, mithilfe von Ereignissen und Ablaufverfolgungsprotokolle. In den folgenden Abschnitten wird beschrieben, wie die drei Ereignisprotokolle zu verwenden, die Benutzerprofilinformationen zu zeichnen.

## <a name="step-1-checking-events-in-the-application-log"></a>Schritt 1: Überprüfen die Ereignisse in das Anwendungsprotokoll

Der erste Schritt bei der Problembehandlung mit laden und Entladen von Benutzer, die Profile (einschließlich der roaming-Benutzerprofile) ist zum Verwenden der Ereignisanzeige Warn- und Fehlerereignisse zu untersuchen, die Benutzerprofildienst Datensätze in der Anwendung anmelden.

Hier ist Benutzer Profildienste Ereignisse in das Anwendungsprotokoll anzeigen:

1. Starten der Ereignisanzeige. Zu diesem Zweck öffnen **Systemsteuerung**Option **System und Sicherheit**, und dann auf die **Verwaltung** wählen Sie im Abschnitt **Anzeigen von Ereignisprotokollen**. Die Ereignis-Viewer-Fenster wird geöffnet.
2. Wechseln Sie in der Konsolenstruktur zuerst zu **Windows-Protokolle**, klicken Sie dann **Anwendung**.
3. Wählen Sie im Aktionsbereich **Aktuelles Protokoll filtern**. Das Dialogfeld "Aktuelles Protokoll filtern" wird geöffnet.
4. In der **Ereignisquellen** Kontrollkästchen die **User Profile Service** Kontrollkästchen, und wählen Sie dann **OK**.
5. Überprüfen Sie die Liste der Ereignisse, achten Sie insbesondere auf Fehlerereignisse.
6. Wenn Sie wichtige Ereignisse gefunden haben, wählen Sie die Onlinehilfe-Link, um weitere Informationen und Verfahren zur Problembehandlung anzuzeigen.
7. Um weitere Informationen zur Problembehandlung auszuführen, beachten Sie das Datum und die Uhrzeit der wichtigsten Ereignisse aus, und untersuchen Sie dann das Betriebsprotokoll (wie in Schritt2 beschrieben) zum Anzeigen von Informationen, was den Benutzerprofildienst ungefähr zum Zeitpunkt der Fehler oder Warnung Ereignisse machte.

>[!NOTE]
>Sie können Benutzerprofildienst ignorieren-Ereignis 1530 "ermittelt Windows, dass Ihre Registrierungsdatei noch von anderen Anwendungen oder Diensten verwendet wird."

## <a name="step-2-view-the-operational-log-for-the-user-profile-service"></a>Schritt 2: Anzeigen des Betriebsprotokolls für den Benutzerprofildienst

Wenn Sie das Problem mit dem Anwendungsprotokoll allein nicht beheben können, verwenden Sie das folgende Verfahren Benutzerprofildienst Ereignisse im Betriebsprotokoll anzeigen. Dieses Protokoll zeigt einige der die interne Funktionsweise des Diensts, und es kann helfen, wo die Profil-Last zu ermitteln oder entladen Prozess, der das Problem auftritt.

Sowohl das Windows-Anwendungsprotokoll als auch das User Profile Service Betriebsprotokoll werden standardmäßig in allen Windows-Installationen aktiviert.

Hier ist das Betriebsprotokoll für den Benutzerprofildienst anzeigen:

1. Wechseln Sie in der Konsolenstruktur der Ereignisanzeige zu **Anwendungs- und Dienstprotokolle**, klicken Sie dann **Microsoft**, klicken Sie dann **Windows**, klicken Sie dann **Benutzerprofildienst**, und klicken Sie dann **Operational**.
2. Überprüfen Sie die Ereignisse, die ungefähr zum Zeitpunkt der Fehler oder Warnung Ereignisse aufgetreten sind, die Sie in das Anwendungsprotokoll notiert haben.

## <a name="step-3-enable-and-view-analytic-and-debug-logs"></a>Schritt 3: Aktivieren und Anzeigen von analytische und Debugprotokolle

Wenn Sie mehr Details benötigen als das Betriebsprotokoll bietet, können Sie aktivieren analytische und Debugprotokolle, auf dem betroffenen Computer. Diese Stufe der Protokollierung finden Sie weitaus und sollte deaktiviert werden, mit Ausnahme beim Versuch, ein Problem zu beheben.

So wird zum Aktivieren und Anzeigen von analytische und Debugprotokolle:

1. In der **Aktionen** Bereich der Ereignisanzeige, wählen Sie **Ansicht**, und wählen Sie dann **analytische und Debugprotokolle**.
2. Navigieren Sie zu **Anwendungs- und Dienstprotokolle**, klicken Sie dann **Microsoft**, klicken Sie dann **Windows**, klicken Sie dann **Benutzerprofildienst**, und klicken Sie dann  **Diagnose**.
3. Wählen Sie **Protokoll aktivieren** und wählen Sie dann **Ja**. Dies ermöglicht das Diagnoseprotokoll, das Protokollierung gestartet wird.
4. Wenn Sie das noch ausführlichere Informationen benötigen, finden Sie unter [Schritt 4: Erstellen und beim Decodieren einer Ablaufverfolgungs](#step-4-creating-and-decoding-a-trace) für Weitere Informationen dazu, wie Sie ein Ablaufverfolgungsprotokoll zu erstellen.
5. Wenn Sie das Problem behoben haben, navigieren Sie zu der **diagnostische** wählen **Protokoll deaktivieren**, wählen **Ansicht** und deaktivieren Sie dann die **anzeigen Analytische und Debugprotokolle** Kontrollkästchen, um analytische ausblenden und die Debugprotokollierung.

## <a name="step-4-creating-and-decoding-a-trace"></a>Schritt 4: Erstellen und beim Decodieren einer Ablaufverfolgungs

Wenn Sie das Problem mithilfe von Ereignissen nicht beheben können, können Sie ein Ablaufverfolgungsprotokoll (ETL-Datei) beim Reproduzieren des Problems zu erstellen und später zu entschlüsseln, die mithilfe öffentlicher Symbole vom Symbolserver von Microsoft. Netzwerkablaufverfolgungs-Protokolle bieten sehr spezielle Informationen, was den Benutzerprofildienst macht, und können ermitteln, wo der Fehler aufgetreten ist.

Die beste Strategie, bei Verwendung von ETL-Ablaufverfolgung werden zuerst die kleinste Protokolldateigröße möglich zu erfassen. Wenn das Protokoll decodiert wird, suchen Sie, Fehler im Protokoll.

Hier ist das Erstellen und zu decodieren eine Ablaufverfolgung für den Benutzerprofildienst:

1. Melden Sie sich bei dem Computer, in denen der Benutzer Probleme aufgetreten sind ist, mit einem Konto an, die ein Mitglied der lokalen Administratorgruppe ist.
2. Geben Sie eine Eingabeaufforderung mit erhöhten Rechten die folgenden Befehle aus, wobei *\<Pfad\>* ist der Pfad zu einem lokalen Ordner, den Sie zuvor erstellt haben, z. B. "c:"\\Protokolle:
        
    ```PowerShell
    logman create trace -n RUP -o <Path>\RUP.etl -ets
    logman update RUP -p {eb7428f5-ab1f-4322-a4cc-1f1a9b2c5e98} 0x7FFFFFFF 0x7 -ets
    ```
3. Über die Startseite, wählen Sie den Benutzernamen ein, und wählen Sie dann **Konto wechseln**, ohne dabei Abmelden an den Administrator. Wenn Sie Remotedesktop verwenden, schließen Sie die Administrator-Sitzung, um die benutzersitzung herzustellen.
4. Das Problem zu reproduzieren. Das Verfahren zum Reproduzieren des Problems ist in der Regel für die Anmeldung bei als für den Benutzer das Problem, das Anmelden des Benutzers aus, oder beides verwendet werden.
5. Melden Sie nachdem das Problem zu reproduzieren als lokaler Administrator erneut an.
6. Führen Sie eine Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus, um das Protokoll in einer ETL-Datei zu speichern:
  
    ```PowerShell
    logman stop -n RUP -ets
    ```
7. Geben Sie den folgenden Befehl zum Exportieren der ETL-Datei in eine lesbare-Datei im aktuellen Verzeichnis (wahrscheinlich in Ihrem Basisordner oder der %windir%\\Ordner "System32"):
    
    ```PowerShell
    Tracerpt <path>\RUP.etl
    ```
8. Öffnen Sie die **Summary.txt** Datei und **"dumpfile.xml"** Datei (Sie können öffnen sie in Microsoft Excel verwenden, um die vollständigen Details des Protokolls leichter anzeigen). Suchen Sie nach Ereignissen, die **fehlschlagen** oder **Fehler**; können Sie ignorieren Zeilen, die enthalten die **unbekannte** Ereignisnamen.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)