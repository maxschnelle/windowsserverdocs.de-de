---
title: Bearbeiten eines vorhandenen Windows Server-Artikels mit GitHub und Visual Studio Code
description: Bearbeiten vorhandener Windows Server-bezogener Artikel mithilfe von GitHub und Visual Studio Code als Microsoft-Mitarbeiter.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: d681d2fc2b69898e841932a95738b89515ffb51a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865077"
---
# <a name="edit-an-existing-windows-server-article-using-github-and-visual-studio-code"></a>Bearbeiten eines vorhandenen Windows Server-Artikels mit GitHub und Visual Studio Code

Es gibt zwei separate Standorte, an denen wir technische Inhalte von Windows Server aufbewahren. Einer der Standorte ist Public (Windows Server docs), während die andere privat ist (windowsserverdocs-PR). Von wem Sie den Speicherort, an dem Sie mitwirken, bestimmen:

- **Ich bin ein Microsoft-Mitarbeiter.** Als Microsoft-Mitarbeiter haben Sie Optionen, die auf dem zu tun haben:

    - **Erstellen Sie einen brandneuen Artikel.** Zum Erstellen eines ganz neuen Artikels müssen Sie Ihr GitHub-Konto und die Tools erstellen und einrichten, das Repository "Windows Server docs-PR", verzweigen und Klonen, den remotebranch einrichten, den Artikel erstellen und schließlich einen neuen Pull Request für die Genehmigung und Veröffentlichung erstellen. Diese Anweisungen finden Sie in den Anweisungen im Artikel [Erstellen neuer Windows Server-Artikel mit GitHub und Visual Studio Code](create-new-using-github.md) .

    - **Nehmen Sie große Änderungen an einem vorhandenen Artikel vor.** Wenn Sie wesentliche Änderungen an einem vorhandenen Artikel vornehmen möchten, können Sie die Anweisungen in diesem Artikel befolgen.

    - **Nehmen Sie geringfügige Änderungen an einem vorhandenen Artikel vor.** Wenn Sie kleinere Änderungen an einem vorhandenen Artikel vornehmen möchten, befolgen Sie die Anweisungen im Artikel [Aktualisieren vorhandener Windows Server-Artikel mithilfe eines Webbrowsers und eines GitHub-](github-browser-updates.md) Artikels.

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter, die nicht von Microsoft sind, müssen Sie am öffentlichen Standort mitwirken. Weitere Informationen hierzu finden Sie im Artikel [Beitrag zur technischen Dokumentation zu Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) .

## <a name="switch-your-repo-and-create-a-new-branch"></a>Wechseln Ihres Repository und Erstellen einer neuen Verzweigung

Führen Sie die folgenden Schritte aus, um einen vorhandenen Artikel zu bearbeiten.

### <a name="create-a-new-branch-and-locate-the-file-you-want-to-update"></a>Erstellen Sie einen neuen Branch, und suchen Sie die Datei, die Sie aktualisieren möchten.

Bevor Sie mit der Arbeit an Ihren Inhalten beginnen können, müssen Sie zuerst in das Repository "Windows Server docs-PR" wechseln und dann den zu aktualisierenden Artikel suchen.

#### <a name="to-create-a-new-branch-in-git-bash"></a>So erstellen Sie einen neuen Branch in git bash

- Öffnen Sie git bash, und geben Sie die Befehle (nacheinander) ein:

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >Wir empfehlen Ihnen dringend, ihre Verzweigung etwas offensichtlich und eindeutig zu benennen, damit Sie Sie später wiederfinden können.

    Nachdem die Befehle abgeschlossen sind, befinden Sie sich in der neuen Verzweigung und sind bereit, die Datei zu bearbeiten.

#### <a name="to-locate-your-article-and-make-your-edits"></a>So finden Sie Ihren Artikel und nehmen Ihre Änderungen vor

1. Öffnen Sie Visual Studio Code, navigieren Sie zu **Datei**, wählen Sie **Ordner öffnen**aus, und navigieren Sie dann zum GitHub-Speicherort des Ordners, der den Artikel enthält, den Sie bearbeiten möchten.

2. Wählen Sie im **Explorer** -Bereich die Datei aus.

3. Aktualisieren Sie die Informationen auf der Seite, und wählen Sie dann **Datei** > **Speichern**aus.

### <a name="preview-your-text"></a>Anzeigen einer Vorschau des Texts

Nachdem Sie den Text aktualisiert haben, müssen Sie die Änderungen in der Vorschau anzeigen, um sicherzustellen, dass Sie richtig angezeigt werden

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

Nachdem Sie Ihre Updates abgeschlossen haben, müssen Sie für die Veröffentlichung eine Genehmigung von Ihrem Writer erhalten (einige Zeit hierfür erlauben).

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