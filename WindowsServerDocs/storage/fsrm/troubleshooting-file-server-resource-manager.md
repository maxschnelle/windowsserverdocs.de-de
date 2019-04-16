---
title: "Problembehandlung im Ressourcen-Manager für Dateiserver"
description: "Dieser Artikel beschreibt, wie Sie allgemeine Probleme bei der Verwendung des Ressourcen-Managers für Dateiserver beheben"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 923710fac426f63d2c38d9b9a68c92427783abb1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="troubleshooting-file-server-resource-manager"></a>Problembehandlung im Ressourcen-Manager für Dateiserver

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Dieser Abschnitt enthält generelle Probleme, die auftreten können, wenn den Ressourcen-Manager für Dateiserver verwenden.

> [!Note]
> Eine gute Option für die Problembehandlung sind die Ereignisprotokolle, die durch den Ressourcen-Manager für Dateiserver generiert wurden. Alle Einträge im Ereignisprotokoll für den Ressourcen-Manager für Dateiserver befinden sich im Ereignisprotokoll **Anwendung** unter der Quelle **SRMSVC**

## <a name="i-am-not-receiving-e-mail-notifications"></a>Ich erhalte keine E-Mail-Benachrichtigungen.

-   **Ursache**: Die E-Mail-Optionen wurden nicht konfiguriert oder sind nicht ordnungsgemäß konfiguriert wurden.

-   **Lösung**: Überprüfen Sie auf der Registerkarte **E-Mail-Benachrichtigungen** das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** und stellen Sie sicher, dass der SMTP-Server und die standardmäßige E-Mail-Empfänger angegeben wurden und gültig sind. Senden Sie eine Test-E-Mail, um zu bestätigen, dass die Informationen korrekt sind und dass der SMTP-Server, der verwendet wird, das Senden von Benachrichtigungen ordnungsgemäß ausführt. Weitere Informationen finden Sie unter [Konfigurieren von E-Mail-Benachrichtigungen](configure-email-notifications.md).


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>Ich erhalte nur eine E-Mail-Benachrichtigung, obwohl das Ereignis, das die Benachrichtigung ausgelöst hat, mehrmals hintereinander aufgetreten ist.

-   **Ursache**: Wenn ein Benutzer mehrere Male versucht, eine Datei zu speichern, die blockiert ist oder eine Datei zu speichern, die einen Schwellenwert überschreitet und eine E-Mail-Benachrichtigung für die Prüfung der Datei oder ein Kontingentereignis konfiguriert wurde, wird standardmäßig nur eine E-Mail-Benachrichtigung an den Administrator über einen Zeitraum von 60Minuten gesendet. Dies verhindert, dass eine Fülle von redundanten Nachrichten an das Administrator-E-Mail-Konto gesendet werden.

-   **Lösung**: Sie können in der Registerkarte **Benachrichtigungslimits** im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** ein Zeitlimit für jeden Benachrichtigungstyp festlegen: E-Mail, Ereignisprotokoll, Befehl und Bericht. Jedes Limit gibt einen Zeitraum an, der vergehen muss, bevor eine weitere Benachrichtigung desselben Typs für ein identisches Problem generiert wird. Weitere Informationen finden Sie unter [Konfigurieren von Benachrichtigungslimits](configure-notification-limits.md).


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>Meine Speicherberichten schlagen fehl und es befinden sich wenig oder keine Informationen im Ereignisprotokoll in Bezug auf die Ursache des Fehlers.

-   **Ursache**: Das Volume, in dem die Berichte gespeichert werden, ist möglicherweise beschädigt.
-   **Lösung**: Führen Sie auf dem Volume **Chkdsk** aus und versuchen Sie erneut, die Berichte zu generieren.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>Meine Dateiprüfungsereignisse in der Überwachungsdatenbank enthalten keine Informationen.

-   **Ursache**: Dieses Ereignis kann durch einen oder mehrere der folgenden Gründe verursacht werden:
    -   Die Überwachungsdatenbank ist nicht für die Aufzeichnung von Dateiprüfungsaktivitäten konfiguriert.
    -   Die Überwachungsdatenbank ist leer (d.h. es wurde keine Dateiprüfungsaktivität aufgezeichnet).
    -   Die Parameter für den Dateiprüfungsüberwachungs-Bericht wählen keine Daten aus der Überwachungsdatenbank aus.
    
-   **Lösung**: Überprüfen Sie auf der Registerkarte **Dateiprüfungsberichte** im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver**, ob das Kontrollkästchen **Dateiprüfungsaktivitäten in einer Überwachungsdatenbank aufzeichnen** aktiviert ist.
    -   Weitere Informationen zum Aufzeichnen von Dateiprüfungsaktivitäten finden Sie unter [Dateiprüfungsberichte konfigurieren](configure-file-screen-audit.md).
    -   Informationen zum Konfigurieren der Standardparameter für Dateiprüfungsüberwachungs-Berichte finden Sie unter [Speicherberichte konfigurieren](configure-storage-reports.md).
    -   Informationen zum Bearbeiten der Berichtsparameter für geplante Berichtaufgaben oder bedarfsgesteuerte Berichte finden Sie unter [Speicherberichtmanagement](storage-reports-management.md).

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>Die "Verwendeten" und "Verfügbaren" Werte für einige der Kontingente, die ich erstellt habe, entsprechen nicht den tatsächlichen Einstellungen des "Grenzwerts".

-   **Ursache**: Sie haben möglicherweise ein verschachteltes Kontingent, wobei das Kontingent eines Unterordners eine restriktivere Grenze des Kontingents als die des übergeordneten Ordners ableitet. Sie haben beispielsweise eine Kontingentgrenze von 100MB (Megabyte) in einem übergeordneten Ordner und ein Kontingent von 200MB auf jedem der Unterordner, das separat angewendet wird. Wenn der übergeordnete Ordner insgesamt 50MB an Daten gespeichert hat (die Summe der in seinen Unterordnern gespeicherten Daten), werden in den einzelnen Unterordner nur 50MB verfügbarem Speicherplatz aufgeführt.

-   **Lösung**: Klicken Sie unter **Kontingentverwaltung** auf **Kontingente**. Wählen Sie im **Ergebnis**bereich den Kontingenteintrag aus, dessen Problem Sie behandeln. Klicken Sie im Bereich **Aktionen** auf **Kontingente anzeigen, die sich auf Ordner auswirken** und suchen Sie nach Kontingente, die auf die übergeordneten Ordner angewendet werden. Dadurch können Sie identifizieren, welche übergeordneten Ordnerkontingente eine niedrigere Speicherbeschränkungen als das Kontingent haben, das Sie ausgewählt haben.

