---
title: nbtstat
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d2ea99e-72f1-471f-9525-d2c49bf3be82
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8077228a6c72302e63a2d1b8123e7f7e0ff6b8e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839023"
---
# <a name="nbtstat"></a>nbtstat

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt NetBT-Protokoll Statistiken (NetBIOS over TCP/IP), NetBIOS-Namens Tabellen sowohl für den lokalen Computer als auch für die Remote Computer und für den NetBIOS-Namen Cache an. **nbtstat** ermöglicht das Aktualisieren des NetBIOS-Namens Caches und der Namen, die mit WINS (Windows Internet Name Service) registriert sind. Wird ohne Parameter verwendet, zeigt **nbtstat** Hilfe an. 

## <a name="syntax"></a>Syntax

```
nbtstat [/a <remoteName>] [/A <IPaddress>] [/c] [/n] [/r] [/R] [/RR] [/s] [/S] [<Interval>]
```

#### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                         Beschreibung                                                                                                                         |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /a <remoteName> |    Zeigt die NetBIOS-Namen Tabelle eines Remote Computers an, wobei *Remotename* der NetBIOS-Computername des Remote Computers ist. Die NetBIOS-Namens Tabelle ist die Liste der NetBIOS-Namen, die NetBIOS-Anwendungen entsprechen, die auf diesem Computer ausgeführt werden.     |
| /A <IPaddress>  |                                                           Zeigt die NetBIOS-Namen Tabelle eines Remote Computers an, der durch die IP-Adresse (in punktierter Dezimal Schreibweise) des Remote Computers angegeben wird.                                                            |
|       /c        |                                                                        Zeigt den Inhalt des NetBIOS-Namens Caches, die Tabelle mit den NetBIOS-Namen und ihre aufgelösten IP-Adressen an.                                                                         |
|       /n        |                                            Zeigt die NetBIOS-Namen Tabelle des lokalen Computers an. Der Status **registriert** gibt an, dass der Name entweder durch Broadcast oder einen WINS-Server registriert wird.                                             |
|       /r        |      Zeigt Statistiken für die NetBIOS-Namensauflösung an. Auf einem Computer mit Windows XP oder Windows Server 2003, der für die Verwendung von WINS konfiguriert ist, gibt dieser Parameter die Anzahl der Namen zurück, die mit Broadcast und WINS aufgelöst und registriert wurden.       |
|       /R        |                                                                      Löscht den Inhalt des NetBIOS-Namens Caches und lädt dann die #Pre markierten Einträge aus der **Lmhosts** -Datei erneut.                                                                      |
|       /RR       |                                                                           Gibt die NetBIOS-Namen für den lokalen Computer frei, der bei WINS-Servern registriert ist, und aktualisiert diese.                                                                            |
|       /s        |                                                                          Zeigt NetBIOS-Client-und Server Sitzungen an und versucht, die Ziel-IP-Adresse in einen Namen zu konvertieren.                                                                           |
|       /S        |                                                                          Zeigt NetBIOS-Client-und Server Sitzungen an und listet die Remote Computer nur durch Ziel-IP-Adresse auf.                                                                          |
|   <Interval>    | Zeigt die ausgewählte Statistik erneut an und hält die Anzahl der Sekunden an, die im *Intervall* zwischen den einzelnen anzeigen angegeben sind. Drücken Sie STRG + C, um die erneute Anzeige der Statistiken zu verhindern. Wenn dieser Parameter ausgelassen wird, druckt **nbtstat** die aktuellen Konfigurationsinformationen nur einmal. |
|       /?        |                                                                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                             |

## <a name="remarks"></a>Hinweise

-   bei **nbtstat** -Befehlszeilen Parametern wird die Groß-/Kleinschreibung beachtet.

-   In der folgenden Tabelle werden die Spaltenüberschriften beschrieben, die von **nbtstat**generiert werden:

    |Richtung|Beschreibung|
    |------|--------|
    |Eingabe|Die Anzahl der empfangenen Bytes.|
    |Ausgabe|Die Anzahl der gesendeten Bytes.|
    |Ein/Aus|Gibt an, ob die Verbindung vom Computer (ausgehend) oder von einem anderen Computer zum lokalen Computer (eingehend) erfolgt.|
    |Menschen|Die verbleibende Zeit, in der ein Name Table Cache-Eintrag aktiv wird, bevor er gelöscht wird.|
    |Lokaler Name|Der lokale NetBIOS-Name, der der Verbindung zugeordnet ist.|
    |Remote Host|Der Name oder die IP-Adresse, die dem Remote Computer zugeordnet ist.|
    |< 03 >|Das letzte Byte eines NetBIOS-Namens, das in Hexadezimal konvertiert wurde. Jeder NetBIOS-Name hat eine Länge von 16 Zeichen. Das letzte Byte hat häufig eine besondere Bedeutung, da derselbe Name mehrmals auf einem Computer vorhanden sein kann, der sich nur im letzten Byte unterscheidet. Beispielsweise ist < 20 > ein Leerzeichen im ASCII-Text.|
    |Typ|Der Typ des Namens. Ein Name kann entweder ein eindeutiger Name oder ein Gruppenname sein.|
    |Status|Gibt an, ob der NetBIOS-Dienst auf dem Remote Computer ausgeführt wird (registriert ist) oder ob ein doppelter Computername denselben Dienst registriert hat (Konflikt).|
    |Phase|Der Status von NetBIOS-Verbindungen.|

-   In der folgenden Tabelle werden die möglichen NetBIOS-Verbindungszustände beschrieben:

    |Phase|Beschreibung|
    |-----|--------|
    |Verbunden|Eine Sitzung wurde eingerichtet.|
    |ierter|Ein Verbindungs Endpunkt wurde erstellt und einer IP-Adresse zugeordnet.|
    |Raum|Dieser Endpunkt ist für eine eingehende Verbindung verfügbar.|
    |Idle|Dieser Endpunkt wurde geöffnet, kann aber keine Verbindungen empfangen.|
    |Verbindung wird aufgebaut|Eine Sitzung befindet sich in der Verbindungs Phase, und die Zuordnung zwischen Name und IP-Adresse des Ziels wird aufgelöst.|
    |Verantwortung|Eine eingehende Sitzung wird derzeit akzeptiert und wird in Kürze verbunden.|
    |Verbindung|Eine Sitzung versucht, erneut eine Verbindung herzustellen (beim ersten Versuch konnte keine Verbindung hergestellt werden).|
    |Ausgehende|Eine Sitzung befindet sich in der Verbindungs Phase, und die TCP-Verbindung wird gerade erstellt.|
    |Eingehende|Eine eingehende Sitzung befindet sich in der Verbindungs Phase.|
    |Verbindung wird getrennt|Eine Sitzung wird gerade getrennt.|
    |getrennt|Der lokale Computer hat eine Verbindung getrennt und wartet auf eine Bestätigung vom Remote System.|

-   Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
Geben Sie Folgendes ein, um die NetBIOS-Namens Tabelle des Remote Computers mit dem NetBIOS-Computernamen CORP07 anzuzeigen:

```
nbtstat /a CORP07
```

Geben Sie Folgendes ein, um die NetBIOS-Namens Tabelle des Remote Computers anzuzeigen, der die IP-Adresse von 10.0.0.99 zugewiesen ist:

```
nbtstat /A 10.0.0.99
```

Geben Sie Folgendes ein, um die NetBIOS-Namens Tabelle des lokalen Computers anzuzeigen:

```
nbtstat /n
```

Geben Sie Folgendes ein, um den Inhalt des NetBIOS-Namens Caches des lokalen Computers anzuzeigen:

```
nbtstat /c
```

Wenn Sie den NetBIOS-Namen Cache löschen und die #Pre markierten Einträge in der lokalen LMHOSTS-Datei erneut laden möchten, geben Sie Folgendes ein:

```
nbtstat /R
```

Geben Sie Folgendes ein, um die beim WINS-Server registrierten NetBIOS-Namen freizugeben und erneut zu registrieren:

```
nbtstat /RR
```

Geben Sie Folgendes ein, um NetBIOS-Sitzungs Statistiken nach IP-Adresse alle fünf Sekunden anzuzeigen:

```
nbtstat /S 5
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


