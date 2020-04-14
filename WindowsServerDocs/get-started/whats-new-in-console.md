---
title: Neuerungen in der Windows-Konsole von Windows Server 2016
description: Listet wichtige neue Features in der Konsole von Windows Server 2016 auf.
ms.prod: windows-server
ms.technology: server-general
ms.date: 10/04/2016
ms.topic: article
ms.assetid: da9fc582-033b-4973-84e7-0c6024ecfcbc
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: b055c379e1d5ee632e420ffd1362389878d3dfd1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825963"
---
# <a name="whats-new-in-the-windows-console-in-windows-server-2016"></a>Neuerungen in der Windows-Konsole von Windows Server 2016
>Gilt für: Windows Server 2016

Der Konsolenhost (d. h. der zugrunde liegende Code, der alle Zeichenmodusanwendungen wie z. B. die Windows-Eingabeaufforderung, die Eingabeaufforderung von Windows PowerShell und andere unterstützt) wurde in mehrfacher Hinsicht aktualisiert und durch eine Reihe von neuen Funktionen ergänzt.  

## <a name="controlling-the-new-features"></a>Steuerung der neuen Features  
Die neuen Funktionen sind standardmäßig aktiviert, aber Sie können jedes neue Feature ein- und ausschalten oder zum vorherigen Konsolenhost zurückwechseln. Dazu verwenden Sie das Dialogfeld „Eigenschaften“ (meist auf der Registerkarte **Optionen**) oder die folgenden Registrierungsschlüssel (alle Schlüssel sind DWORD-Werte unter **HKEY_CURRENT_USER\Console**):  

|Registrierungsschlüssel|Beschreibung|  
|----------------|---------------|  
|ForceV2|1 aktiviert alle neuen Konsolenfeatures; 0 deaktiviert alle neuen Features. Hinweis: Dieser Schlüssel wird nicht in Verknüpfungen gespeichert, sondern nur in diesem Registrierungsschlüssel.|  
|LineSelection|1 aktiviert die Möglichkeit zum Markieren von Zeilen; mit 0 lässt sich nur der Blockmodus verwenden.|  
|FilterOnPaste|1 aktiviert das neue Einfügeverhalten.|  
|LineWrap|1 fügt beim Ändern der Größe des Konsolenfensters passende Zeilenumbrüche ein.|  
|CtrlKeyShortcutsDisabled|0 aktiviert neue Tastenkombinationen; 1 deaktiviert sie.|  
|ExtendedEdit Keys|1 aktiviert alle Auswahltasten auf der Tastatur; 0 deaktiviert sie.|  
|TrimLeadingZeros|1 kürzt führende Nullen in einer per Doppelklick vorgenommenen Auswahl; mit 0 werden die führenden Nullen beibehalten.|  
|WindowsAlpha|Legt für die Deckkraft einen Wert zwischen 30 % und 100 % fest. Verwenden Sie 0x4C bis 0xFF oder 76 bis 255, um den Wert festzulegen.|  
|WordDelimiters|Legt das Zeichen fest, auf das gesprungen wird, wenn in einem Text mithilfe von STRG+UMSCHALT+NACH-LINKS-TASTE oder STRG+UMSCHALT+NACH-RECHTS-TASTE ganze Wörter mit einem Mal markiert werden (Standardwert ist das Leerzeichen). Legen Sie diesen REG_SZ-Wert so fest, dass alle als Trennzeichen zu behandelnden Zeichen enthalten sind. Hinweis: Dieser Schlüssel wird nicht in Verknüpfungen gespeichert, sondern nur in diesem Registrierungsschlüssel.|  

Diese Einstellungen werden in der Registrierung für jeden einzelnen Fenstertitel unter „HKCU\Console“ gespeichert. Bei Konsolenfenstern, die über eine Verknüpfung geöffnet werden, werden diese Einstellungen in der Verknüpfung gespeichert. Wenn die Verknüpfung auf einen anderen Computer kopiert wird, werden die Einstellungen zusammen mit der Verknüpfung auf den neuen Computer übertragen. Einstellungen in Verknüpfungen setzen alle anderen Einstellungen außer Kraft, auch globale Einstellungen und Standardwerte. Wenn Sie jedoch mithilfe der Einstellung **Legacykonsole verwenden** auf der Registerkarte **Optionen** zur ursprünglichen Konsole zurückgewechselt sind, gilt diese Einstellung global und wird fortan für alle Fenster beibehalten, auch nach dem Neustart des Computers.  

Sie können diese Einstellungen vorkonfigurieren oder ein Skript dafür erstellen, indem Sie die Registrierung mit einer Datei für die unbeaufsichtigte Installation entsprechend konfigurieren oder Windows PowerShell verwenden.  

Für 16-Bit-NTVDM-Apps wird immer zum älteren Konsolenhost zurückgewechselt.  

> [!NOTE]  
> Wenn die neuen Konsoleneinstellungen bei Ihnen zu Problemen führen und sich diese nicht mit den hier detailliert aufgelisteten Optionen lösen lassen, können Sie jederzeit zur ursprünglichen Konsole zurückwechseln. Dazu legen Sie für die Einstellung „ForceV2“ den Wert 0 fest, oder Sie verwenden auf der Registerkarte **Optionen** das Steuerelement **Legacykonsole verwenden**.  

## <a name="console-behavior"></a>Verhalten der Konsole  
Sie können die Größe des Konsolenfensters nun nach Belieben ändern, indem Sie einfach eine Kante mit der Maus „anfassen“ und ziehen. Scrollleisten werden nur angezeigt, wenn Sie die Fensterabmessungen unter **Eigenschaften** auf der Registerkarte **Layout** manuell festlegen oder wenn die längste Textzeile im Puffer breiter als die aktuelle Fenstergröße ist.  

Das neue Konsolenfenster unterstützt jetzt Zeilenumbrüche. Wenn Sie jedoch mithilfe der Konsolen-APIs den Text in einem Puffer geändert haben, behält die Konsole den Text so bei, wie er ursprünglich eingefügt wurde.  

Das Konsolenfenster kann jetzt halbtransparent dargestellt werden (bis zu einer Mindesttransparenz von 30 %). Sie können die Transparenz über das Menü „Eigenschaften“ oder mithilfe der folgenden Tastaturbefehle anpassen:  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Transparenz erhöhen|STRG+UMSCHALT+Plus (+) oder STRG+UMSCHALTT+Mausrad nach oben drehen|  
|Transparenz verringern|STRG+UMSCHALT+Minus (-) oder STRG+UMSCHALTT+Mausrad nach unten drehen|  
|In den Vollbildmodus und zurück wechseln|ALT+EINGABE|  

## <a name="selection"></a>Auswahl  
Es gibt viele neue Möglichkeiten zum Auswählen von Text und Zeilen sowie zum Markieren von Text und zum Verwenden des Pufferverlaufs. In der Konsole wird versucht, Konflikte mit anderen Anwendungen zu vermeiden, bei denen die gleichen Tastenkombinationen verwendet werden.  

**Für Entwickler:** Wenn ein Konflikt auftritt, kannst du in der Regel mithilfe der SetConsoleMode()-API steuern, mit welchem Verhalten die Anwendung auf die Nutzung der Modi für Zeileneingaben, verarbeitete Eingaben und Echoeingaben reagiert. Wenn Sie den Modus für verarbeitete Eingaben verwenden, gelten die unten aufgeführten Tastenkombinationen. In anderen Modi müssen diese von Ihrer Anwendung behandelt werden. Alle hier nicht aufgeführten Tastenkombinationen funktionieren genauso wie in den vorherigen Versionen der Konsole. Sie können auch versuchen, Konflikte mithilfe der verschiedenen Einstellungen auf der Registerkarte **Optionen** zu lösen. Wenn alle anderen Versuche fehlschlagen, können Sie jederzeit zur ursprünglichen Konsole zurückwechseln.  

Sie können jetzt auch außerhalb des QuickEdit-Modus einen Textabschnitt durch Klicken und Ziehen markieren. Genauso wie in Editor können Sie Text nun zeilenübergreifend markieren, und zwar nicht nur als rechteckigen Textblock. Für Kopiervorgänge brauchen Sie die Zeilenumbrüche nicht mehr zu entfernen. Neben dem Markieren von Textabschnitten durch Klicken und Ziehen stehen die folgenden Tastenkombinationen zur Verfügung:  

**Textauswahl**  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Cursor um ein Zeichen nach links verschieben und die Markierung erweitern|UMSCHALT+NACH-LINKS-TASTE|  
|Cursor um ein Zeichen nach rechts verschieben und die Markierung erweitern|UMSCHALT+NACH-RECHTS-TASTE|  
|Text ausgehend von der Einfügemarke Zeile für Zeile aufsteigend markieren|UMSCHALT+NACH-OBEN-TASTE|  
|Textmarkierung ausgehend von der Einfügemarke um eine Zeile nach unten erweitern|UMSCHALT+NACH-UNTEN-TASTE|  
|Wenn sich der Cursor in der gerade bearbeiteten Zeile befindet, erweitern Sie durch einmalige Ausführung dieses Befehls die Markierung bis zum letzten Zeichen der Eingabezeile. Verwenden Sie den Befehl ein zweites Mal, um die Markierung bis zum rechten Rand zu erweitern.|UMSCHALT+ENDE|  
|Wenn sich der Cursor **nicht** in der gerade bearbeiteten Zeile befindet, markieren Sie mit diesem Befehl den gesamten Text von der Einfügemarke bis zum rechten Rand.|UMSCHALT+ENDE|  
|Wenn sich der Cursor in der gerade bearbeiteten Zeile befindet, erweitern Sie durch einmalige Ausführung dieses Befehls die Markierung bis zum Zeichen unmittelbar hinter der Eingabeaufforderung. Verwenden Sie den Befehl ein zweites Mal, um die Markierung bis zum rechten Rand zu erweitern.|UMSCHALT+POS1|  
|Wenn sich der Cursor **nicht** in der gerade bearbeiteten Zeile befindet, erweitern Sie mit diesem Befehl die Markierung bis zum linken Rand.|UMSCHALT+POS1|  
|Markierung um den auf dem Bildschirm angezeigten Inhalt nach unten erweitern|UMSCHALT+BILD-AB|  
|Markierung um den auf dem Bildschirm angezeigten Inhalt nach oben erweitern|UMSCHALT+BILD-AUF|  
|Markierung um ein Wort nach rechts erweitern. (Sie können mit dem Registrierungsschlüssel „WordDelimiters“ die Trennzeichen festlegen, die ein Wort definieren.)|STRG+UMSCHALT+NACH-RECHTS-TASTE|  
|Markierung um ein Wort nach links erweitern|STRG+UMSCHALT+POS1|  
|Markierung bis zum Anfang des Bildschirmpuffers erweitern|STRG+UMSCHALT+ENDE|  
|Den gesamten Text nach der Eingabeaufforderung markieren, wenn sich der Cursor in der aktuellen Zeile befindet und die Zeile nicht leer ist|STRG+A|  
|Den gesamten Puffer auswählen, wenn sich der Cursor **nicht** in der aktuellen Zeile befindet|STRG+A|  

**Bearbeiten von Text**  

Sie können nun mithilfe von Tastaturbefehlen in der Konsole Text kopieren und einfügen. STRG+C hat jetzt zwei Funktionen. Wenn bei der Verwendung des Tastaturbefehls kein Text markiert ist, wird wie gewohnt der BREAK-Befehl gesendet. Wenn Text markiert ist, wird dieser Text durch die erste Verwendung des Befehls kopiert und die Markierung aufgehoben. Die zweite Verwendung sendet den BREAK-Befehl. Außerdem können folgende Befehle zum Bearbeiten von Text verwendet werden:  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Text in die Befehlszeile einfügen|STRG+V|  
|Den markierten Text in die Zwischenablage kopieren|STRG+EINFG|  
|Den markierten Text in die Zwischenablage kopieren; BREAK senden|STRG + C|  
|Text in die Befehlszeile einfügen|UMSCHALT+EINFG|  

**Markierungsmodus**  

Sie können zu jedem Zeitpunkt in den Markierungsmodus wechseln. Dazu klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Titelleiste der Konsole, zeigen auf **Bearbeiten** und wählen im nun angezeigten Menü **Markieren** aus. Sie können auch STRG+M eingeben. Wenn der Markierungsmodus aktiviert ist, verwenden Sie die ALT-TASTE, um den Beginn einer Markierung mit Zeilenumbruch anzugeben. (Wenn **Auswahl des Zeilenumbruchs aktivieren** deaktiviert ist, wird im Markierungsmodus der Text als Block markiert.) Wenn der Markierungsmodus aktiviert ist, werden mit STRG+UMSCHALT+NACH-LINKS-TASTE oder STRG+UMSCHALT+NACH-RECHTS-TASTE einzelne Buchstaben markiert und nicht ganze Wörter wie im normalen Modus. Zusätzlich zu den unter **Bearbeiten von Text** beschriebenen Auswahltasten stehen im Markierungsmodus folgende Tastenkombinationen zur Verfügung:  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Markierungsmodus aufrufen, um den Cursor im Fenster verschieben zu können|STRG+M|  
|Beginn einer Markierung mit Zeilenumbruch im Markierungsmodus, zusammen mit anderen Tastenkombinationen|ALT|  
|Den Cursor in die angegebene Richtung verschieben|PFEILTASTEN|  
|Den Cursor um eine Seite in die angegebene Richtung verschieben|BILD-AUF und BILD-AB|  
|Den Cursor an den Anfang des Puffers verschieben|STRG+POS1|  
|Den Cursor an das Ende des Puffers verschieben|STRG+ENDE|  

**Navigieren im Verlauf**  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Im Ausgabeverlauf eine Zeile nach oben springen|STRG+NACH-OBEN-TASTE|  
|Im Ausgabeverlauf eine Zeile nach unten springen|STRG+NACH-UNTEN-TASTE|  
|Anzeigebereich an den Anfang des Puffers verschieben (wenn die Befehlszeile leer ist) oder alle Zeichen links vom Cursor löschen (wenn die Befehlszeile nicht leer ist)|STRG+POS1|  
|Anzeigebereich zur Befehlszeile verschieben (wenn die Befehlszeile leer ist) oder alle Zeichen rechts vom Cursor löschen (wenn die Befehlszeile nicht leer ist)|STRG+ENDE|  

**Weitere Tastaturbefehle**  

|Aufgabe:|Tastenkombination:|  
|---------------|-----------------------------|  
|Dialogfeld „Suchen“ öffnen|STRG+F|  
|Konsolenfenster schließen|ALT+F4|  
