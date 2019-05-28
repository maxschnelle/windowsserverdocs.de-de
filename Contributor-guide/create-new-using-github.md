---
title: Erstellen Sie neue Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code
description: 'Vorgehensweise: Erstellen Sie neue Windows Server-bezogenen Artikeln, GitHub und Visual Studio Code als ein Mitarbeiter von Microsoft.'
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d75bf135266a4783ab2617977b344782cea679ef
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624561"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>Erstellen Sie neue Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code

Es gibt zwei verschiedenen Standorten, in dem wir Windows Server technische Inhalte zu halten. Einen der Standorte ist öffentlich (Windowsserverdocs), während die andere privat ist (Windowsserverdocs-Pr). Die Sie bestimmt, welchem Speicherort, die Sie an mitwirken:

- **Ich bin ein Microsoft-Mitarbeiter.** Als Mitarbeiter von Microsoft haben Sie die Optionen, die basierend auf was Sie tun möchten:

    - **Erstellen Sie einen ganz neuen Artikel.** Um einen ganz neuen Artikel erstellen möchten, müssen Sie erstellen und richten Ihre GitHub-Konto und die Tools, Verzweigen und Klonen das Repository Windowsserverdocs-Pr Ihre remotebranch einrichten, erstellen Sie im Artikel und schließlich erstellen Sie einen neuen Pull Request zur Genehmigung und Veröffentlichung. Diese Anweisungen die weiteren Sie Verlauf dieses Artikels aus.

    - **Große Änderungen an einem vorhandenen Artikel vornehmen.** Um wesentliche Änderungen an einem vorhandenen Artikel vornehmen, befolgen Sie die Anweisungen in der [bearbeiten einen vorhandenen Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](edit-existing-using-github.md) Artikel.

    - **Geringfügige Änderungen an einen vorhandenen Artikel vornehmen.** Um kleinere Änderungen an einem vorhandenen Artikel vornehmen möchten, befolgen Sie die Anweisungen in der [Aktualisieren von vorhandenen Windows Server-Artikel, die über einen Webbrowser und GitHub](github-browser-updates.md) Artikel.

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter von nicht-Microsoft müssen Sie sich an den öffentlichen Ort mitwirken. Informationen dazu, wie Sie dies tun, finden Sie unter den [beitragen, technische Dokumentation zu Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) Artikel.

## <a name="prerequisites"></a>Vorraussetzungen

Bevor Sie beginnen können, in das Repository arbeiten, müssen Sie zu erstellen und richten Sie Ihr GitHub-Konto, Einrichten der zweistufigen Überprüfung, und installieren und konfigurieren alle notwendigen Tools. Wenn Sie dies getan haben, können Sie nach unten zum Überspringen der [Abschnitt Repository Forken](#fork-the-repository) dieses Artikels.

1. [Erstellen Sie eine GitHub-Konto und ein Profil](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [Verknüpfen Sie Ihr Konto aus, um Ihr Microsoft-Konto und die Organisationen "Microsoft" und "MicrosoftDocs](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [Zweistufige Überprüfung aktivieren](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [Autorisieren des Buildsystems für den Zugriff auf Ihr GitHub-Konto](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Installieren von Visual Studio Code](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [Installieren von GitHub und die zugehörigen tools](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Installieren Sie das Docs Authoring Pack](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>Richten Sie Ihre eigene Version des Repositorys

Nachdem Sie erstellt und richten Sie Ihre GitHub-Konto und die Tools haben, können Sie eine persönliche Version des Repositorys erstellen. Dies ist, in dem Sie Ihre Branches erstellen und alle Änderungen vornehmen.

### <a name="fork-the-repository"></a>Verzweigen Sie das Repository

Sie benötigen eine lokale Kopie der Quelldateien an, damit Sie aus Ihrem Fork Pull-Anforderungen an das Repository für die Produktion erstellen können.

#### <a name="to-fork-the-repository"></a>Das Repository zu forken

1. Melden Sie sich bei Ihrem GitHub-Konto, und wechseln Sie zu https://github.com/microsoftdocs/windowsserverdocs-pr.

2. Wählen Sie **Fork**.

    ![Schaltfläche zum forken auf der Seite hervorgehoben sind](media/create-new-using-github/fork-button.png)

3. Wählen Sie Ihr GitHub-Konto als Speicherort für die Verzweigung.

    ![Schaltfläche zum forken auf der Seite hervorgehoben sind](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>Klonen Sie das Repository

Sie müssen die Repository-Get eine lokale Kopie des Repositorys auf Ihrem lokalen Gerät klonen.

#### <a name="to-clone-the-repository"></a>Um das Repository Klonen

1. Wechseln Sie zu https://github.com/settings/developers, und wählen Sie dann **persönliche Zugriffstoken** im linken Bereich.

2. Wählen Sie **neues Token generieren**, benennen Sie Ihr Token sinnvolle und eindeutige, wählen Sie alle verfügbaren Bereiche, und wählen Sie dann **Token generieren**.

3. Kopieren Sie das Token, und speichern Sie diese an einem sicheren Ort. Sie benötigen diese für den Rest des Prozesses, und nachdem Sie die Seite verlassen, nicht möglich, Sie zu ihr zurückgelangen.

4. Öffnen Sie einen Git Bash-Befehl aus, und wechseln Sie in Ihrem Repository gespeichert werden sollen. Es wird empfohlen, `C:\users\<your_name>\GitHub`.

5. Geben Sie die folgenden Befehle, die über Ihre jeweiligen Informationen, einzeln nacheinander, Klonen Ihres Repositorys aus, und richten Sie Ihre remotebranches:

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. Führen Sie diesen Befehl aus, um sicherzustellen, dass der Remoteverweise ordnungsgemäß eingerichtet ist:

    `git remote -v`

7. Sie sollten etwa folgende Ausgabe angezeigt:

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    Wenn die remote-Ausgabe wie folgt aussieht, können Sie erneut versuchen nach der ersten Ausführung `git remote remove upstream`.

## <a name="create-a-branch-and-a-new-article"></a>Erstellen Sie einen Branch und ein neuer Artikel

Um einen Artikel zu erstellen, gehen Sie wie folgt vor.

### <a name="create-a-new-branch-and-a-new-file"></a>Erstellen Sie einen neuen Branch und eine neue Datei

Bevor Sie beginnen können, um auf Ihre Inhalte zu arbeiten, müssen Sie einen neuen Branch in Ihrem lokalen Repository erstellen.

#### <a name="to-create-a-new-branch-in-git-bash"></a>Zum Erstellen eines neuen branchs in Git Bash

- Öffnen Sie Git Bash, und geben Sie die Befehle (einzeln):

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >Es wird dringend empfohlen, benennen Ihres branchs klar und eindeutig, damit Sie es später noch Mal gefunden werden können.

    Nachdem die Befehle abgeschlossen haben, Sie werden in Ihren neuen Branch und bereit für die neue Datei erstellen. Sie müssen nur so ändern Sie in das Repository Windowsserverdocs-Pr, jede Instanz von Ihrer Git Bash. Wenn Sie Git Bash schließen, müssen Sie Verzeichnisse wieder ändern, nachdem Sie es öffnen.

#### <a name="to-create-a-new-file-in-your-branch"></a>Um eine neue Datei in Ihrem Branch zu erstellen.

1. Öffnen Sie Windows Explorer, wechseln Sie zu Ihrem GitHub-Verzeichnis, und erstellen Sie eine neue Textdatei, in der Ordnerstruktur. Dem Namen Ihrer Datei muss es sich um alle Kleinbuchstaben und durch Bindestriche getrennt sein. Z. B. _Was-ist-Windows-server.md_.

     Sie müssen auch die Dateierweiterung von .txt zu ändern. Md. Wählen Sie in der Fehlermeldung, die angezeigt wird, **Ja** zum Speichern der Datei mit der neuen Erweiterung.

2. Öffnen Sie Visual Studio Code, und wechseln Sie zu **Datei**Option **"Ordner öffnen"** , und fahren Sie mit der GitHub-Speicherort der Datei, die Sie in Schritt 1 erstellt haben.

3. Von der **Explorer** Bereich, wählen Sie die neue Datei.

4. Fügen Sie den Text auf der Seite hinzu, und wählen Sie dann **Datei** > **speichern**.

### <a name="preview-your-text"></a>Eine Vorschau Ihres Texts

Nachdem Sie den Text auf die neue Datei hinzufügen, müssen Sie eine Vorschau die Änderungen, um sicherzustellen, dass sie ordnungsgemäß angezeigt werden.

#### <a name="to-preview-your-text"></a>Den Text-Vorschau

1. Wählen Sie in Visual Studio Code, entweder von der **Vorschau** Schaltflächen in der oberen rechten Ecke.

    ![Symbol für die Vorschau](media/create-new-using-github/preview-button-full-page.png): Wechselt zu einer ganzseitigen Vorschau Ihrer Inhalte.

    ![Symbol für die Vorschau](media/create-new-using-github/preview-button-side-by-side.png): Öffnet die Seite "Vorschau" neben Ihrer Arbeit-Seite, Seite-an-Seite.

2. Stellen Sie sicher, dass Ihr Artikel aussieht, wie Sie sehen wie erwartet.

    Nachdem Sie sichergestellt, dass sie das richtige Aussehen, können committen Ihrer Änderungen und erstellen eine Pull-Anforderung für die Veröffentlichung.

### <a name="commit-your-changes"></a>Committen Sie Ihrer Änderungen

Wenn Sie, dass der Text das richtige Aussehen sicherstellen, können Sie Ihre Änderungen an der lokalen Version Ihres Repositorys bestätigen.

#### <a name="to-commit-your-changes"></a>Um Ihre Änderungen zu übernehmen.

- Öffnen Sie Git Bash, und geben Sie die Befehle (einzeln nacheinander, entfernen die optionale Tags ein):

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    Die optionale Git-statusbefehls erfahren Sie, welche Dateien als Teil dieser Commit geändert wurden. Die optionale Git pull upstream master ruft Sie die neuesten Inhalte Änderungen aus dem masterbranch MicrosoftDocs Synchronisieren Ihrer lokalen Inhalte mit dem Hauptinhalt der master. Dadurch soll veranschaulicht werden mögliche Zusammenführungskonflikte voraus, damit Sie sie beheben können, bevor Sie an die Pull Request-Phase erhalten.

### <a name="submit-a-pull-request-for-review-and-publication"></a>Senden eines Pull Requests für die Überprüfung und Veröffentlichung

Nachdem Sie Ihren Artikel abgeschlossen haben, müssen Sie die Genehmigung erhalten, aus Ihrem Writer (einige Zeit, bis dies zulassen) für die Veröffentlichung.

#### <a name="to-submit-your-pull-request"></a>Um Ihr Pull Request zu übermitteln.

1. Wechseln Sie zu https://github.com/MicrosoftDocs/windowsserverdocs-pr , und wählen Sie die **Pullanforderungen** Registerkarte.

2. In der **Reviewer** Teil des rechten Bereichs, wählen Sie das Zahnradsymbol, und geben Sie dann die _Windowsservercontent_ Alias zur Überprüfung.

    Ein Mitglied der _Windowsservercontent_ Alias wird Ihre Änderungen zu überprüfen oder Hinzufügen von Kommentaren zu Programmen, die geändert werden müssen, bevor das Zusammenführen von auftreten kann.

3. Typ **#-Sign-off** in den Kommentaren, damit die Reviewer wissen Sie sind Dienstprozessen für Überprüfung und Veröffentlichung. Die **#-Sign-off** Kommentar:

    - Aktualisiert die Bezeichnung für den Pull Request aus **-Not-Merge** zu **Ready-to-Merge**.

    - Können den Alias und Writer, die wissen, dass Sie bereit sind, haben Ihre Inhalte geprüft.

    - Können die Administratoren wissen, dass nach der Genehmigung Ihrer Inhalte bereit, Go live.

    >[!Important]
    >Nachdem Sie die #-Sign-off-Kommentar hinzugefügt haben, ein Mitglied des Teams Windowsservercontent wird Überprüfen Sie den Text und per push zu zeitaufwändig, damit sie mit der nächsten raus werden geplante Live-(10:30 Uhr und 15:30 Uhr an Wochentagen) veröffentlichen.
    >
    >Wenn Sie #-Sign-off als eine letzte Bemerkung zu Ihrem PR nicht hinzufügen, Ihre Inhalte bleiben in der Warteschlange ohne Push zu Master und schließlich Gültigkeitsdauer.

## <a name="related-information"></a>Verwandte Informationen

Weitere Informationen zu GitHub und die Markdown-Sprache finden Sie unter:

### <a name="git-concepts"></a>Git-Konzepte

- [GitHub-Leitfäden-Git-Benutzerhandbuch:-Einführung](https://guides.github.com/introduction/git-handbook/)

- [Führungslinien GitHub-Verzweigung-Projekte](https://guides.github.com/activities/forking/)

- [GitHub Anleitungen: Grundlegendes zu GitHub-Flows](https://guides.github.com/introduction/flow/)

- [Erfahren Sie, Git-Verzweigung](https://learngitbranching.js.org/ (visual lerner geeignet!))

### <a name="markdown"></a>Markdown

- [Unsere interne Markdown-Leitfaden](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [Extern und GitHub-tutorial](https://www.markdowntutorial.com/)
