---
title: Anzeigen von Aufgabendetails und Benachrichtigungen
description: Server-Manager
ms.topic: article
ms.assetid: 95117407-2dd3-4f9a-841f-4331be3544c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b347f5cf3a3d752c500e602b84889afa9c580ab0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895699"
---
# <a name="view-task-details-and-notifications"></a>Anzeigen von Aufgabendetails und Benachrichtigungen

>Gilt für: Windows Server 2016

Wenn Sie in Server-Manager unter Windows Server 2012 R2 oder Windows Server 2012 Verwaltungsaufgaben durchführen, z. b. Rollen und Features hinzufügen, Dienste starten, Daten aktualisieren, die in der Server-Manager-Konsole angezeigt werden, oder eine benutzerdefinierte Gruppe von Servern erstellen, wird im **Benachrichtigungs** Bereich des Server-Manager-Konsolen Headers eine Benachrichtigung angezeigt. Benachrichtigungen und das Dialogfeld **Aufgaben Details** , das Sie über das Menü **Benachrichtigungen** öffnen können, indem Sie auf das Flag-Symbol klicken, den Status von Benutzer Aufgaben oder-Anforderungen anzeigen, anzeigen, wenn eine Aufgabe fehlgeschlagen ist, und bei der Problembehandlung helfen, indem Sie auf detaillierte Fehlermeldungen zu Aufgaben Fehlern verweisen.

## <a name="the-notifications-area"></a>Infobereich
Der **Benachrichtigungs** Bereich in der Menüleiste Server-Manager, der durch ein flagsymbol gekennzeichnet ist, zeigt die Ergebnisse der Aufgaben an, die Sie in Server-Manager starten. Benachrichtigungen informieren Sie darüber, ob Aufgaben, die Sie in Server-Manager gestartet haben, erfolgreich waren oder fehlgeschlagen sind. Wenn Benachrichtigungen zur Ansicht verfügbar sind, wird die Anzahl verfügbarer Benachrichtigungen neben dem Flaggensymbol angezeigt. Falls eine Aufgabe fehlgeschlagen ist, nur teilweise abgeschlossen werden konnte (wenn sie beispielsweise nicht auf allen gewünschten Remoteservern durchgeführt werden konnte) oder mit Warnungen abgeschlossen wurde, wird die Benachrichtigungsflagge**** rot. Für folgende Aufgaben werden Benachrichtigungen angezeigt.

-   Manuelles Aktualisieren der in Server-Manager angezeigten Daten (Benachrichtigungen werden nur für automatische Aktualisierungen angezeigt, wenn die Aktualisierungen fehlschlagen)

-   Starten oder Beenden von Diensten

-   Installieren oder Deinstallieren von Rollen, Rollen Diensten und Features

-   Starten eines Best Practices Analyzer-Scans (BPA)

-   Hinzufügen von zu verwaltenden Remote Servern (Benachrichtigungen werden angezeigt, um die für Remote Server angezeigten Daten zu kontaktieren oder zu aktualisieren)

Zu den Elementen im Menü **Benachrichtigungen** gehören eine Statusleiste, eine kurze Beschreibung der Aufgabe, der Name des Zielservers für die Aufgabe (oder eines der Zielserver, falls mehrere Zielserver ausgewählt wurden), ggf. ein Link zu einem dazugehörigen Steuerelement oder Dialogfeld und das Menü **Aufgaben**. Das Menü **Aufgaben** zeigt Befehle für die aktive Benachrichtigung an (die Benachrichtigung, über die der Mauszeiger bewegt wird). Wenn Sie beispielsweise einen Dienst beenden, können Sie im Menü **Aufgaben** der Benachrichtigung auf **Neu starten** klicken, um den Dienst neu zu starten.

Benachrichtigungen sind besonders nützlich für das Installieren oder Deinstallieren von Rollen, Rollen Diensten und Features. Wenn Sie z. b. eine Featureinstallation auf einem Remote Server starten, können Sie den Assistenten zum Hinzufügen von Rollen und Features schließen, während die Installation noch läuft, die aktive Aufgabe bleibt jedoch in der **Benachrichtigungs** Liste. Das **Benachrichtigungs** Element zeigt eine Statusanzeige für die Installation an, und Sie können den Assistenten zum Hinzufügen von Rollen und Features bei Bedarf erneut öffnen, indem Sie auf **Assistent zum Hinzufügen von Rollen und Features**klicken. Die Elemente in der Liste informieren Sie darüber, ob eine Installation fehlgeschlagen ist oder zusätzliche Konfigurationsschritte erforderlich sind, um die Bereitstellung des Features abzuschließen.

Benachrichtigungen spielen auch einen wichtigen Teil bei der Behebung von Problemen mit Aufgaben oder Prozessen in Server-Manager. Weitere Informationen zum Verwenden von Nachrichten im **Benachrichtigungs** Bereich und im Dialogfeld **Aufgaben Details** zur Problembehandlung bei fehlgeschlagenen Tasks oder Prozessen finden Sie im [Server-Manager Forum](https://docs.microsoft.com/answers/topics/windows-server-manager.html).

Um eine Benachrichtigung zu löschen, die Sie nicht mehr in der **Benachrichtigungs** Liste anzeigen möchten, zeigen Sie mit dem Mauszeiger auf die Benachrichtigung, und klicken Sie dann auf **Aufgabe entfernen** (**X**).

## <a name="viewing-and-troubleshooting-tasks-by-using-task-details"></a>Anzeigen und Problembehandlung von Aufgaben mithilfe von Aufgaben Details
Der **Task Details** -Befehl unten im **Benachrichtigungs** Menü öffnet das Dialogfeld **Aufgaben Details** , das vollständige Beschreibungen von Aufgaben Ereignissen (starten, beenden, Warnungen, Erfolg oder Fehlern) bereitstellt. Wie bei anderen Listen Steuerelementen in Server-Manager, z. b. **Ereignisse**, **Dienste**und **Best Practices Analyzer** Kacheln, können Sie Abfragen filtern und erstellen, die für die Aufgaben ausgeführt werden, die im Dialogfeld Aufgaben **Details** angezeigt werden. (Weitere Informationen zum Filtern und Erstellen von Abfragen für Listen Steuerelemente finden Sie unter [Filtern, Sortieren und Abfragen von Daten in Server-Manager Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md).) Im oberen Bereich können Sie Benachrichtigungen überprüfen, wie Sie im Menü **Benachrichtigungen** angezeigt werden, und sehen, wie viele Benachrichtigungen zu derselben Aufgabe generiert wurden. Wenn Sie im oberen Bereich eine Benachrichtigung auswählen, werden im unteren Bereich vollständige Details zu der Benachrichtigung angezeigt.

Der untere Bereich ist vor allem bei der Problembehandlung fehlgeschlagener Aufgaben hilfreich. Wenn Server-Manager keine Verbindung mit einem Server herstellen oder Daten für einen Server mit dem Server Pool erhalten kann, enthalten Einträge in diesem Bereich häufig detaillierte Meldungen, darunter den vollständigen Text der zugrunde liegenden Windows-Remote Verwaltung (WinRM), Netzwerk-oder Sicherheitsprobleme, die verhindern, dass Server-Manager mit einem Ziel Server kommunizieren.

## <a name="see-also"></a>Weitere Informationen
[Filtern, Sortieren und Abfragen von Daten in Server-Manager Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md) 
 [Server-Manager Forum](https://docs.microsoft.com/answers/topics/windows-server-manager.html).
