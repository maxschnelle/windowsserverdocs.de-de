# <a name="rename-or-delete-an-article"></a>Umbenennen oder Löschen eines Artikels

Bevor Sie Sie umbenennen oder Löschen eines Artikels, müssen Sie folgen diesen Vorgang, um zu vermeiden oder reduzieren Sie die Anzahl fehlerhafter links. Kunden ungern auf fehlerhafte Links und nicht über klingende deaktiviert bei einem Treffer dabei. Beachten Sie, dass das Umbenennen oder Löschen eines Artikels der letzte Schritt bei diesem Vorgang wird nicht das erste.


## <a name="step-1-manage-inbound-links"></a>Schritt 1: Verwalten Sie eingehende links

Bestimmen Sie, ob alle eingehenden nicht-Microsoft-Links auf Inhalte, z. B. Blogs, Foren und andere Inhalte im Web. Wenden Sie sich an der Blogbesitzer aus, um diesen Links, ändern und entfernen oder aktualisieren Sie Links aus Beiträge im Forum. Web-Analysetools können eingehende Links von hohem Datenverkehr zu identifizieren, die Sie möglicherweise auf diese Weise verwalten müssen.

## <a name="step-2-remove-all-crosslinks-to-the-article-from-the-windowsserverdocs-pr-repository"></a>Schritt 2: Entfernen Sie alle querlinks im Artikel aus dem Repository WindowsServerDocs-pr

1. Aktualisieren Sie Ihren lokalen Branch – führen Sie `git pull upstream <branch>`, d. h. um aus dem masterbranch zu aktualisieren, führen Sie `git pull upstream master`

2.  Überprüfen Sie den Ordner WindowsServerDocs-Pr, um nach Artikeln zu suchen, die einen Link zum Artikel, die Sie umbenennen oder außer Kraft setzen möchten, und aktualisieren Sie die Artikel, um die Links zu entfernen oder Ersetzen Sie sie mit Links zu einem anderen Artikel. Sie können eine Suche verwenden, und ersetzen die Hilfsprogramm aus, um die querlinks zu ermitteln, ob Sie installiert haben. Wenn Sie dies nicht tun, können Sie Windows PowerShell verwenden:

 a. Starten Sie Windows PowerShell.

 b. Ändern Sie an der PowerShell-Eingabeaufforderung in den Ordner "WindowsServerDocs-Pr":

 `cd WindowsServerDocs-pr\WindowsServerDocs-pr`

 c. Führen Sie einen Befehl aus, um alle Dateien aufgeführt, die enthalten einen Link zum Artikel umbenennen oder löschen:

 `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name`

  Um die Liste der Dateinamen in eine Textdatei (in diesem Fall mit dem Namen psoutput.txt) zu senden, führen Sie Folgendes aus:

  `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name | Out-File C:\Users\<your account>\psoutput.txt`

3. Hinzufügen und committen Sie alle Ihre Änderungen per push an Ihre Verzweigung und eines Pull Requests. Anweisungen hierzu finden Sie unter [Git-Befehle zum Erstellen oder Aktualisieren eines Artikels](git-steps-create-update-content.md).

## <a name="step-3-update-fwlinks"></a>Schritt 3: Aktualisieren Sie FWLinks

Überprüfen Sie das Tool FWLink alle FWLinks, die im Artikel zu verweisen. Zeigen Sie alle FWLinks an den ersetzenden Inhalt; Wenn Sie nicht auf den Alias, die den Link besitzt sind, verknüpfen Sie es. Wenn die Besitzer den Link wird nicht aktualisiert werden, ein supportticket MSCOM auf den Link geändert haben. Weitere Informationen – [interne Wiki](http://sharepoint/sites/azurecontentguidance/wiki/Pages/Manage%20inbound%20links%20to%20retired%20topics.aspx).

## <a name="step-4-remove-crosslinks-to-the-article-from-table-of-contents"></a>Schritt 4: Entfernen Sie im Artikel Querverbindungen Inhaltsverzeichnis

Arbeiten Sie mit die Person, die die ToC.md-Datei verwaltet. Diese Datei wird aufgefüllt, die Links im Inhaltsverzeichnis in der technischen Bibliothek. Wenn Sie nicht, dass wer der Ansprechpartner wissen, senden eine e-Mail an wssc-pra@microsoft.com.

## <a name="step-5-add-redirects"></a>Schritt 5: Hinzufügen von umleitungen
Wenn beim Löschen einer Datei oder umbenannt haben, fügen Sie eine Umleitung, sodass vorhandene Links nicht unterbrochen:

1. Lassen Sie die alte Datei am bestehenden Speicherort mit dem Namen der vorhandenen Datei.
2. Ersetzen Sie den Inhalt der Datei mit diesem Teil der Metadaten:
   ```
   ---
   redirect_url: <redirection-URL-or-file>
   ---
   ```
   \<umleitungs-URL-oder-File > ist die vollständige URL zu einem anderen Speicherort oder der Pfad + Dateiname, der einem anderen Thema in der gleichen OPS-Repositorys.

   Beispiel: wäre dies die gesamte Datei:

   ```
   ---
   redirect_url: ../../failover-clustering/whats-new-in-failover-clustering
   ---
   ```

3. Nach dem Erstellen eines Pull Requests für die Umleitung, klicken Sie auf die können Sie die Links in die Kommentare für Pull Request - Wenn die Umleitung, Sie funktioniert sich an das Zielthema.

## <a name="step-6-rename-or-delete-the-article"></a>Schritt 6: Umbenennen Sie oder löschen Sie den Artikel

Wenn Sie eine Umleitung nicht verwenden, führen Sie diesen Schritt aus, nachdem Sie die vorherigen Schritte abgeschlossen haben, und alle betroffenen Artikel veröffentlicht. Wenn Sie eine Umleitung verwenden, würde umbenennen oder löschen den Artikel dies rückgängig zu machen und verursachen einen fehlerhaften Link. Umbenennen einer Datei, benennen Sie sie einfach im Dateisystem, und klicken Sie dann hinzufügen, commit und push von der Änderung, und öffnen Sie dann einen Pull Request.
Um eine Datei zu löschen, müssen Sie zuerst wissen, dass es nicht funktioniert, um nur eine Datei aus dem Dateisystem gelöscht werden, da dies ein Quellcodeverwaltungssystem ist und muss man dazu vorgesehen. Andernfalls werden die gelöschten Dateien möglicherweise erneut angezeigt.
Es gibt zwei Möglichkeiten zur Verfügung:

- "Dateisystem" und "Git": Löschen Sie die Datei aus dem Dateisystem. Führen Sie dann Ihre Git-Clienttool, einen der folgenden  ```Git add -A``` | ```Git add --all``` | ```Git add -u```
- Nur Git:   Ausführen von ```git rm foo.md```

    Weitere Informationen [ http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo ](http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo) und [https://git-scm.com/docs/git-rm](https://git-scm.com/docs/git-rm) 

## <a name="step-7-find-and-fix-straggler-broken-links"></a>Schritt 7: Suchen und Beheben von Straggler fehlerhaften links

Verwenden Sie das Content QA-Tool, um auf fehlerhafte Links zu die vorherigen Schritten nicht abfangen, und klicken Sie dann entfernen oder korrigieren Sie die Links zu finden.

## <a name="step-8-remove-cached-pages-from-search-engines"></a>Schritt 8: Entfernen von zwischengespeicherten Seiten über Suchmaschinen

Wechseln Sie zu diesen Webseiten zwischengespeicherte Webseiten über Suchmaschinen zu entfernen: [Bing](https://www.bing.com/webmaster/tools/content-removal?rflid=1)
[Google](https://www.google.com/webmasters/tools/removals?pli=1)


### <a name="contributors-guide-links"></a>Links im Leitfaden Mitwirkende

- [Index der Artikel mit Hinweisen](./contributor-guide-index.md)

