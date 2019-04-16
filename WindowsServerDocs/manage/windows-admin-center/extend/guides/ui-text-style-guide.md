---
title: Windows Admin Center Text- und Designformatanleitung
description: Windows Admin Center Text- und designformatanleitung SDK
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab5bee55975b803a77db0b6cdb179b76590e1d83
ms.sourcegitcommit: 56cccb09a35b2d3eef9056e2406c3a1762d28682
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2018
ms.locfileid: "4739980"
---
# Windows Admin Center Text- und Designformatanleitung

>Gilt für: Windows Admin Center

In diesem Thema wird der allgemeine Ansatz zum Schreiben von Text in Benutzeroberflächen (UI) für Windows Admin Center als auch einige bestimmte Konventionen und Ansätze behandelt.

Windows Admin Center und andere Erweiterungen sollten [Microsofts VoIP-Prinzipien](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human) folgen, damit die Erfahrung benutzerfreundlich ist. Diese Entwurfsrichtlinien basieren auf folgenden Sprachprinzipien genau wie der [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/), stellen Sie daher sicher, dass Sie beide Ressourcen für Informationen über die [Eingabehilfen](https://docs.microsoft.com/style-guide/accessibility/accessibility-guidelines-requirements), [Akronyme](https://docs.microsoft.com/style-guide/acronyms)und [Wortwahl](https://docs.microsoft.com/style-guide/word-choice/)haben, wie beispielsweise [Bitte](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/p/please) und [Entschuldigung](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/s/sorry).

## Schaltflächen

- Schaltflächen sollten möglicherweise ein Wort enthalten, besonders dann, wenn Sie das Tool lokalisieren möchten. Zwei oder drei ist in Ordnung, aber versuchen, mehr zu vermeiden. Bei vier Wörter oder mehr, würde es besser, ein Linksteuerelement verwendet werden.
- Schaltflächenetikette sollten präzise, bestimmt und selbsterklärend sein. Anstelle der generischen Schaltfläche "Übermitteln", verwenden Sie ein Verb für die Aktion des Benutzers, wie "Erstellen", "Löschen", "Hinzufügen", "Formatieren" usw..
- Wenn eine Schaltfläche auf eine Frage folgt, sollte dessen Beschriftung der Frage deutlich entsprechen (in der Regel "Ja" oder "Nein").

## Großschreibung

Wir folgen der Microsoft-Formatvorlage für die [Großschreibung](https://docs.microsoft.com/style-guide/capitalization) - der Verwendung der Satz-Groß-/Kleinschreibung für ziemlich alles.

| UI-Element              |Großschreibung|Anmerkungen|
|-------------------------|--------------|--------|
|Badges (beispielsweise PREVIEW) |Großbuchstaben      ||
|Alle anderen          |Satzstil|Es gibt jedoch einige Ausnahmen, bei denen Objekteigenschaften von WMI oder PowerShell in Betracht ziehen, die außerhalb unserer Steuerelement sind.|

## Doppelpunkte

Verwenden Sie Doppelpunkte Listen einführen. Beispiel:

    Choose one of the following:
    Cats
    Dogs
    Quokkas

Verwenden Sie Doppelpunkte nicht im UI-Text wird eine Beschriftung auf einem anderen Linie, die bei das, was sie Beschriftungen oder es wird eine klare Unterscheidung zwischen der Bezeichnung und das, was ist es beschriften.

Verwenden Sie Doppelpunkte im UI-Text, wenn eine Beschriftung in der gleichen Zeile wie den Text ist, es beschriftet und um zu verhindern, dass die beiden Elemente werden zusammen ausgeführt werden müssen.

## Bestätigungsnachrichten

Bestätigungsdialogfelder sind nützlich, wenn Sie den Vorgang fortsetzen möglicherweise unerwartete Ergebnisse zu erzielen, z. B. Daten verloren gehen. Sie sollten strukturieren, nützliche Informationen mit einer klar Ergebnis, insbesondere bei Ereignissen enthalten, die nicht rückgängig gemacht werden kann. 

- Stellen Sie sicher, dass eine Bestätigung erforderlich ist. Es ist keine neuen Informationen angeboten werden soll (z. B. "wirklich?") und dann eine Bestätigungsnachricht möglicherweise nicht erforderlich.  
- Stellen Sie sicher, dass der Kunde die Aktion fortsetzen möchte.
- Stellen Sie sicher, dass die hauptanweisung (Überschrift) und erklärender Text (Text) nicht redundant.
- Definieren Sie in der Überschrift der möglichen Ergebnisse als eine Frage oder eine Anweisung darüber, was als Nächstes passieren wird. Beispielsweise "löscht alle Daten auf dem Laufwerk? oder "Sie sind dabei, Ihre Daten löschen".
- Fügen Sie Details im Text hinzu. Es ist eine Variable, z. B. den Namen des Elements, die Sie zu ändern, fügen Sie ihn hier.
- Fügen Sie eine einfache Frage (entweder in der Kopfzeile oder im Textkörper), die eine klare Wahl zwischen zwei Aktionsschaltflächen frames.
- Verwenden Sie für eine komplexe Wahl Ja/Nein Schaltflächen, die vorsichtig lesen fördern. Für eine einfachere Wahl verwenden-Schaltflächen, die speziell für die Aktion sind wie z. B. löschen Sie alle oder Abbrechen.

## Erstausführung

Das ersten Mal, wenn ein Benutzer eine Seite besucht, haben Sie die Möglichkeit, ihn bei der Benutzung des Tools zu unterstützen. Dies kann folgendes sein:

- Eine Textzeichenfolge in einer leeren Seite mit kurzen Anweisungen zum Start - wählen Sie zum Beispiel""Hinzufügen", um eine App hinzuzufügen."
- Eine Verknüpfung mit dem Steuerelement, das dem Benutzer beim Start hilft – beispielsweise "Fügen Sie eine App hinzu, um zu beginnen".
- Eine kurze Animation oder ein Video, die den Benutzern die Konfiguration erklärt

Hier sind einige Tipps aus unserem Styleguide für Windows:

### 1. Seien Sie hilfreich

- Vermeiden Sie Marketingstil und -Sprache.
- Wenn Sie etwas vorschlagen, stellen Sie sicher, dass das Endergebnis klar ist. Den Kunden die Funktionsweise zu zeigen, ist nicht wirksam, wenn sie nicht wissen, warum sie es tun.
- Präsentieren Sie keine Tipps, die der Kunde nicht braucht.

### 2. Zeigen Sie Dinge, anstatt sie zu erklären

Halten Sie Ihren Text so einfach wie möglich (kleine Animationen oder Videos).

### 3. Bleiben Sie übersichtlich

- Beschränken Sie Popups und Tipps auf 4 pro Sitzung – einschließlich Systembenachrichtigungen und Shell-Benachrichtigungen.
- Stellen Sie sicher, dass die Popups zeitlich hilfreich sind.
- Verhindern Sie nicht, dass der Kunde eine Aktion durchführt.
- Stellen Sie sicher, dass Popups auf einfache Weise geschlossen werden.

### 4. Bleiben Sie Kontextbezogen

- Lernphasen sind am effektivsten, wenn sie zur richtigen Zeit angezeigt werden.
- Wenn Sie Lernprogramme oder Bildschirmpräsentationen erstellen, machen Sie die Infos konkret.
- Kein Marketing "Geplapper" – Schwerpunkt auf bestimmte Tipps und Tricks.
- Bieten Sie eine Möglichkeit für Kunden auf das Lernprogramm später zurückzugreifen, wenn es relevant ist (Personen behalten häufig Informationen nicht beim ersten Mal bei, Setupinfos sollten jedoch nur einmal angezeigt werden).
- Leerstatusanzeigen sind ein natürlicher Platz zum Lernen und/oder Spass – bleiben Sie einfach und informativ.

### 5. Minimieren Sie mühsame Setups

Wenn der Kunde zum Ausführen des vollständigen Umgebung mehr Aktionen benötigt (Anmeldung an einem Onlinedienst usw.), machen Sie es so einfach wie möglich.

- Nachrichten sollten kurz und direkt sein.
- Vermeiden sie das sofortige Senden. Wenn möglich, bieten Sie eine Möglichkeit für die Verbindung vom Standort aus.
- Wenn möglich, bieten Sie die Option, die Aktion später durchzuführen, und erinnern Sie den Benutzer später daran.
- Wenn Sie die Aktion wechseln, geben Sie eine Möglichkeit, schnell und einfach wieder zurückzukehren.

## Hilfelinks

Hier sind einige Tipps aus unserem Styleguide für Windows:

### Wenn bieten wir einen Hilfelink?

Fast nie. Bieten Sie eine Verknüpfung zur Hilfe nur, wenn:

- Es gibt eine offensichtliche und wichtige Frage, die Kunden können, während sie in der Benutzeroberfläche sind die Antwort auf die sie an den UI-Task erfolgreich hilft. 
- Es ist nicht genügend Platz in der Benutzeroberfläche, um die Menge an Informationen erforderlich ist, damit Benutzer bei der UI-Aufgabe erfolgreich bereitzustellen. 

### In denen anhand der nachfolgenden Links angezeigt werden können? 

- Textlinks sollten so nah bei der UI-Element angezeigt werden, die die Hilfe wie möglich an gerichtet ist. 
- Wenn Sie einen Textlink, die für eine gesamte UI-Bildschirm gilt angeben müssen, platzieren Sie es am linken unteren Rand des Bildschirms. 
- Wenn Sie eine Verknüpfung über eine Hilfeschaltfläche (?) bereitstellen, sollte die QuickInfo sein "Hilfe".

### Welche URL sollte werden verwendet?

Niemals einen direkten link zum eine Webadresse – verwenden Sie stattdessen ein Umleitungsdienst.

Microsoft-Entwickler sollten eine FWLink es sei denn, es eine Verknüpfung zur Hilfe Benutzer haben möglicherweise manuell eingeben, in der Fall ist, verwenden einen Link aka.ms (solange das Ziel der URL eine Website, die automatisch das Gebietsschema ein Browser, z. B. Docs.microsoft.com erkennt ist) verwenden

### Text-Richtlinien 

- Verwenden Sie vollständige Sätze.
- Schließen Sie keine am Satzende mit Ausnahme von Fragezeichen. 
- Sie müssen nicht den gleichen Text als Aufgabentitel verwenden. Verwenden Sie Text, der im Kontext der Benutzeroberfläche sinnvoll ist, aber stellen Sie sicher, dass eine logische Verbindung zwischen den beiden besteht. Beispiel: 
- Link zur Hilfe: Was sind die Risiken zulassen von Ausnahmen? 
- Hilfethema: "Ein Programm für die Kommunikation über Windows-Firewall zulassen"
- So spezifisch wie möglich über den Inhalt der im Hilfethema sein. 
    - Unsere Stil
        - Wie trägt Windows-Firewall zum Schutz des Computers?
        - Warum ein Bild Highlights verbessert werden kann
    - Nicht unsere Stil
        - Weitere Informationen zu Windows-Firewall
        - Erfahren Sie mehr über Farbe management
        - Mehr erfahren
- Verwenden Sie den gesamten Satz für den Text des Links, nicht nur die Wörter Key. 
    - Unsere Stil 
        - [Was sind die Risiken zulassen von Ausnahmen?]()
    - Nicht unsere Stil
        - Was sind die [Risiken zulassen von Ausnahmen]()? 

## Fehlermeldungen

Hier sehen Sie einige Richtlinien aus der Windows-Formatanleitungen anzupassen:

Schreiben eine gute Nachricht ist ein ausgewogenes Verhältnis zwischen genügend Erläuterung bereitstellen, aber nicht die übermäßig technische; zwischen eingestellt Ungezwungen und Verhalten jedoch keine störende oder anstößige Inhalte enthalten.

### Allgemeine Richtlinien

Verwenden Sie eine Nachricht pro Fehler Groß-/Kleinschreibung.

#### Überschriften

- Fassen Sie sich kurz und erklären Sie prägnant, was das Problem ist oder **im Idealfall was zu tun ist**. <br>Einige UI-Oberflächen möglicherweise Überschriften, die anstelle von umschließen, wenn sie zu lang sind abgeschnitten, achten Sie also für diese.
- Verwenden Sie die Projektmappe in der Überschrift, wenn sie einen einfachen Schritt ist.
- Stellen Sie sicher, dass die Überschrift direkt auf die Schaltfläche "bezieht sich für den Fall, dass Sie der Reader den Textkörper ignoriert.
- Verwenden Sie keine "Ist ein Problem aufgetreten" in Überschriften, es sei denn, Sie keine andere Wahl haben. Seien Sie mehr über das Problem spezifisch.
- Verwenden Sie keine Variablen (z. B. Dateien, Ordnern und app-Namen) in Überschriften. Verwenden sie den Text.

#### Textkörper

- Wenn die Überschrift ausreichend das Problem oder die Projektmappe wird erläutert, benötigen Sie keine Textkörper.
- Wiederholen Sie nicht den Titel in der Meldung mit anderen Worten.
- Deutlich zu kommunizieren und prägnant was die Lösung ist.
- Konzentrieren Sie sich auf die Fakten zuerst erteilen.
- Nicht allem Benutzer für den Fehler.
- Liegt ein Fehlercode mit dem Fehler verknüpft ist und wenn Sie der Meinung sind, einschließlich den Fehlercode der Kunden oder Microsoft-Support, um das Problem untersuchen hilfreiche direkt unterhalb der Textkörper enthalten und Schreiben Sie es wie folgt:

    Fehlercode: ###

    Wenn der Kunde alle Informationen zum Beheben des Fehlers ohne den Code verfügt, müssen Sie nicht einschließen.

#### Schaltflächen

- Schreiben von Text der Schaltfläche, damit sie eine spezifische Antwort auf die hauptanweisung ist. Wenn dies nicht möglich ist, verwenden Sie "Schließen" für den Schaltflächentext Kündigung (anstelle von "In Ordnung" oder "Fertig").
- Wenn Sie mehr als eine Schaltfläche "haben, stellen der am weitesten links stehende Schaltfläche" der Aktion, die der Benutzer empfohlen wird, um zu ergreifen. Stellen Sie der am weitesten rechts stehende Schaltfläche die stärker einschränkende Aktion, z. B. "" Abbrechen"."

#### Hilfelinks

Berücksichtigen Sie dabei nur Hilfelinks für Fehlermeldungen, die Sie bestimmte und aussagekräftig herstellen können.

## Zustand NULL text

Hier sehen Sie einige Informationen aus der Styleguide für Windows.

Zustand NULL tritt auf, wenn Kundendaten oder Inhalte nicht vorhanden ist aus einer app oder ein Feature, wenn keine Ergebnisse zurückgegeben werden nach einer Suche oder bei Bedarf fehlen Informationen eines Formulars, z. B. Abrechnungsinformationen für eine Transaktion.

### Anleitungen

 - Verwenden Sie möglichst Zustand null Situationen als Gelegenheit enthalten, die Menschen dazu, wie Sie das Feature (z. B. wie Musik, hinzugefügt, in denen suchen Bilder usw.) verwenden, erklären  
- Wenn Sie einen Titel in Ihrer Benutzeroberfläche haben, erklären Sie die Aktion um "Update" Zustand null (z. B. "Musik hinzufügen") 
- Spaß mit dem Text. Hier kann Spass bereitzustellen, da er wahrscheinlich nicht mehrmals angezeigt wird. 
- Vermeiden Sie "Es ist einsames hier." Dies ist hilfreich und hat verwendet wurde. 
- Vermeiden Sie Fragen wie "Noch nicht Ihr Drucker verbunden?" OK einmal, aber dieses Format in der Regel übermäßiger abrufen, und Fragen erstmals zusätzlichen Aufwand/Druck des Kunden. Sie können auch condescending sich so anfühlt. 
- Verschiedene im Zustand null Text ist gut. 

### Beispiele

- "Eine Person als Favoriten hinzufügen, und Sie sehen sie hier."
- "Haben Sie alle Erfolge oder spielclips, die Sie besonders stolz? Fügen sie Sie Ihre Showcase."
- "Niemand des in einer Partei noch nicht. Starten!"
- "Wenn ein Benutzer Sie als Freund hinzufügt, diese hier sehen Sie."
- "Wenn Sie die erforderlichen Schritte wie Erfolge freischalten und spielclips aufzeichnen Freunde, es alle hier sehen Sie."
- "Ihre bevorzugten Freunde werden hier angezeigt, damit Sie sehen können, wenn sie online sind und was sind bis zu."

## Zeichensetzung

- Keine Interpunktion am Ende (Punkte, Fragezeichen) für Überschriften oder unvollständigen Sätze. Eine Ausnahme ist in ein Bestätigungsdialogfeld, in dem die Überschrift die Frage ist
- Verwenden Sie Microsoft-Styleguideanleitungen für [Punkte](https://docs.microsoft.com/style-guide/punctuation/periods) und [Fragezeichen](https://docs.microsoft.com/style-guide/punctuation/question-marks).

## Statusnachrichten

Statusnachrichten bestehen aus Popup (Toast)-Nachrichten und Benachrichtigungen.

|String-Typ         | Anmerkungen                               |
|------------        |-------------------------------------|
|Popup               |Zeichensetzung am Satzende - idealerweise mit einer Objektvariable, damit Benutzer verstehen, welches Objekt die Nachricht betrifft, für den Fall, dass sie sich vom Objekt entfernt haben|
|Überschrift für Benachrichtigungen|Keine Zeichensetzung am Satzende (für Überschriften) - idealerweise mit einer Objektvariablen|
|Benachrichtigungsdetails|Vollständige Sätze, idealerweise mit Links zur Benutzeroberfläche, die das Objekt anzeigt|

Es folgen einige detaillierten Empfehlungen für die Benachrichtigung aus:

|String-Typ         | Anmerkungen                               |
|------------        |-------------------------------------|
|Gestartet             |Sollte ausgelassen werden, wenn möglich - sie können in der Regel die Nachricht in Bearbeitung überspringen und so die Anzahl der Ablenkungen minimieren.|
|In Bearbeitung         |Beginnen Sie mit dem Verb der Aktion, die Sie durchführen und enden Sie mit Ellipsen, um einen laufenden Vorgang anzugeben. Beispiel:<br> *Erstellen des Volumes "Kundendaten"...*|
|Erfolgreich             |Beginnen Sie mit "Erfolgreich" und enden Sie mit dem Vorgang der Software. Beispiel:<br> *Das Volume "Kundendaten" wurde erfolgreich erstellt.*|
|Fehler             |Beginnen Sie mit "Konnte nicht" und enden Sie damit, was die Software nicht konnte. Beispiel:<br> *Das Volume konnte die "Kundendaten" nicht erstellen.*|

## QuickInfos

Gute QuickInfos kurz beschrieben, ohne Bezeichnung Steuerelemente oder etwas zusätzliche Informationen für mit der Bezeichnung Steuerelemente bereitstellen, wenn dies sinnvoll ist. Sie können auch die Kunden, die die Benutzeroberfläche bietet zusätzliche Jahre – nicht redundant – Informationen steuerelementbeschriftungen, Symbole, Links.

QuickInfos sollte nur selten oder gar nicht verwendet werden. Sie können eine Unterbrechung an den Kunden, daher keine QuickInfo enthalten, die einfach wiederholt wird eine Beschriftung oder Zustände der offensichtlich sein. Es sollte immer wertvolle Informationen hinzufügen.

|    Kontext                                 |    Informationen zum Schreiben von QuickInfos    |
|    -----------------------                 |    -------------------------    |
|Wenn ein Steuerelement oder UI-Element ohne Bezeichnung ist …|Verwenden Sie einen einfache, beschreibende substantivierten Ausdruck. Beispiel:<br> Hervorheben Stift |
|Wenn ein UI-Element wird mit der Bezeichnung, doch deren Zweck benötigt Klarstellung …|<ul><li>Beschreiben Sie kurz, wofür Sie dieses UI-Element verwenden können. </li><li>Verwenden Sie das Formular imperativen Verb. Beispielsweise "Suchen von Text in diese Datei" (nicht "sucht Text in diese Datei").</li><li>Fügen Sie keine Interpunktion am Ende, es sei denn, es mehrere vollständige Sätze gibt.</li> </ul>|
|Wenn eine Beschriftung abgeschnitten oder in einigen Sprachen Abschneiden wahrscheinlich ist …|<ul><li>Geben Sie die ungekürzte Bezeichnung in der QuickInfo.</li><li>Optional: In einer anderen Position bieten Sie eine Zusammenhänge Beschreibung, aber nur bei Bedarf.</li><li>Eine QuickInfo nicht bereitgestellt werden, wenn die ungekürzte Informationen an anderer Stelle auf der Seite oder des Flusses bereitgestellt wird.</li></ul>|
|Wenn eine Tastenkombination verfügbar ist …|<ul><li>Optional: Bieten Sie die Tastenkombination in runden Klammern nach der Beschriftung oder beschreibende Begriff, z. B. "Drucken (STRG + P)" oder "Suchen von Text in dieser Datei (STRG + F)"</li><li>Es ist in Ordnung, eine nützliche Tastenkombination zu einer Zusammenhänge QuickInfo hinzuzufügen und zu vermeiden, Hinzufügen einer QuickInfos nur um eine Tastenkombination anzuzeigen. </li></ul>|