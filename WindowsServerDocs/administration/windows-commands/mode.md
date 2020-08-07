---
title: Modus
description: Referenz Artikel für den Befehl "Modus", der den Systemstatus anzeigt, Systemeinstellungen ändert oder Ports oder Geräte neu konfiguriert.
ms.topic: article
ms.assetid: b59b04f2-b41d-42df-b5be-19c3721445b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae436d5ed1328799f7c20d98274a574d40ef796d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886395"
---
# <a name="mode"></a>Modus

Zeigt den Systemstatus an, ändert Systemeinstellungen oder konfiguriert Ports oder Geräte neu. Bei Verwendung ohne Parameter zeigt der- **Modus** alle steuerbaren Attribute der Konsole und der verfügbaren com-Geräte an.

## <a name="serial-port"></a>Serieller Anschluss

Konfiguriert einen seriellen Kommunikationsport und legt den Ausgabe Hand Shake fest.

### <a name="syntax"></a>Syntax

```
mode com<m>[:] [baud=<b>] [parity=<p>] [data=<d>] [stop=<s>] [to={on|off}] [xon={on|off}] [odsr={on|off}] [octs={on|off}] [dtr={on|off|hs}] [rts={on|off|hs|tg}] [idsr={on|off}]
```

#### <a name="parameters"></a>Parameter

| Parameter  | BESCHREIBUNG |
| ---------- | ----------- |
| `com<m>[:]` | Gibt die Nummer des asynchronen prncnfg. vbshrton-Kommunikationsports an. |
| `baud=<b>`  | Gibt die Übertragungsrate in Bits pro Sekunde an. Gültige Werte sind:<ul><li>**11** -110 Baudrate</li><li>**15** -150-Baudrate</li><li>**30** -300-Baudrate</li><li>**60** -600-Baudrate</li><li>**12** -1200-Baudrate</li><li>**24** -2400-Baudrate</li><li>**48** -4800-Baudrate</li><li>**96** -9600-Baudrate</li><li>**19** -19.200-Baudrate</li></ul> |
| `parity=<p>` | Gibt an, wie das System das Paritäts Bit zum Überprüfen von Übertragungsfehlern verwendet. Gültige Werte sind:<ul><li>**n** nicht zutreffend</li><li>**e** -even (Standardwert)</li><li>**o** -ungerade</li><li>**m** -Markierung</li><li>**s** -Speicherplatz</li></ul>Nicht alle Geräte unterstützen die Verwendung der **m** -oder **s** -Parameter. |
| `data=<d>` | Gibt die Anzahl der Datenbits in einem Zeichen an. Gültige Werte liegen im Bereich von **5** bis **8**. Der Standardwert ist **7**. Die Werte **5** und **6**werden nicht von allen Geräten unterstützt. |
| `stop=<s>` | Gibt die Anzahl von Stoppbits an, die das Ende eines Zeichens definieren: **1**, **1,5**oder **2**. Wenn die Baudrate **110**beträgt, ist der Standardwert **2**. Andernfalls ist der Standardwert **1**. Der Wert **1,5**wird nicht von allen Geräten unterstützt. |
| `to={on | off}` | Gibt an, ob das Gerät eine unbegrenzte Timeout Verarbeitung verwendet. Der Standardwert ist **Off**. Wenn Sie diese **Option aktivieren** , bedeutet dies, dass das Gerät niemals darauf wartet, eine Antwort von einem Host oder Client Computer zu empfangen. |
| `xon={on | off}` | Gibt an, ob das System das XON/XOFF-Protokoll zulässt. Dieses Protokoll bietet Fluss Steuerung für die serielle Kommunikation, verbessert die Zuverlässigkeit, verringert jedoch die Leistung. |
| `odsr={on | off}` | Gibt an, ob das System den DSR-Ausgabe Hand Shake (Data Set Ready) einschaltet. |
| `octs={on | off}` | Gibt an, ob das System den Lösch-Ausgabe Handshake (CTS) aktiviert. |
| `dtr={on | off | hs}` | Gibt an, ob das System den DTR-Ausgabe Hand Shake (Data Terminal Ready) einschaltet. Wenn dieser Wert **auf on** festgelegt wird, wird ein konstantes Signal angezeigt, um anzuzeigen, dass das Terminal zum Senden von Daten bereit ist. Das Festlegen dieses Werts auf den **HS** -Modus stellt ein Hand Shake Signal zwischen den beiden Terminals dar. |
| `rts={on | off | hs | tg}` | Gibt an, ob das System die Anforderung zum Senden von (RTS)-Ausgabe Hand Shake schaltet. Wenn dieser Wert **auf on** festgelegt wird, wird ein konstantes Signal angezeigt, um anzuzeigen, dass das Terminal zum Senden von Daten bereit ist. Das Festlegen dieses Werts auf den **HS** -Modus stellt ein Hand Shake Signal zwischen den beiden Terminals dar. Wenn Sie diesen Wert auf den **TG** -Modus festlegen, können Sie zwischen den Status "bereit" und "nicht bereit" umschalten. |
| `idsr={on | off}` | Gibt an, ob das System die DSR-Empfindlichkeit einschaltet. Sie müssen diese Option für aktivieren, damit DSR-Handler verwendet werden können.
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="device-status"></a>Gerätestatus

Zeigt den Status eines angegebenen Geräts an. Bei Verwendung ohne Parameter zeigt der- **Modus** den Status aller Geräte an, die auf Ihrem System installiert sind.

### <a name="syntax"></a>Syntax

```
mode [<device>] [/status]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<device>` | Gibt den Namen des Geräts an, für das der Status angezeigt werden soll. Zu den Standard Namen zählen, LPT1: bis LPT3:, COM1: bis COM9: und con. |
| /status | Fordert den Status sämtlicher umgeleiteter paralleler Drucker an. Sie können **/STA** auch als abgekürzte Version dieses Befehls verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="redirect-printing"></a>Umleitungs Druck

Leitet die Druckerausgabe um. Sie müssen ein Mitglied der Gruppe "Administratoren" sein, um den Druck umzuleiten.

> [!NOTE]
Wenn Sie Ihr System so einrichten möchten, dass eine parallele Druckerausgabe an einen seriellen Drucker gesendet wird, müssen Sie den **Mode** -Befehl zweimal verwenden. Beim ersten Mal müssen Sie den- **Modus** verwenden, um den seriellen Anschluss zu konfigurieren. Beim zweiten Mal müssen Sie den- **Modus** verwenden, um die parallele Druckerausgabe an den seriellen Port umzuleiten, den Sie im Befehl für den ersten **Modus** angegeben haben.

### <a name="syntax"></a>Syntax

```
mode LPT<n>[:]=COM<m>[:]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| LPT `<n>` [:] | Gibt die Anzahl der zu konfigurierenden LPT an. In der Regel bedeutet dies, dass ein Wert von **LTP1: bis LTP3:** bereitgestellt wird, es sei denn, Ihr System umfasst besondere parallele Port Unterstützung. Dieser Parameter ist erforderlich.|
| COM `<m>` [:] | Gibt den COM-Port an, der konfiguriert werden soll. In der Regel bedeutet dies, dass Sie einen Wert von **COM1: bis COM9**angeben müssen, es sei denn, Ihr System verfügt über spezielle Hardware für zusätzliche com-Anschlüsse. Dieser Parameter ist erforderlich. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an.|

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen seriellen Drucker, der mit 4800-Baudraten mit gleichmäßiger Parität betrieben wird, mit dem COM1-Port (die erste serielle Verbindung auf Ihrem Computer) zu umleiten:

```
mode com1 48,e,,,b
mode lpt1=com1
```

Geben Sie den folgenden Befehl ein, bevor Sie die Datei drucken, um die parallele Druckerausgabe von LPT1 zu COM1 umzuleiten und dann eine Datei mithilfe von LPT1 zu drucken:

```
mode lpt1
```

Dieser Befehl verhindert die Umleitung der Datei von LPT1 an COM1.

## <a name="select-code-page"></a>Codepage auswählen

Konfiguriert oder fragt die Code Page Informationen für ein ausgewähltes Gerät ab.

### <a name="syntax"></a>Syntax

```
mode <device> codepage select=<yyy>
mode <device> codepage [/status]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<device>` |Gibt das Gerät an, für das Sie eine Codepage auswählen möchten. CON ist der einzige gültige Name für ein Gerät. Dieser Parameter ist erforderlich. |
| codepage | Gibt an, welche Codepage mit dem angegebenen Gerät verwendet werden soll. Sie können **CP** auch als abgekürzte Version dieses Befehls verwenden. Dieser Parameter ist erforderlich. |
| SELECT =`<yyy>` | Gibt die Nummer der Codepage an, die mit dem Gerät verwendet werden soll. Die unterstützten Codepages nach Land/Region oder Sprache umfassen Folgendes:<ul><li>**437:** USA</li><li>**850:** Mehrsprachig (lateinisch I)</li><li>**852:** Slawisch (Lateinisch II)</li><li>**855:** Kyrillisch (Russisch)</li><li>**857:** Türkisch</li><li>**860:** Portugiesisch</li><li>**861:** Isländisch</li><li>**863:** Französisch (Kanada)</li><li>**865:** Nordischen</li><li>**866:** Russisch</li><li>**869:** Modernes Griechisch</li></ul> Dieser Parameter ist erforderlich. |
| /status | Zeigt die Anzahl der aktuellen Codepages an, die für das angegebene Gerät ausgewählt wurden. Sie können **/STA** auch als abgekürzte Version dieses Befehls verwenden. Unabhängig davon, ob Sie **/Status**angeben, zeigt der **Modus-Codepage** -Befehl die Anzahl der Codepages an, die für das angegebene Gerät ausgewählt wurden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="display-mode"></a>Anzeigemodus

Ändert die Größe des Bildschirm Puffers für die Eingabeaufforderung.

### <a name="syntax"></a>Syntax

```
mode con[:] [cols=<c>] [lines=<n>]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| con [:] | Gibt an, dass die Änderung für das Eingabe Aufforderungs Fenster gilt. Dieser Parameter ist erforderlich. |
| cols =`<c>` | Gibt die Anzahl der Spalten im Bildschirm Puffer der Eingabeaufforderung an. Die Standardeinstellung ist 80 Spalten, Sie können diese jedoch auf einen beliebigen Wert festlegen. Wenn Sie nicht die Standardeinstellung verwenden, sind die typischen Werte 40 und 135 Spalten. Die Verwendung von nicht standardmäßigen Werten kann zu Problemen bei der Eingabeaufforderung der APP führen. |
| Zeilen =`<n>` | Gibt die Anzahl der Zeilen im Bildschirm Puffer der Eingabeaufforderung an. Der Standardwert ist 25. Sie können diesen Wert jedoch auf einen beliebigen Wert festlegen. Wenn Sie nicht die Standardeinstellung verwenden, ist der andere typische Wert 50 Zeilen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="typematic-rate"></a>Typematische Rate

Legt die typematische Tastatur Rate fest. Die typematische Rate ist die Geschwindigkeit, mit der Fenster ein Zeichen wiederholen können, wenn Sie die Taste auf einer Tastatur drücken.

> [!NOTE]
> Einige Tastaturen erkennen diesen Befehl nicht.

### <a name="syntax"></a>Syntax

```
mode con[:] [rate=<r> delay=<d>]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| con [:] | Gibt die Tastatur an. Dieser Parameter ist erforderlich. |
| Rate =`<r>` | Gibt die Rate an, mit der ein Zeichen auf dem Bildschirm wiederholt wird, wenn Sie eine Taste gedrückt halten. Der Standardwert ist 20 Zeichen pro Sekunde für IBM-kompatible Tastaturen und 21 für IBM PS/2-kompatible Tastaturen, Sie können jedoch einen beliebigen Wert zwischen 1 und 32 verwenden. Wenn Sie diesen Parameter festlegen, müssen Sie auch den **Delay** -Parameter festlegen.|
| Verzögerung =`<d>` | Gibt die Zeitspanne an, die verbleibt, nachdem Sie eine Taste gedrückt halten, bevor die Zeichenausgabe wiederholt wird. Der Standardwert ist 2 (. 50 Sekunden), Sie können jedoch auch 1 (. 25 Sekunden), 3 (. 75 Sekunden) oder 4 (1 Sekunde) verwenden. Wenn Sie diesen Parameter festlegen, müssen Sie auch den **Rate** -Parameter festlegen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)