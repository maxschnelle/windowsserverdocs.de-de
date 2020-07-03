---
title: Bearbeiten vorhandener Windows Server-Artikel mithilfe eines Webbrowsers und GitHub
description: Erfahren Sie, wie Sie mithilfe eines Webbrowsers und GitHub (als Microsoft-Mitarbeiter) schnell Änderungen an der vorhandenen Windows Server-Dokumentation vornehmen können.
author: eross-msft
ms.author: lizross
ms.date: 07/02/2020
ms.openlocfilehash: 61ceb05b6cb9602faaa4d17b4dc2d978cb571ddb
ms.sourcegitcommit: d754f9e39fc28e4c8768b77bcc9d02ffe2fa6535
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85911229"
---
# <a name="update-existing-windows-server-and-azure-stack-hci-articles-using-a-web-browser-and-github"></a>Aktualisieren vorhandener Windows Server-und Azure Stack HCI-Artikel mithilfe eines Webbrowsers und GitHub

Es gibt zwei separate Standorte, an denen wir technische Inhalte von Windows Server aufbewahren. Einer der Standorte ist Public (Windows Server docs), während die andere privat ist (windowsserverdocs-PR). Von wem Sie den Speicherort, an dem Sie mitwirken, bestimmen:

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter, die nicht von Microsoft sind, müssen Sie am öffentlichen Standort mitwirken. Weitere Informationen hierzu finden Sie in der Datei [Contributing.MD](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) .

- **Ich bin ein Microsoft-Mitarbeiter.** Als Microsoft-Mitarbeiter haben Sie Optionen, die auf dem zu tun haben:

    - **Erstellen Sie einen brandneuen Artikel.** Zum Erstellen eines ganz neuen Artikels müssen Sie Ihr GitHub-Konto und die Tools erstellen und einrichten, das Repository "Windows Server docs-PR", verzweigen und Klonen, den remotebranch einrichten, den Artikel erstellen und schließlich einen neuen Pull Request für die Genehmigung und Veröffentlichung erstellen. Diese Anweisungen finden Sie im Artikel [Erstellen neuer Windows Server-Artikel mit GitHub und Visual Studio Code](create-new-using-github.md) .

    - **Nehmen Sie große Änderungen an einem vorhandenen Artikel vor.** Um wesentliche Änderungen an einem vorhandenen Artikel vorzunehmen, befolgen Sie die Anweisungen im [Artikel Bearbeiten eines vorhandenen Windows-Servers mithilfe von GitHub und Visual Studio Code](edit-existing-using-github.md) .

    - **Nehmen Sie geringfügige Änderungen an einem vorhandenen Artikel vor.** Um geringfügige Änderungen an einem vorhandenen Artikel vorzunehmen, befolgen Sie die Anweisungen in diesem Artikel.

    > [!IMPORTANT]
    > Für alle Repositorys, die Veröffentlichungen auf docs.microsoft.com durchführen, gilt der Verhaltenskodex von [Microsoft Open-Source](https://opensource.microsoft.com/codeofconduct/) oder von [.NET Foundation](https://dotnetfoundation.org/code-of-conduct) (beide in englischer Sprache). Weitere Informationen finden Sie in den [häufig gestellten Fragen zum Verhaltenskodex](https://opensource.microsoft.com/codeofconduct/faq/). Wenden Sie sich mit Ihren Fragen oder Kommentaren alternativ an [opencode@microsoft.com](mailto:opencode@microsoft.com) oder [conduct@dotnetfoundation.org](mailto:conduct@dotnetfoundation.org).
    >
    > Für kleinere Korrekturen oder Klarstellungen zu Dokumentation und Codebeispielen in öffentlichen Repositorys gelten die [Nutzungsbestimmungen zu docs.microsoft.com](https://docs.microsoft.com/legal/termsofuse). Neue oder signifikante Änderungen haben einen Kommentar im Pull Request zur Folge, in dem Sie gebeten werden, online eine Lizenzvereinbarung für Beiträge (Contribution License Agreement, CLA) zu akzeptieren. Dies gilt, wenn Sie kein Mitarbeiter von Microsoft sind. Sie müssen das Onlineformular ausfüllen, damit wir Ihren Pull Request prüfen oder annehmen können.

## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>Schnelles Bearbeiten vorhandener Artikel mithilfe von GitHub und einem Webbrowser

Schnelle Änderungen optimieren das Melden und Beheben von geringfügigen Fehlern und Auslassungen in Dokumenten. Trotz aller Bemühungen kommt es zu _geringfügigen_ Grammatik- und Rechtschreibfehlern in unseren Dokumenten.

1. Befolgen Sie die Anweisungen unter [Einrichten des GitHub-Kontos](https://review.docs.microsoft.com/en-us/help/contribute/contribute-get-started-setup-github?branch=master).

1. Wechseln Sie zum [Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs) -oder [Azure Stack privaten HCI](https://github.com/MicrosoftDocs/azure-stack-docs-pr/tree/master/azure-stack/hci) -Repository. Die privaten Depots werden häufiger überwacht, sodass unsere Genehmigungszeit schneller ist. Sie profitieren von höheren Qualitätsprüfungen und bieten die Möglichkeit, Inhalte in der Stagingumgebung anzuzeigen, wie Sie auf unserer Live Website angezeigt werden.

2. Navigieren Sie zu dem Artikel, den Sie bearbeiten möchten, und wählen Sie dann die Schaltfläche **Diese Datei bearbeiten** aus.

   ![Schaltfläche "diese Datei bearbeiten"](media/github-browser-updates/edit-this-file.png)

3. Bearbeiten Sie das Thema, Scrollen Sie nach unten, beschreiben Sie die Änderungen kurz, und wählen Sie dann **Commit-Änderungen**aus.

    ![Commit für Änderungen mit Titelinformationen übertragen](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>Übermitteln des Pull Request

Nachdem Sie Ihre Pull Request erstellt haben, müssen Sie Sie zur Genehmigung und Veröffentlichung einreichen.

### <a name="to-submit-your-pull-request"></a>So senden Sie Ihre Pull Request

1. Aktualisieren Sie auf der Seite **Pull Request öffnen** die Commit-Nachricht, damit Sie für einen PR besser geeignet ist. Beispiel: Korrigieren von Tippfehler im ersten Absatz.

2. Stellen Sie sicher, dass nur die Commits und Dateien eingeschlossen werden, die erwartet werden. Überprüfen Sie auch, ob der PR in den richtigen Branch im upstreamrepository wechselt, entweder Master (in der Regel) oder ein releasebranch (gelegentlich).

3. Wählen Sie im Bereich **Reviewer** des rechten Bereichs das Zahnrad Symbol aus, und geben Sie dann _windowsservercontent_ein. Ein Member des Alias ist an der Stelle, an der Sie die Änderungen überprüfen und entweder die Pull Request zusammenführen oder Kommentare zu Änderungen hinzufügen, die vor dem Zusammenführen geändert werden müssen.

4. Klicken Sie auf **Pull Request erstellen**. Der neue PR ist mit dem arbeitbranch in Ihrem Fork verknüpft. Bis der PR zusammengeführt wird, werden alle neuen Commits, die Sie per Push an denselben arbeitsbranch in Ihrem Fork überführen, automatisch in den PR eingeschlossen. Dem Pull Request wird eine neue Bezeichnung hinzugefügt, die besagt, dass " **do-not-Merge**" lautet. Dies bedeutet einfach, dass Ihre Inhalte noch in Bearbeitung sind und nicht überprüft oder auf die Live-Website übermittelt werden sollten.

5. Wenn Sie für eine Person des Alias zum Überprüfen Ihres Inhalts bereit sind, müssen Sie den Text hinzufügen, **#Sign** den Kommentaren hinzufügen. Dieser Kommentar:

    - Aktualisiert die Bezeichnung für Ihre Pull Request von " **nicht zusammenführen** " zu " **bereit zum Zusammenführen**".

    - Ermöglicht dem Alias und den Writern, dass Sie bereit sind, ihre Inhalte zu überprüfen.

    - Ermöglicht den Administratoren, dass Ihre Inhalte nach der Genehmigung sofort online geschaltet sind.
