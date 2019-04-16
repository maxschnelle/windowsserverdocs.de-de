---
title: Verbindung mit einem Remotecomputer herstellen
description: "In diesem Artikel wird beschrieben, wie eine Verbindung mit einem Remotecomputer zum Verwalten von Speicherressourcen vom Ressourcen-Manager für Dateiserver hergestellt wird"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 93d2be926437b65ed8eb84a828ea0d7da6a51086
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="connect-to-a-remote-computer"></a>Verbindung mit einem Remotecomputer herstellen 

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um Speicherressourcen von einem Remotecomputer zu verwalten, können Sie vom Ressourcen-Manager für Dateiserver eine Verbindung mit dem Computer herstellen. Während der Verbindung, ermöglicht der Ressourcen-Manager für Dateiserver Kontingente zu verwalten, Dateien zu überprüfen, Klassifizierungen zu verwalten, Dateiverwaltungsaufgaben zu planen und Berichte mit diesen Remote-Ressourcen zu verwalten.

> [!Note]
> Der Ressourcen-Manager für Dateiserver kann Ressourcen auf dem lokalen Computer oder auf einem Remotecomputer verwalten, jedoch nicht gleichzeitig.

## <a name="to-connect-to-a-remote-computer-from-file-server-resource-manager"></a>So stellen Sie eine Verbindung zum Remotecomputer vom Ressourcen-Manager für Dateiserver her

1.  Klicken Sie unter **Verwaltung** auf **Ressourcen-Manager für Dateiserver**.

2.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Verbindung mit anderem Computer herstellen**.

3.  Klicken Sie im Dialogfeld **Verbindung mit anderem Computer herstellen** auf **Anderer Computer**. Geben Sie anschließend den Namen des Servers ein, mit dem Sie eine Verbindung herstellen möchten (oder klicken Sie auf **Durchsuchen**, um nach dem Remotecomputer zu suchen).

4.  Klicken Sie auf **OK**.

> [!Important]
> Der Befehl **Verbindung mit anderem Computer herstellen** ist nur verfügbar, wenn Sie den Ressourcen-Manager für Dateiserver von **Verwaltung** aus öffnen. Wenn Sie den Ressourcen-Manager für Dateiserver vom Server-Manager aus öffnen, ist der Befehl nicht verfügbar.

## <a name="additional-considerations"></a>Weitere Überlegungen

So verwalten Sie Remote-Ressourcen mit dem Ressourcen-Manager für Dateiserver:

-   Sie müssen auf dem lokalen Computer mit einem Domänenkonto, das Mitglied einer lokalen **Administratoren**gruppe ist, angemeldet sein.
-   Auf dem Remotecomputer muss Windows Server ausgeführt werden und der Ressourcen-Manager für Dateiserver muss installiert sein.
-   Die **Remotedateiserver Ressourcen-Manager für Dateiserver**-Ausnahme muss auf dem Remotecomputer aktiviert sein. Aktivieren Sie diese Ausnahme mithilfe von Windows-Firewall in der Systemsteuerung.

## <a name="see-also"></a>Weitere Informationen:

-   [Verwalten von Remotespeicherressourcen](managing-remote-storage-resources.md)