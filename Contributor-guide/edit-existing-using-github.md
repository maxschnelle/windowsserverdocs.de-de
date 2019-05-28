---
title: Bearbeiten Sie einen vorhandenen Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code
description: Wie Sie eine vorhandene, mithilfe von GitHub und Visual Studio Code als Mitarbeiter von Microsoft Windows Server-bezogenen Artikeln zu bearbeiten.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: d2d95cc28089ceb74bf9690f6bd78611e7d9a27a
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624586"
---
# <a name="edit-an-existing-windows-server-article-using-github-and-visual-studio-code"></a>Bearbeiten Sie einen vorhandenen Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code

Es gibt zwei verschiedenen Standorten, in dem wir Windows Server technische Inhalte zu halten. Einen der Standorte ist öffentlich (Windowsserverdocs), während die andere privat ist (Windowsserverdocs-Pr). Die Sie bestimmt, welchem Speicherort, die Sie an mitwirken:

- **Ich bin ein Microsoft-Mitarbeiter.** Als Mitarbeiter von Microsoft haben Sie die Optionen, die basierend auf was Sie tun möchten:

    - **Erstellen Sie einen ganz neuen Artikel.** Um einen ganz neuen Artikel erstellen möchten, müssen Sie erstellen und richten Ihre GitHub-Konto und die Tools, Verzweigen und Klonen das Repository Windowsserverdocs-Pr Ihre remotebranch einrichten, erstellen Sie im Artikel und schließlich erstellen Sie einen neuen Pull Request zur Genehmigung und Veröffentlichung. Diese Anweisungen befolgen Sie die Anweisungen in der [Erstellen neuer Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](create-new-using-github.md) Artikel.

    - **Große Änderungen an einem vorhandenen Artikel vornehmen.** Um wesentliche Änderungen an einem vorhandenen Artikel vornehmen, können Sie die Anweisungen in diesem Artikel befolgen.

    - **Geringfügige Änderungen an einen vorhandenen Artikel vornehmen.** Um kleinere Änderungen an einem vorhandenen Artikel vornehmen möchten, befolgen Sie die Anweisungen in der [Aktualisieren von vorhandenen Windows Server-Artikel, die über einen Webbrowser und GitHub](github-browser-updates.md) Artikel.

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter von nicht-Microsoft müssen Sie sich an den öffentlichen Ort mitwirken. Informationen dazu, wie Sie dies tun, finden Sie unter den [beitragen, technische Dokumentation zu Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) Artikel.

## <a name="switch-your-repo-and-create-a-new-branch"></a>Wechseln Sie Ihr Repository und erstellen einen neuen branch

Um einen vorhandenen Artikel zu bearbeiten, gehen Sie wie folgt vor.

### <a name="create-a-new-branch-and-locate-the-file-you-want-to-update"></a>Erstellen eines neuen Branch aus, und suchen Sie die Datei, die Sie aktualisieren möchten

Bevor Sie beginnen können, um auf Ihre Inhalte zu arbeiten, müssen zuerst auf das Repository Windowsserverdocs-Pr ändern und suchen Sie im Artikel, die, den Sie aktualisieren möchten.

#### <a name="to-create-a-new-branch-in-git-bash"></a>Zum Erstellen eines neuen branchs in Git Bash

- Öffnen Sie Git Bash, und geben Sie die Befehle (einzeln):

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >Es wird dringend empfohlen, benennen Ihres branchs klar und eindeutig, damit Sie es später noch Mal gefunden werden können.

    Nachdem die Befehle abgeschlossen haben, Sie werden in Ihren neuen Branch und bereit für die Datei zu bearbeiten.

#### <a name="to-locate-your-article-and-make-your-edits"></a>Suchen Sie Ihren Artikel, und nehmen Ihre Bearbeitungen vor

1. Öffnen Sie Visual Studio Code, und wechseln Sie zu **Datei**Option **"Ordner öffnen"** , und fahren Sie mit der GitHub-Speicherort des Ordners, der der Artikel enthält, Sie bearbeiten möchten.

2. Von der **Explorer** Bereich, wählen Sie die Datei.

3. Aktualisieren Sie die Informationen auf der Seite, und wählen Sie dann **Datei** > **speichern**.

### <a name="preview-your-text"></a>Eine Vorschau Ihres Texts

Nachdem Sie den Text zu aktualisieren, müssen Sie eine Vorschau die Änderungen, um sicherzustellen, dass sie ordnungsgemäß angezeigt werden.

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

Nachdem Sie Ihre Änderungen abgeschlossen haben, müssen Sie die Genehmigung erhalten, aus Ihrem Writer (einige Zeit, bis dies zulassen) für die Veröffentlichung.

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