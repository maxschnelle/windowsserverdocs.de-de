---
title: Speicherberichtmanagement
description: In diesem Artikel wird beschrieben, wie Speicher Berichte generiert, geplant und überwacht werden.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a43dbeac08c1cb851df48cb8412343928e07b1d0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957347"
---
# <a name="storage-reports-management"></a>Speicherberichtmanagement

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Im Knoten **Speicher Berichte-Verwaltung** des-Dateiservers Ressourcen-Manager Microsoft<sup>®</sup> Management Console (MMC)-Snap-in können Sie die folgenden Aufgaben ausführen:

-   Planen Sie regelmäßige Speicher Berichte, mit denen Sie Trends bei der Datenträger Verwendung identifizieren können.
-   Monitor versucht, nicht autorisierte Dateien für alle Benutzer oder eine ausgewählte Benutzergruppe zu speichern.
-   Speicher Berichte sofort generieren.

Sie haben unter anderem folgende Möglichkeiten:

-   Planen eines Berichts, der jeden Sonntag um Mitternacht ausgeführt wird und eine Liste mit den Dateien generiert, auf die in den beiden vorherigen Tagen zuletzt zugegriffen wurde. Mit diesen Informationen können Sie die Speicher Aktivität für das Wochenende überwachen und die Server-Betriebszeit planen, die weniger Auswirkungen auf die Benutzer haben, die über das Wochenende eine Verbindung herstellen.
-   Sie können jederzeit einen Bericht ausführen, um alle doppelten Dateien in einem Volume auf einem Server zu identifizieren, damit der Speicherplatz schnell freigegeben werden kann, ohne dass Daten verloren gehen.
-   Ausführen eines Dateien nach Dateigruppe Berichts, um zu ermitteln, wie Speicherressourcen in verschiedenen Dateigruppen segmentiert werden
-   Führen Sie einen Dateien nach Besitzer Bericht aus, um zu analysieren, wie einzelne Benutzer freigegebene Speicherressourcen verwenden.

Dieser Abschnitt schließt folgende Themen ein:

-   [Planen eines Satzes von Berichten](schedule-set-of-reports.md)
-   [Berichte nach Bedarf erstellen](generate-reports-on-demand.md)

> [!Note]
> Um e-Mail-Benachrichtigungen und bestimmte Berichterstattungs Funktionen festzulegen, müssen Sie zunächst die allgemeinen Optionen für den Datei Server Ressourcen-Manager konfigurieren.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


