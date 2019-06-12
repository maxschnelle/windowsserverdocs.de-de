---
title: nbtstat
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d2ea99e-72f1-471f-9525-d2c49bf3be82
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e670b1490f1c4c54b8cf377d48755849faa16f8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437119"
---
# <a name="nbtstat"></a>nbtstat

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt die NetBIOS über TCP/IP (NetBT) von Protokollstatistik und NetBIOS-Namen von Tabellen für den lokalen Computer und Remotecomputer und der NetBIOS-Namen Cache. **Nbtstat** ermöglicht das Aktualisieren des NetBIOS-Namencaches und die Namen, die mit Windows Internet Name Service (WINS) registriert. Ohne Parameter verwendet **Nbtstat** zeigt die Hilfe. 

## <a name="syntax"></a>Syntax

```
nbtstat [/a <remoteName>] [/A <IPaddress>] [/c] [/n] [/r] [/R] [/RR] [/s] [/S] [<Interval>]
```

### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                         Beschreibung                                                                                                                         |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /a <remoteName> |    Zeigt die NetBIOS-Namentabelle eines Remotecomputers an, wobei *RemoteName* ist der NetBIOS-Computername des Remotecomputers. Die NetBIOS-Namentabelle ist die Liste der NetBIOS-Namen, die NetBIOS-Anwendungen auf diesem Computer entspricht.     |
| /A <IPaddress>  |                                                           Zeigt die NetBIOS-Namentabelle eines Remotecomputers an, durch die IP-Adresse (in punktierter Dezimalschreibweise) des Remotecomputers angegeben.                                                            |
|       /c        |                                                                        Zeigt den Inhalt des NetBIOS-Namen, Cache, der Tabelle der NetBIOS-Namen und die aufgelösten IP-Adressen.                                                                         |
|       /n        |                                            Zeigt die NetBIOS-Namentabelle des lokalen Computers. Der Status des **registriert** gibt an, dass der Name von Broadcast oder einem WINS-Server registriert ist.                                             |
|       /r        |      Zeigt Statistiken für NetBIOS-Namen auflösen. Auf einem Computer unter Windows XP oder Windows Server 2003, die Verwendung von WINS konfiguriert ist, gibt dieser Parameter die Anzahl der Namen, die behoben wurden, und broadcast und WINS registrierten verwenden.       |
|       /R        |                                                                      Löscht den Inhalt, der den NetBIOS-Namencache und lädt dann erneut die Anzahl vorab tagged Einträge aus der **Lmhosts** Datei.                                                                      |
|       /RR       |                                                                           Gibt an, und anschließend aktualisiert NetBIOS-Namen für den lokalen Computer, der mit WINS-Servern registriert ist.                                                                            |
|       /s        |                                                                          Zeigt die NetBIOS-Client und Server Sitzungen, bei dem Versuch, die Ziel-IP-Adresse in einen Namen zu konvertieren.                                                                           |
|       /S        |                                                                          Zeigt die NetBIOS-Client und Server Sitzungen, den remote-PCs durch die Ziel-IP-Adresse nur auflisten.                                                                          |
|   <Interval>    | Zeigt die gewählte Statistik der angegebenen Anzahl von Sekunden *Intervall* an. Drücken Sie STRG + C, Sitzungstabelle Statistiken. Wenn dieser Parameter ausgelassen wird, **Nbtstat** druckt die aktuelle Konfigurationsinformationen nur einmal. |
|       /?        |                                                                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                             |

## <a name="remarks"></a>Hinweise

-   **Nbtstat** -Befehlszeilenparametern wird Groß-/Kleinschreibung beachtet.

-   Die folgende Tabelle beschreibt die Spaltenüberschriften, die vom generierten **Nbtstat**:

    |Richtung|Beschreibung|
    |------|--------|
    |Input|Die Anzahl der empfangenen Bytes.|
    |Ausgabe|Die Anzahl der gesendeten Bytes.|
    |Eingabe/Ausgabe|Gibt an, ob die Verbindung des Computers (ausgehend) oder einem anderen Computer, auf dem lokalen Computer ist (eingehend).|
    |Life|Die verbleibende Zeit, der vor dem ein Cacheeintrag des Name-Tabelle gespeichert wird, wird es gelöscht.|
    |Lokaler Name|Der lokale NetBIOS-Name der Verbindung zugeordnet.|
    |Remote-Host|Der Name oder IP-Adresse zugeordnet, mit dem Remotecomputer.|
    |<03>|Das letzte Byte mit einem NetBIOS-Namen, die in Hexadezimal konvertiert werden. Jeder NetBIOS-Name ist 16 Zeichen lang sein. Dieses letzte Byte hat häufig besondere Bedeutung, da es sich bei der gleiche Namen mehrere Male auf einem Computer nur in der das letzte Byte sein kann. Beispielsweise ist < 20 > ist ein Bereich in ASCII-Text.|
    |Typ|Der Typ des Namens. Ein Name kann entweder einen eindeutigen Namen oder -Gruppenname sein.|
    |Status|Angibt, ob der NetBIOS-Dienst auf dem Remotecomputer wird ausgeführt (registrierter) oder ein doppelter Computername wurde (Konflikt) über den gleichen Dienst registriert.|
    |Status|Der Status der NetBIOS-Verbindungen.|

-   Die folgende Tabelle beschreibt die möglichen Status der NetBIOS-Verbindung:

    |Status|Beschreibung|
    |-----|--------|
    |Verbunden|Eine Sitzung wurde hergestellt.|
    |verknüpft ist|Ein Verbindungsendpunkt des wurde erstellt und einer IP-Adresse zugeordnet.|
    |Lauschen|Dieser Endpunkt ist für eine eingehende Verbindung verfügbar.|
    |Idle|Dieser Endpunkt geöffnet wurde, aber es kann keine Verbindungen empfangen.|
    |Verbindung wird aufgebaut|Eine Sitzung ist in der eine Verbindung herstellt, und die Adresszuordnung der Namen zu IP-des Ziels aufgelöst wird.|
    |Akzeptieren|Eine eingehende Sitzung wird derzeit akzeptiert werden und wird in Kürze verbunden werden.|
    |Wiederherstellen der Verbindung|Eine Sitzung versucht, eine Verbindung herzustellen (it, das für die Verbindung beim ersten Versuch ist fehlgeschlagen).|
    |Outbound|Eine Sitzung ist in der eine Verbindung herstellt, und die TCP-Verbindung wird gerade erstellt.|
    |Inbound|Eine eingehende Sitzung ist in der eine Verbindung herstellt.|
    |Verbindung wird getrennt|Eine Sitzung ist gerade getrennt.|
    |Disconnected|Der lokale Computer eine Trennung der Verbindung ausgegeben hat und er darauf wartet, bis sich die Bestätigung vom Remotesystem.|

-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele für
Um die NetBIOS-Namentabelle des Remotecomputers mit dem NetBIOS-Computernamen CORP07 anzuzeigen, geben Sie Folgendes ein:

```
nbtstat /a CORP07
```

Um die NetBIOS-Namentabelle des Remotecomputers zugewiesen die IP-Adresse 10.0.0.99 anzuzeigen, geben Sie Folgendes ein:

```
nbtstat /A 10.0.0.99
```

Um die NetBIOS-Namentabelle des lokalen Computers anzuzeigen, geben Sie Folgendes ein:

```
nbtstat /n
```

Um den Inhalt des lokalen Computers NetBIOS-Namencache anzuzeigen, geben Sie Folgendes ein:

```
nbtstat /c
```

Den NetBIOS-Namencache zu löschen und neu laden die Anzahl vorab tagged Einträge in der Lmhosts-Datei, geben:

```
nbtstat /R
```

Um den NetBIOS-Namen, mit dem WINS-Server freigeben und erneut registrieren, geben Sie Folgendes ein:

```
nbtstat /RR
```

Um NetBIOS-Sitzungsstatistiken über die IP-Adresse alle fünf Sekunden anzuzeigen, geben Sie Folgendes ein:

```
nbtstat /S 5
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


