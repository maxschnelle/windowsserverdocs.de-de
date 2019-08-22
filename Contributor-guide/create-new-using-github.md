---
title: Erstellen Sie neue Windows Server-Artikel mithilfe von GitHub und Visual Studio Code
description: Erstellen neuer Windows Server-bezogener Artikel mithilfe von GitHub und Visual Studio Code als Microsoft-Mitarbeiter.
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: f5e7e3d0cd17c64175fddaaac73c12daa2c2a32c
ms.sourcegitcommit: ffd9c42374c7448deb5f53f7a865cb427b5e4e9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2019
ms.locfileid: "69887947"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>Erstellen Sie neue Windows Server-Artikel mithilfe von GitHub und Visual Studio Code

Es gibt zwei separate Standorte, an denen wir technische Inhalte von Windows Server aufbewahren. Einer der Standorte ist Public (Windows Server docs), während die andere privat ist (windowsserverdocs-PR). Von wem Sie den Speicherort, an dem Sie mitwirken, bestimmen:

- **Ich bin ein Microsoft-Mitarbeiter.** Als Microsoft-Mitarbeiter haben Sie Optionen, die auf dem zu tun haben:

    - **Erstellen Sie einen brandneuen Artikel.** Zum Erstellen eines ganz neuen Artikels müssen Sie Ihr GitHub-Konto und die Tools erstellen und einrichten, das Repository "Windows Server docs-PR", verzweigen und Klonen, den remotebranch einrichten, den Artikel erstellen und schließlich einen neuen Pull Request für die Genehmigung und Veröffentlichung erstellen. Weitere Informationen finden Sie in diesem Artikel.

    - **Nehmen Sie große Änderungen an einem vorhandenen Artikel vor.** Um wesentliche Änderungen an einem vorhandenen Artikel vorzunehmen, befolgen Sie die Anweisungen im [Artikel Bearbeiten eines vorhandenen Windows-Servers mithilfe von GitHub und Visual Studio Code](edit-existing-using-github.md) .

    - **Nehmen Sie geringfügige Änderungen an einem vorhandenen Artikel vor.** Wenn Sie kleinere Änderungen an einem vorhandenen Artikel vornehmen möchten, befolgen Sie die Anweisungen im Artikel [Aktualisieren vorhandener Windows Server-Artikel mithilfe eines Webbrowsers und eines GitHub-](github-browser-updates.md) Artikels.

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter, die nicht von Microsoft sind, müssen Sie am öffentlichen Standort mitwirken. Weitere Informationen hierzu finden Sie im Artikel [Beitrag zur technischen Dokumentation zu Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) .

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie mit der Arbeit im Repository beginnen können, müssen Sie Ihr GitHub-Konto erstellen und einrichten, die zweistufige Überprüfung einrichten und alle notwendigen Tools installieren und konfigurieren. Wenn Sie dies bereits getan haben, können Sie zum [Abschnitt verzweigen des Repository](#fork-the-repository) in diesem Artikel springen.

1. [Erstellen eines GitHub-Kontos und-Profils](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [Verknüpfen Sie Ihr Konto mit Ihrem Microsoft-Konto und mit den Microsoft-und microsoftdocs-Organisationen.](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [Aktivieren der zweistufigen Überprüfung](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [Autorisieren des Buildsystems für den Zugriff auf Ihr GitHub-Konto](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Installieren von Visual Studio Code](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [Installieren von GitHub und der dazugehörigen Tools](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Installieren des docs Authoring Pack](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>Einrichten Ihrer eigenen Version des Repository

Nachdem Sie Ihr GitHub-Konto und die Tools erstellt und eingerichtet haben, können Sie eine persönliche Version Ihres Repository erstellen. Hier erstellen Sie Ihre branches und nehmen alle Änderungen vor.

### <a name="fork-the-repository"></a>Verzweigen Sie das Repository

Sie benötigen eine lokale Kopie der Quelldateien, damit Sie Pull Requests von ihrer Verzweigung zum produktionsrepository erstellen können.

#### <a name="to-fork-the-repository"></a>So verzweigen Sie das Repository

1. Melden Sie sich bei Ihrem GitHub-Konto an https://github.com/microsoftdocs/windowsserverdocs-pr , und navigieren Sie zu.

2. Wählen Sie **Fork**aus.

    ![Auf Seite hervorgehobene Fork-Schaltfläche](media/create-new-using-github/fork-button.png)

3. Wählen Sie Ihr GitHub-Konto als Verzweigungs Speicherort aus.

    ![Auf Seite hervorgehobene Fork-Schaltfläche](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>Klonen Sie das Repository

Sie müssen das Repository Klonen, um eine lokale Kopie des Repository auf Ihrem lokalen Gerät zu erhalten.

#### <a name="to-clone-the-repository"></a>So Klonen Sie das Repository

1. Wechseln Sie https://github.com/settings/developers zu, und wählen Sie dann im linken Bereich **persönliche Zugriffs Token** aus.

2. Wählen Sie **neues Token generieren**aus, benennen Sie das Token mit einem sinnvollen und eindeutigen Namen, wählen Sie alle verfügbaren Bereiche aus, und wählen Sie dann **Token generieren**aus.

3. Kopieren Sie das Token, und platzieren Sie es an einem sicheren Ort. Sie benötigen dies für den Rest des Prozesses, und nachdem Sie die Seite verlassen haben, können Sie nicht mehr dorthin zurückkehren.

4. Öffnen Sie einen git bash-Befehl, und wechseln Sie in das Verzeichnis, in dem Sie Ihr Repository speichern möchten. Wir empfehlen die Verwendung `C:\users\<your_name>\GitHub`von,.

5. Geben Sie nacheinander die folgenden Befehle ein, um Ihr Repository zu klonen und ihre remotebranches einzurichten:

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. Führen Sie diesen Befehl aus, um sicherzustellen, dass die Remote Einrichtung ordnungsgemäß eingerichtet ist:

    `git remote -v`

7. Ihnen sollte etwa folgende Ausgabe angezeigt werden:

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    Wenn die Remote Ausgabe nicht wie folgt aussieht, können Sie den Vorgang wiederholen, `git remote remove upstream`indem Sie zuerst ausführen.

## <a name="create-a-branch-and-a-new-article"></a>Erstellen einer Verzweigung und eines neuen Artikels

Führen Sie diese Schritte aus, um einen Artikel zu erstellen.

### <a name="create-a-new-branch-and-a-new-file"></a>Erstellen einer neuen Verzweigung und einer neuen Datei

Bevor Sie mit der Arbeit an den Inhalten beginnen können, müssen Sie in Ihrem lokalen Repository einen neuen Branch erstellen.

#### <a name="to-create-a-new-branch-in-git-bash"></a>So erstellen Sie einen neuen Branch in git bash

- Öffnen Sie git bash, und geben Sie die Befehle (nacheinander) ein:

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >Wir empfehlen Ihnen dringend, ihre Verzweigung etwas offensichtlich und eindeutig zu benennen, damit Sie Sie später wiederfinden können.

    Nachdem die Befehle abgeschlossen sind, befinden Sie sich in der neuen Verzweigung und können die neue Datei erstellen. Sie müssen nur einmal pro Instanz von git bash in das Repository "windowsserverdocs-PR" wechseln. Wenn Sie git bash schließen, müssen Sie die Verzeichnisse nach dem Öffnen erneut ändern.

#### <a name="to-create-a-new-file-in-your-branch"></a>So erstellen Sie eine neue Datei in Ihrem Branch

1. Öffnen Sie Windows-Explorer, navigieren Sie zu Ihrem GitHub-Verzeichnis, und erstellen Sie eine neue Textdatei in der Ordnerstruktur. Der Dateiname darf nur aus Kleinbuchstaben bestehen und durch Bindestriche getrennt sein. Beispielsweise _What-is-Windows-Server.MD_.

     Außerdem müssen Sie die Dateierweiterung von ". txt" in ". MD" ändern. Wählen Sie in der angezeigten Fehlermeldung **Ja** aus, um die Datei mit der neuen Dateierweiterung zu speichern.

2. Öffnen Sie Visual Studio Code, navigieren Sie zu **Datei**, wählen Sie **Ordner öffnen**aus, und navigieren Sie dann zum GitHub-Speicherort der Datei, die Sie in Schritt 1 erstellt haben.

3. Wählen Sie im Bereich **Explorer** die neue Datei aus.

4. Fügen Sie den Text der Seite hinzu. Wenn Sie einen neuen Artikel erstellen, stellen Sie sicher, dass Sie [die erforderlichen Metadatentags zu Ihrem Windows Server-bezogenen Artikel hinzufügen](metadata-requirements-for-articles.md).

5. Wählen Sie **Datei** > **Speichern**aus.

### <a name="preview-your-text"></a>Anzeigen einer Vorschau des Texts

Nachdem Sie den Text der neuen Datei hinzugefügt haben, müssen Sie die Änderungen in der Vorschau anzeigen, um sicherzustellen, dass Sie richtig angezeigt werden.

#### <a name="to-preview-your-text"></a>So sehen Sie eine Vorschau des Texts

1. Wählen Sie in Visual Studio Code eine der **Vorschau** Schaltflächen in der oberen rechten Ecke aus.

    ![Symbol "Vorschau"](media/create-new-using-github/preview-button-full-page.png): Wechselt zu einer vollständigen Vorschau Ihrer Inhalte.

    ![Symbol "Vorschau"](media/create-new-using-github/preview-button-side-by-side.png): Öffnet die Vorschau Seite neben ihrer Arbeitsseite nebeneinander.

2. Stellen Sie sicher, dass Ihr Artikel aussieht, wie Sie es erwarten.

    Nachdem Sie sicher sind, dass Sie richtig aussieht, können Sie Ihre Änderungen übertragen und einen Pull Request für die Veröffentlichung erstellen.

### <a name="commit-your-changes"></a>Commit für Ihre Änderungen

Nachdem Sie sichergestellt haben, dass Ihr Text richtig aussieht, können Sie Ihre Änderungen auf Ihre lokale Version Ihres Repository übertragen.

#### <a name="to-commit-your-changes"></a>So übertragen Sie die Änderungen

- Öffnen Sie git bash, und geben Sie die Befehle ein (jeweils nacheinander, und entfernen Sie die optionalen Tags):

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    Der optionale Befehl git-Status zeigt an, welche Dateien im Rahmen dieses Commit geändert wurden. Der optionale git Pull Upstream-Master Ruft die neuesten Inhalts Änderungen aus der microsoftdocs-masterb Ranch ab und synchronisiert Ihren lokalen Inhalt mit dem primären Master Inhalt. Auf diese Weise können Sie potenzielle Mergekonflikte im Voraus anzeigen, damit Sie Sie beheben können, bevor Sie zur PR-Phase gelangen.

### <a name="submit-a-pull-request-for-review-and-publication"></a>Übermitteln eines Pull Request zur Überprüfung und Veröffentlichung

Nachdem Sie den Artikel abgeschlossen haben, müssen Sie für die Veröffentlichung eine Genehmigung von Ihrem Writer erhalten (einige Zeit hierfür erlauben).

#### <a name="to-submit-your-pull-request"></a>So senden Sie Ihre Pull Request

1. Wechseln Sie https://github.com/MicrosoftDocs/windowsserverdocs-pr zu, und wählen Sie die Registerkarte **Pull Requests** aus.

2. Wählen Sie im Bereich **Reviewer** des rechten Bereichs das Zahnrad Symbol aus, und geben Sie dann den _Windows Server Content_ -Alias für Review ein.

    Ein Mitglied des Alias _Windows Server Content_ überprüft Ihre Änderungen oder fügt Kommentare zu Dingen hinzu, die vor dem Zusammenführen geändert werden müssen.

3. Geben Sie **#Sign-Off** in die Kommentare ein, damit die Reviewer wissen, dass Sie sowohl für die Überprüfung als auch für die Veröffentlichung ausgeben. Der **#Sign** Kommentar:

    - Aktualisiert die Bezeichnung für Ihre Pull Request von " **nicht zusammenführen** " zu " **bereit zum Zusammenführen**".

    - Ermöglicht dem Alias und den Writern, dass Sie bereit sind, ihre Inhalte zu überprüfen.

    - Ermöglicht den Administratoren, dass Ihre Inhalte nach der Genehmigung sofort online geschaltet sind.

    >[!Important]
    >Nachdem Sie den #Sign Kommentar hinzugefügt haben, prüft ein Mitglied des Windows Server Content-Teams den Text und überträgt ihn an den Master, damit er mit der nächsten geplanten Veröffentlichung in Live (10:30 Uhr und 3:30Uhr Wochentage) fortgesetzt wird.
    >
    >Wenn Sie Ihrem PR nicht als Abschließender Kommentar #Sign hinzufügen, verbleiben Ihre Inhalte in der Warteschlange, ohne dass Sie per Pushvorgang an den Master übertragen werden.

## <a name="related-information"></a>Verwandte Informationen

Weitere Informationen zu GitHub und der markdown-Sprache finden Sie unter:

### <a name="git-concepts"></a>Git-Konzepte

- [GitHub-Leitfäden: git-Handbuch Intro](https://guides.github.com/introduction/git-handbook/)

- [GitHub-Leitfäden: Forking-Projekte](https://guides.github.com/activities/forking/)

- [GitHub-Leitfäden: Grundlegendes zum GitHub-Flow](https://guides.github.com/introduction/flow/)

- [Erlernen von git-Verzweigungen] (https://learngitbranching.js.org/ (Hervorragend für visuelle Lernmodule!))

### <a name="markdown"></a>Markdown

- [Unsere interne markdown-Anleitung](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [Externes, GitHub-Tutorial](https://www.markdowntutorial.com/)
