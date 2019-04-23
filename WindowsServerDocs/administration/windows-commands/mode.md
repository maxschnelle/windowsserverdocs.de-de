---
title: mode
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b59b04f2-b41d-42df-b5be-19c3721445b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cde0e9786f72823f446202f1c87ad8e9e181d29c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848201"
---
# <a name="mode"></a>mode



Zeigt den Systemstatus, Systemeinstellungen geändert oder neu konfiguriert, Ports oder Geräte. Wenn Sie ohne Angabe von Parametern **Modus** zeigt die steuerbar Attribute der Verwaltungskonsole und die verfügbaren COM-Geräte an.

Können Sie **Modus** auf die folgenden Aufgaben ausführen – jede Aufgabe wird eine andere Syntax verwendet:
-   [So konfigurieren Sie einen seriellen Anschluss](#BKMK_1)
-   [Zum Anzeigen des Status aller Geräte oder eines einzelnen Geräts](#BKMK_2)
-   [Die Ausgabe von einem parallelen auf einem seriellen Anschluss umgeleitet](#BKMK_3)
-   [Um auszuwählen, aktualisieren oder die Zahlen der Codepages für die Konsole anzeigen](#BKMK_4)
-   [Ändern die Größe des Bildschirmpuffers Eingabeaufforderung](#BKMK_5)
-   [Die Tastaturwiederholrate festlegen](#BKMK_6)

## <a name="BKMK_1"></a>So konfigurieren Sie einen seriellen Anschluss

### <a name="syntax"></a>Syntax

```
mode com<M>[:] [baud=<B>] [parity=<P>] [data=<D>] [stop=<S>] [to={on|off}] [xon={on|off}] [odsr={on|off}] [octs={on|off}] [dtr={on|off|hs}] [rts={on|off|hs|tg}] [idsr={on|off}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Com\<M > [::]|Gibt die Anzahl der asynchronen Prncnfg.vbshronous Kommunikationsport.|
|baud=\<B>|Gibt die Übertragungsrate in Bits pro Sekunde an. Die folgende Tabelle enthält die zulässigen Werte für *B* und deren zugehörigen Gebühren.</br>-   **11** = 110 baud</br>-   **15** = 150 baud</br>-   **30** = 300 baud</br>-   **60** = 600 baud</br>-   **12** = 1200 baud</br>-   **24** = 2400 baud</br>-   **48** = 4800 baud</br>-   **96** = 9600 baud</br>-   **19** = 19.200 Baudrate|
|parity=\<P>|Gibt an, wie das System das Paritätsbit Übertragung fehlerüberprüfung verwendet. Die folgende Tabelle enthält die gültigen Werte für *P*. Der Standardwert ist **e**. Nicht alle Computer unterstützen die Werte **m** und **s**.</br>-   **n** = keine</br>-   **e** = even</br>-   **o** = odd</br>-   **m** = markieren</br>-   **s** = Leerzeichen|
|data=\<D>|Gibt die Anzahl der Datenbits in ein Zeichen an. Gültige Werte für **d** liegen im Bereich von 5 bis 8. Der Standardwert ist 7. Nicht alle Computer unterstützen die Werte, 5 und 6.|
|stop=\<S>|Gibt die Anzahl von Stoppbits an, die das Ende eines Zeichens zu definieren: 1, 1.5, oder 2. Wenn die Baudrate 110 ist, ist der Standardwert 2 auf. Andernfalls ist der Standardwert 1. Nicht alle Computer unterstützen den Wert von 1,5.|
|Um = {on | {Off}|Gibt an, ob ein unendliches Timeout-Verarbeitung aktiviert oder deaktiviert ist. Der Standardwert ist off.|
|xon={on | {Off}|Gibt an, ob das Xon oder Xoff-Protokoll für die Data-flusssteuerung aktiviert oder deaktiviert ist.|
|odsr={on | {Off}|Gibt an, ob die Ausgabehandshake, der die Verbindung Data Set Ready (DSR) verwendet, aktiviert oder deaktiviert ist.|
|ÜLG = {on | {Off}|Gibt an, ob die Ausgabehandshake, der die Verbindung zum Senden von CTS (Clear) verwendet, aktiviert oder deaktiviert ist.|
|dtr={on | Ortung erlauben | hs}|Gibt an, ob die Verbindung Data Terminal Ready (DTR) aktiviert deaktiviert oder ist, oder legen Sie auf Handshake.|
|RTS = {on | Ortung erlauben | hs | tg}|Gibt an, ob die Request To Send (RTS)-Verbindung auf on, off festgelegt ist, Handshake oder ein-/ausschalten.|
|idsr={on | {Off}|Gibt an, ob die Verbindung DSR-Empfindlichkeit aktiviert oder deaktiviert ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_2"></a>Zum Anzeigen des Status aller Geräte oder eines einzelnen Geräts

### <a name="syntax"></a>Syntax

```
mode [<Device>] [/status]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Gerät >|Gibt den Namen des Geräts für die der Status angezeigt werden sollen.|
|/status|Fordert an alle umgeleiteten parallele Drucker den Status. Sie können auch abkürzen, die **/Status** als Befehlszeilenoption **/STA**.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

Wenn Sie ohne Angabe von Parametern **Modus** zeigt den Status aller Geräte, die auf Ihrem System installiert sind.

## <a name="BKMK_3"></a>Die Ausgabe von einem parallelen auf einem seriellen Anschluss umgeleitet

### <a name="syntax"></a>Syntax

```
mode lpt<N>[:]=com<M>[:]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|lpt\<N>[:]|Erforderlich. Gibt den parallelen Port. Gültige Werte für *N* liegen im Bereich von 1 bis 3.|
|com\<M > [::]|Erforderlich. Gibt den seriellen Anschluss. Gültige Werte für *M* liegen im Bereich von 1 bis 4.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

Sie müssen ein Mitglied der Gruppe "Administratoren" Drucken umgeleitet werden.

### <a name="examples"></a>Beispiele

Um Ihr System einzurichten, damit es parallel Druckerausgabe zu einem seriellen Drucker sendet, müssen Sie verwenden die **Modus** Befehl. Verwenden Sie beim ersten **Modus** so konfigurieren Sie den seriellen Anschluss. Verwenden Sie bei der zweiten **Modus** zum Umleiten der parallele Druckerausgabe an den seriellen Port in der ersten angegebenen **Modus** Befehl.

Wenn der serielle Drucker, die bei sogar Parität und eine Baudrate 4800 arbeitet, und es an den Anschluss "COM1" (die erste serielle Verbindung auf Ihrem Computer) verbunden ist, geben Sie beispielsweise:
```
mode com1 48,e,,,b
mode lpt1=com1
```
Wenn Sie parallele Drucker die Ausgabe von LPT1 an COM1 umleiten, aber dann Sie entscheiden, dass Sie eine Datei zu drucken, indem Sie LPT1 möchten, geben Sie den folgenden Befehl, bevor Sie die Datei zu drucken:
```
mode lpt1
```
Dieser Befehl verhindert, dass die Umleitung der Datei von LPT1 COM1.

## <a name="BKMK_4"></a>Um auszuwählen, aktualisieren oder die Zahlen der Codepages für die Konsole anzeigen

### <a name="syntax"></a>Syntax

```
mode <Device> codepage select=<YYY>
mode <Device> codepage [/status]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Gerät >|Erforderlich. Gibt das Gerät für das Sie eine Codepage auswählen möchten. CON ist der einzige gültige Name für ein Gerät.|
|Wählen Sie die Codepage =|Erforderlich. Gibt die Codepage für die Verwendung mit dem angegebenen Gerät. Sie können abkürzen **Codepage** **wählen** als **cp** **Sel**.|
|\<YYY &GT;|Erforderlich. Gibt die Anzahl der Codepage auswählen. Die folgende Liste zeigt code jeder Seite, die unterstützt wird und die Sprache/Land oder die Sprache.</br>437: USA</br>850: Mehrsprachige (Lateinisch I)</br>852: Altslawisch (Lateinisch II)</br>855: Kyrillisch (Russisch)</br>857: Türkisch</br>860: Portugiesisch</br>861: Isländisch</br>863: Französisch (Kanada)</br>865: Nordisch</br>866: Russisch</br>869: Neugriechisch|
|codepage|Erforderlich. Zeigt Seiten die Zahlen des Codes (sofern vorhanden), die für das angegebene Gerät ausgewählt sind.|
|/status|Zeigt die Anzahl der dem aktuellen Codepages, die für das angegebene Gerät ausgewählt. Sie können abkürzen **/Status** zu **/STA**. Angabe, ob **/Status**, **Modus Codepage** zeigt die Anzahl von Codepages, die für das angegebene Gerät ausgewählt sind.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_5"></a>Ändern die Größe des Bildschirmpuffers Eingabeaufforderung

### <a name="syntax"></a>Syntax

```
mode con[:] [cols=<C>] [lines=<N>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|con[:]|Erforderlich. Gibt an, dass die Änderung für das Fenster "Eingabeaufforderung" gilt.|
|cols=\<C>|Gibt die Anzahl der Spalten in den Bildschirmpuffer Eingabeaufforderung an.|
|Zeilen =\<N >|Gibt die Anzahl der Zeilen in den Bildschirmpuffer Eingabeaufforderung an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_6"></a>Die Tastaturwiederholrate festlegen

### <a name="syntax"></a>Syntax

```
mode con[:] [rate=<R> delay=<D>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|con[:]|Erforderlich. Bezieht sich auf der Tastatur.|
|rate=\<R>|Gibt die Rate, mit der ein Zeichen wiederholt wird, auf dem Bildschirm an, wenn Sie eine Taste gedrückt halten.|
|Verzögerung =\<D >|Gibt die Zeitspanne, die verstreicht, nach dem Drücken und eine Taste gedrückt wird, bevor die Ausgabe von Zeichen wiederholt an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Die Wiederholrate ist die Rate, mit der ein Zeichen wiederholt wird, wenn Sie die Taste für das Zeichen gedrückt halten. Die Wiederholrate verfügt über zwei Komponenten, die Geschwindigkeit und die Verzögerung. Einige Tastaturen erkannt mit diesem Befehl nicht.
-   Mithilfe von **Rate = *** R*

    Gültige Werte liegen im Bereich von 1 bis 32. Diese Werte entsprechen ungefähr 2 bis 30 Zeichen pro Sekunde. Der Standardwert ist 20 für IBM-AT-kompatiblen Tastaturen und 21 für Tastaturen mit IBM PS/2-kompatibel. Wenn Sie die Rate festlegen, müssen Sie auch die Verzögerung festlegen.
-   Mithilfe von **Verzögerung**=*D*

    Gültige Werte für *D* sind 1, 2, 3 und 4 (0,25, 0,50, 0,75 und darstellt 1 Sekunde). Der Standardwert ist 2. Wenn Sie die Verzögerung festlegen, müssen Sie auch die Rate festlegen.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)