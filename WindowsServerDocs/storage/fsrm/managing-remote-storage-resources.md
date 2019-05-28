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
ms.openlocfilehash: 29870c33e17c75fe25601237d7de47302662d21f
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476166"
---
# <a name="managing-remote-storage-resources"></a>Verwalten von Remotespeicherressourcen

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

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

-   [Verbindung mit einem Remotecomputer herstellen](connect-to-remote-computer.md)
-   [Befehlszeilentools](command-line-tools.md)
