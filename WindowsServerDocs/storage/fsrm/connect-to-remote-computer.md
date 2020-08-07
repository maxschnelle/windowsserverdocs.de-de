---
title: Verbindung mit einem Remotecomputer herstellen
description: In diesem Artikel wird beschrieben, wie Sie eine Verbindung mit einem Remote Computer herstellen, um Speicherressourcen von Dateiservern zu verwalten Ressourcen-Manager
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a412fcc0e1979ed158f01f6fba17fb6a9c4a20c7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935879"
---
# <a name="connect-to-a-remote-computer"></a>Verbindung mit einem Remotecomputer herstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Zum Verwalten von Speicherressourcen auf einem Remote Computer können Sie vom Datei Server Ressourcen-Manager aus eine Verbindung mit dem Computer herstellen. Wenn Sie verbunden sind, können Sie mit dem Datei Server Ressourcen-Manager Kontingente, Bildschirm Dateien verwalten, Klassifizierungen verwalten, Datei Verwaltungsaufgaben planen und Berichte mit diesen Remote Ressourcen generieren.

> [!Note]
> Datei Server Ressourcen-Manager können Ressourcen auf dem lokalen Computer oder einem Remote Computer verwalten, jedoch nicht beides gleichzeitig.

## <a name="to-connect-to-a-remote-computer-from-file-server-resource-manager"></a>So stellen Sie eine Verbindung mit einem Remote Computer über den Datei Server her Ressourcen-Manager

1.  Klicken Sie unter **Verwaltung**auf **Datei Server Ressourcen-Manager**.

2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Verbindung mit anderem Computer herstellen**.

3.  Klicken Sie im Dialogfeld **Verbindung mit einem anderen Computer herstellen** auf **einen anderen Computer**. Geben Sie dann den Namen des Servers ein, mit dem Sie eine Verbindung herstellen möchten (oder klicken Sie auf **Durchsuchen** , um nach einem Remote Computer zu suchen).

4.  Klicken Sie auf **OK**.

> [!Important]
> Der Befehl **mit einem anderen Computer verbinden** ist nur verfügbar, wenn Sie Datei Server Ressourcen-Manager aus **Verwaltungs Tools**öffnen. Wenn Sie von Server-Manager aus auf Datei Server Ressourcen-Manager zugreifen, ist der Befehl nicht verfügbar.

## <a name="additional-considerations"></a>Weitere Überlegungen

So verwalten Sie Remote Ressourcen mit Datei Server Ressourcen-Manager:

-   Sie müssen auf dem lokalen Computer mit einem Domänen Konto angemeldet sein, das Mitglied der Gruppe " **Administratoren** " auf dem Remote Computer ist.
-   Auf dem Remote Computer muss Windows Server ausgeführt werden, und es muss ein Datei Server Ressourcen-Manager installiert sein.
-   Die Ausnahme für den **Remote Datei Server Ressourcen-Manager Verwaltung** auf dem Remote Computer muss aktiviert sein. Aktivieren Sie diese Ausnahme mithilfe der Windows-Firewall in der Systemsteuerung.

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten von Remotespeicherressourcen](managing-remote-storage-resources.md)