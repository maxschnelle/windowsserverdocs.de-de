---
title: Anzeigen von Aufgabendetails und Benachrichtigungen
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95117407-2dd3-4f9a-841f-4331be3544c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44fd23b917d08aad663c0d3fb8da4bebef47783e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831511"
---
# <a name="view-task-details-and-notifications"></a>Anzeigen von Aufgabendetails und Benachrichtigungen

>Gilt für: Windows Server 2016

In Windows Server 2012 R2 oder Windows Server 2012 im Server-Manager beim Ausführen von Verwaltungsaufgaben, z. B. das Hinzufügen von Rollen und Features, Dienste starten, Aktualisieren von Daten, die in der Server-Manager-Konsole angezeigt wird, oder erstellen eine benutzerdefinierte Gruppe von Servern, ein Benachrichtigung wird angezeigt, der **Benachrichtigungen** Bereich des Server-Manager-Konsole Headers. Benachrichtigungen und die **Aufgabe Details** Dialogfeld, das Sie öffnen können die **Benachrichtigungen** Menü, indem Sie auf das Flaggensymbol klicken, zeigt den Status von Benutzeraufgaben oder-Anforderungen, zeigen Ihnen, wenn eine Aufgabe fehlgeschlagen, und hilft Ihnen Beheben Sie Probleme, indem Sie auf detaillierte Fehlermeldungen zu Aufgabenfehlern verwiesen.

## <a name="the-notifications-area"></a>Infobereich
Die **Benachrichtigungen** Bereich in der Menüleiste des Server-Manager durch ein Flaggensymbol gekennzeichnete Zeigt die Ergebnisse von Aufgaben, die Sie im Server-Manager starten. Benachrichtigungen informieren Sie, ob Aufgaben, die Sie im Server-Manager gestartet erfolgreich waren oder fehlgeschlagen sind. Wenn Benachrichtigungen zur Ansicht verfügbar sind, wird die Anzahl verfügbarer Benachrichtigungen neben dem Flaggensymbol angezeigt. Falls eine Aufgabe fehlgeschlagen ist, nur teilweise abgeschlossen werden konnte (wenn sie beispielsweise nicht auf allen gewünschten Remoteservern durchgeführt werden konnte) oder mit Warnungen abgeschlossen wurde, wird die Benachrichtigungsflagge**** rot. Für folgende Aufgaben werden Benachrichtigungen angezeigt.

-   Manuelles Aktualisieren der Daten, die im Server-Manager angezeigt (Benachrichtigungen für automatische Aktualisierungen angezeigt sind nur dann, wenn diese fehlgeschlagen)

-   Starten oder Beenden von Diensten

-   Installieren oder Deinstallieren von Rollen, Rollendienste und features

-   Starten Sie eine Best Practices Analyzer (BPA)-Überprüfung

-   Hinzufügen von Remoteservern für die Verwaltung (Benachrichtigungen werden bei Ausfällen, wenden Sie sich an, oder aktualisieren die Daten, die für Remoteserver angezeigten angezeigt)

Zu den Elementen im Menü **Benachrichtigungen** gehören eine Statusleiste, eine kurze Beschreibung der Aufgabe, der Name des Zielservers für die Aufgabe (oder eines der Zielserver, falls mehrere Zielserver ausgewählt wurden), ggf. ein Link zu einem dazugehörigen Steuerelement oder Dialogfeld und das Menü **Aufgaben** . Das Menü **Aufgaben** zeigt Befehle für die aktive Benachrichtigung an (die Benachrichtigung, über die der Mauszeiger bewegt wird). Wenn Sie beispielsweise einen Dienst beenden, können Sie im Menü **Aufgaben** der Benachrichtigung auf **Neu starten** klicken, um den Dienst neu zu starten.

Benachrichtigungen sind besonders nützlich für das Installieren oder Deinstallieren von Rollen, Rollendienste und Features. Z. B. Wenn Sie eine Featureinstallation auf einem Remoteserver starten, Sie können schließen das Hinzufügen von Rollen und Features-Assistenten während die Installation ist noch nicht die aktive Aufgabe bleibt jedoch in der **Benachrichtigungen** Liste. Die **Benachrichtigungen** zeigt eine Statusanzeige für die Installation, und Sie können Sie die Hinzufügen von Rollen und Features-Assistenten erneut öffnen, falls erforderlich, indem Sie auf **hinzufügen Rollen und Features – Assistent**. Die Elemente in der Liste informieren Sie darüber, ob eine Installation fehlgeschlagen ist oder zusätzliche Konfigurationsschritte erforderlich sind, um die Bereitstellung des Features abzuschließen.

Benachrichtigungen spielen auch einen wichtigen Teil bei der Behandlung von Problemen mit Aufgaben oder Prozesse im Server-Manager. Weitere Informationen zur Verwendung von Nachrichten in der **Benachrichtigungen** Bereich und **Aufgabe Details** Dialogfeld zur Problembehandlung bei fehlgeschlagenen Tasks oder Prozessen finden Sie unter den [Server-Manager Handbuch zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/13443.windows-server-2012-server-manager-troubleshooting-guide-part-i-overview.aspx).

So löschen Sie eine Benachrichtigung, die Sie nicht mehr sehen möchten die **Benachrichtigungen** auflisten, bewegen Sie den Mauszeiger auf die Benachrichtigung, und klicken Sie dann auf **Aufgabe entfernen** (**X**).

## <a name="viewing-and-troubleshooting-tasks-by-using-task-details"></a>Anzeigen und Problembehandlung von Aufgaben mithilfe von Aufgabendetails
Die **Details zum Vorgang** Befehl am Ende der **Benachrichtigungen** Menü geöffnet wird der **Aufgabe Details** Dialogfeld bietet ausführliche Beschreibungen von Aufgabenereignissen (Starten Beenden, Warnungen, Erfolge oder Fehler). Wie bei anderen Listensteuerelementen in Server-Manager, z. B. **Ereignisse**, **Services**, und **Best Practices Analyzer** Kacheln, Sie können filtern und Erstellen von Abfragen für die Aufgaben, die werden angezeigt, der **Aufgabe Details** Dialogfeld. (Weitere Informationen zum Filtern und Erstellen von Abfragen für Listensteuerelemente finden Sie unter [filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md).) Im oberen Bereich können Sie Benachrichtigungen lesen, die im Menü **Benachrichtigungen** angezeigt werden, und sehen, wie viele Benachrichtigungen zu einer Aufgaben generiert wurden. eine Benachrichtigung im oberen Bereich auswählen, werden Einzelheiten zur Benachrichtigung im unteren Bereich zeigt.

Der untere Bereich ist vor allem bei der Problembehandlung fehlgeschlagener Aufgaben hilfreich. Wenn der Server-Manager kann nicht Herstellen einer Verbindung mit oder Abrufen von Daten für einen Server, der ein Member, der zum Serverpool ist, enthalten Einträge in diesem Bereich häufig detaillierte Meldungen, darunter den vollständigen Text der zugrunde liegenden Windows-Remoteverwaltung (WinRM), Netzwerk- oder Sicherheitsprobleme, die Hiermit können verhindern Sie, dass Server-Manager kommuniziert mit einem Zielserver.

## <a name="see-also"></a>Siehe auch
[Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md)
[Server Manager Troubleshooting Guide](https://social.technet.microsoft.com/wiki/contents/articles/13443.windows-server-2012-server-manager-troubleshooting-guide-part-i-overview.aspx)
