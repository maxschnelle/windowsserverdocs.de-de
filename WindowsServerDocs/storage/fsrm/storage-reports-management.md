---
title: Speicherberichtmanagement
description: Dieser Artikel beschreibt, wie Speicherberichte in regelmäßigen Abständen generiert, geplant und überwacht werden
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 62215aa802e2509be5305aef53069ae9643562f1
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476101"
---
# <a name="storage-reports-management"></a>Speicherberichtmanagement

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Sie können auf dem Knoten **Speicherberichteverwaltung** des Ressourcen-Manager für Dateiserver Microsoft <sup>®</sup> Management Console (MMC)-Snap-Ins folgende Aufgaben ausführen:

-   Planen Sie regelmäßige Speicherberichte, mit denen Sie Trends bei der Datenträgerverwendung identifizieren können.
-   Überwachen Sie Versuche, nicht autorisierte Dateien für alle Anwender oder für ausgewählte Gruppen von Anwendern zu speichern.
-   Generieren Sie umgehend Speicherberichte.

Sie haben u. a. folgende Möglichkeiten:

-   Planen eines Berichts, der jeden Sonntag um Mitternacht ausgeführt wird und eine Liste mit den Dateien generiert, auf die in den beiden vorherigen Tagen zuletzt zugegriffen wurde. Anhand dieser Informationen können Sie Speicheraktivität am Wochenende überwachen und Server-Ausfallzeit mit den weniger Auswirkungen auf Benutzer planen, die von zu Hause aus am Wochenende eine Verbindung herstellen.
-   Führen Sie jederzeit einen Bericht aus, um alle doppelt vorhandenen Dateien eines Volumes auf einem Server zu identifizieren, damit der Festplattenspeicher ohne Verlust von Daten schnell freigegeben werden kann.
-   Führen Sie einen Bericht „Dateien nach Dateigruppe” aus, um zu identifizieren, wie Speicherressourcen zwischen verschiedenen Dateigruppen aufgeteilt sind 
-   Führen Sie einen Bericht „Dateien nach Besitzer” aus, um zu analysieren, wie einzelne Benutzer freigegebene Speicherressourcen verwenden.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Planen eines Satzes von Berichten](schedule-set-of-reports.md)
-   [Berichte nach Bedarf erstellen](generate-reports-on-demand.md)

> [!Note]
> Zum Festlegen von E-Mail-Benachrichtigungen und bestimmten Berichtsfunktionen müssen Sie zuerst die Optionen des Ressourcen-Manager für Dateiserverkonfigurieren konfigurieren.

## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


