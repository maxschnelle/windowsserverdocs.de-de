---
title: Windows Admin Center Text- und Designformatanleitung
description: Windows Admin Center Benutzeroberflächen Text und Design-Styleguide SDK
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: be41267d6584002ebf87e5fe828a41575d305e1b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445908"
---
# <a name="windows-admin-center-ui-text-and-design-style-guide"></a>Windows Admin Center Text- und Designformatanleitung

>Gilt für: Windows Admin Center

In diesem Thema wird der allgemeine Ansatz zum Schreiben von Text in Benutzeroberflächen (UI) für Windows Admin Center als auch einige bestimmte Konventionen und Ansätze behandelt.

Windows Admin Center und andere Erweiterungen sollten [Microsofts VoIP-Prinzipien](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human) folgen, damit die Erfahrung benutzerfreundlich ist. Diese Entwurfsrichtlinien basieren auf folgenden Sprachprinzipien genau wie der [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/), stellen Sie daher sicher, dass Sie beide Ressourcen für Informationen über die [Eingabehilfen](https://docs.microsoft.com/style-guide/accessibility/accessibility-guidelines-requirements), [Akronyme](https://docs.microsoft.com/style-guide/acronyms)und [Wortwahl](https://docs.microsoft.com/style-guide/word-choice/)haben, wie beispielsweise [Bitte](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/p/please) und [Entschuldigung](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/s/sorry).

## <a name="buttons"></a>Schaltflächen

- Schaltflächen sollten möglicherweise ein Wort enthalten, besonders dann, wenn Sie das Tool lokalisieren möchten. Zwei oder drei ist in Ordnung, aber versuchen, mehr zu vermeiden. Wenn Sie über vier Wörter oder länger betragen, es besser wäre, eine Link-Steuerelement zu verwenden.
- Schaltflächenetikette sollten präzise, bestimmt und selbsterklärend sein. Anstelle der generischen Schaltfläche "Übermitteln", verwenden Sie ein Verb für die Aktion des Benutzers, wie "Erstellen", "Löschen", "Hinzufügen", "Formatieren" usw.
- Wenn eine Schaltfläche auf eine Frage folgt, sollte dessen Beschriftung der Frage deutlich entsprechen (in der Regel "Ja" oder "Nein").

## <a name="capitalization"></a>Großschreibung

Wir folgen der Microsoft-Formatvorlage für die [Großschreibung](https://docs.microsoft.com/style-guide/capitalization) - der Verwendung der Satz-Groß-/Kleinschreibung für ziemlich alles.

| UI-Element              |Großschreibung|Kommentare|
|-------------------------|--------------|--------|
|Badges (beispielsweise PREVIEW) |Großbuchstaben      ||
|Alle anderen          |Satzstil|Es gibt jedoch einige Ausnahmen, bei denen Objekteigenschaften von WMI oder PowerShell in Betracht ziehen, die außerhalb unserer Steuerelement sind.|

## <a name="colons"></a>Doppelpunkte

Verwenden Sie Doppelpunkte Listen einführen. Zum Beispiel:

    Choose one of the following:
    Cats
    Dogs
    Quokkas

Doppelpunkte nicht im UI-Text verwendet werden, wenn eine Bezeichnung auf einem anderen Zeile in das, was Bezeichnungen oder wenn es einen klaren Unterschied zwischen der Bezeichnung und das, was denn wird diese Bezeichnung.

Verwenden Sie Doppelpunkte in Benutzeroberflächentext, wenn eine Bezeichnung in der gleichen Zeile wie der Text ist, sie Bezeichnungen und verhindern, dass die beiden Elemente zusammen ausgeführt werden sollen.

## <a name="confirmation-messages"></a>Bestätigungsnachrichten

Bestätigungsdialogfelder sind nützlich, wenn Sie den Vorgang fortsetzen möglicherweise unerwartete Ergebnisse, z.B. zu Datenverlust. Sie sollten gescannt werden, nützliche Informationen mit einem klar Ergebnis, insbesondere für Ereignisse enthalten, die nicht rückgängig gemacht werden kann. 

- Stellen Sie sicher, dass eine Bestätigung erforderlich ist. Es ist keine neuen Informationen zu bieten (z. B. "sind Sie sicher?") und dann eine Bestätigungsnachricht nicht erforderlich sein kann.  
- Stellen Sie sicher, dass der Kunde die Aktion nicht fortsetzen möchte.
- Stellen Sie sicher, dass die hauptanweisung (Überschrift) und erläuternden Text (Text) redundant sind.
- Definieren Sie in der Überschrift die möglichen Ergebnisse als eine Frage oder eine Anweisung zum was als Nächstes geschieht. Z. B. "Löschen aller Daten auf diesem Laufwerk? oder "Sie sind im Begriff, alle Ihre Daten zu löschen".
- Fügen Sie Details im Text hinzu. Es ist eine Variable ein, z. B. den Namen des Elements, die Sie zu ändern, fügen Sie es hier.
- Zählen Sie eine einfache Frage (entweder im Header oder im Text), die eine eindeutige Entscheidung zwischen zwei Aktionsschaltflächen umgibt.
- Verwenden Sie für eine komplexe Wahl Ja/Nein Schaltflächen, die sorgfältig lesen zu empfehlen. Für eine einfachere Auswahl, mit Schaltflächen, die spezifisch für die Aktion, z. B. alle löschen oder Abbrechen.

## <a name="first-run-experiences"></a>Die erste Ausführung Erfahrungen

Das ersten Mal, wenn ein Benutzer eine Seite besucht, haben Sie die Möglichkeit, ihn bei der Benutzung des Tools zu unterstützen. Dies kann folgendes sein:

- Eine Textzeichenfolge in einer leeren Seite mit kurzen Anweisungen zum Start - wählen Sie zum Beispiel""Hinzufügen", um eine App hinzuzufügen."
- Eine Verknüpfung mit dem Steuerelement, das dem Benutzer beim Start hilft – beispielsweise "Fügen Sie eine App hinzu, um zu beginnen".
- Eine kurze Animation oder ein Video, die den Benutzern die Konfiguration erklärt

Hier sind einige Tipps aus unserem Styleguide für Windows:

### <a name="1-be-helpful"></a>1. Seien Sie behilflich

- Vermeiden Sie Marketingstil und -Sprache.
- Wenn Sie etwas vorschlagen, stellen Sie sicher, dass das Endergebnis klar ist. Den Kunden die Funktionsweise zu zeigen, ist nicht wirksam, wenn sie nicht wissen, warum sie es tun.
- Präsentieren Sie keine Tipps, die der Kunde nicht braucht.

### <a name="2-show-dont-tell"></a>2. Mehr

Halten Sie Ihren Text so einfach wie möglich (kleine Animationen oder Videos).

### <a name="3-dont-overwhelm"></a>3. Nicht zu überlasten

- Beschränken Sie Popups und Tipps auf 4 pro Sitzung – einschließlich Systembenachrichtigungen und Shell-Benachrichtigungen.
- Stellen Sie sicher, dass die Popups zeitlich hilfreich sind.
- Verhindern Sie nicht, dass der Kunde eine Aktion durchführt.
- Stellen Sie sicher, dass Popups auf einfache Weise geschlossen werden.

### <a name="4-keep-it-contextual"></a>4. Bewahren Sie sie kontextbezogene

- Lernphasen sind am effektivsten, wenn sie zur richtigen Zeit angezeigt werden.
- Wenn Sie Lernprogramme oder Bildschirmpräsentationen erstellen, machen Sie die Infos konkret.
- Kein Marketing "Geplapper" – Schwerpunkt auf bestimmte Tipps und Tricks.
- Bieten Sie eine Möglichkeit für Kunden auf das Lernprogramm später zurückzugreifen, wenn es relevant ist (Personen behalten häufig Informationen nicht beim ersten Mal bei, Setupinfos sollten jedoch nur einmal angezeigt werden).
- Leerstatusanzeigen sind ein natürlicher Platz zum Lernen und/oder Spass – bleiben Sie einfach und informativ.

### <a name="5-minimize-painful-setup"></a>5. Zu minimieren, oft schwierigen setup

Wenn der Kunde zum Ausführen des vollständigen Umgebung mehr Aktionen benötigt (Anmeldung an einem Onlinedienst usw.), machen Sie es so einfach wie möglich.

- Nachrichten sollten kurz und direkt sein.
- Vermeiden sie das sofortige Senden. Wenn möglich, bieten Sie eine Möglichkeit für die Verbindung vom Standort aus.
- Wenn möglich, bieten Sie die Option, die Aktion später durchzuführen, und erinnern Sie den Benutzer später daran.
- Wenn Sie die Aktion wechseln, geben Sie eine Möglichkeit, schnell und einfach wieder zurückzukehren.

## <a name="help-links"></a>Links zu Hilfethemen

Hier sind einige Tipps aus unserem Styleguide für Windows:

### <a name="when-should-we-provide-a-help-link"></a>Wann sollten wir einen Hilfelink klicken bereitstellen?

Fast nie. Geben Sie einen Hilfelink nur, wenn:

- Es gibt eine offensichtliche und wichtige Frage, die Kunden haben, während sie in der Benutzeroberfläche sind die Antwort auf die zu den an den UI-Task erfolgreich treffen können. 
- Es ist nicht genügend Platz auf der Benutzeroberfläche, um die Menge der erforderlichen Informationen für den Benutzer an der UI-Task erfolgreich bereitzustellen. 

### <a name="where-should-help-links-appear"></a>Wo soll Hilfelinks angezeigt werden? 

- Textlinks sollte wie in der Nähe der UI-Element angezeigt werden, die die Hilfe möglichst gerichtet ist. 
- Wenn Sie einen Texthyperlink, der für einen ganzen Bildschirm der Benutzeroberfläche gilt bereitstellen müssen, platzieren Sie es unten links auf dem Bildschirm. 
- Wenn Sie einen Link, über eine Schaltfläche "Hilfe" (?) angeben, muss die QuickInfo "Help".

### <a name="what-url-should-we-use"></a>Welche URL sollten wir verwenden?

Nie direkt zu einer Webadresse zu verknüpfen, verwenden Sie stattdessen einen Umleitung-Dienst.

Microsoft-Entwickler sollten eine FWLink, es sei denn, es einen Hilfelink klicken, dass Benutzer manuell eingeben ggf., die Groß-/Kleinschreibung verwendet einen Link aka.ms (solange das Ziel der URL einer Website, die die browsergebietsschema, z. B. Docs.microsoft.com erkennt automatisch ist) verwenden

### <a name="text-guidelines"></a>Text-Richtlinien 

- Verwenden Sie vollständige Sätze.
- Fügen Sie keine setzen Sie satzendpunkte mit Ausnahme von Fragezeichen. 
- Sie müssen nicht den gleichen Text als den Aufgabentitel verwenden. Verwenden Sie Text, der im Kontext der Benutzeroberfläche sinnvoll, aber stellen Sie sicher, dass eine logische Verbindung zwischen den beiden vorhanden ist. Zum Beispiel: 
- Hilfe-Link: Was sind die Risiken für das Zulassen von Ausnahmen? 
- Hilfethema-Titel: "Ein Programm für die Kommunikation über Windows-Firewall zulassen"
- Werden Sie möglichst genaue Angaben über den Inhalt des Hilfethemas. 
    - Unsere Stil
        - Wie trägt die Windows-Firewall zum Schutz des Computers?
        - Warum ein Bild von Highlights verbessert werden kann
    - Nicht in unserem Stil
        - Weitere Informationen zur Windows-Firewall
        - Erfahren Sie mehr über farbverwaltung
        - Mehr erfahren
- Verwenden Sie den gesamten Satz für die der Text des Links, nicht nur die Schlüsselwörter. 
    - Unsere Stil 
        - [Was sind die Risiken für das Zulassen von Ausnahmen?]()
    - Nicht in unserem Stil
        - Was sind die [Risiken zulassen von Ausnahmen]()? 

## <a name="error-messages"></a>Fehlermeldungen

Hier einige Hinweise, die aus der Windows-Style-Guide angepasst wird:

Schreiben eine gute Nachricht ist eine Balance zwischen Bereitstellung genügend Erklärung aber nicht zu technischen; zwischen gelegentlichen und Verhalten jedoch keine lästigen oder anstößigen.

### <a name="general-guidelines"></a>Allgemeine Richtlinien

Verwenden Sie eine Nachricht pro auftretender Fehler.

#### <a name="headings"></a>Spaltenüberschriften

- Halten Sie es kurz und präzise erklären, worin das Problem besteht oder **im Idealfall Vorgehensweise**. <br>Einige Benutzeroberflächen möglicherweise Überschriften, die abgeschnitten wird, anstatt zu umschließen, wenn sie zu lang sind, also ein Auge für diese.
- Verwenden Sie die Projektmappe in der Überschrift, wenn es sich um einen einfachen Schritt handelt.
- Stellen Sie sicher, dass die Überschrift direkt auf die Schaltfläche mit den bezieht, für den Fall, dass der Reader den Textkörper ignoriert.
- Verwenden Sie "Gab es ein Problem" in Überschriften, es sei denn, Sie keine andere Wahl haben. Spezifischer über das Problem sein.
- Vermeiden Sie Variablen (z. B. Datei-, Ordner- und app-Namen) in Überschriften. Fügen Sie sie in den Text ein.

#### <a name="body"></a>Text

- Wenn die Überschrift ausreichend der Lösung oder das Problem erläutert, benötigen Sie nicht den Textkörper.
- Nicht wiederholen Sie den Titel in der Nachricht mit etwas anderen Wortlaut aus.
- Klar kommunizieren und präzise wie die Lösung ist.
- Erteilen die Fakten zuerst darauf konzentrieren.
- Keine Verantwortung für den Fehler die Benutzer zuweisen.
- Wenn ein Fehlercode des Fehlers und, wenn Sie glauben, dass den Fehlercode einschließlich den Kunden oder Microsoft-Support, um das Problem untersuchen kann, fügen Sie es direkt unter dem Textkörpertext, und wie folgt zu schreiben:

    Fehlercode: ###

    Wenn der Kunde über alle erforderlichen Informationen zum Beheben des Fehlers, ohne den Code verfügt, müssen Sie nicht einschließen.

#### <a name="buttons"></a>Schaltflächen

- Schreiben von Text der Schaltfläche, damit es sich um eine bestimmte Antwort an die Haupt-Anweisung ist. Wenn dies nicht möglich ist, verwenden Sie "Schließen" für den Text der Schaltfläche Kündigung (anstelle von "OK" oder "Fertig").
- Wenn Sie mehr als eine Schaltfläche verfügen, stellen der Schaltfläche ganz links die Aktion, die der Benutzer wird ermutigt ist. Stellen Sie der Schaltfläche ganz rechts die konservativere Aktion, z. B. "Cancel".

#### <a name="help-links"></a>Links zu Hilfethemen

Nur erwägen Sie, Links zu Hilfethemen für Fehlermeldungen, die Sie keine bestimmte und handlungsrelevante vornehmen können.

## <a name="null-state-text"></a>Text für NULL-Dienststatus

Hier ist brauchen Hilfe aus der Windows-Style-Guide.

Nullzustand tritt auf, wenn Kundendaten oder Inhalt nicht vorhanden ist aus einer app oder ein Feature, wenn keine Ergebnisse zurückgegeben werden, nachdem eine Suche oder bei Bedarf Informationen fehlen in ein Format, z. B. die Abrechnungsinformationen für eine Transaktion.

### <a name="guidelines"></a>Richtlinien

- Wenn möglich, als Gelegenheit verwenden Sie Nullzustand Situationen, informieren Sie Benutzer zur Verwendung die Funktion (z. B. wie Musik, hinzugefügt werden, suchen, Bilder usw.)  
  - Wenn Sie einen Titel auf der Benutzeroberfläche haben, erklären Sie die Aktion "beheben" den Status null (z. B. "Musik hinzufügen") 
  - Spaß mit dem Text. Dieser Speicherplatz kann die Gelegenheit, begeistern zu bieten, da es wahrscheinlich nicht mehrmals angezeigt werden, wird sein. 
  - Vermeiden Sie "Es ist sehr einsam hier." Dies ist eine traurige Sache, und ist übermäßig beansprucht wurde. 
  - Vermeiden Sie Fragen wie "Ihr Drucker noch nicht verbunden werden?" Okay, um einmal zu verwenden, aber dieses Format ist übermäßig beansprucht zu erhalten, und Fragen stellen zusätzliche Belastung/Druck auf den Kunden. Sie können auch ein herablassender können. 
  - Verschiedene Status null-Text ist eine gute Sache. 

### <a name="examples"></a>Beispiele

- "Fügen Sie eine Person als Favorit hinzu, und sehen Sie ihn hier."
- "Haben alle Erfolge oder Spiele Clips, die Sie besonders stolz sind? Fügen sie Sie Ihrem Showcase."
- "No one in noch keiner Partei. Starten eines!"
- "Wenn jemand Sie als Friend hinzufügt, werden Sie diese hier angezeigt."
- "Wenn Sie die erforderlichen Schritte wie Erfolge zu entsperren, Spiele Clips aufzeichnen und Hinzufügen von Freunden, sie alle hier sehen Sie."
- "Ihre Favoriten Freunden werden hier oben angezeigt, damit Sie sehen können, wenn sie online sind und was sie nutzen."

## <a name="punctuation"></a>Zeichensetzung

- Keine Interpunktion am Ende (Punkte, Fragezeichen) für Überschriften oder unvollständigen Sätze. Eine Ausnahme ist in ein Bestätigungsdialogfeld, in dem die Überschrift die Frage ist
- Verwenden Sie Microsoft-Styleguideanleitungen für [Punkte](https://docs.microsoft.com/style-guide/punctuation/periods) und [Fragezeichen](https://docs.microsoft.com/style-guide/punctuation/question-marks).

## <a name="status-messages"></a>Statusmeldungen

Statusnachrichten bestehen aus Popup (Toast)-Nachrichten und Benachrichtigungen.

|String-Typ         | Hinweise                               |
|------------        |-------------------------------------|
|Toast               |Zeichensetzung am Satzende - idealerweise mit einer Objektvariable, damit Benutzer verstehen, welches Objekt die Nachricht betrifft, für den Fall, dass sie sich vom Objekt entfernt haben|
|Überschrift für Benachrichtigungen|Keine Zeichensetzung am Satzende (für Überschriften) - idealerweise mit einer Objektvariablen|
|Benachrichtigungsdetails|Vollständige Sätze, idealerweise mit Links zur Benutzeroberfläche, die das Objekt anzeigt|

Es folgen einige detaillierten Empfehlungen für die Benachrichtigung aus:

|String-Typ         | Hinweise                               |
|------------        |-------------------------------------|
|Started             |Sollte ausgelassen werden, wenn möglich - sie können in der Regel die Nachricht in Bearbeitung überspringen und so die Anzahl der Ablenkungen minimieren.|
|In Bearbeitung         |Beginnen Sie mit dem Verb der Aktion, die Sie durchführen und enden Sie mit Ellipsen, um einen laufenden Vorgang anzugeben. Im Folgenden ein Beispiel:<br> *Das Volume "Kundendaten" wird erstellt...*|
|Erfolgreich             |Beginnen Sie mit "Erfolgreich" und enden Sie mit dem Vorgang der Software. Im Folgenden ein Beispiel:<br> *Das Volume erstellt "Kundendaten".*|
|Nicht möglich             |Beginnen Sie mit "Konnte nicht" und enden Sie damit, was die Software nicht konnte. Im Folgenden ein Beispiel:<br> *"Kundendaten" für das Volume konnte nicht erstellt werden.*|

## <a name="tooltips"></a>QuickInfos

Gute QuickInfos kurz beschreiben von Steuerelementen ohne Beschriftung oder etwas zusätzliche Informationen für beschriftete Steuerelemente ein, geben Sie bei der dies hilfreich ist. Zudem können Kunden, die die Benutzeroberfläche durch zusätzliche Angebot zu navigieren – nicht redundant, Informationen zu den steuerelementbezeichnungen, Symbole, Links usw.

QuickInfos sollten nur selten oder gar nicht verwendet werden. Sie können eine Unterbrechung an den Kunden damit keine QuickInfo enthalten, die einfach wiederholt eine Bezeichnung oder das Offensichtliche hinausblicken angegeben werden. Sie sollten immer wertvolle Informationen hinzufügen.

|    Kontext                                 |    Gewusst wie: Schreiben von QuickInfos    |
|    -----------------------                 |    -------------------------    |
|Wenn ein Steuerelement oder UI-Element ohne Bezeichnung ist...|Verwenden Sie einen einfache, aussagekräftigen-nominaler Ausdruck. Zum Beispiel:<br> Hervorheben des Stifts |
|Wenn ein Element der Benutzeroberfläche ist mit der Bezeichnung, aber ihr Zweck benötigt Informationen...|<ul><li>Beschreiben Sie kurz, was Sie mit diesem Element der Benutzeroberfläche tun können. </li><li>Verwenden Sie das Formular für die imperative Verb. Z. B. "Suchen von Text in der Datei" (nicht "sucht nach Text in der Datei").</li><li>Enthalten Sie keine Interpunktion, es sei denn, es mehrere vollständige Sätzen gibt.</li> </ul>|
|Wenn eine Bezeichnung abgeschnitten ist oder sich in einigen Sprachen abgeschnitten ist...|<ul><li>Geben Sie die ungekürzte Bezeichnung in der QuickInfo.</li><li>Optional: Geben Sie in einer anderen Zeile eine klärende Beschreibung, jedoch nur bei Bedarf.</li><li>Geben Sie eine QuickInfo nicht, wenn die ungekürzte Informationen an anderer Stelle auf der Seite oder den Flow bereitgestellt wird.</li></ul>|
|Wenn eine Tastenkombination verfügbar ist...|<ul><li>Optional: Geben Sie die Tastenkombination in Klammern, die die Bezeichnung oder beschreibenden Ausdruck, z. B. nach "Print (STRG + P)" oder "Suchen von Text in dieser Datei (STRG + F)"</li><li>Es ist OK, um eine nützliche Tastenkombination klärende QuickInfo hinzufügen, aber vermeiden Sie das Hinzufügen einer QuickInfos nur, um Tastenkombinationen anzuzeigen. </li></ul>|