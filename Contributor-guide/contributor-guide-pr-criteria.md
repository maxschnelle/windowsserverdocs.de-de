# <a name="quality-criteria-for-pull-request-review"></a>Qualitätskriterien für Pull Request überprüfen

Pull-Anforderungen erfüllt die minimale Kriterien für die Integration in das Repository akzeptiert werden. Pull Request-Prüfer prüfen in der Regel nur was neu eingeführt oder geändert wird, verwenden die Blockierung ist und nicht blockierend Qualität Review-Elemente aufgeführt, die in diesem Artikel, um die Änderungen zu bewerten. Prüfer unter Umständen für Weitere Informationen oder ein anforderer, Probleme zu beheben, bevor er akzeptiert einen Pull Request erforderlich. Der anforderer ist verantwortlich für die Änderungen vorgenommen wurden.

>[!IMPORTANT] 
>Öffnen eine Pull-Anforderung löst Prüfungen der Datenqualität und Veröffentlichung an unserer internen staging-Website aus. Es liegt in Ihrer Verantwortung, sowohl über Links in Kommentaren überprüfen \(klicken Sie auf der Registerkarte "Unterhaltung" des Pull Requests, **zeigen alle Überprüfungen** > **Details**\). Nachdem Sie dies getan haben, geben Sie es durch Hinzufügen der **"Ready-to-Merge"** Bezeichnung, die dem PR passen. \(Klicken Sie auf **Bezeichnungen** oder das Zahnrad rechts neben den kommentarstream tippt, in dem PR passen.) Wenn Sie die Bezeichnung hinzufügen können \(stammen Mitwirkende gemeldet, die dies) Pull Request "Ready-to-Merge" einen Kommentar hinzu, und Senden von e-Mail-Adresse an des Bearbeiters Alias wssc-pra@microsoft.com.

## <a name="blocking-content-quality-items"></a>Blockierende inhaltsqualitätselemente

Die Updates müssen zusammengeführt werden die folgenden Kriterien entsprechen.

| Kategorie | Qualitätsprüfelement |
|----------|---------------------|
|Vorraussetzungen| Der Pull Request hat keine:<br>-Validierungsfehler und-Warnungen<br>-Konflikte zusammenführen<br>-offensichtlichen inhaltsregressionen<br>-eingebetteten Repositorys oder ungewöhnlichen, zusätzliche Dateien|
|Integrität des Repositorys |Pull Request enthält maximal 100 geänderte Dateien, es sei denn, einen releasebranch aus dem Master- oder Ausführen eines Massenupdates ähnlich, wie eine Korrektur Metadaten aktualisiert wird. (Tatsächlich sollte enthalten, ein Pull Request weitaus weniger als, aber nach 100 geänderte Dateien, nicht GitHub die Unterschiede angezeigt).|
|Integrität des Repositorys| Pull-Anforderung wird nicht von der Person zusammengeführt, die den Pull Request erstellt hat.|
|Benennung |Führen Sie die Dateinamen für neue Dateien die [dateibenennungsrichtlinien](file-names-and-locations.md).|
|Benennung |Neue Ordner im Repository eingefügt wurden, gehen Sie vor der [ordnerbenennungsrichtlinien](file-names-and-locations.md#folder-names-in-the-repo).|
|Benennen von SEO /|Die H1-Überschrift verfügt über genügend Informationen, um den Inhalt des Artikels, die zur Unterscheidung von anderen Artikeln, und eine Zuordnung mit wahrscheinlichen kundenschlüsselwörtern zu beschreiben. Z. B. erfüllen keine H1-Überschrift von "Übersicht" diese Kriterien.|
|Content|Es wird kein technisches Dokument darstellt. Finden Sie unter den [zuweisungsleitfaden Anleitungen](content-channel-guidance.md).|
|Content|Enthält einen einleitungsabsatz und einen Text Verfahren oder Konzept des Inhalts. Es verfügt über genügend Inhalte an seine eigene als Artikel stehen auf und wird nicht von einem kleinen informationsfragment.|
|Content| Es gelten standardformatierung und inhaltsdesign: Elemente, die nummerierte Listen sein sollen, sind nummeriert, Elemente, die unsortierte Listen sein sollen, werden aufgezählt. Dies ist die grundlegende Nutzbarkeit inbegriffen.|
|Content| Es wurde keine ungewöhnlichen Grafiken, informationsarchitekturen oder Strukturen oder offensichtlich nicht dem standard entsprechende Entwürfe.|
|Website-/designfunktionalität| Der Artikel keine manuell erstellte Inhaltsverzeichnis in den Inhalten. Der Artikel muss H2s für seine Inhaltsverzeichnis auf der Seite verwenden.|
|Website-/designfunktionalität| Wenn H2-Überschriften verwendet werden, sind mindestens zwei. Alle H3 Mal "Kopf" wird eine Überschrift "H2" vorangestellt. Mit einer Überschrift "H2" klicken, wird ein artikelinhaltsverzeichnis mit einzelnen Element erstellt. Verwenden Sie eine H2-Überschriften, bevor Sie eine Überschrift "H3", um sicherzustellen, dass ein Inhaltsverzeichnis erstellt werden kann.|
|Markdown| Artikel enthält keine HTML-Codeblöcke; kleinere Inline-HTML ist zulässig, z. B. hochgestellte, tiefgestellte, Sonderzeichen und andere geringfügige Formatierungen, die Markdown nicht unterstützt –. HTML-Tabellen sind nur zulässig, wenn die Tabelle enthält die Liste mit Aufzählungszeichen oder nummerierte Listen, sondern, dass in der Regel gibt an, dass der Inhalt vereinfacht werden kann, damit es in Markdown codiert werden kann.|
|Markdown   |Benutzerdefinierte Markdown-Elemente werden verwendet. Beispiel: Anmerkungen zu dieser codiert werden das! Beachten Sie-Erweiterung nicht als nur-Text.|
|Abbilder|Bilder enthalten Alternativtext. **Dies ist eine Voraussetzung Barrierefreiheit, die als Teil des Freigabekriterien erfüllt werden müssen.** [Hier](https://worldready.cloudapp.net/Styleguide/Read?id=2665&topicid=28349). |
|Abbilder |Animierte GIF-Dateien werden in das Repository nicht akzeptiert.|
|Abbilder | Bilder weisen eine hohe Auflösung, falsch geschriebene Wörter und enthalten keine privaten Informationen [finden Sie im Leitfaden zu Bildern](https://github.com/Azure/azure-content/blob/master/contributor-guide/create-images-markdown.md). |
|Wird bereitgestellt| Der Artikel hat wurde in der Vorschau angezeigten Staging und enthält keine offensichtlichen Formatierungsfehler:<br>-Eine nummerierte Liste oder Aufzählung, die als Absatz angezeigt wird. <br> -Code in einem Codeblock, der angezeigt wird, zum Teil im Codeblock als auch teilweise außerhalb <br>-Nummerierte Schritte, die aufgrund einer fehlerhaften Einrückung falsch nummeriert sind|

## <a name="non-blocking-content-quality-items"></a>Nicht blockierende inhaltsqualitätselemente

Geben Sie für diese Elemente Pull Request-Prüfer Feedback und Anweisungen für den Autor, um Behebungen in einem nachfolgenden Pull Request nachverfolgung. Dieses Feedback blockiert jedoch nicht die Entscheidung zur Zusammenführung. Autoren sollten innerhalb von 3 Arbeitstagen Korrekturen nachverfolgung.

| Kategorie | Qualitätsprüfelement |
|----------|---------------------|
|Content|Artikel sollten den Abschnitt "Nächste Schritte" am Ende mit 1 bis 3 relevanten und nützlichen nächsten Schritten enthalten. Kurzer Text eingeschlossen werden sollen, mit dessen Hilfe die Kunden zu verstehen, warum die nächsten Schritte relevant sind. (Nur neue Artikel).
|Abbilder|Images verwenden, den richtigen Stil und die Farbe und Screenshots verwenden Sie das richtige Format für und. [Finden Sie im Leitfaden zu Bildern](https://github.com/Azure/azure-content/blob/master/contributor-guide/create-images-markdown.md).|
|Website-/designfunktionalität|Die H2-Überschriften sollten beim Rendern im Inhaltsverzeichnis auf der Seite, sollte im Idealfall nicht mehr als 2 Zeilen umschließen. Längere Überschriften erschweren die Überprüfung Inhaltsverzeichnisses des Artikels.|
|Stilkonventionen|Bei allen Titeln und Überschriften sind großgeschrieben.|
|Verarbeiten|Wenn Sie zu löschen oder eines Artikels umbenennen, stellen Sie sicher, dass Sie den Prozess folgen. Pull Request-Prüfer den folgenden Kommentar und den Link in einem Kommentar hinzufügen sollten:<br><br>*Stellen Sie sicher, dass Sie den Prozess im Handbuch für die Mitwirkende ausgeführt: [Der Name eines Artikels zu ändern oder löschen](rename-or-retire.md).*|
