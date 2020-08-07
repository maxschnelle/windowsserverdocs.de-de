---
title: openfiles
description: Referenz Artikel für den openfiles-Befehl, der es einem Administrator ermöglicht, Dateien und Verzeichnisse, die auf einem System geöffnet wurden, abzufragen, anzuzeigen oder zu trennen.
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79163a717746cfb43d0195cf30c7bbf7e1766623
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885126"
---
# <a name="openfiles"></a>openfiles

Ermöglicht es einem Administrator, Dateien und Verzeichnisse abzufragen, anzuzeigen oder zu trennen, die auf einem System geöffnet wurden. Mit diesem Befehl wird auch das globale Flag für die Liste der System verwalteten **Objekte** aktiviert oder deaktiviert.

## <a name="openfiles-disconnect"></a>openfiles/disconnect

Ermöglicht einem Administrator das Trennen von Dateien und Ordnern, die per Remote Zugriff über einen freigegebenen Ordner geöffnet wurden.

### <a name="syntax"></a>Syntax

```
openfiles /disconnect [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] {[/id <openfileID>] | [/a <accessedby>] | [/o {read | write | read/write}]} [/op <openfile>]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s`<system>` | Gibt das Remote System an, mit dem eine Verbindung hergestellt werden soll (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrten Schrägstriche. Wenn Sie die Option **/s** nicht verwenden, wird der Befehl standardmäßig auf dem lokalen Computer ausgeführt. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u`[<domain>\]<username>` | Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Wenn Sie die Option **/u** nicht verwenden, werden standardmäßig System Berechtigungen verwendet. |
| /p`[<password>]` | Gibt das Kennwort des Benutzerkontos an, das in der **/u** -Option angegeben ist. Wenn Sie die Option **/p** nicht verwenden, wird beim Ausführen des Befehls eine Kenn Wort Eingabeaufforderung angezeigt. |
| /ID`<openfileID>` | Trennt geöffnete Dateien mit der angegebenen Datei-ID. Mit diesem Parameter können Sie das Platzhalter Zeichen (**&#42;**) verwenden.<p>Hinweis: Sie können den Befehl **openfiles/Query "aus** verwenden, um die Datei-ID zu suchen. |
| /a`<accessedby>` | Trennt alle geöffneten Dateien, die mit dem im *Access sedby* -Parameter angegebenen Benutzernamen verknüpft sind. Mit diesem Parameter können Sie das Platzhalter Zeichen (**&#42;**) verwenden. |
| /o`{read | write | read/write}` | Trennt alle geöffneten Dateien mit dem angegebenen Wert für den offenen Modus. Gültige Werte sind **Lese**-, **Schreib** **-oder Lese-/Schreibzugriff**. Mit diesem Parameter können Sie das Platzhalter Zeichen (**&#42;**) verwenden. |
| /op`<openfile>` | Trennt alle geöffneten Datei Verbindungen, die mit einem bestimmten geöffneten Dateinamen erstellt werden. Mit diesem Parameter können Sie das Platzhalter Zeichen (**&#42;**) verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie alle geöffneten Dateien mit der *Datei-ID 26843578*trennen möchten, geben Sie Folgendes ein:

```
openfiles /disconnect /id 26843578
```

Wenn Sie alle geöffneten Dateien und Verzeichnisse trennen möchten, auf die der Benutzer *hiropln*zugreifen, geben Sie Folgendes ein:

```
openfiles /disconnect /a hiropln
```

Geben Sie Folgendes ein, um alle geöffneten Dateien und Verzeichnisse mit dem *Lese-/Schreibmodus*zu trennen:

```
openfiles /disconnect /o read/write
```

Geben Sie Folgendes ein, um die Verbindung zwischen dem Verzeichnis und dem geöffneten Dateinamen * c:\testshare \* unabhängig davon, wer darauf zugreift, getrennt zu werden:

```
openfiles /disconnect /a * /op c:\testshare\
```

Wenn Sie alle geöffneten Dateien auf dem Remote Computer *srvmain* trennen möchten, auf die der Benutzer " *hiropln*" zugreift, unabhängig von ihrer ID, geben Sie Folgendes ein:

```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="openfiles-query"></a>openfiles/Query "aus

Fragt alle geöffneten Dateien ab und zeigt diese an.

### <a name="syntax"></a>Syntax

```
openfiles /query [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

#### <a name="parameters"></a>Parameter


| Parameter | BESCHREIBUNG |
|--|--|
| /s`<system>` | Gibt das Remote System an, mit dem eine Verbindung hergestellt werden soll (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrten Schrägstriche. Wenn Sie die Option **/s** nicht verwenden, wird der Befehl standardmäßig auf dem lokalen Computer ausgeführt. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u`[<domain>\]<username>` | Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Wenn Sie die Option **/u** nicht verwenden, werden standardmäßig System Berechtigungen verwendet. |
| /p`[<password>]` | Gibt das Kennwort des Benutzerkontos an, das in der **/u** -Option angegeben ist. Wenn Sie die Option **/p** nicht verwenden, wird beim Ausführen des Befehls eine Kenn Wort Eingabeaufforderung angezeigt. |
| [/FO `{TABLE | LIST | CSV}` ] | Zeigt die Ausgabe im angegebenen Format an. Gültige Werte:<ul><li>**Tabelle** : zeigt die Ausgabe in einer Tabelle an.</li><li>**List** : zeigt die Ausgabe in einer Liste an.</li><li>**CSV** : zeigt die Ausgabe im CSV-Format (Komma getrennte Werte) an.</li></ul> |
| /nh | Unterdrückt die Spaltenüberschriften in der Ausgabe. Nur gültig, wenn der **/FO** -Parameter auf **Table** oder **CSV**festgelegt ist. |
| /v | Gibt an, dass detaillierte (ausführliche) Informationen in der Ausgabe angezeigt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle geöffneten Dateien abzufragen und anzuzeigen:

```
openfiles /query
```

Wenn Sie alle geöffneten Dateien im Tabellenformat ohne Header Abfragen und anzeigen möchten, geben Sie Folgendes ein:

```
openfiles /query /fo table /nh
```

Wenn Sie alle geöffneten Dateien im Listenformat mit detaillierten Informationen Abfragen und anzeigen möchten, geben Sie Folgendes ein:

```
openfiles /query /fo list /v
```

Wenn Sie alle geöffneten Dateien auf dem Remote System *srvmain* mithilfe der Anmelde Informationen für den Benutzer *hiropln* in der *Maindom* -Domäne Abfragen und anzeigen möchten, geben Sie Folgendes ein:

```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> In diesem Beispiel wird das Kennwort in der Befehlszeile angegeben. Wenn Sie die Anzeige des Kennworts verhindern möchten, lassen Sie die Option **/p** aus. Sie werden zur Eingabe des Kennworts aufgefordert, das nicht auf dem Bildschirm angezeigt wird.

## <a name="openfiles-local"></a>openfiles/local ein

Aktiviert oder deaktiviert das globale Flag für die **Liste der Objekte** der Systemverwaltung. Bei Verwendung ohne Parameter zeigt **openfiles/local ein** den aktuellen Status der globalen Flag zum **Auflisten von Objekten** an.

> [!NOTE]
> Änderungen, die mithilfe der Option **on** oder **Off** vorgenommen wurden, werden erst wirksam, wenn Sie das System neu starten. Wenn Sie das globale Flag zum Verwalten von **Objekten** aktivieren, kann das System verlangsamt werden.

### <a name="syntax"></a>Syntax

```
openfiles /local [on | off]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[on | off]` | Aktiviert oder deaktiviert das globale Flag für die Liste der System verwalteten **Objekte** , das lokale Datei Handles nachverfolgt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den aktuellen Status des globalen Flags für die Liste der verwalteten **Objekte** zu überprüfen:

```
openfiles /local
```

Standardmäßig ist das Flag zum **Auflisten von Objekten** in der Liste deaktiviert, und die folgende Meldung wird angezeigt:`INFO: The system global flag 'maintain objects list' is currently disabled.`

Geben Sie Folgendes ein, um das globale Flag " **Objekte auflisten** " zu aktivieren:

```
openfiles /local on
```

Die folgende Meldung wird angezeigt, wenn das globale Flag aktiviert ist.`SUCCESS: The system global flag 'maintain objects list' is enabled. This will take effect after the system is restarted.`

Geben Sie Folgendes ein, um das globale Flag zum Verwalten von **Objekten** zu deaktivieren:

```
openfiles /local off
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
