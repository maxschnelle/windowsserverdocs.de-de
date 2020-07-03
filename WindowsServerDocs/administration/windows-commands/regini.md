---
title: regini
description: Referenz Artikel für den "Regini-Befehl, der die Registrierung über die Befehlszeile oder ein Skript ändert und Änderungen anwendet, die in einer oder mehreren Textdateien voreingestellt wurden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 56e2d4505db56248b6e4ce9c11caaae1df9a4f08
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931015"
---
# <a name="regini"></a>regini

Ändert die Registrierung über die Befehlszeile oder ein Skript und wendet die Änderungen an, die in einer oder mehreren Textdateien voreingestellt wurden. Sie können Registrierungsschlüssel zusätzlich zum Ändern der Berechtigungen für die Registrierungsschlüssel erstellen, ändern oder löschen.

Ausführliche Informationen zum Format und Inhalt der Text Skriptdatei, die regini.exe verwendet, um Änderungen an der Registrierung vorzunehmen, finden Sie unter [Ändern von Registrierungs Werten oder Berechtigungen in einer Befehlszeile oder einem Skript](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a).

## <a name="syntax"></a>Syntax

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputwidth][-b] textfiles...
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| -m`<\\computername>` | Gibt den Namen des Remote Computers mit einer Registrierung an, die geändert werden soll. Verwenden Sie das Format ** \\ Computername**. |
| -h`<hivefile hiveroot>` | Gibt die zu ändernde lokale Registrierungs Struktur an. Sie müssen den Namen der Hive-Datei und den Stamm der Struktur im Format **hivefile hiveroot**angeben. |
| -i`<n>` | Gibt die Ebene des Einzugs an, der verwendet wird, um die Struktur der Registrierungsschlüssel in der Befehlsausgabe anzugeben. Das **regdmp.exe** Tool (das die aktuellen Berechtigungen eines Registrierungsschlüssels im Binärformat abruft) verwendet den Einzug in Vielfachen von vier, sodass der Standardwert **4**ist. |
| -o`<outputwidth>` | Gibt die Breite der Befehlsausgabe in Zeichen an. Wenn die Ausgabe im Befehlsfenster angezeigt wird, ist der Standardwert die Breite des Fensters. Wenn die Ausgabe an eine Datei weitergeleitet wird, ist der Standardwert **240** Zeichen. |
| -b | Gibt an, dass **regini.exe** Ausgabe abwärts kompatibel mit früheren Versionen von **regini.exe**ist. |
| TextFiles | Gibt den Namen einer oder mehrerer Textdateien an, die Registrierungsdaten enthalten. Eine beliebige Anzahl von ANSI-oder Unicode-Textdateien kann aufgelistet werden. |

#### <a name="remarks"></a>Hinweise

Die folgenden Richtlinien gelten in erster Linie für den Inhalt der Textdateien, die Registrierungsdaten enthalten, die Sie mithilfe von **regini.exe**anwenden.

- Verwenden Sie das Semikolon als zeilenendekommentarzeichen. Es muss das erste Zeichen in einer Zeile sein, das kein Leerzeichen ist.

- Verwenden Sie den umgekehrten Schrägstrich, um die Fortsetzung einer Zeile anzugeben. Der Befehl ignoriert alle Zeichen des umgekehrten Schrägstrichs bis zu (aber nicht einschließlich) des ersten nicht leeren Zeichens der nächsten Zeile. Wenn Sie mehr als ein Leerzeichen vor dem umgekehrten Schrägstrich einschließen, wird es durch ein einzelnes Leerzeichen ersetzt.

- Verwenden Sie hart Tabstopps, um den Einzug zu steuern. Dieser Einzug gibt die Struktur der Registrierungsschlüssel an. Diese Zeichen werden jedoch unabhängig von ihrer Position in ein einzelnes Leerzeichen konvertiert.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
