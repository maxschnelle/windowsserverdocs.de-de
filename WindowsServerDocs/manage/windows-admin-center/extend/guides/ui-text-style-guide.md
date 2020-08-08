---
title: Windows Admin Center UI-Text und Entwurfs Stil Handbuch
description: Windows Admin Center UI-Text und Design Style Guide SDK
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 01/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: a784bdfdfbfbbc4f91579d40cedb22230a70b13a
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993583"
---
# <a name="windows-admin-center-ui-text-and-design-style-guide"></a>Windows Admin Center UI-Text und Entwurfs Stil Handbuch

>Gilt für: Windows Admin Center

In diesem Thema wird der allgemeine Ansatz zum Schreiben von Text der Benutzeroberfläche (UI) für das Windows Admin Center sowie einige spezifische Konventionen und Ansätze beschrieben.

Das Windows Admin Center und alle Erweiterungen sollten den [sprach Prinzipien von Microsoft](/style-guide/brand-voice-above-all-simple-human) folgen, damit die Benutzerfreundlichkeit einfach zu verwenden und benutzerfreundlich ist. Dieser Stil Leitfaden baut auf diesen sprach Prinzipien und dem Microsoft- [Leitfaden für Schreib](/style-guide/welcome/)Vorgänge auf. Achten Sie daher darauf, dass Sie sich diese beiden Ressourcen ansehen, um Informationen zu den Themen wie [Barrierefreiheit](/style-guide/accessibility/accessibility-guidelines-requirements), [Akronyme](/style-guide/acronyms)und [Word](/style-guide/word-choice/) -Auswahl [sorry](/style-guide/a-z-word-list-term-collections/s/sorry)zu [erhalten](/style-guide/a-z-word-list-term-collections/p/please).

## <a name="buttons"></a>Schaltflächen

- Schaltflächen sollten immer ein Wort sein, insbesondere, wenn Sie planen, das Tool zu lokalisieren. Zwei oder drei ist in Ordnung, aber versuchen Sie, länger zu vermeiden. Wenn Sie über vier Wörter oder länger verfügen, wäre es besser, ein Link Steuerelement zu verwenden.
- Schaltflächen Bezeichnungen sollten präzise, spezifisch und selbsterklärend sein. Verwenden Sie anstelle einer generischen Schaltfläche "Senden" ein Verb, das der Benutzeraktion entspricht, z. b. "erstellen", "Löschen", "hinzufügen", "Format" usw.
- Wenn eine Schaltfläche einer Frage folgt, sollte ihre Bezeichnung eindeutig der Frage entsprechen (in der Regel "yes" oder "No").

## <a name="capitalization"></a>Großschreibung

Wir folgen dem [Microsoft-Stil](/style-guide/capitalization) für die Groß-/Kleinschreibung. verwenden Sie die Groß-/Kleinschreibung im Satz.

| Benutzeroberflächenelement              |Großschreibung|Kommentare|
|-------------------------|--------------|--------|
|Abzeichen (z. b. Vorschau) |Alle Obergrenzen      ||
|Alle anderen          |Satz Stil|Es gibt jedoch einige Ausnahmen, bei denen wir Objekteigenschaften aus WMI oder PowerShell außerhalb unserer Kontrolle ablegen.|

## <a name="colons"></a>Doppelpunkte

Verwenden Sie Doppelpunkte zum Einführen von Listen. Zum Beispiel:

Wählen Sie eine der folgenden Optionen aus:

Katzen Hunde quokkas

Verwenden Sie keinen Doppelpunkt in der Benutzeroberfläche, wenn sich eine Bezeichnung in einer anderen Zeile als die Bezeichnung befindet oder wenn zwischen der Bezeichnung und der Bezeichnung eindeutig unterschieden wird.

Verwenden Sie Doppelpunkte in Benutzeroberflächen Text, wenn sich eine Bezeichnung in derselben Zeile wie der Text befindet, den Sie bezeichnet, und dass die beiden Elemente nicht gleichzeitig ausgeführt werden müssen.

## <a name="confirmation-messages"></a>Bestätigungsmeldungen

Bestätigungs Dialogfelder sind hilfreich, wenn die Fortsetzung unerwartete Ergebnisse aufweisen kann, z. b. Datenverlust. Sie sollten scanable, nützliche Informationen mit einem klaren Ergebnis enthalten, insbesondere bei Ereignissen, die nicht rückgängig gemacht werden können.

- Stellen Sie sicher, dass eine Bestätigung erforderlich ist. Wenn keine neuen Informationen zur Verfügung stehen (z. b. "sind Sie sicher?"), ist möglicherweise keine Bestätigungsmeldung erforderlich.
- Vergewissern Sie sich, dass der Kunde die Aktion fortsetzen möchte.
- Stellen Sie sicher, dass die Haupt Anweisung (Überschrift) und der erklärende Text (Body) nicht redundant sind.
- Definieren Sie in der Überschrift die möglichen Ergebnisse als Frage oder eine-Anweisung darüber, was als nächstes geschieht. Beispiel: "Löschen Sie alle Daten auf diesem Laufwerk? oder "Sie sind im Begriff, alle Ihre Daten zu löschen".
- Fügen Sie Details im Text hinzu. Wenn eine Variable vorhanden ist, z. b. der Name des Elements, das Sie ändern möchten, fügen Sie Sie hier ein.
- Fügen Sie eine einfache Frage (entweder im Header oder im Text) ein, die eine klare Auswahl zwischen zwei Aktions Schaltflächen bildet.
- Verwenden Sie für eine komplexe Auswahl die Schaltflächen Ja/Nein, um das sorgfältige lesen zu unterstützen. Verwenden Sie für eine einfachere Auswahl Schaltflächen, die für die Aktion spezifisch sind, z. b. "Alle löschen" oder "Abbrechen".

## <a name="first-run-experiences"></a>Oberfläche für den ersten Testlauf

Wenn ein Benutzer zum ersten Mal eine Seite besucht, haben Sie die Möglichkeit, den Einstieg in das Tool zu erleichtern. Dies könnte wie folgt lauten:

- Eine Text Zeichenfolge auf einer leeren Seite mit kurzen Anweisungen für den Einstieg, z. b. "SELECT ' Add ' zum Hinzufügen einer App".
- Ein Link zu dem Steuerelement, mit dem der Benutzer gestartet wird, z. b. "Hinzufügen einer APP zu den ersten Schritten".
- Eine kleine und kurze Animation oder ein Video, in dem der Benutzer die ersten Schritte anzeigt

Im folgenden finden Sie einige Tipps aus unserem Windows Style Guide:

### <a name="1-be-helpful"></a>1. seien Sie hilfreich

- Vermeiden Sie Marketing Stil und-Sprache.
- Wenn Sie eine Demo durchführen oder etwas vorschlagen, stellen Sie sicher, dass das Endergebnis eindeutig ist. die Vorgehensweise, mit der der Kunde etwas zu tun hat, ist nicht effektiv, wenn Sie nicht wissen, warum dies der Fall ist.
- Stellen Sie keine Tipps vor, wenn der Kunde Sie nicht benötigt.

### <a name="2-show-dont-tell"></a>2. anzeigen, nicht teilen

Halten Sie Ihren Text so einfach wie möglich (denken Sie an kleine Animationen oder Videos).

### <a name="3-dont-overwhelm"></a>3. nicht überfordern

- Beschränken Sie Popups und Tipps auf eine Kombination aus 4 pro Nutzungs Sitzung – einschließlich System Benachrichtigungen und Shell-Benachrichtigungen.
- Stellen Sie sicher, dass die zeitliche Steuerung von Popups hilfreich ist.
- Verhindern Sie, dass der Kunde etwas tut.
- Stellen Sie sicher, dass Popups problemlos verworfen werden.

### <a name="4-keep-it-contextual"></a>4. bleiben Sie kontextbezogen.

- Lehr Momente sind am effektivsten, wenn Sie zum richtigen Zeitpunkt präsentiert werden.
- Wenn Sie Tutorials oder Diashows erstellen, behalten Sie die Informationen konkret bei.
- Kein Marketing "Fluff" – Schwerpunkt auf bestimmten Tipps und Tricks.
- Bieten Sie Kunden die Möglichkeit, später zum Tutorial zurückzukehren, falls dies relevant ist (Personen, die die Informationen zum ersten Mal nicht aufbewahren, aber die Setup Anweisungen sind möglicherweise nur einmal relevant).
- "Empty-State Messaging" ist eine natürliche Stelle zum Erlernen und/oder begeistern – es ist einfach und informativ.

### <a name="5-minimize-painful-setup"></a>5. minimieren von schmerzhafter Einrichtung

Wenn Sie möchten, dass der Kunde eine weitere Aktion ausführt, um den vollständigen Wert (Anmelden bei einem Onlinedienst usw.) auszuführen, machen Sie ihn so unkompliziert wie möglich.

- Messaging sollte kurz und direkt sein.
- Vermeiden Sie es, Sie zu senden. Stellen Sie nach Möglichkeit eine Möglichkeit zum Herstellen einer Verbindung her, wo Sie sich befinden.
- Wenn dies möglich ist, lassen Sie die Option später zu, und erinnern Sie diese später daran, dies zu tun.
- Wenn Sie diese nicht mehr benötigen, können Sie schnell und einfach zurück wechseln.

## <a name="help-links"></a>Hilfe Links

Im folgenden finden Sie einige Tipps aus unserem Windows Style Guide:

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
- Hilfelink: welche Risiken besteht darin, Ausnahmen zuzulassen?
- Hilfe Thementitel: "zulassen, dass ein Programm über die Windows-Firewall kommuniziert"
- Gehen Sie so spezifisch wie möglich zum Inhalt des Hilfe Themas.
    - Unser Stil
        - Wie unterstützt die Windows-Firewall den Schutz meines Computers?
        - Warum Highlights ein Bild verbessern können
    - Nicht unser Stil
        - Weitere Informationen zur Windows-Firewall
        - Weitere Informationen zur Farbverwaltung
        - Weitere Informationen
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

#### <a name="headings"></a>Überschriften

- Informieren Sie sich darüber, was das Problem ist oder **was ideal**ist. <br>Einige Oberflächen Oberflächen verfügen möglicherweise über Überschriften, die abgeschnitten werden, anstatt Sie zu überspringen, wenn Sie zu lang sind. Achten Sie daher darauf.
- Verwenden Sie die Projekt Mappe in der Überschrift, wenn es sich um einen einfachen Schritt handelt.
- Stellen Sie sicher, dass die Überschrift direkt mit der Schaltfläche verknüpft ist, wenn der Reader den Textkörper Text ignoriert.
- Vermeiden Sie die Verwendung von "Es gab ein Problem" in Überschriften, es sei denn, Sie haben keine andere Wahl. Spezifischere Informationen zum Problem.
- Vermeiden Sie die Verwendung von Variablen (wie Datei-, Ordner-und APP-Namen) in Überschriften. Fügen Sie Sie in den Text ein.

#### <a name="body"></a>Body

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

## <a name="punctuation"></a>Interpunktion

- Keine endende Interpunktions Zeichen (Zeiträume, Fragezeichen) für Überschriften oder unvollständige Sätze. Eine Ausnahme wird in einem Bestätigungs Dialogfeld angezeigt, in dem die Frage angezeigt wird.
- Verwenden Sie die Anleitung des Microsoft-Styleguides zu [Zeiträumen](/style-guide/punctuation/periods) und [Fragezeichen](/style-guide/punctuation/question-marks).

## <a name="status-messages"></a>Statusmeldungen

Status Meldungen bestehen aus Popup-und Benachrichtigungs Meldungen.

|Zeichen Folgentyp         | Hinweise                               |
|------------        |-------------------------------------|
|Toast               |Satz Fall mit endeinterpunktions Zeichen (idealerweise mit einer Objektvariablen), damit Benutzer erkennen können, auf welches Objekt die Nachricht angewendet wird, wenn Sie vom Objekt entfernt wurden.|
|Benachrichtigungs Überschrift (Titel) |Satz Fall ohne endende Interpunktions Zeichen (eine Überschrift), idealerweise mit einer Objektvariablen|
|Benachrichtigungsdetails|Vollständige Sätze, idealerweise mit einem Link zur Benutzeroberfläche, auf der das Objekt angezeigt wird|

Im folgenden finden Sie einige ausführliche Empfehlungen für Benachrichtigungs Meldungen:

|Zeichen Folgentyp         | Hinweise                               |
|------------        |-------------------------------------|
|Gestartet             |Nach Möglichkeit weglassen: Normalerweise können Sie einfach mit der in Bearbeitung befindlichen Nachricht fortfahren, um die Anzahl der Ablenkungen zu minimieren.|
|In Bearbeitung         |Beginnen Sie mit dem Verb der Aktion, die Sie ausführen, und beenden Sie mit Auslassungs Zeichen, um einen laufenden Vorgang anzuzeigen. Hier sehen Sie ein Beispiel:<br> *Das Volume "Kundendaten" wird erstellt...* <br><br>Wenn mehrere Variablen vorhanden sind, verwenden Sie dieses Muster: <br>*Der folgende virtuelle Computer wird gelöscht: {0} ; Host{1}* |
|Erfolg             |Beginnen Sie mit "erfolgreich", und beenden Sie das, was die Software soeben getan hat. Hier sehen Sie ein Beispiel:<br> *Das Volume "Customer Data" wurde erfolgreich erstellt.*|
|Fehler             |Beginnen Sie mit "was nicht", und beenden Sie den Funktionsumfang der Software. Hier sehen Sie ein Beispiel:<br> *Das Volume "Customer Data" konnte nicht erstellt werden.*|

## <a name="tooltips"></a>QuickInfos

Gute Quick Infos beschreiben kurz nicht beschriftete Steuerelemente oder geben einige zusätzliche Informationen für beschriftete Steuerelemente an, wenn dies nützlich ist. Sie können Kunden außerdem beim Navigieren in der Benutzeroberfläche helfen, indem Sie zusätzliche – nicht redundante – Informationen zu Steuerelement Bezeichnungen, Symbolen, Links usw. anbieten.

Quick Infos sollten sehr sparsam oder gar nicht verwendet werden. Dies kann eine Unterbrechung des Kunden sein. nehmen Sie also keine QuickInfo auf, die einfach eine Bezeichnung wiederholt oder die offensichtliche angibt. Er sollte immer wertvolle Informationen hinzufügen.

|    Kontext                                 |    Schreiben der Quick Infos    |
|    -----------------------                 |    -------------------------    |
|Wenn ein Steuerelement oder ein Benutzeroberflächen Element nicht beschriftet ist...|Verwenden Sie einen einfachen, beschreibenden Substantiv Ausdruck. Zum Beispiel:<br> Stift hervorheben |
|Wenn ein Benutzeroberflächen Element gekennzeichnet ist, aber sein Zweck eine Erläuterung erfordert...|<ul><li>Beschreiben Sie kurz, was Sie mit diesem UI-Element tun können. </li><li>Verwenden Sie das imperative Verb-Formular. Beispiel: "Text in dieser Datei suchen" (nicht "sucht nach Text in dieser Datei").</li><li>Schließen Sie keine Endpunkte ein, es sei denn, es gibt mehrere vollständige Sätze.</li> </ul>|
|Wenn eine Text Bezeichnung abgeschnitten wird oder in einigen Sprachen abgeschnitten wird...|<ul><li>Geben Sie die nicht gekürzte Bezeichnung in der QuickInfo an.</li><li>Optional: Geben Sie in einer anderen Zeile eine Beschreibungs Beschreibung an, aber nur bei Bedarf.</li><li>Geben Sie keine QuickInfo an, wenn die nicht abgeschnittene Informationen an anderer Stelle auf der Seite oder im Flow bereitgestellt werden.</li></ul>|
|Wenn eine Tastenkombination verfügbar ist...|<ul><li>Optional: Geben Sie die Tastenkombination in Klammern nach der Bezeichnung oder dem beschreibenden Ausdruck an, z. b. "Drucken (STRG + P)" oder "Text in dieser Datei suchen (STRG + F)".</li><li>Es ist in Ordnung, eine hilfreiche Tastenkombination zu einer QuickInfo-QuickInfo hinzuzufügen. vermeiden Sie jedoch, eine QuickInfo hinzuzufügen, um eine Tastenkombination anzuzeigen. </li></ul>|