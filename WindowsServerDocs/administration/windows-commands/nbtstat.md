---
title: nbtstat
description: Referenz Thema für den nbtstat-Befehl, der NetBT-Protokoll Statistiken (NetBIOS over TCP/IP), NetBIOS-Namens Tabellen sowohl für den lokalen Computer als auch für die Remote Computer und den NetBIOS-Namen Cache anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d2ea99e-72f1-471f-9525-d2c49bf3be82
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e205013dc5716b76981e0c9bae667d48802dfc74
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354320"
---
# <a name="nbtstat"></a>nbtstat

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt NetBT-Protokoll Statistiken (NetBIOS over TCP/IP), NetBIOS-Namens Tabellen sowohl für den lokalen Computer als auch für die Remote Computer und für den NetBIOS-Namen Cache an. Mit diesem Befehl können Sie auch den NetBIOS-Namen Cache und die Namen aktualisieren, die mit WINS (Windows Internet Name Service) registriert sind. Wird ohne Parameter verwendet, zeigt dieser Befehl Hilfe Informationen an.

Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="syntax"></a>Syntax

```
nbtstat [/a <remotename>] [/A <IPaddress>] [/c] [/n] [/r] [/R] [/RR] [/s] [/S] [<interval>]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /a`<remotename>` | Zeigt die NetBIOS-Namen Tabelle eines Remote Computers an, wobei *Remote Name* der NetBIOS-Computername des Remote Computers ist. Die NetBIOS-Namens Tabelle ist die Liste der NetBIOS-Namen, die NetBIOS-Anwendungen entsprechen, die auf diesem Computer ausgeführt werden. |
| /A`<IPaddress>` | Zeigt die NetBIOS-Namen Tabelle eines Remote Computers an, der durch die IP-Adresse (in punktierter Dezimal Schreibweise) des Remote Computers angegeben wird. |
| /C | Zeigt den Inhalt des NetBIOS-Namens Caches, die Tabelle mit den NetBIOS-Namen und ihre aufgelösten IP-Adressen an. |
| /n | Zeigt die NetBIOS-Namen Tabelle des lokalen Computers an. Der Status **registriert** gibt an, dass der Name entweder durch Broadcast oder einen WINS-Server registriert wird. |
| /r | Zeigt Statistiken für die NetBIOS-Namensauflösung an. |
| /R | Löscht den Inhalt des NetBIOS-Namen Caches und lädt dann die vorab markierten Einträge aus der **Lmhosts** -Datei erneut. |
| /RR | Gibt die NetBIOS-Namen für den lokalen Computer frei, der bei WINS-Servern registriert ist, und aktualisiert diese. |
| /s | Zeigt NetBIOS-Client-und Server Sitzungen an und versucht, die Ziel-IP-Adresse in einen Namen zu konvertieren. |
| /S | Zeigt NetBIOS-Client-und Server Sitzungen an und listet die Remote Computer nur durch Ziel-IP-Adresse auf. |
| `<interval>` | Zeigt die ausgewählte Statistik an und hält die Anzahl der Sekunden an, die im *Intervall* zwischen den einzelnen anzeigen angegeben sind. Drücken Sie STRG + C, um die Anzeige von Statistiken zu verhindern. Wenn dieser Parameter ausgelassen wird, druckt **nbtstat** die aktuellen Konfigurationsinformationen nur einmal. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Bei den **nbtstat** -Befehlszeilen Parametern wird die Groß-/Kleinschreibung beachtet.

- Die vom **nbtstat** -Befehl generierten Spaltenüberschriften umfassen Folgendes:

    | Richtung | BESCHREIBUNG |
    | ------- | ----------- |
    | Eingabe | Die Anzahl der empfangenen Bytes. |
    | Output | Die Anzahl der gesendeten Bytes. |
    | Ein/Aus | Gibt an, ob die Verbindung vom Computer (ausgehend) oder von einem anderen Computer zum lokalen Computer (eingehend) erfolgt. |
    | Life | Die verbleibende Zeit, in der ein Name Table Cache-Eintrag aktiv wird, bevor er gelöscht wird. |
    | Lokaler Name | Der lokale NetBIOS-Name, der der Verbindung zugeordnet ist. |
    | Remote Host | Der Name oder die IP-Adresse, die dem Remote Computer zugeordnet ist. |
    | `<03>` | Das letzte Byte eines NetBIOS-Namens, das in Hexadezimal konvertiert wurde. Jeder NetBIOS-Name hat eine Länge von 16 Zeichen. Das letzte Byte hat häufig eine besondere Bedeutung, da derselbe Name mehrmals auf einem Computer vorhanden sein kann, der sich nur im letzten Byte unterscheidet. Beispielsweise `<20>` ist ein Leerzeichen im ASCII-Text. |
    | type | Der Typ des Namens. Ein Name kann entweder ein eindeutiger Name oder ein Gruppenname sein. |
    | Status | Gibt an, ob der NetBIOS-Dienst auf dem Remote Computer ausgeführt wird (registriert ist) oder ob ein doppelter Computername denselben Dienst registriert hat (Konflikt). |
    | Staat | Der Status von NetBIOS-Verbindungen. |

- Folgende NetBIOS-Verbindungszustände sind möglich:

    | Staat | BESCHREIBUNG |
    | ------- | ----------- |
    | Verbunden | Eine Sitzung wurde eingerichtet. |
    | Raum | Dieser Endpunkt ist für eine eingehende Verbindung verfügbar. |
    | Idle | Dieser Endpunkt wurde geöffnet, kann aber keine Verbindungen empfangen. |
    | Verbindung | Eine Sitzung befindet sich in der Verbindungs Phase, und die Zuordnung zwischen Name und IP-Adresse des Ziels wird aufgelöst. |
    | Verantwortung | Eine eingehende Sitzung wird derzeit akzeptiert und wird in Kürze verbunden. |
    | Verbindung | Eine Sitzung versucht, erneut eine Verbindung herzustellen (beim ersten Versuch konnte keine Verbindung hergestellt werden). |
    | Ausgehend | Eine Sitzung befindet sich in der Verbindungs Phase, und die TCP-Verbindung wird gerade erstellt. |
    | Eingehend | Eine eingehende Sitzung befindet sich in der Verbindungs Phase. |
    | Verbindung wird getrennt | Eine Sitzung wird gerade getrennt. |
    | Getrennt | Der lokale Computer hat eine Verbindung getrennt und wartet auf eine Bestätigung vom Remote System. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die NetBIOS-Namens Tabelle des Remote Computers mit dem NetBIOS-Computernamen *CORP07*anzuzeigen:

```
nbtstat /a CORP07
```

Geben Sie Folgendes ein, um die NetBIOS-Namens Tabelle des Remote Computers anzuzeigen, der die IP-Adresse von *10.0.0.99*zugewiesen ist:

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

Wenn Sie den NetBIOS-Namen Cache löschen und die vorab markierten Einträge in der lokalen *Lmhosts* -Datei erneut laden möchten, geben Sie Folgendes ein:

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
