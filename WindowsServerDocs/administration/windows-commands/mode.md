---
title: Modus
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b59b04f2-b41d-42df-b5be-19c3721445b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 528277075f7448c86ca2d660c5e65c59098afbc0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839433"
---
# <a name="mode"></a>Modus



Zeigt den Systemstatus an, ändert Systemeinstellungen oder konfiguriert Ports oder Geräte neu. Bei Verwendung ohne Parameter zeigt der- **Modus** alle steuerbaren Attribute der Konsole und der verfügbaren com-Geräte an.

Sie können den- **Modus** verwenden, um die folgenden Aufgaben auszuführen – jede Aufgabe verwendet eine andere Syntax:
-   [So konfigurieren Sie einen seriellen Kommunikationsport](#BKMK_1)
-   [So zeigen Sie den Status aller Geräte oder eines einzelnen Geräts an](#BKMK_2)
-   [So leiten Sie die Ausgabe von einem parallelen Anschluss an einen seriellen Kommunikationsport um](#BKMK_3)
-   [So können Sie die Anzahl der Codepages für die Konsole auswählen, aktualisieren oder anzeigen](#BKMK_4)
-   [So ändern Sie die Größe des Bildschirm Puffers für die Eingabeaufforderung](#BKMK_5)
-   [So legen Sie die typematische Tastatur Rate fest](#BKMK_6)

## <a name="to-configure-a-serial-communications-port"></a><a name=BKMK_1></a>So konfigurieren Sie einen seriellen Kommunikationsport

### <a name="syntax"></a>Syntax

```
mode com<M>[:] [baud=<B>] [parity=<P>] [data=<D>] [stop=<S>] [to={on|off}] [xon={on|off}] [odsr={on|off}] [octs={on|off}] [dtr={on|off|hs}] [rts={on|off|hs|tg}] [idsr={on|off}]
```

#### <a name="parameters"></a>Parameter

|  Parameter  |                                                                                                                                                                                     Beschreibung                                                                                                                                                                                     |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Com-\<M > [:]  |                                                                                                                                                      Gibt die Nummer des asynchronen prncnfg. vbshrton-Kommunikationsports an.                                                                                                                                                      |
|  Baud =\<B >  | Gibt die Übertragungsrate in Bits pro Sekunde an. In der folgenden Tabelle sind die gültigen Abkürzungen für *B* und ihre zugehörigen Sätze aufgeführt.</br>-   **11** = 110 Baudrate</br>-   **15** = 150 Baudrate</br>-   **30** = 300 Baudrate</br>-   **60** = 600 Baudrate</br>-   **12** = 1200 Baudrate</br>-   **24** = 2400 Baudrate</br>-   **48** = 4800 Baudrate</br>-   **96** = 9600 Baudrate</br>-   **19** = 19.200 Baudrate |
| Parität =\<P > |                              Gibt an, wie das System das Paritäts Bit zum Überprüfen von Übertragungsfehlern verwendet. In der folgenden Tabelle sind gültige Werte für *P*aufgeführt. Der Standardwert ist **e**. Nicht alle Computer unterstützen die Werte **m** und **s**.</br>-   **n** = None</br>-   **e** = auch</br>-   **o** = ungerade</br>-   **m** = Markierung</br>-   **s** = Leerraum                              |
|  Data =\<D >  |                                                                                                    Gibt die Anzahl der Datenbits in einem Zeichen an. Gültige Werte für **d** liegen im Bereich von 5 bis 8. Der Standardwert ist 7. Die Werte 5 und 6 werden nicht von allen Computern unterstützt.                                                                                                     |
|  beendet =\<S >  |                                                                                  Gibt die Anzahl von Stoppbits an, die das Ende eines Zeichens definieren: 1, 1,5 oder 2. Wenn die Baudrate 110 beträgt, ist der Standardwert 2. Andernfalls ist der Standardwert 1. Der Wert 1,5 wird nicht von allen Computern unterstützt.                                                                                   |
|   in = {on    |                                                                                                                                                                                        off}                                                                                                                                                                                         |
|   XOn = {on   |                                                                                                                                                                                        off}                                                                                                                                                                                         |
|  odsr = {on   |                                                                                                                                                                                        off}                                                                                                                                                                                         |
|  OCTs = {on   |                                                                                                                                                                                        off}                                                                                                                                                                                         |
|   DTR = {on   |                                                                                                                                                                                         Ortung erlauben                                                                                                                                                                                         |
|   RTS = {on   |                                                                                                                                                                                         Ortung erlauben                                                                                                                                                                                         |
|  idsr = {on   |                                                                                                                                                                                        off}                                                                                                                                                                                         |
|     /?      |                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                         |

## <a name="to-display-the-status-of-all-devices-or-of-a-single-device"></a><a name=BKMK_2></a>So zeigen Sie den Status aller Geräte oder eines einzelnen Geräts an

### <a name="syntax"></a>Syntax

```
mode [<Device>] [/status]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Gerät >|Gibt den Namen des Geräts an, für das der Status angezeigt werden soll.|
|/status|Fordert den Status sämtlicher umgeleiteter paralleler Drucker an. Sie können die Befehlszeilenoption **/Status** als **/STA**abkürzen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

Bei Verwendung ohne Parameter zeigt der- **Modus** den Status aller Geräte an, die auf Ihrem System installiert sind.

## <a name="to-redirect-output-from-a-parallel-port-to-a-serial-communications-port"></a><a name=BKMK_3></a>So leiten Sie die Ausgabe von einem parallelen Anschluss an einen seriellen Kommunikationsport um

### <a name="syntax"></a>Syntax

```
mode lpt<N>[:]=com<M>[:]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|LPT\<N > [:]|Erforderlich Gibt den parallelen Port an. Gültige Werte für *N* liegen im Bereich von 1 bis 3.|
|com-\<M > [:]|Erforderlich Gibt den seriellen Anschluss an. Gültige Werte für *M* liegen im Bereich von 1 bis 4.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

Sie müssen ein Mitglied der Gruppe "Administratoren" sein, um den Druck umzuleiten.

### <a name="examples"></a>Beispiele

Wenn Sie Ihr System so einrichten möchten, dass eine parallele Druckerausgabe an einen seriellen Drucker gesendet wird, müssen Sie den **Mode** -Befehl zweimal verwenden. Verwenden Sie zum ersten Mal den- **Modus** , um den seriellen Anschluss zu konfigurieren. Verwenden Sie beim zweiten Mal den- **Modus** , um die parallele Druckerausgabe an den seriellen Anschluss umzuleiten, den Sie im Befehl "erster **Modus** " angegeben haben.

Wenn der serielle Drucker z. b. bei 4800-Baudraten mit gleichmäßiger Parität operiert und mit dem COM1-Port (der ersten seriellen Verbindung auf Ihrem Computer) verbunden ist, geben Sie Folgendes ein:
```
mode com1 48,e,,,b
mode lpt1=com1
```
Wenn Sie die parallele Druckerausgabe von LPT1 zu COM1 umleiten, aber dann entscheiden, dass Sie eine Datei mithilfe von LPT1 drucken möchten, geben Sie den folgenden Befehl ein, bevor Sie die Datei ausdrucken:
```
mode lpt1
```
Dieser Befehl verhindert die Umleitung der Datei von LPT1 an COM1.

## <a name="to-select-refresh-or-display-the-numbers-of-the-code-pages-for-the-console"></a><a name=BKMK_4></a>So können Sie die Anzahl der Codepages für die Konsole auswählen, aktualisieren oder anzeigen

### <a name="syntax"></a>Syntax

```
mode <Device> codepage select=<YYY>
mode <Device> codepage [/status]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Gerät >|Erforderlich Gibt das Gerät an, für das Sie eine Codepage auswählen möchten. CON ist der einzige gültige Name für ein Gerät.|
|Codepage SELECT =|Erforderlich Gibt an, welche Codepage mit dem angegebenen Gerät verwendet werden soll. Sie können die **Codepage** **Select** als **CP** **SEL**abkürzen.|
|\<yyy >|Erforderlich Gibt die Nummer der zu ausgewäfenden Codepage an. In der folgenden Liste werden die einzelnen Codepages, die unterstützt werden, sowie Ihr Land/Ihre Region oder Sprache angezeigt</br>437: USA</br>850: mehrsprachig (lateinisch I)</br>852: slawisch (Lateinisch II)</br>855: Kyrillisch (Russisch)</br>857: Türkisch</br>860: Portugiesisch</br>861: Isländisch</br>863: Französisch (Kanada)</br>865: Nordisch</br>866: Russisch</br>869: modernes Griechisch|
|Codepage|Erforderlich Zeigt die Anzahl der Codepages (sofern vorhanden) an, die für das angegebene Gerät ausgewählt wurden.|
|/status|Zeigt die Anzahl der aktuellen Codepages an, die für das angegebene Gerät ausgewählt wurden. Sie können **/Status** auf **/STA**abkürzen. Unabhängig davon, ob Sie **/Status**angeben, wird im **Modus "Codepage** " die Anzahl der Codepages angezeigt, die für das angegebene Gerät ausgewählt wurden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="to-change-the-size-of-the-command-prompt-screen-buffer"></a><a name=BKMK_5></a>So ändern Sie die Größe des Bildschirm Puffers für die Eingabeaufforderung

### <a name="syntax"></a>Syntax

```
mode con[:] [cols=<C>] [lines=<N>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|con [:]|Erforderlich Gibt an, dass die Änderung für das Eingabe Aufforderungs Fenster gilt.|
|cols =\<C >|Gibt die Anzahl der Spalten im Bildschirm Puffer der Eingabeaufforderung an.|
|Lines =\<N >|Gibt die Anzahl der Zeilen im Bildschirm Puffer der Eingabeaufforderung an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="to-set-the-keyboard-typematic-rate"></a><a name=BKMK_6></a>So legen Sie die typematische Tastatur Rate fest

### <a name="syntax"></a>Syntax

```
mode con[:] [rate=<R> delay=<D>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|con [:]|Erforderlich Verweist auf die Tastatur.|
|Rate =\<R >|Gibt die Rate an, mit der ein Zeichen auf dem Bildschirm wiederholt wird, wenn Sie eine Taste gedrückt halten.|
|Delay =\<D >|Gibt die Zeitspanne an, die verbleibt, nachdem Sie eine Taste gedrückt halten, bevor die Zeichenausgabe wiederholt wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

- Die typematische Rate ist die Rate, mit der ein Zeichen wiederholt wird, wenn Sie den Schlüssel für das Zeichen gedrückt halten. Die typematische Rate umfasst zwei Komponenten: die Rate und die Verzögerung. Einige Tastaturen erkennen diesen Befehl nicht.
- Using **Rate =** <em>R</em>

  Gültige Werte liegen im Bereich von 1 bis 32. Diese Werte sind gleich ungefähr 2 bis 30 Zeichen pro Sekunde. Der Standardwert ist 20 für IBM-kompatible Tastaturen und 21 für IBM PS/2-kompatible Tastaturen. Wenn Sie die Rate festlegen, müssen Sie auch die Verzögerung festlegen.
- Verwenden von **Delay**=*D*

  Gültige Werte für *D* sind 1, 2, 3 und 4 (repräsentiert 0,25, 0,50, 0,75 und 1 Sekunde). Der Standardwert ist 2. Wenn Sie die Verzögerung festlegen, müssen Sie auch die Rate festlegen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)