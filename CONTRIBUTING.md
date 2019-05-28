# <a name="contributing-to-windows-server-technical-documentation"></a>Mitwirkung an der technischen Windows Server-Dokumentation

Vielen Dank für Ihr Interesse an der Windows Server Technische Dokumentation! Wir freuen uns über Ihr Feedback, Änderungen und Ergänzungen unserer Dokumente. Es gibt zwei verschiedenen Standorten, in dem wir Windows Server technische Inhalte zu halten. Einen der Standorte ist öffentlich (Windowsserverdocs), während die andere privat ist (Windowsserverdocs-Pr). Die Sie bestimmt, welchem Speicherort, die Sie an mitwirken:

- **Ich bin kein Microsoft-Mitarbeiter.** Als Mitarbeiter von nicht-Microsoft müssen Sie sich an den öffentlichen Ort mitwirken. Informationen dazu, wie Sie dies tun weiteren Sie Verlauf dieses Artikels.

- **Ich bin ein Microsoft-Mitarbeiter.** Als Mitarbeiter von Microsoft haben Sie die Optionen, die basierend auf was Sie tun möchten:

    - **Erstellen Sie einen ganz neuen Artikel.** Um einen ganz neuen Artikel erstellen möchten, müssen Sie erstellen und richten Ihre GitHub-Konto und die Tools, Verzweigen und Klonen das Repository Windowsserverdocs-Pr Ihre remotebranch einrichten, erstellen Sie im Artikel und schließlich erstellen Sie einen neuen Pull Request zur Genehmigung und Veröffentlichung. Diese Anweisungen finden Sie in der [Erstellen neuer Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/create-new-using-github.md) Artikel.

    - **Große Änderungen an einem vorhandenen Artikel vornehmen.** Um wesentliche Änderungen an einem vorhandenen Artikel vornehmen, befolgen Sie die Anweisungen in der [bearbeiten einen vorhandenen Windows Server-Artikel, die mithilfe von GitHub und Visual Studio Code](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/edit-existing-using-github.md) Artikel.

    - **Geringfügige Änderungen an einen vorhandenen Artikel vornehmen.** Um kleinere Änderungen an einem vorhandenen Artikel vornehmen möchten, befolgen Sie die Anweisungen in der [Aktualisieren von vorhandenen Windows Server-Artikel, die über einen Webbrowser und GitHub](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/github-browser-updates.md) Artikel.

## <a name="sign-a-cla"></a>Unterzeichnen einer CLA

Alle Mitwirkenden, die ***nicht*** muss ein Microsoft-Mitarbeiter [signieren Sie eine Microsoft Contribution Licensing Agreement (CLA)](https://cla.microsoft.com/) vor der Bearbeitung alle Microsoft-Repositorys. Wenn Sie bereits in der Microsoft-Repositorys in der Vergangenheit Herzlichen Glückwunsch bearbeitet haben.
Sie haben diesen Schritt bereits abgeschlossen.

## <a name="editing-topics"></a>Bearbeiten von Themen

Wir haben versucht, damit die Bearbeitung einer vorhandenen, öffentlichen Datei, die so einfach wie möglich.

### <a name="to-edit-a-topic"></a>So bearbeiten Sie ein Thema

1. Wechseln Sie zur Seite https://docs.microsoft.com/windows-server , die Sie verwenden möchten, aktualisieren, und wählen Sie dann **bearbeiten**.

    ![GitHub-Web, mit dem Link "Bearbeiten"](media/contribute-link.png)

2. Melden Sie sich bei (oder registrieren Sie sich für) ein GitHub-Konto.

    Sie benötigen ein GitHub-Konto, um die Seite zu erhalten, die Sie ein Thema bearbeiten können.

3. Wählen Sie die **Zeichenstift** Symbol (in Rot), den Inhalt bearbeiten.

    ![GitHub-Web, mit dem Stiftsymbol Rot](media/pencil-icon.png)

4. Stellen Sie mithilfe von Markdown-Sprache, die Änderungen an das Thema. Informationen zum Bearbeiten von Inhalten mit Markdown, finden Sie unter:

    - **Wenn Sie mit der Microsoft-Organisation in GitHub verknüpft sind:** [Handbuch für Windows Server-Mitwirkender](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/Contributor-guide)

    - **Wenn Sie außerhalb von Microsoft sind:** [Verwenden von Markdown](https://guides.github.com/features/mastering-markdown/)

5. Stellen Sie die vorgeschlagene Änderung, und wählen Sie dann **Vorschau der Änderungen** um sicherzustellen, dass sie korrekt aussieht.

    ![GitHub-Web, mit der Registerkarte "Vorschau der Änderungen"](media/preview-changes.png)

6. Wenn Sie fertig sind bearbeiten das Thema, führen Sie einen Bildlauf zum unteren Rand der Seite Geben Sie einen beschreibenden Namen für Ihren Fork, und klicken Sie dann auf **dateiänderung vorschlagen** die Verzweigung in Ihrem persönlichen GitHub-Konto erstellen.

    ![GitHub-Web, mit der Schaltfläche "Datei-Änderung vorschlagen"](media/propose-file-change.png)

    Die **Änderungen vergleichen** angezeigt wird, um festzustellen, was die Änderungen zwischen Ihrer Verzweigung und den ursprünglichen Inhalt sind.

7. Auf der **Änderungen vergleichen** Bildschirm wird angezeigt, wenn Probleme mit der Datei, die Sie einchecken.

    Wenn keine Probleme vorhanden sind, sehen Sie die Nachricht **Möglichkeit zum Zusammenführen**.

    ![GitHub-Web, Bildschirm wechselt das Vergleichen mit](media/compare-changes.png)

8. Wählen Sie **Anforderung zum Erstellen eines Pull**.

    Pull-Anforderungen können Sie Erzählen Sie andere Änderungen, die Sie die in einen Branch in einem Repository auf GitHub abgelegt haben. Nachdem ein Pull Request geöffnet wurde, können Sie diskutieren und überprüfen Sie die potenziellen Änderungen mit Mitarbeitern und zur nachverfolgung Commits hinzufügen, bevor die Änderungen in der basisverzweigung zusammengeführt werden. Weitere Informationen finden Sie unter [zu Pull Requests](https://help.github.com/articles/about-pull-requests)

9. Geben Sie einen Titel und Beschreibung der genehmigenden Person geben Sie den geeigneten Kontext zu den Neuigkeiten in der Anforderung.

10. Führen Sie einen Bildlauf zum unteren Rand der Seite, um sicherzustellen, dass nur die geänderten Dateien in diesem Pull Request befinden. Andernfalls können Sie Änderungen von anderen Personen, überschreiben.

11. Wählen Sie **Anforderung zum Erstellen eines Pull** erneut aus, um die tatsächlich den Pull Request zu übermitteln.

    Der Pull Request wird in den Writer des Themas gesendet, und Ihre Änderungen werden überprüft. Wenn Ihre Anforderung akzeptiert wird, werden Ihre Updates veröffentlicht.

## <a name="resources"></a>Ressourcen

- Sie können Ihren bevorzugten Texteditor verwenden, zum Bearbeiten von Markdown. Es wird empfohlen [Visual Studio Code](https://code.visualstudio.com/), ein kostenloses lightweight-open-Source-Editor von Microsoft.