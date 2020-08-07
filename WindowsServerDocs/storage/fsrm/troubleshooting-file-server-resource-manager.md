---
title: Problembehandlung im Ressourcen-Manager für Dateiserver
description: In diesem Artikel wird beschrieben, wie Sie häufige Probleme bei der Verwendung des Ressourcen-Managers für Dateiserver beheben.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: fbd44938f57cc27576ba3d3bfa39b3e87e4989ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950444"
---
# <a name="troubleshooting-file-server-resource-manager"></a>Problembehandlung im Ressourcen-Manager für Dateiserver

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

In diesem Abschnitt werden häufige Probleme aufgelistet, die bei der Verwendung von Datei Server Ressourcen-Manager auftreten können.

> [!Note]
> Eine gute Problem Behandlungsoption besteht darin, nach Ereignisprotokollen zu suchen, die von Datei Server Ressourcen-Manager generiert wurden. Alle Ereignisprotokoll Einträge für Datei Server Ressourcen-Manager befinden sich im**Anwendungs** Ereignisprotokoll unter der Quelle **SRMSVC** .

## <a name="i-am-not-receiving-e-mail-notifications"></a>Ich erhalte keine e-Mail-Benachrichtigungen.

-   **Ursache**: die e-Mail-Optionen wurden nicht konfiguriert oder falsch konfiguriert.

-   **Lösung**: Überprüfen Sie auf der Registerkarte **e-Mail-Benachrichtigungen** im Dialogfeld **Datei Server Ressourcen-Manager Optionen** , ob der SMTP-Server und die Standard-e-Mail-Empfänger angegeben und gültig sind. Senden Sie eine Test-e-Mail, um zu bestätigen, dass die Informationen korrekt sind und der SMTP-Server, der zum Senden der Benachrichtigungen verwendet wird, ordnungsgemäß funktioniert. Weitere Informationen finden Sie unter [e-Mail-Benachrichtigungen konfigurieren](configure-email-notifications.md).


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>Ich erhalte nur eine e-Mail-Benachrichtigung, obwohl das Ereignis, das diese Benachrichtigung ausgelöst hat, mehrmals in einer Zeile aufgetreten ist.

-   **Ursache**: Wenn ein Benutzer mehrmals versucht, eine Datei zu speichern, die blockiert ist, oder eine Datei zu speichern, die einen Kontingent Schwellenwert 60 überschreitet, und eine e-Mail-Benachrichtigung für diese Dateiüberprüfung oder ein Kontingent Ereignis konfiguriert ist, wird standardmäßig nur eine e-Mail an den Administrator gesendet. Dadurch wird eine Fülle redundanter Nachrichten im e-Mail-Konto des Administrators verhindert.

-   **Lösung**: auf der Registerkarte **Benachrichtigungs Limits** im Dialogfeld **Optionen für Datei Server Ressourcen-Manager** können Sie ein Zeitlimit für die einzelnen Benachrichtigungs Typen festlegen: e-Mail, Ereignisprotokoll, Befehl und Bericht. Jedes Limit gibt einen Zeitraum an, der verstreichen muss, bevor eine andere Benachrichtigung desselben Typs für das gleiche Problem generiert wird. Weitere Informationen finden Sie unter [Konfigurieren von Benachrichtigungs Limits](configure-notification-limits.md).


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>Meine Speicher Berichte schlagen fehl, und es sind nur wenige oder gar keine Informationen im Ereignisprotokoll für die Fehlerquelle verfügbar.

-   **Ursache**: das Volume, auf dem die Berichte gespeichert werden, ist möglicherweise beschädigt.
-   **Lösung**: führen Sie **chkdsk** auf dem Volume aus, und versuchen Sie erneut, die Berichte zu erstellen.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>Meine Dateiprüfungsüberwachung Berichte enthalten keine Informationen.

-   **Ursache**: eine oder mehrere der folgenden Ursachen können folgende Ursachen haben:
    -   Die Überwachungs Datenbank ist nicht für die Aufzeichnung von Datei Überprüfungs Aktivitäten konfiguriert.
    -   Die Überwachungs Datenbank ist leer (d. h., es wurde keine Datei Überprüfungs Aktivität aufgezeichnet).
    -   In den Parametern für den Dateiprüfungsüberwachung Bericht werden keine Daten aus der Überwachungs Datenbank ausgewählt.

-   **Lösung**: Vergewissern Sie sich, dass auf der Registerkarte **Datei Bildschirm** Überwachung im Dialogfeld **Datei Server Ressourcen-Manager Optionen** das Kontrollkästchen **Dateiüberprüfung aufzeichnen im Kontrollkästchen Daten Bank** Überwachung aktiviert ist.
    -   Weitere Informationen zum Aufzeichnen der Dateiüberprüfung finden Sie unter [configure File Screen Audit](configure-file-screen-audit.md).
    -   Informationen zum Konfigurieren von Standardparametern für den Dateiprüfungsüberwachung Bericht finden Sie unter [Konfigurieren von Speicher Berichten](configure-storage-reports.md).
    -   Informationen zum Bearbeiten von Berichts Parametern für geplante Berichts Tasks oder Bedarfs gesteuerte Berichte finden Sie unter [Speicher Berichte-Verwaltung](storage-reports-management.md).

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>Die Werte "used" und "available" für einige der erstellten Kontingente entsprechen nicht der tatsächlichen Einstellung "Limit".

-   **Ursache**: Sie verfügen möglicherweise über ein geschachtelte-Kontingent, bei dem das Kontingent eines unter Ordners eine restriktivere Grenze aus dem Kontingent seines übergeordneten Ordners ableitet. Angenommen, Sie verfügen über eine Kontingent Grenze von 100 Megabyte (MB), die auf einen übergeordneten Ordner angewendet wird, und ein Kontingent von 200 MB, das separat auf die einzelnen Unterordner angewendet wird. Wenn für den übergeordneten Ordner insgesamt 50 MB Daten gespeichert sind (die Summe der in den Unterordnern gespeicherten Daten), werden in jedem der Unterordner nur 50 MB verfügbarer Speicherplatz aufgeführt.

-   **Lösung**: Klicken Sie unter **Kontingent Verwaltung**auf **Kontingente**. Wählen Sie im Ergebnisbereich den Kontingent Eintrag aus, für den Sie eine Problembehandlung durch **führen** möchten. Klicken Sie im **Aktions** Bereich auf **Kontingente für den Ordner anzeigen**, und suchen Sie dann nach Kontingenten, die auf die übergeordneten Ordner angewendet werden. Auf diese Weise können Sie ermitteln, welche Kontingente für übergeordnete Ordner eine niedrigere Einstellung für das Speicherlimit aufweisen als das von Ihnen ausgewählte Kontingent.

