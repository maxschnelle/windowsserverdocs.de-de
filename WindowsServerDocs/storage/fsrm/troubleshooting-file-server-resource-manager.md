---
title: Problembehandlung im Ressourcen-Manager für Dateiserver
description: Dieser Artikel beschreibt, wie Sie allgemeine Probleme bei der Verwendung des Ressourcen-Managers für Dateiserver beheben
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 413cf51e5ceb1c4507b71fb77ee6005807a0ff13
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476181"
---
# <a name="troubleshooting-file-server-resource-manager"></a>Problembehandlung im Ressourcen-Manager für Dateiserver

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Dieser Abschnitt enthält generelle Probleme, die auftreten können, wenn den Ressourcen-Manager für Dateiserver verwenden.

> [!Note]
> Eine gute Option für die Problembehandlung sind die Ereignisprotokolle, die durch den Ressourcen-Manager für Dateiserver generiert wurden. Alle Einträge im Ereignisprotokoll für den Ressourcen-Manager für Dateiserver befinden sich im Ereignisprotokoll **Anwendung** unter der Quelle **SRMSVC**

## <a name="i-am-not-receiving-e-mail-notifications"></a>Ich erhalte keine E-Mail-Benachrichtigungen.

-   **Ursache**: E-Mail-Optionen wurden nicht konfiguriert oder nicht ordnungsgemäß konfiguriert wurden.

-   **Lösung**: Auf der **e-Mail-Benachrichtigungen** Registerkarte die **File Server Resource Manager-Optionen** Dialogfeld Vergewissern Sie sich, dass der SMTP-Server und die standardmäßige e-Mail-Empfänger angegeben wurden und gültig sind. Senden Sie eine Test-E-Mail, um zu bestätigen, dass die Informationen korrekt sind und dass der SMTP-Server, der verwendet wird, das Senden von Benachrichtigungen ordnungsgemäß ausführt. Weitere Informationen finden Sie unter [Konfigurieren von E-Mail-Benachrichtigungen](configure-email-notifications.md).


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>Ich erhalte nur eine E-Mail-Benachrichtigung, obwohl das Ereignis, das die Benachrichtigung ausgelöst hat, mehrmals hintereinander aufgetreten ist.

-   **Ursache**: Wenn ein Benutzer mehrmals versucht Speichern einer Datei, der blockiert ist oder zum Speichern einer Datei, die einen Kontingentschwellenwert überschreitet und es screening-eine e-Mail-Benachrichtigung für diese Datei konfiguriert ist oder Kontingent-Ereignis, nur eine E-mail an den Administrator gesendet wird, über einen Zeitraum von 60 Minuten durch  Standardmäßig. Dies verhindert, dass eine Fülle von redundanten Nachrichten an das Administrator-E-Mail-Konto gesendet werden.

-   **Lösung**: Auf der **Benachrichtigung Grenzwerte** Registerkarte die **File Server Resource Manager-Optionen** im Dialogfeld können Sie ein Zeitlimit für jeden der die Benachrichtigungstypen festlegen:-e-Mail "," Ereignisprotokoll "," Befehl "und" Bericht. Jedes Limit gibt einen Zeitraum an, der vergehen muss, bevor eine weitere Benachrichtigung desselben Typs für ein identisches Problem generiert wird. Weitere Informationen finden Sie unter [Konfigurieren von Benachrichtigungslimits](configure-notification-limits.md).


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>Meine Speicherberichten schlagen fehl und es befinden sich wenig oder keine Informationen im Ereignisprotokoll in Bezug auf die Ursache des Fehlers.

-   **Ursache**: Das Volume, in dem die Berichte gespeichert werden, ist möglicherweise beschädigt.
-   **Lösung**: Führen Sie **Chkdsk** auf dem Volume und versuchen Sie es erneut, die Berichte zu generieren.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>Meine Dateiprüfungsereignisse in der Überwachungsdatenbank enthalten keine Informationen.

-   **Ursache**: Die Ursache kann sein, eine oder mehrere der folgenden:
    -   Die Überwachungsdatenbank ist nicht für die Aufzeichnung von Dateiprüfungsaktivitäten konfiguriert.
    -   Die Überwachungsdatenbank ist leer (d. h. es wurde keine Dateiprüfungsaktivität aufgezeichnet).
    -   Die Parameter für den Dateiprüfungsüberwachungs-Bericht wählen keine Daten aus der Überwachungsdatenbank aus.
    
-   **Lösung**: Auf der **Bildschirm Dateiüberwachung** Registerkarte die **File Server Resource Manager-Optionen** Dialogfeld überprüfen Sie, ob die **Datensatz Dateiprüfungsereignisse-Aktivität in der Überwachungsdatenbank** überprüfen aktiviert ist.
    -   Weitere Informationen zum Aufzeichnen von Dateiprüfungsaktivitäten finden Sie unter [Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md).
    -   Informationen zum Konfigurieren der Standardparameter für Dateiprüfungsüberwachungs-Berichte finden Sie unter [Speicherberichte konfigurieren](configure-storage-reports.md).
    -   Informationen zum Bearbeiten der Berichtsparameter für geplante Berichtaufgaben oder bedarfsgesteuerte Berichte finden Sie unter [Speicherberichtmanagement](storage-reports-management.md).

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>Die "Verwendeten" und "Verfügbaren" Werte für einige der Kontingente, die ich erstellt habe, entsprechen nicht den tatsächlichen Einstellungen des "Grenzwerts".

-   **Ursache**: Sie ggf. ein Kontingent geschachtelte, in dem das Kontingent eines Unterordners das Kontingent von seinem übergeordneten Ordner eine restriktivere Beschränkung abgeleitet. Sie haben beispielsweise eine Kontingentgrenze von 100 MB (Megabyte) in einem übergeordneten Ordner und ein Kontingent von 200 MB auf jedem der Unterordner, das separat angewendet wird. Wenn der übergeordnete Ordner insgesamt 50 MB an Daten gespeichert hat (die Summe der in seinen Unterordnern gespeicherten Daten), werden in den einzelnen Unterordner nur 50 MB verfügbarem Speicherplatz aufgeführt.

-   **Lösung**: Klicken Sie unter **Kontingentverwaltung**, klicken Sie auf **Kontingente**. Wählen Sie im **Ergebnis**bereich den Kontingenteintrag aus, dessen Problem Sie behandeln. Klicken Sie im Bereich **Aktionen** auf **Kontingente anzeigen, die sich auf Ordner auswirken** und suchen Sie nach Kontingente, die auf die übergeordneten Ordner angewendet werden. Dadurch können Sie identifizieren, welche übergeordneten Ordnerkontingente eine niedrigere Speicherbeschränkungen als das Kontingent haben, das Sie ausgewählt haben.

