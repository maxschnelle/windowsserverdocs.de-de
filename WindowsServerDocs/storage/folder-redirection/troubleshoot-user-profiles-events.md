---
title: Problembehandlung von Benutzerprofilen mithilfe von Ereignissen
description: Behandlung von Problemen beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablaufverfolgungsprotokolle.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6099dac7d77e37b761785b4f58b6106472e5ba1e
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082205"
---
# <a name="troubleshoot-user-profiles-with-events"></a>Problembehandlung von Benutzerprofilen mithilfe von Ereignissen

>Betrifft: 10 Windows, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2 und WindowsServer 2016.

In diesem Thema wird die Behandlung von Problemen beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablaufverfolgungsprotokolle. In den folgenden Abschnitten wird beschrieben, wie die drei Ereignisprotokolle verwenden können, die von Benutzerprofilinformationen aufzeichnen.

## <a name="step-1-checking-events-in-the-application-log"></a>Schritt 1: Überprüfen der Ereignisse im Anwendungsprotokoll protokolliert

Der erste Schritt beim Beheben von Problemen mit laden und entladen Benutzer, die Profile (einschließlich servergespeicherte Benutzerprofile) Ereignisanzeige verwenden, um alle Ereignisse Warn- und untersuchen, die Benutzerprofildienst-Datensätze in der Anwendung anmelden.

Sieht aus wie die Benutzerprofildienste Ereignisse im Anwendungsprotokoll anzeigen:

1. Starten Sie die Ereignisanzeige. Hierzu öffnen Sie **Systemsteuerung**zu, wählen Sie **System und Sicherheit**und wählen Sie dann im Abschnitt **Verwaltung** **Anzeigen von Ereignisprotokollen**. Das Fenster Ereignisanzeige wird geöffnet.
2. Navigieren Sie in der Konsolenstruktur zuerst zu **Windows-Protokolle**, klicken Sie dann die **Anwendung**.
3. Wählen Sie im Bereich Aktionen **Aktuelles Protokoll filtern**. Das Dialogfeld Aktuelles Protokoll filtern wird geöffnet.
4. Klicken Sie im Feld **Ereignisquellen** aktivieren Sie das Kontrollkästchen **User Profile Service** , und wählen Sie dann auf **OK**.
5. Überprüfen Sie das Angebot von Ereignissen, insbesondere Fehlerereignisse.
6. Wenn Sie erwähnenswerte Ereignisse gefunden haben, wählen Sie den Link Ereignisprotokoll Online-Hilfe, um zusätzliche Informationen und Verfahren zur Problembehandlung anzuzeigen.
7. Um eine zusätzliche Problembehandlung durchführen, beachten Sie Datum und Uhrzeit der erwähnenswerte Ereignisse und überprüfen Sie anschließend betriebliche Protokoll (wie in Schritt2 beschrieben) zum Anzeigen von Details zu den Benutzerprofildienst ungefähr zur Zeit der Fehlermeldung oder einer Warnung Ereignisse.

>[!NOTE]
>Sie können den Benutzerprofildienst ignorieren Ereignis 1530 "ermittelt Windows, dass Ihre Registrierungsdatei noch von anderen Anwendungen oder Dienste verwendet wird."

## <a name="step-2-view-the-operational-log-for-the-user-profile-service"></a>Schritt 2: Anzeigen des betrieblichen Protokolls für den Benutzerprofildienst

Wenn Sie das Problem mithilfe der im Anwendungsprotokoll allein nicht auflösen können, verwenden Sie das folgende Verfahren, um Benutzerprofildienst-Ereignisse im Protokoll betrieblichen anzuzeigen. Dieses Protokoll enthält einige der das Innenleben des Diensts, und helfen zu ermitteln, an welcher Stelle die Last Profil oder entladen Prozess, der das Problem auftritt.

Das Windows-Anwendungsprotokoll und das Protokoll User Profile Service betriebsbereit sind standardmäßig in allen Windows-Installationen aktiviert.

Sieht aus wie betriebliche Protokoll für den Benutzerprofildienst angezeigt:

1. In der Ereignisprozedur Viewer console Struktur, navigieren Sie zu **Anwendungs- und Dienstprotokolle**, und klicken Sie dann **Microsoft**, **Windows**, und klicken Sie dann **Benutzerprofildienst**und dann **operationale**.
2. Untersuchen Sie die Ereignisse, die etwa zur Zeit der Fehlermeldung oder einer Warnung Ereignisse aufgetreten sind, die Sie in das Anwendungsprotokoll notiert haben.

## <a name="step-3-enable-and-view-analytic-and-debug-logs"></a>Schritt 3: Aktivieren und anzeigen analytische und Debugprotokolle

Wenn ausführlicher als operative Protokoll bereitgestellt werden soll, können Sie aktivieren analytische und Debugprotokolle auf dem betreffenden Computer. Diese Stufe der Protokollierung ist viel schneller detaillierten und deaktiviert werden sollen, mit Ausnahme beim Versuch, ein Problem zu beheben.

So aktivieren und anzeigen analytische und Debugprotokolle funktioniert:

1. Klicken Sie im **Aktionsbereich** der Ereignisanzeige wählen Sie **Ansicht**, und wählen Sie dann **Anzeigen analytische und Debugprotokolle**aus.
2. Navigieren Sie zu **Anwendungs- und Dienstprotokolle**, und klicken Sie dann **Microsoft**, **Windows**, und klicken Sie dann **User Profile Service**und dann **Diagnostic**.
3. Wählen Sie **Protokoll aktivieren** , und wählen Sie dann auf **Ja**. Auf diese Weise können das Diagnoseprotokoll, das Protokollierung gestartet wird.
4. Wenn Sie noch weitere detaillierte Informationen benötigen, finden Sie unter [Schritt 4: Erstellen und eine Verfolgung Decodierung](#step-4:-creating-and-decoding-a-trace) für Weitere Informationen zum Erstellen eines Protokolls.
5. Wenn Sie die Problembehandlung abgeschlossen haben, navigieren Sie zu **der Diagnoseprotokoll** , aktivieren Sie **Protokoll deaktivieren**, wählen Sie **Ansicht** und deaktivieren Sie dann das Kontrollkästchen **Anzeigen analytische und Debugprotokolle** zum Ausblenden von analytischen und debug-Protokollierung.

## <a name="step-4-creating-and-decoding-a-trace"></a>Schritt 4: Erstellen und eine Verfolgung Decodierung

Wenn Sie das Problem mithilfe von Ereignissen nicht auflösen können, können Sie ein Ablaufverfolgungsprotokoll (ETL-Datei) erstellen, während das Problem zu reproduzieren, und klicken Sie dann mithilfe von Microsoft Symbolserver öffentlicher Symbole decodieren. Ablaufverfolgungsprotokolle bereitstellen sehr spezifische Informationen zu den Benutzerprofildienst wird wie folgt, und helfen zu ermitteln, in dem der Fehler aufgetreten ist.

Die beste Strategie bei Verwendung von ETL-Protokollierung wird zuerst das kleinste mögliche Protokoll erfasst. Nachdem das Protokoll decodiert wird, suchen Sie das Ereignisprotokoll auf Fehler.

Hier wird zum Erstellen und Decodieren einer Ablaufverfolgungs für den Benutzerprofildienst aus:

1. Melden Sie sich an dem Computer, auf dem der Benutzer Probleme auftreten ist, mit einem Konto, das Mitglied der lokalen Administratorgruppe ist.
2. Geben Sie die folgenden Befehle aus einer Eingabeaufforderung mit erhöhten Rechten, in dem *\ < p >* ist der Pfad in einen lokalen Ordner, die Sie zuvor erstellt haben, beispielsweise C:\\logs:
        
    ```PowerShell
    logman create trace -n RUP -o <Path>\RUP.etl -ets
    logman update RUP -p {eb7428f5-ab1f-4322-a4cc-1f1a9b2c5e98} 0x7FFFFFFF 0x7 -ets
    ```
3. Wählen Sie auf der Startseite den Benutzernamen ein, und wählen Sie **Konto Switch**, ohne dabei den Administrator abmelden. Bei Verwendung von Remotedesktop schließen Sie die Administrator-Sitzung, um die benutzersitzung herzustellen.
4. Das Problem zu reproduzieren. Das Verfahren, um das Problem zu reproduzieren ist in der Regel zum Anmelden als der Benutzer das Problem, den Benutzer abmelden, oder beides.
5. Nachdem das Problem zu reproduzieren, als lokaler Administrator erneut anmelden.
6. Führen Sie aus einer Eingabeaufforderung mit erhöhten Rechten aus den folgenden Befehl aus, um das Protokoll in einer ETL-Datei zu speichern:
  
    ```PowerShell
    logman stop -n RUP -ets
    ```
7. Geben Sie zum Exportieren der ETL-Datei in eine lesbare Datei im aktuellen Verzeichnis (wahrscheinlich Ihre Basisordner oder der Ordner %WINDIR%\\System32) den folgenden Befehl ein:
    
    ```PowerShell
    Tracerpt <path>\RUP.etl
    ```
8. Öffnen Sie die Datei **"Summary.txt"** und **Dumpfile.xml** -Datei (Sie können in Microsoft Excel so leichter die vollständige Details des Protokolls anzeigen diese öffnen). Suchen Sie nach den Ereignissen, die **ein Fehler auftritt** oder **Fehler bei**enthalten; Sie können Zeilen ignorieren, die die **Unbekannte** Ereignisname enthalten.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von servergespeicherten Benutzerprofilen](deploy-roaming-user-profiles.md)