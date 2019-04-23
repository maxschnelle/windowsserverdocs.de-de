---
title: Verwalten von Remotespeicherressourcen
description: In diesem Artikel wird beschrieben, wie Sie Speicherressourcen einem Remotecomputer verwalten können.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 583c36f399848cf67c6f3a850e62015b224768d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836631"
---
# <a name="managing-remote-storage-resources"></a>Verwalten von Remotespeicherressourcen

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Wenn Sie Speicherressourcen auf einem Remotecomputer verwalten möchten, haben Sie zwei Optionen:

-   Verbinden Sie vom MMC-Snap-In (Microsoft Management Console) des Ressourcen-Managers für Dateiserver<sup>®</sup> aus den Remotecomputer (das Sie anschließend zum Verwalten der Remote-Ressourcen verwenden können).
-   Verwenden Sie die Befehlszeilentools, die auf dem Ressourcen-Manager für Dateiserver installiert sind.

Beide Optionen ermöglichen Ihnen, Kontingente zu verwalten, Dateien zu überprüfen, Klassifizierungen zu verwalten, Dateiverwaltungsaufgaben zu planen und Berichte mit diesen Remote-Ressourcen zu verwalten.

> [!Note]
> Der Ressourcen-Manager für Dateiserver kann Ressourcen auf dem lokalen Computer oder auf einem Remotecomputer verwalten, jedoch nicht gleichzeitig.

Sie haben u. a. folgende Möglichkeiten:

-   Stellen Sie mithilfe des MMC-Snap-In (Microsoft Management Console) des Ressourcen-Managers für Dateiserver eine Verbindung mit einem anderen Computer in der Domäne her und überprüfen Sie die Speichernutzung eines Volume oder eines Ordners auf dem Remotecomputer.
-   Erstellen Sie Kontingent- und Datenprüfungsvorlagen auf einem lokalen Server und verwenden Sie anschließend die Befehlszeilentools, um diese Vorlagen in einem Dateiserver in einer Zweigstelle zu importieren.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Verbinden Sie mit einem Remotecomputer](connect-to-remote-computer.md)
-   [Befehlszeilentools](command-line-tools.md)
