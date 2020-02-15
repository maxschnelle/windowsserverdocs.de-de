---
title: Problembehandlung von Benutzerprofilen mit Ereignissen
description: Behandeln von Problemen beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablaufverfolgungsprotokollen.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e927a77627e786015a928d798aafee13a2cc34b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394378"
---
# <a name="troubleshoot-user-profiles-with-events"></a>Problembehandlung von Benutzerprofilen mit Ereignissen

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server (halbjährlicher Kanal).

In diesem Thema wird beschrieben, wie Probleme beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablaufverfolgungsprotokollen behandelt werden. In den folgenden Abschnitten wird beschrieben, wie die drei Ereignisprotokolle verwendet werden, die Benutzerprofilinformationen aufzeichnen.

## <a name="step-1-checking-events-in-the-application-log"></a>Schritt 1: Überprüfen von Ereignissen im Anwendungsprotokoll

Der erste Schritt bei der Behebung von Problemen beim Laden und Entladen von Benutzerprofilen (einschließlich Roamingbenutzerprofilen) ist die Verwendung der Ereignisanzeige, um Warn- und Fehlerereignisse zu untersuchen, die vom Benutzerprofildienst im Anwendungsprotokoll aufgezeichnet werden.

So zeigen Sie Ereignisse der Benutzerprofildienste im Anwendungsprotokoll an:

1. Starten Sie die Ereignisanzeige. Öffnen Sie hierzu **Systemsteuerung**, wählen Sie **System und Sicherheit** aus, und wählen Sie dann im Abschnitt **Verwaltungstools** die Option **Ereignisprotokolle anzeigen** aus. Das Fenster der Ereignisanzeige wird geöffnet.
2. Navigieren Sie in der Konsolenstruktur zuerst zu **Windows-Protokolle** und dann zu **Anwendung**.
3. Wählen Sie im Bereich „Aktionen“ die Option **Aktuelles Protokoll filtern** aus. Das Dialogfeld „Aktuelles Protokoll filtern“ wird geöffnet.
4. Aktivieren Sie im Feld **Ereignisquellen** das Kontrollkästchen **Benutzerprofildienst**, und wählen Sie dann **OK** aus.
5. Überprüfen Sie die Auflistung von Ereignissen, und achten Sie dabei besonders auf Fehlerereignisse.
6. Wenn Sie bemerkenswerte Ereignisse finden, wählen Sie den Link Onlinehilfe des Ereignisprotokolls aus, um weitere Informationen und Problembehandlungsverfahren anzuzeigen.
7. Um weitere Problembehandlung durchzuführen, notieren Sie das Datum und die Uhrzeit von bemerkenswerten Ereignissen, und untersuchen Sie dann das Betriebsprotokoll (wie in Schritt 2 beschrieben), um Details dazu anzuzeigen, welche Aktionen der Benutzerprofildienst zum Zeitpunkt der Fehler- oder Warnungsereignisse ausgeführt hat.

>[!NOTE]
>Sie können das Ereignis 1530 „Es wurde festgestellt, dass Ihre Registrierungsdatei noch von anderen Anwendungen oder Diensten verwendet wird“ des Benutzerprofildiensts sicher ignorieren.

## <a name="step-2-view-the-operational-log-for-the-user-profile-service"></a>Schritt 2: Anzeigen des Betriebsprotokolls für den Benutzerprofildienst

Wenn Sie das Problem nicht allein mithilfe des Anwendungsprotokolls lösen können, können Sie das folgende Verfahren verwenden, um Ereignisse des Benutzerprofildiensts im Betriebsprotokoll anzuzeigen. Dieses Protokoll zeigt einige der inneren Abläufe des Diensts auf und kann helfen, die Stelle im Lade- oder Entladevorgang des Profils zu bestimmen, an der das Problem auftritt.

Sowohl das Windows-Anwendungsprotokoll als auch das Betriebsprotokoll des Benutzerprofildiensts sind in allen Windows-Installationen standardmäßig aktiviert.

So wird das Betriebsprotokoll für den Benutzerprofildienst angezeigt:

1. Navigieren Sie in der Konsolenstruktur der Ereignisanzeige zu **Anwendungs- und Dienstprotokolle**, **Microsoft**, **Windows**, **Benutzerprofildienst** und **Betrieb**.
2. Untersuchen Sie die Ereignisse, die zum Zeitpunkt der Fehler- oder Warnungsereignisse aufgetreten sind, die Sie im Anwendungsprotokoll bemerkt haben.

## <a name="step-3-enable-and-view-analytic-and-debug-logs"></a>Schritt 3: Aktivieren und Anzeigen von Analyse- und Debugprotokollen

Wenn Sie mehr Details benötigen, als das Betriebsprotokoll bereitstellt, können Sie Analyse- und Debugprotokolle auf dem betroffenen Computer aktivieren. Diese Protokollierungsebene ist wesentlich ausführlicher und sollte deaktiviert werden, es sei denn, es wird versucht, ein Problem zu beheben.

So aktivieren Sie Analyse- und Debugprotokolle und zeigen diese an:

1. Wählen Sie im Bereich **Aktionen** der Ereignisanzeige **Anzeigen** aus, und wählen Sie dann **Analyse- und Debugprotokolle anzeigen** aus.
2. Navigieren Sie zu **Anwendungs- und Dienstprotokolle**, **Microsoft**, **Windows**, **Benutzerprofildienst** und **Diagnose**.
3. Wählen Sie **Protokoll aktivieren** und dann **Ja** aus. Dadurch wird das Diagnoseprotokoll aktiviert, das mit der Protokollierung beginnt.
4. Wenn Sie noch ausführlichere Informationen benötigen, finden Sie weitere Informationen zum Erstellen eines Ablaufverfolgungsprotokolls unter [Schritt 4: Erstellen und Decodieren einer Ablaufverfolgung](#step-4-creating-and-decoding-a-trace).
5. Wenn Sie die Problembehandlung abgeschlossen haben, navigieren Sie zum **Diagnoseprotokoll**, wählen Sie **Protokoll deaktivieren** aus, wählen Sie **Anzeigen** aus, und deaktivieren Sie dann das Kontrollkästchen **Analyse-und Debugprotokolle anzeigen**, um die Analyse- und Debugprotokollierung auszublenden.

## <a name="step-4-creating-and-decoding-a-trace"></a>Schritt 4: Erstellen und Decodieren einer Ablaufverfolgung

Wenn Sie das Problem nicht mithilfe von Ereignissen lösen können, können Sie ein Ablaufverfolgungsprotokoll (eine ETL-Datei) erstellen, während Sie das Problem reproduzieren, und es dann mit öffentlichen Symbolen vom Microsoft-Symbolserver decodieren. Ablaufverfolgungsprotokolle bieten sehr spezifische Informationen dazu, welche Aktionen der Benutzerprofildienst ausführt. Sie können bei der Ermittlung hilfreich sein, wo der Fehler aufgetreten ist.

Die beste Strategie bei Verwendung von ETL-Ablaufverfolgung besteht darin, zuerst das kleinstmögliche Protokoll zu erfassen. Nachdem das Protokoll decodiert wurde, suchen Sie im Protokoll nach Fehlern.

So erstellen und decodieren Sie eine Ablaufverfolgung für den Benutzerprofildienst:

1. Melden Sie sich bei dem Computer, auf dem der Benutzer Probleme hat, mit einem Konto an, das Mitglied der Gruppe „Lokale Administratoren“ ist.
2. Geben Sie an einer Eingabeaufforderung mit erhöhten Rechten die folgenden Befehle ein, wobei *\<Path\>* der Pfad zu einem lokalen Ordner ist, den Sie zuvor erstellt haben, z. B. C:\\Logs:
        
    ```PowerShell
    logman create trace -n RUP -o <Path>\RUP.etl -ets
    logman update RUP -p {eb7428f5-ab1f-4322-a4cc-1f1a9b2c5e98} 0x7FFFFFFF 0x7 -ets
    ```
3. Wählen Sie auf dem Startbildschirm den Benutzernamen aus, und wählen Sie dann **Konto wechseln** aus. Achten Sie darauf, dass Sie den Administrator nicht abmelden. Wenn Sie Remotedesktop verwenden, schließen Sie die Administratorsitzung, um die Benutzersitzung einzurichten.
4. Reproduzieren Sie das Problem. Die Vorgehensweise zum Reproduzieren des Problems besteht in der Regel darin, sich als der Benutzer anzumelden, bei dem das Problem auftritt, den Benutzer abzumelden oder beide Vorgänge auszuführen.
5. Melden Sie sich erneut als lokaler Administrator an, nachdem Sie das Problem reproduziert haben.
6. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus, um das Protokoll in einer ETL-Datei zu speichern:
  
    ```PowerShell
    logman stop -n RUP -ets
    ```
7. Geben Sie den folgenden Befehl ein, um die ETL-Datei in eine von Menschen lesbare Datei im aktuellen Verzeichnis zu exportieren (wahrscheinlich Ihr Basisordner oder der Ordner „%WINDIR%\\System32):
    
    ```PowerShell
    Tracerpt <path>\RUP.etl
    ```
8. Öffnen Sie die Dateien **Summary.txt** und **Dumpfile.xml** (Sie können sie in Microsoft Excel öffnen, um die gesamten Details des Protokolls leichter anzuzeigen). Suchen Sie nach Ereignissen, die **fail** oder **failed** enthalten. Sie können Zeilen, die den Ereignisnamen **Unknown** enthalten, problemlos ignorieren.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)