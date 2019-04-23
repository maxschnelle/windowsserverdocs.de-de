# <a name="metadata-and-version-identifiers"></a>Metadaten und -Bezeichner

Hier ist, was Sie über Marken, versionsverwaltung und Metadaten für die Artikel in Windowsserverdocs-Pr-Repository wissen müssen. Autoren sind dafür verantwortlich, dass Sie sicher, dass ihre Artikel dieser Standards und Vorschriften entsprechen.

## <a name="trademarks"></a>Warenzeichen
Verwenden Sie keine Markensymbole nach Produktverweise in den Artikeln in der technischen Bibliothek. Sie sind nicht erforderlich, da technet.microsoft.com, docs.microsoft.com und andere offizielle Microsoft-Kanäle veröffentlichen enthalten eine [Marke](https://www.microsoft.com/trademarks) Fußzeile-Link zu einer Liste von Microsoft-Marken. Dieser Link erfüllt der rechtliche Anforderung. Hintergrundinformationen finden Sie Anleitungen von [CELA](https://microsoft.sharepoint.com/sites/LCAWeb/Home/Copyrights-Trademarks-and-Patents/Trademarks/Trademark-List-and-Usage)unter "Websites" und der Microsoft-Stilvorgaben für [Urheberrechte und Marken](https://worldready.cloudapp.net/Styleguide/Read?id=2700&topicid=26696) Seite unter "Webseiten auf Microsoft.com" 

## <a name="versioning"></a>Versionskontrolle
Mehrere Typen von versionsverwaltung gelten in den Artikeln in diesem Repository: 

-  Versionsverwaltung, der die Produktversion, der angibt für ein Artikel gilt, wird auf zwei Arten erreicht:
    - Manuell in einer Zeile in diesem Artikel, sodass er auf einem veröffentlichten Artikel als Text angezeigt wird.
    - Durch die Metadaten, die im folgenden beschrieben werden.
-  Source-Content-versionsverwaltung erfolgt über Githubs-Verlauf für die Datei. 

## <a name="metadata-structure-and-format"></a>Metadaten-Struktur und das format

- Fügen Sie am Anfang der Datei oberhalb der H1-Überschrift Metadaten.
- Trennen des Blocks vom Rest der Inhalt der Datei mit nur drei Bindestriche in den ersten und letzten Zeilen des Blocks. Fügen Sie einen beliebigen anderen Text nicht in diesen Zeilen.
- Fügen Sie jedes Name/Wert-Paar von Metadaten in einer separaten Zeile ein.
- Verwenden Sie eine der folgenden Syntax Muster, je nachdem, ob die Metadaten sind vordefinierte Werte erforderlich, oder benutzerdefinierte Werte akzeptiert. 

        ---
        name1: predefined-value
        name2: "my custom value"
        ---

## <a name="metadata-names-and-values"></a>Metadaten-Namen und Werte

Bestimmte Metadaten sind erforderlich, damit alle Dateien, die als Artikel in der technischen Bibliothek von TechNet, veröffentlicht werden, während andere Metadaten wird empfohlen, jedoch nicht erforderlich. In einigen Fällen sind nur bestimmte Werte für einen bestimmten Teil der Metadaten zulässig. 

|Name|Wert|
|---|---|
|title|Benutzerdefinierter Wert, der die H1-Überschrift entspricht. Bestimmt, was in der Browserregisterkarte angezeigt.|
|description|Zeigt in den Suchergebnissen aus, und wirkt sich auf die SEO. Enthalten Sie geeignete Schlüsselwörter, aber behalten Sie die Länge kleiner als 160 Zeichen enthalten.|
|Autor|Github-Alias, der der primäre Autor des Artikels|
|ms.author|MSFT-Alias des des Artikels Autor oder den Inhalt verantwortlichen Entwickler für die Technologiebereich, der in diesem Artikel behandelt.|
|ms.date|Datum der letzten Aktualisierung von Inhalt. Aktualisieren Sie nicht, damit die Änderungen nur Metadaten. Verwenden Sie das Format mm/tt/jjjj.|
|ms.prod|Windows Server-Version identifiziert, für die BI-berichterstellung, auf der Grundlage eines vordefinierten [Wert](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969).|
|ms.technology|Identifiziert die Technologiebereich, für die BI-berichterstellung, auf der Grundlage eines vordefinierten [Wert](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969)|
|ms.asset|GUID, die Artikel in allen Gebietsschemas für BI-berichterstellung identifiziert. Artikel, die von früheren authoring migriert Systeme nicht über diese. Für Artikel in Github erstellt verwenden Sie ein Tool wie z. B. [ https://guidgenerator.com/ ](https://guidgenerator.com/).| 

## <a name="troubleshooting"></a>Problembehandlung

Metadaten, die von einem veröffentlichten Artikel die oben angezeigt wird geschieht, wenn es sich bei die Quelldatei Formatierungsfehler hat. Einige häufige Fehler sind:

- Fehlt die dreifache Bindestriche an die erste und letzte Zeile des Blocks, oder eine falsche Anzahl von Bindestrichen.
- Metadaten nicht die erforderliche Syntax folgen: \<Namen\>:\<einmaliges Speicherplatz\>\<Wert >

Überprüfen Sie die Datei für diese und andere offensichtliche Fehler, Sie dann einen Pull Request veröffentlicht die aktualisierte Datei senden. Wenn Sie kommen nicht weiter, e-Mail-Adresse der PR-Reviewer-Alias: wssc-pra@microsoft.com

## <a name="see-also"></a>Siehe auch
Metadaten, die in diesem Repository verwendet wird basierend auf Metadaten, die in Content Services & International verwendet \(CSI\). Weitere Informationen, einschließlich optionale Metadaten, finden Sie unter [ http://aka.ms/skyeye/meta ](http://aka.ms/skyeye/meta).
Business Intelligence-Ressourcen finden Sie unter der CSI-BI-Teams [Wiki](https://microsoft.sharepoint.com/teams/STBCSI/Insights/Selfserve%20BI%20wiki/Self-serve%20BI%20wiki.aspx).