---
title: Problembehandlung bei Benutzerprofilen mit Ereignissen
description: Behandeln von Problemen beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablauf Verfolgungs Protokollen.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e927a77627e786015a928d798aafee13a2cc34b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394378"
---
# <a name="troubleshoot-user-profiles-with-events"></a>Problembehandlung bei Benutzerprofilen mit Ereignissen

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server (halbjährlicher Kanal).

In diesem Thema wird erläutert, wie Probleme beim Laden und Entladen von Benutzerprofilen mithilfe von Ereignissen und Ablauf Verfolgungs Protokollen behoben werden. In den folgenden Abschnitten wird beschrieben, wie die drei Ereignisprotokolle verwendet werden, die Benutzerprofil Informationen aufzeichnen.

## <a name="step-1-checking-events-in-the-application-log"></a>Schritt 1: Überprüfen von Ereignissen im Anwendungsprotokoll

Der erste Schritt bei der Behebung von Problemen beim Laden und Entladen von Benutzerprofilen (einschließlich Roamingbenutzerprofilen) ist die Verwendung von Ereignisanzeige, um Warn-und Fehlerereignisse zu untersuchen, die vom Benutzerprofil Dienst im Anwendungsprotokoll aufgezeichnet werden.

Im folgenden wird erläutert, wie Benutzerprofil Dienst-Ereignisse im Anwendungsprotokoll angezeigt werden:

1. Starten Sie Ereignisanzeige. Öffnen Sie hierzu die System **Steuerung**, wählen Sie **System und Sicherheit**aus, und wählen Sie dann im Abschnitt **Verwaltung** die Option **Ereignisprotokolle anzeigen**aus. Das Ereignisanzeige Fenster wird geöffnet.
2. Navigieren Sie in der Konsolen Struktur zunächst zu **Windows-Protokolle**und dann zu **Anwendung**.
3. Wählen Sie im Bereich Aktionen die Option **Aktuelles Protokoll filtern**aus. Das Dialogfeld Aktuelles Protokoll filtern wird geöffnet.
4. Wählen Sie im Feld **Ereignis Quellen** das Kontrollkästchen **Benutzerprofil Dienst** aus, und klicken Sie dann auf **OK**.
5. Überprüfen Sie die Auflistung von Ereignissen, und achten Sie dabei besonders auf Fehlerereignisse.
6. Wenn Sie bemerkenswerte Ereignisse finden, wählen Sie den Link Ereignisprotokoll Online Hilfe aus, um weitere Informationen und Problem Behandlungsverfahren anzuzeigen.
7. Beachten Sie zur weiteren Problembehandlung das Datum und die Uhrzeit von bemerkenswerten Ereignissen, und überprüfen Sie dann das Betriebsprotokoll (wie in Schritt 2 beschrieben), um Details dazu anzuzeigen, was der Benutzerprofil Dienst zum Zeitpunkt der Fehler-oder Warnungs Ereignisse ausgeführt hat.

>[!NOTE]
>Sie können das Benutzerprofil Dienst-Ereignis 1530 "Windows hat erkannt, dass Ihre Registrierungsdatei noch von anderen Anwendungen oder Diensten verwendet wird, sicher ignorieren."

## <a name="step-2-view-the-operational-log-for-the-user-profile-service"></a>Schritt 2: Anzeigen des Betriebs Protokolls für den Benutzerprofil Dienst

Wenn Sie das Problem nicht allein mithilfe des Anwendungs Protokolls lösen können, können Sie das folgende Verfahren verwenden, um Benutzerprofil Dienst-Ereignisse im Betriebsprotokoll anzuzeigen. In diesem Protokoll werden einige der inneren Abläufe des Dienstanbieter angezeigt, und Sie können ermitteln, an welchen Stellen im Profil geladen oder entladen wird.

Sowohl das Windows-Anwendungsprotokoll als auch das Betriebsprotokoll des Benutzerprofil Dienstanbieter sind in allen Windows-Installationen standardmäßig aktiviert.

Hier sehen Sie, wie das Betriebsprotokoll für den Benutzerprofil Dienst angezeigt wird:

1. Navigieren Sie in der Konsolen Struktur Ereignisanzeige zu **Anwendungs-und Dienst Protokolle**, und klicken Sie dann auf **Microsoft**, dann auf **Windows**, dann auf **Benutzerprofil Dienst**und dann auf **betriebsbereit**.
2. Überprüfen Sie die Ereignisse, die zum Zeitpunkt der Fehler-oder Warnungs Ereignisse aufgetreten sind, die Sie im Anwendungsprotokoll notiert haben.

## <a name="step-3-enable-and-view-analytic-and-debug-logs"></a>Schritt 3: Aktivieren und Anzeigen von analytischen und Debugprotokollen

Wenn Sie mehr Details benötigen, als das Betriebsprotokoll bereitstellt, können Sie analytische und Debugprotokolle auf dem betroffenen Computer aktivieren. Diese Protokollierungsebene ist ausführlicher und sollte deaktiviert werden, es sei denn, es wird versucht, ein Problem zu beheben.

Im folgenden wird erläutert, wie Sie analytische und Debugprotokolle aktivieren und anzeigen:

1. Wählen Sie im **Aktions** Bereich von Ereignisanzeige **Ansicht**aus, und wählen Sie dann **analytische und Debugprotokolle anzeigen**aus.
2. Navigieren Sie zu **Anwendungs-und Dienst Protokolle**, dann zu **Microsoft**, dann zu **Windows**und dann zu **Benutzerprofil Dienst**und **Diagnose**.
3. Wählen Sie **Protokoll aktivieren** aus, und wählen Sie dann **Ja**. Dadurch wird das Diagnoseprotokoll aktiviert, das mit der Protokollierung beginnt.
4. Weitere Informationen zum Erstellen eines Ablauf Verfolgungs Protokolls finden Sie unter [Schritt 4: Erstellen und Decodieren einer Ablauf Verfolgung](#step-4-creating-and-decoding-a-trace) .
5. Wenn Sie die Problembehandlung abgeschlossen haben, navigieren Sie zum **Diagnose** Protokoll, wählen Sie **Protokoll deaktivieren**und **anzeigen** aus, und deaktivieren Sie dann das Kontrollkästchen **analytische und Debugprotokolle anzeigen** , um die analytische und Debugprotokollierung auszublenden.

## <a name="step-4-creating-and-decoding-a-trace"></a>Schritt 4: Erstellen und Decodieren einer Ablauf Verfolgung

Wenn Sie das Problem nicht mithilfe von Ereignissen lösen können, können Sie ein Ablauf Verfolgungs Protokoll (eine ETL-Datei) erstellen, während Sie das Problem reproduzieren, und es dann mit öffentlichen Symbolen vom Microsoft-Symbol Server decodieren. Ablauf Verfolgungs Protokolle bieten sehr spezifische Informationen dazu, was der Benutzerprofil Dienst leistet, und können ermitteln, wo der Fehler aufgetreten ist.

Die beste Strategie bei der Verwendung der ETL-Ablauf Verfolgung besteht darin, zuerst das kleinste Protokoll zu erfassen. Nachdem das Protokoll decodiert wurde, suchen Sie im Protokoll nach Fehlern.

So erstellen und Decodieren Sie eine Ablauf Verfolgung für den Benutzerprofil Dienst:

1. Melden Sie sich bei dem Computer, auf dem der Benutzer Probleme aufweist, mit einem Konto an, das Mitglied der lokalen Administratoren Gruppe ist.
2. Geben Sie an einer Eingabeaufforderung mit erhöhten Rechten die folgenden Befehle ein, wobei *\<Pfad\>* der Pfad zu einem lokalen Ordner ist, den Sie zuvor erstellt haben, z. b. C:\\Logs:
        
    ```PowerShell
    logman create trace -n RUP -o <Path>\RUP.etl -ets
    logman update RUP -p {eb7428f5-ab1f-4322-a4cc-1f1a9b2c5e98} 0x7FFFFFFF 0x7 -ets
    ```
3. Wählen Sie auf der Start Seite den Benutzernamen aus, und wählen Sie dann **Konto wechseln**aus. Achten Sie darauf, dass Sie den Administrator nicht abmelden. Wenn Sie Remotedesktop verwenden, schließen Sie die Administrator Sitzung, um die Benutzersitzung einzurichten.
4. Reproduzieren Sie das Problem. Die Vorgehensweise zum Reproduzieren des Problems besteht in der Regel darin, sich bei dem Benutzer, der das Problem auftritt, den Benutzer abzumelden oder beides zu melden.
5. Melden Sie sich nach der Reproduktion des Problems erneut als lokaler Administrator an.
6. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus, um das Protokoll in einer ETL-Datei zu speichern:
  
    ```PowerShell
    logman stop -n RUP -ets
    ```
7. Geben Sie den folgenden Befehl ein, um die ETL-Datei in eine lesbare Datei im aktuellen Verzeichnis zu exportieren (wahrscheinlich Ihr Basisordner oder der Ordner% windir%\\system32):
    
    ```PowerShell
    Tracerpt <path>\RUP.etl
    ```
8. Öffnen Sie die Datei " **Summary. txt** " und die Datei " **dumpfile. XML** " (Sie können Sie in Microsoft Excel öffnen, um die gesamten Protokoll Details leichter anzuzeigen). Suchen Sie nach Ereignissen, die **Fehler oder** **fehlgeschlagene**Ereignisse einschließen. Sie können Zeilen, die den **unbekannten** Ereignis Namen enthalten, gefahrlos ignorieren.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)