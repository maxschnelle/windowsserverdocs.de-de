<properties pageTitle="Git-Befehlen zum Erstellen eines neuen Artikels oder Aktualisieren eines vorhandenen Artikels" description="Schritte zum Erstellen und aktualisieren einen Artikel in WindowsServerDocs-Pr." metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy Davies" videoId="" scriptId="" manager="dongill" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="08/24/16" ms.author="kathydav" />

# <a name="git-commands-to-create-or-update-an-article"></a>Git-Befehle zum Erstellen oder Aktualisieren eines Artikels

>! HINWEIS: Diesen Befehlen wird vorausgesetzt, Sie haben so konfiguriert, Github, um das Standard-Repository angeben, in dem Sie Dateien aus abrufen. In Github, in dem Sie Dateien von pull-Terminologie ist Ihre *upstream*. Ist, in dem Sie Dateien mithilfe von Push übertragen Ihrer *Ursprung*. Basierend auf unserem Repository und den Workflow wie dienen, Ihrem upstream sollte festgelegt werden unser Repository, handelt es sich unter der Microsoft-Organisation - https://github.com/Microsoft/WindowsServerDocs-pr und Ihres Ursprungs sollte Ihr Fork des diesem Repository in Ihr Github-Konto sein. Beispielsweise ist die Kathy https://github.com/KBDAzure/WindowsServerDocs-pr 

>Um Ihre Einstellungen zu überprüfen, geben Sie ```git config -l```. Sehen Sie sich die URLs, um sicherzustellen, dass sie auf Speicherort zu verweisen, die Sie erstellen wollten.

## <a name="add-or-update-an-article"></a>Hinzufügen oder Aktualisieren eines Artikels

Hier ist eine lokale Verzweigung erstellen, die Änderungen zu speichern und übertragen die Änderungen dann in Ihrem remotefork.

1. Starten Sie Git Bash (oder das Befehlszeilentool für Git verwendeten "").

2. Ändern Sie WindowsServerDocs-Pr:

        cd WindowsServerDocs-pr

3. Es wird empfohlen, behalten Sie Ihre lokalen Master-Branch und dem remote-Master branch in Ihrem Fork synchron mit dem des Repositorys Master Branch. Damit können Sie viele der Frustration, und verlorene Zeit – Sie sind eher Probleme schnell abfangen und halber in einem lauffähigen Zustand geeignete, bekannte. Führen Sie Folgendes aus:

        git checkout master
        git pull upstream master
        git push origin master

4. Nachdem Sie zum Erstellen eines branchs Sie bereit sind arbeiten Ihre täglichen oder lieferleistungen-basierten. Die beste Möglichkeit zum Erstellen eines lokalen arbeitsbranchs aus einem releasebranch ist zum Ausführen:

        git checkout upstream/upstream-branch-name -b your-local-branch-name

   Erstellt den lokalen Branch direkt aus dem upstreambranch, und vermeiden Sie die falschen Dateien in Ihrem neuen lokalen Branch zusammenführen. Um einen arbeitsbranch basierend auf dem Ga-Threshold-Branch zu erstellen, können Sie beispielsweise einen Befehl wie diesen ausführen:
      
        git checkout upstream/master -b working-11-18

   Wenn Sie Inhalt verwenden, die in Branch zusammengeführt werden sollen, die nicht ist         

5. Fügen Sie den lokalen arbeitsbranch auf Ihren Fork:

        git push origin <working branch>

6. Ihre neuen Artikel erstellen oder Änderungen an einem vorhandenen Artikel vornehmen. Verwenden Sie Windows Explorer, um Markdown-Dateien und Ihrem Markdown-Editor zum Erstellen und Bearbeiten von Dateien zu öffnen. Grundlegende Hilfe Formatierung finden Sie in diesem [Artikel](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/) in Github.

7. Hinzufügen von erforderlichen Metadaten und Informationen zu Version, gemäß [Metadaten und produktversionsverwaltung](metadata-OSversioning-and-trademarks.md).

8. Überprüfen Sie Status, fügen Sie hinzu und committen Sie Ihre Änderungen:

        git status

   Überprüfen Sie die Ergebnisse, um sicherzustellen, dass die Dateien aufgeführt sind, die Sie geändert haben. Wenn alle Dateien auf Ihren vorstellungen entsprechen, führen Sie diesen Befehl aus, um alle Dateien hinzuzufügen:

        git add .
        git commit –m "<comment>"

   Nur die Dateien hinzufügen (z. B. wenn ```git status``` Listet Dateien, die Sie nicht senden möchten), müssen Sie stattdessen ausführen:

        git add <file path>
        git commit –m "<comment>"

   >[!IMPORTANT]
   >Der Befehl ```git add .``` fügt alle ausstehende Änderungen, die von gemeldeten ```git status```. Dies bedeutet, dass bei ```git status``` zeigt nicht verfolgte Updates, die Sie nicht hinzufügen möchten, verwenden Sie ```git add <file path>``` stattdessen.  

9. Aktualisieren Sie Ihren lokalen arbeitsbranch mit Änderungen vom upstream ein:

        git pull upstream master

10. Übertragen Sie die Änderungen in Ihren Fork auf GitHub:

        git push origin <working branch>

## <a name="submit-your-changes"></a>Ihre Änderungen senden

Wenn Sie zum Übermitteln Ihrer Inhalte für das Staging, die Überprüfung und/oder die Veröffentlichung bereit sind, verwenden Sie die GitHub-UI, um einen Pull Request zu erstellen. 

Wenn Sie einen Pull Request (PR) öffnen, einen Testdurchlauf löst diese, erstellt das Projekt, und in unserer internen staging-Website veröffentlicht. Es ist in Ordnung, einen Pull Request öffnen, den Sie nicht möchten, zusammengeführt wurden, da es sich handelt, wie Sie einen Testdurchlauf zu erhalten und überprüfen Sie Ihre Änderungen auf die Stagingsite sind. Builddetails und staginglinks sind als Kommentare an dem PR gesendet 

Es ist Ihre Aufgabe die folgenden Schritte **, bevor Sie Fragen, damit die Änderungen zusammengeführt**:
  - Überprüfen Sie erstellen die Details, um sicherzustellen, dass es keine Fehler enthält. 
  - Überprüfen Sie Ihre Änderungen auf die staging-Website.

Nachdem Sie dies getan haben, geben sie entweder:
- Der PR hinzugefügt die Bezeichnung "Ready-to-Merge" \(Klicken Sie auf **Bezeichnungen** oder das Zahnradsymbol rechts neben den kommentarstream tippt, in dem PR passen.)
- Hinzufügen von Ready-to-Merge als Kommentar aus, und Senden von e-Mail an den Alias WSSC Pull Prüfer: Wssc-Pra

Der Pull Request-Prüfer überprüft die Änderungen und der Pull Request akzeptiert, es sei denn, es Probleme oder Fragen gibt. Feedback oder Vorschläge zum Beheben von Problemen werden als Kommentare hinzugefügt. Überprüfen Sie [Qualitätskriterien für Pull request überprüfen](contributor-guide-pr-criteria.md) um zu erfahren, wie erwartet wird.

## <a name="publishing"></a>Publishing

- Artikel werden veröffentlicht, etwa 10:00 Uhr und 15:00 Uhr Pacific Time, Montag bis Freitag. Denken Sie daran, die einem Pull Request-Prüfer muss Zeit zum Lesen und akzeptieren die Änderungen, bevor sie können zusammengeführt werden. Änderungen müssen zusammengeführt werden, um im nächsten geplanten Veröffentlichungszyklus übernommen werden. Wenn Sie einen Artikel veröffentlicht, die für eine bestimmte Veröffentlichung Zyklus benötigen, können Sie einen Pull Request-Prüfer voraus zu wissen. Wenn Ihr Pull Request akzeptiert wird, werden die Änderungen in das Repository zusammengeführt und werden in der nächsten Zeit Veröffentlichung ausführen enthalten sein. Es dauert bis zu 30 Minuten, bis Artikel nach der Veröffentlichung online erscheinen. 
