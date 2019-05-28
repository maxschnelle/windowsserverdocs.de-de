---
title: Bearbeiten Sie vorhandene Windows Server-Artikel, die über einen Webbrowser und GitHub
description: So stellen Sie schnelle Bearbeitungen in der vorhandenen Windows Server-Dokumentation, die über einen Webbrowser und GitHub als Mitarbeiter von Microsoft.
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d4574de7774a43092815a3d154020559c50fdcf9
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624590"
---
# <a name="update-existing-windows-server-articles-using-a-web-browser-and-github"></a>Aktualisieren von vorhandenen Windows Server-Artikel, die über einen Webbrowser und GitHub

Es gibt zwei verschiedenen Standorten, in dem wir Windows Server technische Inhalte zu halten. Einen der Standorte ist öffentlich (Windowsserverdocs), während die andere privat ist (Windowsserverdocs-Pr). Die Sie bestimmt, welchem Speicherort, die Sie an mitwirken:

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter von nicht-Microsoft müssen Sie sich an den öffentlichen Ort mitwirken. Informationen dazu, wie Sie dies tun, finden Sie unter den [Contributing.md](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) Datei.

- **Ich bin ein Microsoft-Mitarbeiter.** Als Mitarbeiter von Microsoft haben Sie die Optionen, die basierend auf was Sie tun möchten:

    - **Erstellen Sie einen ganz neuen Artikel.** Um einen ganz neuen Artikel erstellen möchten, müssen Sie erstellen und richten Ihre GitHub-Konto und die Tools, Verzweigen und Klonen das Repository Windowsserverdocs-Pr Ihre remotebranch einrichten, erstellen Sie im Artikel und schließlich erstellen Sie einen neuen Pull Request zur Genehmigung und Veröffentlichung. Diese Anweisungen finden Sie in der [Erstellen neuer Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](create-new-using-github.md) Artikel.

    - **Große Änderungen an einem vorhandenen Artikel vornehmen.** Um wesentliche Änderungen an einem vorhandenen Artikel vornehmen, befolgen Sie die Anweisungen in der [bearbeiten einen vorhandenen Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](edit-existing-using-github.md) Artikel.

    - **Geringfügige Änderungen an einen vorhandenen Artikel vornehmen.** Um kleinere Änderungen an einen vorhandenen Artikel vornehmen, können Sie die Anweisungen in diesem Artikel befolgen.

    > [!IMPORTANT]
    > Alle Repositorys, die auf docs.microsoft.com veröffentlichen, gilt die [Microsoft Open Source-Verhaltenskodex](https://opensource.microsoft.com/codeofconduct/) oder [.NET Foundation Verhaltenskodex](https://dotnetfoundation.org/code-of-conduct). Weitere Informationen finden Sie unter den [Code von durchführen – häufig gestellte Fragen](https://opensource.microsoft.com/codeofconduct/faq/). Oder wenden Sie sich an [ opencode@microsoft.com ](mailto:opencode@microsoft.com), oder [ conduct@dotnetfoundation.org ](mailto:conduct@dotnetfoundation.org) mit Ihren Fragen oder Kommentaren.
    >
    > Kleinere Korrekturen oder klarstellungen zu Dokumentation und Codebeispielen in öffentlichen Repositorys, unterliegen der [docs.microsoft.com-Nutzungsbestimmungen](https://docs.microsoft.com/legal/termsofuse). Neue oder signifikante Änderungen generieren Sie einen Kommentar im Pull Request, werden Sie aufgefordert, eine online Contribution License Agreement (CLA) zu senden, wenn Sie kein Mitarbeiter von Microsoft sind. Wir benötigen Sie das Onlineformular ausfüllen, bevor wir überprüfen oder Ihr Pull Request annehmen können.

## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>Schnelle Bearbeitungen vorhandener Artikel mithilfe von GitHub und in einem Webbrowser

Schnelle Bearbeitungen optimieren Sie den Vorgang, um zu melden, und beheben kleine Fehler und auslassungen zu finden, in Dokumenten. Trotz aller bemühungen, kleine Grammatik und Rechtschreibfehler _führen_ stellen Sie ihren Weg in die veröffentlichten Dokumente.

1. Wechseln Sie zu https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs.

2. Navigieren Sie im Artikel, die Sie bearbeiten möchten, und wählen Sie dann die **bearbeiten Sie diese Datei** Schaltfläche.

   ![Diese Datei Schaltfläche "Bearbeiten"](media/github-browser-updates/edit-this-file.png)

3. Bearbeiten Sie das Thema, und klicken Sie dann einen Bildlauf nach unten, beschreiben Sie kurz die Änderungen, und wählen **Änderungen**.

    ![Änderungen Sie mit dem Titel der Information](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>Den Pull Request übermitteln

Nachdem Sie Ihren Pull Request erstellt haben, müssen Sie es zur Genehmigung und Veröffentlichung übermitteln.

### <a name="to-submit-your-pull-request"></a>Um Ihr Pull Request zu übermitteln.

1. Auf der **eines Pull Requests** Seite, aktualisieren Sie Ihr Commit-Nachricht, um es für einen PR besser geeignet machen. Zum Beispiel: Korrigieren Sie Tippfehler im ersten Absatz ein.

2. Stellen Sie sicher, dass nur die Commits und die Dateien, die Sie erwarten, eingeschlossen werden sollen, enthalten sind. Aktivieren Sie außerdem, die der PR, der richtige Branch in das upstreamrepository entweder Master (normalerweise) gesendet wird, oder ein releasebranch (gelegentlich).

3. In der **Reviewer** Teil des rechten Bereichs, wählen Sie das Zahnradsymbol, und geben Sie dann _Windowsservercontent_. Ein Mitglied der Alias wird zeigen Sie auf Ihre Änderungen zu überprüfen und entweder zusammenführen, dass Ihre Pull anfordern oder Hinzufügen von Kommentaren zu Aspekten, die vor dem Zusammenführen zu ändern.

4. Wählen Sie **Anforderung zum Erstellen eines Pull**. Der neue Pull Request ist mit Ihrem arbeitsbranch in Ihrem Fork verknüpft. Bis der PR zusammengeführt wird, sind neue Commits, die Sie auf den gleichen arbeitsbranch in Ihrem Fork übertragen automatisch in den PR enthalten Eine neue Bezeichnung wird hinzugefügt, Ihrem Pull Request, die besagt, **-Not-Merge**. Dies bedeutet einfach, dass Ihre Inhalte noch ausgeführt wird und sollte nicht überprüft oder per an der live-Website Push.

5. Wenn Sie für eine Person aus dem Alias, um Ihren Inhalt überprüfen möchten, müssen Sie den Text hinzufügen **#-Sign-off** in den Kommentaren. Dieser Kommentar:

    - Aktualisiert die Bezeichnung für den Pull Request aus **-Not-Merge** zu **Ready-to-Merge**.

    - Können den Alias und Writer, die wissen, dass Sie bereit sind, haben Ihre Inhalte geprüft.

    - Können die Administratoren wissen, dass nach der Genehmigung Ihrer Inhalte bereit, Go live.