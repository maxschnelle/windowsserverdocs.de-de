---
title: Windows Admin Center Text- und Designformatanleitung
description: Windows Admin Center UI-Text und Design Style Guide SDK
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 159202fcb8c6125134154094e67e862ce8eb12ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357029"
---
# <a name="windows-admin-center-ui-text-and-design-style-guide"></a>Windows Admin Center Text- und Designformatanleitung

>Gilt für: Windows Admin Center

In diesem Thema wird der allgemeine Ansatz zum Schreiben von Text in Benutzeroberflächen (UI) für Windows Admin Center als auch einige bestimmte Konventionen und Ansätze behandelt.

Windows Admin Center und andere Erweiterungen sollten [Microsofts VoIP-Prinzipien](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human) folgen, damit die Erfahrung benutzerfreundlich ist. Diese Entwurfsrichtlinien basieren auf folgenden Sprachprinzipien genau wie der [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/), stellen Sie daher sicher, dass Sie beide Ressourcen für Informationen über die [Eingabehilfen](https://docs.microsoft.com/style-guide/accessibility/accessibility-guidelines-requirements), [Akronyme](https://docs.microsoft.com/style-guide/acronyms)und [Wortwahl](https://docs.microsoft.com/style-guide/word-choice/)haben, wie beispielsweise [Bitte](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/p/please) und [Entschuldigung](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/s/sorry).

## <a name="buttons"></a>Schaltflächen

- Schaltflächen sollten möglicherweise ein Wort enthalten, besonders dann, wenn Sie das Tool lokalisieren möchten. Zwei oder drei ist in Ordnung, aber versuchen Sie, länger zu vermeiden. Wenn Sie über vier Wörter oder länger verfügen, wäre es besser, ein Link Steuerelement zu verwenden.
- Schaltflächenetikette sollten präzise, bestimmt und selbsterklärend sein. Anstelle der generischen Schaltfläche "Übermitteln", verwenden Sie ein Verb für die Aktion des Benutzers, wie "Erstellen", "Löschen", "Hinzufügen", "Formatieren" usw.
- Wenn eine Schaltfläche auf eine Frage folgt, sollte dessen Beschriftung der Frage deutlich entsprechen (in der Regel "Ja" oder "Nein").

## <a name="capitalization"></a>Großschreibung

Wir folgen der Microsoft-Formatvorlage für die [Großschreibung](https://docs.microsoft.com/style-guide/capitalization) - der Verwendung der Satz-Groß-/Kleinschreibung für ziemlich alles.

| UI-Element              |Großschreibung|Kommentare|
|-------------------------|--------------|--------|
|Badges (beispielsweise PREVIEW) |Großbuchstaben      ||
|Alle anderen          |Satzstil|Es gibt jedoch einige Ausnahmen, bei denen Objekteigenschaften von WMI oder PowerShell in Betracht ziehen, die außerhalb unserer Steuerelement sind.|

## <a name="colons"></a>Doppelpunkte

Verwenden Sie Doppelpunkte zum Einführen von Listen. Zum Beispiel:

    Choose one of the following:
    Cats
    Dogs
    Quokkas

Verwenden Sie keinen Doppelpunkt in der Benutzeroberfläche, wenn sich eine Bezeichnung in einer anderen Zeile als die Bezeichnung befindet oder wenn zwischen der Bezeichnung und der Bezeichnung eindeutig unterschieden wird.

Verwenden Sie Doppelpunkte in Benutzeroberflächen Text, wenn sich eine Bezeichnung in derselben Zeile wie der Text befindet, den Sie bezeichnet, und dass die beiden Elemente nicht gleichzeitig ausgeführt werden müssen.

## <a name="confirmation-messages"></a>Bestätigungsnachrichten

Bestätigungs Dialogfelder sind hilfreich, wenn die Fortsetzung unerwartete Ergebnisse aufweisen kann, z. b. Datenverlust. Sie sollten scanable, nützliche Informationen mit einem klaren Ergebnis enthalten, insbesondere bei Ereignissen, die nicht rückgängig gemacht werden können. 

- Stellen Sie sicher, dass eine Bestätigung erforderlich ist. Wenn keine neuen Informationen zur Verfügung stehen (z. b. "sind Sie sicher?"), ist möglicherweise keine Bestätigungsmeldung erforderlich.  
- Vergewissern Sie sich, dass der Kunde die Aktion fortsetzen möchte.
- Stellen Sie sicher, dass die Haupt Anweisung (Überschrift) und der erklärende Text (Body) nicht redundant sind.
- Definieren Sie in der Überschrift die möglichen Ergebnisse als Frage oder eine-Anweisung darüber, was als nächstes geschieht. Beispiel: "Löschen Sie alle Daten auf diesem Laufwerk? oder "Sie sind im Begriff, alle Ihre Daten zu löschen".
- Fügen Sie Details im Text hinzu. Wenn eine Variable vorhanden ist, z. b. der Name des Elements, das Sie ändern möchten, fügen Sie Sie hier ein.
- Fügen Sie eine einfache Frage (entweder im Header oder im Text) ein, die eine klare Auswahl zwischen zwei Aktions Schaltflächen bildet.
- Verwenden Sie für eine komplexe Auswahl die Schaltflächen Ja/Nein, um das sorgfältige lesen zu unterstützen. Verwenden Sie für eine einfachere Auswahl Schaltflächen, die für die Aktion spezifisch sind, z. b. "Alle löschen" oder "Abbrechen".

## <a name="first-run-experiences"></a>Oberfläche für den ersten Testlauf

Das ersten Mal, wenn ein Benutzer eine Seite besucht, haben Sie die Möglichkeit, ihn bei der Benutzung des Tools zu unterstützen. Dies kann folgendes sein:

- Eine Textzeichenfolge in einer leeren Seite mit kurzen Anweisungen zum Start - wählen Sie zum Beispiel""Hinzufügen", um eine App hinzuzufügen."
- Eine Verknüpfung mit dem Steuerelement, das dem Benutzer beim Start hilft – beispielsweise "Fügen Sie eine App hinzu, um zu beginnen".
- Eine kurze Animation oder ein Video, die den Benutzern die Konfiguration erklärt

Hier sind einige Tipps aus unserem Styleguide für Windows:

### <a name="1-be-helpful"></a>1. Seien Sie behilflich

- Vermeiden Sie Marketingstil und -Sprache.
- Wenn Sie eine Demo durchführen oder etwas vorschlagen, stellen Sie sicher, dass das Endergebnis eindeutig ist. die Vorgehensweise, mit der der Kunde etwas zu tun hat, ist nicht effektiv, wenn Sie nicht wissen, warum dies der Fall ist.
- Stellen Sie keine Tipps vor, wenn der Kunde Sie nicht benötigt.

### <a name="2-show-dont-tell"></a>2. Anzeigen, nicht sagen

Halten Sie Ihren Text so einfach wie möglich (kleine Animationen oder Videos).

### <a name="3-dont-overwhelm"></a>3. Nicht überfordern

- Beschränken Sie Popups und Tipps auf 4 pro Sitzung – einschließlich Systembenachrichtigungen und Shell-Benachrichtigungen.
- Stellen Sie sicher, dass die Popups zeitlich hilfreich sind.
- Verhindern Sie, dass der Kunde etwas tut.
- Stellen Sie sicher, dass Popups auf einfache Weise geschlossen werden.

### <a name="4-keep-it-contextual"></a>4. Kontextbezogen beibehalten

- Lernphasen sind am effektivsten, wenn sie zur richtigen Zeit angezeigt werden.
- Wenn Sie Lernprogramme oder Bildschirmpräsentationen erstellen, machen Sie die Infos konkret.
- Kein Marketing "Geplapper" – Schwerpunkt auf bestimmte Tipps und Tricks.
- Bieten Sie Kunden die Möglichkeit, später zum Tutorial zurückzukehren, falls dies relevant ist (Personen, die die Informationen zum ersten Mal nicht aufbewahren, aber die Setup Anweisungen sind möglicherweise nur einmal relevant).
- Leerstatusanzeigen sind ein natürlicher Platz zum Lernen und/oder Spass – bleiben Sie einfach und informativ.

### <a name="5-minimize-painful-setup"></a>5. Minimieren Sie das mühsam

Wenn der Kunde zum Ausführen des vollständigen Umgebung mehr Aktionen benötigt (Anmeldung an einem Onlinedienst usw.), machen Sie es so einfach wie möglich.

- Nachrichten sollten kurz und direkt sein.
- Vermeiden sie das sofortige Senden. Wenn möglich, bieten Sie eine Möglichkeit für die Verbindung vom Standort aus.
- Wenn möglich, bieten Sie die Option, die Aktion später durchzuführen, und erinnern Sie den Benutzer später daran.
- Wenn Sie die Aktion wechseln, geben Sie eine Möglichkeit, schnell und einfach wieder zurückzukehren.

## <a name="help-links"></a>Hilfe Links

Hier sind einige Tipps aus unserem Styleguide für Windows:

### <a name="when-should-we-provide-a-help-link"></a>Wann sollte ein Hilfelink bereitgestellt werden?

Fast nie. Geben Sie nur dann einen Hilfelink an, wenn:

- Es gibt eine offensichtliche und wichtige Frage, die Kunden wahrscheinlich haben, während Sie sich in der Benutzeroberfläche befinden. die Antwort darauf hilft Ihnen, bei der UI-Aufgabe erfolgreich zu sein. 
- In der Benutzeroberfläche ist nicht genügend Speicherplatz vorhanden, um die erforderliche Menge an Informationen bereitzustellen, damit Benutzer bei der UI-Aufgabe erfolgreich sein können. 

### <a name="where-should-help-links-appear"></a>Wo sollen Hilfe Links angezeigt werden? 

- Text Verknüpfungen sollten in der Nähe des Elements der Benutzeroberfläche angezeigt werden, auf die die Hilfe so weitergeleitet wird. 
- Wenn Sie einen Textlink angeben müssen, der für einen gesamten Bildschirm der Benutzeroberfläche gilt, platzieren Sie ihn unten links auf dem Bildschirm. 
- Wenn Sie über eine Hilfe Schaltfläche (?) einen Link bereitstellen, sollte die QuickInfo "Help" lauten.

### <a name="what-url-should-we-use"></a>Welche URL sollte verwendet werden?

Verknüpfen Sie niemals direkt mit einer Webadresse – verwenden Sie stattdessen einen Umleitungs Dienst.

Microsoft-Entwickler sollten einen fwlink verwenden, außer wenn es sich um einen Hilfelink handelt, den Benutzer möglicherweise manuell eingeben müssen. in diesem Fall verwenden Sie einen aka.MS-Link (sofern das Ziel der URL eine Website ist, die das Browser Gebiets Schema automatisch erkennt, z. b. docs.Microsoft.com).

### <a name="text-guidelines"></a>Text Richtlinien 

- Verwenden Sie vollständige Sätze.
- Fügen Sie keine endpunktierungen mit Ausnahme von Fragezeichen ein. 
- Sie müssen nicht denselben Text wie den Aufgaben Titel verwenden. Verwenden Sie Text, der im Kontext der Benutzeroberfläche sinnvoll ist, aber stellen Sie sicher, dass zwischen den beiden eine logische Verbindung besteht. Zum Beispiel: 
- Hilfelink: Welche Risiken besteht darin, Ausnahmen zuzulassen? 
- Titel des Hilfe Themas: "Zulassen, dass ein Programm über die Windows-Firewall kommuniziert"
- Gehen Sie so spezifisch wie möglich zum Inhalt des Hilfe Themas. 
    - Unser Stil
        - Wie unterstützt die Windows-Firewall den Schutz meines Computers?
        - Warum Highlights ein Bild verbessern können
    - Nicht unser Stil
        - Weitere Informationen zur Windows-Firewall
        - Weitere Informationen zur Farbverwaltung
        - Mehr erfahren
- Verwenden Sie den gesamten Satz für den Linktext, nicht nur die Schlüsselwörter. 
    - Unser Stil 
        - [Welche Risiken besteht darin, Ausnahmen zuzulassen?]()
    - Nicht unser Stil
        - Welche [Risiken besteht darin, Ausnahmen zuzulassen]()? 

## <a name="error-messages"></a>Fehlermeldungen

Im folgenden finden Sie einige Anleitungen, die im Windows-Stil Handbuch beschrieben werden:

Das Schreiben einer guten Nachricht ist ein Gleichgewicht zwischen der Bereitstellung einer ausreichenden Erläuterung, aber nicht übermäßig technisch. zwischen dem Gelegenheits-und personalisierbaren, aber nicht ärgerlichem oder anstößigen

### <a name="general-guidelines"></a>Allgemeine Richtlinien

Verwenden Sie eine Nachricht pro Fehlerfall.

#### <a name="headings"></a>He

- Informieren Sie sich darüber, was das Problem ist oder **was ideal**ist. <br>Einige Oberflächen Oberflächen verfügen möglicherweise über Überschriften, die abgeschnitten werden, anstatt Sie zu überspringen, wenn Sie zu lang sind. Achten Sie daher darauf.
- Verwenden Sie die Projekt Mappe in der Überschrift, wenn es sich um einen einfachen Schritt handelt.
- Stellen Sie sicher, dass die Überschrift direkt mit der Schaltfläche verknüpft ist, wenn der Reader den Textkörper Text ignoriert.
- Vermeiden Sie die Verwendung von "Es gab ein Problem" in Überschriften, es sei denn, Sie haben keine andere Wahl. Spezifischere Informationen zum Problem.
- Vermeiden Sie die Verwendung von Variablen (wie Datei-, Ordner-und APP-Namen) in Überschriften. Fügen Sie Sie in den Text ein.

#### <a name="body"></a>Text

- Wenn die Überschrift ausreichend das Problem oder die Lösung erläutert, benötigen Sie keinen Textkörper.
- Wiederholen Sie den Titel in der Nachricht nicht mit einem etwas anderen Wortlaut.
- Kommunizieren Sie eindeutig, und verdeutlichen Sie genau, was die Lösung ist.
- Konzentrieren Sie sich darauf, die Fakten zuerst zu geben.
- Machen Sie die Benutzer nicht für den Fehler verantwortlich.
- Wenn dem Fehler ein Fehlercode zugeordnet ist und Sie der Ansicht sind, dass der Fehlercode durch Einschließen des Fehlercodes dem Kunden oder dem Microsoft-Support helfen kann, das Problem zu untersuchen, fügen Sie ihn direkt unterhalb des Text Texts ein, und schreiben Sie ihn wie folgt:

    Fehlercode: ####

    Wenn der Kunde über alle erforderlichen Informationen zum Beheben des Fehlers ohne den Code verfügt, müssen Sie ihn nicht einschließen.

#### <a name="buttons"></a>Schaltflächen

- Schreiben Sie den Schaltflächen Text, sodass er eine bestimmte Antwort auf die main-Anweisung ist. Wenn dies nicht möglich ist, verwenden Sie "Close" für den Text der Kündigungs Schaltfläche (anstelle von "okay" oder "Done").
- Wenn Sie über mehr als eine Schaltfläche verfügen, legen Sie die Schaltfläche ganz links auf die Aktion fest, die für den Benutzer empfohlen wird. Legen Sie die Schaltfläche ganz rechts auf die konservative Aktion (z. b. "Abbrechen").

#### <a name="help-links"></a>Hilfe Links

Beachten Sie nur Hilfe Links zu Fehlermeldungen, die Sie nicht speziell und Handlungs relevant machen können.

## <a name="null-state-text"></a>NULL-Zustands Text

Im folgenden finden Sie eine Hilfe im Windows-Stil Handbuch.

Der Status NULL tritt auf, wenn Kundendaten oder-Inhalte nicht in einer APP oder einem Feature fehlen, wenn nach einer Suche keine Ergebnisse zurückgegeben werden oder wenn erforderliche Informationen in einem Formular fehlen, wie z. b. Abrechnungsinformationen für eine Transaktion.

### <a name="guidelines"></a>Richtlinien

- Verwenden Sie nach Möglichkeit NULL-Status Situationen als Gelegenheit, Personen darüber zu informieren, wie Sie das Feature verwenden können (z. b. Hinzufügen von Musik, wo Sie Bilder finden usw.).  
  - Wenn Sie in der Benutzeroberfläche über einen Titel verfügen, erklären Sie die Aktion, die Sie zum "korrigieren" des NULL-Zustands ausführen müssen (z. b. "Add some Music"). 
  - Sie haben Spaß mit dem Text. Dieser Platz kann eine Gelegenheit sein, Freude zu schaffen, da er wahrscheinlich nicht mehrmals angezeigt wird. 
  - Vermeiden Sie "Es ist einsam hier." Dies ist traurig und wurde über ausgelastet. 
  - Vermeiden Sie Fragen wie "Ihr Drucker wurde nicht verbunden?" Sie können einmal verwenden, doch dieses Format wird tendenziell überlastet, und Fragen werden dem Kunden zusätzliche Belastung und Belastung ausgesetzt. Dies kann auch als absteigend angezeigt werden. 
  - Die Vielfalt im Text des NULL-Zustands ist eine gute Sache. 

### <a name="examples"></a>Beispiele

- "Jemand als Favorit hinzufügen, und Sie sehen Sie hier."
- "Haben Sie alle Erfolge oder Spiel Clips, von denen Sie besonders stolz sind? Fügen Sie Sie Ihrem Showcase hinzu. "
- "Es gibt noch keine Partei in einer Partei. Starten Sie einen! "
- "Wenn jemand Sie als Freund hinzufügt, werden Sie hier angezeigt."
- "Wenn Sie die Ergebnisse entsperren, Spiele Ausschnitte aufzeichnen und Freunde hinzufügen, sehen Sie alles hier."
- "Ihre bevorzugten Freunde werden hier angezeigt, sodass Sie sehen können, wann Sie online sind und was Sie sind."

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
|Erfolgreich             |Beginnen Sie mit "Erfolgreich" und enden Sie mit dem Vorgang der Software. Im Folgenden ein Beispiel:<br> *Das Volume "Kundendaten" wurde erfolgreich erstellt.*|
|Nicht möglich             |Beginnen Sie mit "Konnte nicht" und enden Sie damit, was die Software nicht konnte. Im Folgenden ein Beispiel:<br> *Das Volume "Kundendaten" konnte nicht erstellt werden.*|

## <a name="tooltips"></a>QuickInfos

Gute Quick Infos beschreiben kurz nicht beschriftete Steuerelemente oder geben einige zusätzliche Informationen für beschriftete Steuerelemente an, wenn dies nützlich ist. Sie können Kunden außerdem beim Navigieren in der Benutzeroberfläche helfen, indem Sie zusätzliche – nicht redundante – Informationen zu Steuerelement Bezeichnungen, Symbolen, Links usw. anbieten.

Quick Infos sollten sehr sparsam oder gar nicht verwendet werden. Dies kann eine Unterbrechung des Kunden sein. nehmen Sie also keine QuickInfo auf, die einfach eine Bezeichnung wiederholt oder die offensichtliche angibt. Er sollte immer wertvolle Informationen hinzufügen.

|    Kontext                                 |    Schreiben der Quick Infos    |
|    -----------------------                 |    -------------------------    |
|Wenn ein Steuerelement oder ein Benutzeroberflächen Element nicht beschriftet ist...|Verwenden Sie einen einfachen, beschreibenden Substantiv Ausdruck. Zum Beispiel:<br> Stift hervorheben |
|Wenn ein Benutzeroberflächen Element gekennzeichnet ist, aber sein Zweck eine Erläuterung erfordert...|<ul><li>Beschreiben Sie kurz, was Sie mit diesem UI-Element tun können. </li><li>Verwenden Sie das imperative Verb-Formular. Beispiel: "Text in dieser Datei suchen" (nicht "sucht nach Text in dieser Datei").</li><li>Schließen Sie keine Endpunkte ein, es sei denn, es gibt mehrere vollständige Sätze.</li> </ul>|
|Wenn eine Text Bezeichnung abgeschnitten wird oder in einigen Sprachen abgeschnitten wird...|<ul><li>Geben Sie die nicht gekürzte Bezeichnung in der QuickInfo an.</li><li>Optional: Geben Sie in einer anderen Zeile eine Beschreibungs Beschreibung ein, jedoch nur bei Bedarf.</li><li>Geben Sie keine QuickInfo an, wenn die nicht abgeschnittene Informationen an anderer Stelle auf der Seite oder im Flow bereitgestellt werden.</li></ul>|
|Wenn eine Tastenkombination verfügbar ist...|<ul><li>Optional: Geben Sie die Tastenkombination in Klammern nach der Bezeichnung oder dem beschreibenden Ausdruck an, z. b. "Print (STRG + P)" oder "Text in dieser Datei suchen (STRG + F)"</li><li>Es ist in Ordnung, eine hilfreiche Tastenkombination zu einer QuickInfo-QuickInfo hinzuzufügen. vermeiden Sie jedoch, eine QuickInfo hinzuzufügen, um eine Tastenkombination anzuzeigen. </li></ul>|