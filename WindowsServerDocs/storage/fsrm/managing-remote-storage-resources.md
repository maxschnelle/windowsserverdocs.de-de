---
title: Verwalten von Remotespeicherressourcen
description: In diesem Artikel wird beschrieben, wie Speicherressourcen auf einem Remote Computer verwaltet werden.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8498d55cbdeab609bb3526c9ef884e330148d714
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950634"
---
# <a name="managing-remote-storage-resources"></a>Verwalten von Remotespeicherressourcen

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Zum Verwalten von Speicherressourcen auf einem Remote Computer haben Sie zwei Möglichkeiten:

-   Stellen Sie vom Datei Server Ressourcen-Manager Microsoft<sup>®</sup> Management Console (MMC)-Snap-in eine Verbindung mit dem Remote Computer her (die Sie dann zum Verwalten der Remote Ressourcen verwenden können).
-   Verwenden Sie die Befehlszeilen Tools, die mit Datei Server Ressourcen-Manager installiert werden.

Mit beiden Optionen können Sie Kontingente, Bildschirm Dateien, Klassifizierungen verwalten, Datei Verwaltungsaufgaben planen und Berichte mit diesen Remote Ressourcen generieren.

> [!Note]
> Datei Server Ressourcen-Manager können Ressourcen auf dem lokalen Computer oder einem Remote Computer verwalten, jedoch nicht beides gleichzeitig.

Sie haben unter anderem folgende Möglichkeiten:

-   Stellen Sie über das MMC-Snap-in "Datei Server Ressourcen-Manager" eine Verbindung mit einem anderen Computer in der Domäne her, und überprüfen Sie die Speicherauslastung auf einem Volume oder Ordner auf dem Remote Computer
-   Erstellen Sie Kontingent-und Datei Bildschirm Vorlagen auf einem lokalen Server, und verwenden Sie dann die Befehlszeilen Tools, um diese Vorlagen in einen Dateiserver in einer Zweigstelle zu importieren.

Dieser Abschnitt schließt folgende Themen ein:

-   [Verbindung mit einem Remotecomputer herstellen](connect-to-remote-computer.md)
-   [Befehlszeilentools](command-line-tools.md)
