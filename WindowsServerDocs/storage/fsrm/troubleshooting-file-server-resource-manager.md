---
title: Problembehandlung im Ressourcen-Manager für Dateiserver
description: Dieser Artikel beschreibt, wie Sie allgemeine Probleme bei der Verwendung des Ressourcen-Managers für Dateiserver beheben
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0f30bcfd07f28ecd3fa1618e4f5d89b7a0b4d14f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403083"
---
# <a name="troubleshooting-file-server-resource-manager"></a>Problembehandlung im Ressourcen-Manager für Dateiserver

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Dieser Abschnitt enthält generelle Probleme, die auftreten können, wenn den Ressourcen-Manager für Dateiserver verwenden.

> [!Note]
> Eine gute Option für die Problembehandlung sind die Ereignisprotokolle, die durch den Ressourcen-Manager für Dateiserver generiert wurden. Alle Einträge im Ereignisprotokoll für den Ressourcen-Manager für Dateiserver befinden sich im Ereignisprotokoll **Anwendung** unter der Quelle **SRMSVC**

## <a name="i-am-not-receiving-e-mail-notifications"></a>Ich erhalte keine E-Mail-Benachrichtigungen.

-   **Ursache**: Die e-Mail-Optionen wurden nicht konfiguriert oder nicht ordnungsgemäß konfiguriert.

-   **Lösung**: Überprüfen Sie auf der Registerkarte **e-Mail-Benachrichtigungen** im Dialogfeld **Datei Server Ressourcen-Manager Optionen** , ob der SMTP-Server und die Standard-e-Mail-Empfänger angegeben und gültig sind. Senden Sie eine Test-E-Mail, um zu bestätigen, dass die Informationen korrekt sind und dass der SMTP-Server, der verwendet wird, das Senden von Benachrichtigungen ordnungsgemäß ausführt. Weitere Informationen finden Sie unter [Konfigurieren von E-Mail-Benachrichtigungen](configure-email-notifications.md).


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>Ich erhalte nur eine E-Mail-Benachrichtigung, obwohl das Ereignis, das die Benachrichtigung ausgelöst hat, mehrmals hintereinander aufgetreten ist.

-   **Ursache**: Wenn ein Benutzer mehrmals versucht, eine Datei zu speichern, die blockiert ist, oder eine Datei zu speichern, die einen Kontingent Schwellenwert überschreitet, und eine e-Mail-Benachrichtigung für diese Dateiüberprüfung oder das Kontingent Ereignis konfiguriert ist, wird nur eine e-Mail über einen Zeitraum von 60 Minuten an den Administrator gesendet.  vorgegebene. Dies verhindert, dass eine Fülle von redundanten Nachrichten an das Administrator-E-Mail-Konto gesendet werden.

-   **Lösung**: Im Dialogfeld Optionen für den **Datei Server Ressourcen-Manager** auf der Registerkarte **Benachrichtigungs Limits** können Sie ein Zeitlimit für die einzelnen Benachrichtigungs Typen festlegen: e-Mail, Ereignisprotokoll, Befehl und Bericht. Jedes Limit gibt einen Zeitraum an, der vergehen muss, bevor eine weitere Benachrichtigung desselben Typs für ein identisches Problem generiert wird. Weitere Informationen finden Sie unter [Konfigurieren von Benachrichtigungslimits](configure-notification-limits.md).


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>Meine Speicherberichten schlagen fehl und es befinden sich wenig oder keine Informationen im Ereignisprotokoll in Bezug auf die Ursache des Fehlers.

-   **Ursache**: Das Volume, auf dem die Berichte gespeichert werden, ist möglicherweise beschädigt.
-   **Lösung**: Führen Sie **chkdsk** auf dem Volume aus, und versuchen Sie erneut, die Berichte zu erstellen.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>Meine Dateiprüfungsereignisse in der Überwachungsdatenbank enthalten keine Informationen.

-   **Ursache**: Eine oder mehrere der folgenden Ursachen können folgende Ursachen haben:
    -   Die Überwachungsdatenbank ist nicht für die Aufzeichnung von Dateiprüfungsaktivitäten konfiguriert.
    -   Die Überwachungsdatenbank ist leer (d. h. es wurde keine Dateiprüfungsaktivität aufgezeichnet).
    -   Die Parameter für den Dateiprüfungsüberwachungs-Bericht wählen keine Daten aus der Überwachungsdatenbank aus.
    
-   **Lösung**: Vergewissern Sie sich, dass auf der Registerkarte **Datei Bildschirm** Überwachung im Dialogfeld **Datei Server Ressourcen-Manager Optionen** das Kontrollkästchen **Dateiüberprüfung aufzeichnen im Kontrollkästchen Daten Bank** Überwachung aktiviert ist.
    -   Weitere Informationen zum Aufzeichnen von Dateiprüfungsaktivitäten finden Sie unter [Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md).
    -   Informationen zum Konfigurieren der Standardparameter für Dateiprüfungsüberwachungs-Berichte finden Sie unter [Speicherberichte konfigurieren](configure-storage-reports.md).
    -   Informationen zum Bearbeiten der Berichtsparameter für geplante Berichtaufgaben oder bedarfsgesteuerte Berichte finden Sie unter [Speicherberichtmanagement](storage-reports-management.md).

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>Die "Verwendeten" und "Verfügbaren" Werte für einige der Kontingente, die ich erstellt habe, entsprechen nicht den tatsächlichen Einstellungen des "Grenzwerts".

-   **Ursache**: Möglicherweise verfügen Sie über ein geschachtelte-Kontingent, bei dem das Kontingent eines unter Ordners eine restriktivere Grenze von dem Kontingent seines übergeordneten Ordners ableitet. Sie haben beispielsweise eine Kontingentgrenze von 100 MB (Megabyte) in einem übergeordneten Ordner und ein Kontingent von 200 MB auf jedem der Unterordner, das separat angewendet wird. Wenn der übergeordnete Ordner insgesamt 50 MB an Daten gespeichert hat (die Summe der in seinen Unterordnern gespeicherten Daten), werden in den einzelnen Unterordner nur 50 MB verfügbarem Speicherplatz aufgeführt.

-   **Lösung**: Klicken Sie unter **Kontingent Verwaltung**auf **Kontingente**. Wählen Sie im **Ergebnis**bereich den Kontingenteintrag aus, dessen Problem Sie behandeln. Klicken Sie im Bereich **Aktionen** auf **Kontingente anzeigen, die sich auf Ordner auswirken** und suchen Sie nach Kontingente, die auf die übergeordneten Ordner angewendet werden. Dadurch können Sie identifizieren, welche übergeordneten Ordnerkontingente eine niedrigere Speicherbeschränkungen als das Kontingent haben, das Sie ausgewählt haben.

