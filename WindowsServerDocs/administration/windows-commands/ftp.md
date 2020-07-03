---
title: ftp
description: Referenz Artikel für den FTP-Befehl, der Dateien an einen Computer überträgt, auf dem ein Dateiübertragungsprotokoll (FTP)-Server Dienst ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e78148e1e7dc4f402d80bb4ebfbcbdac52249407
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925617"
---
# <a name="ftp"></a>ftp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überträgt Dateien an einen und von einem Computer, auf dem ein Dateiübertragungsprotokoll (FTP)-Server Dienst ausgeführt wird. Dieser Befehl kann interaktiv oder im Batch Modus durch Verarbeitung von ASCII-Textdateien verwendet werden.

## <a name="syntax"></a>Syntax

```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<filename>] [-a] [-A] [-x:<sendbuffer>] [-r:<recvbuffer>] [-b:<asyncbuffers>][-w:<windowssize>][<host>] [-?]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ----------| ----------- |
| -v | Unterdrückt die Anzeige von Remote Server Antworten. |
| -d | Aktiviert das Debuggen und zeigt alle Befehle an, die zwischen dem FTP-Client und dem FTP-Server |
| -i | Deaktiviert die interaktive Eingabeaufforderung während mehrerer Dateiübertragungen. |
| -n | Unterdrückt die automatische Anmeldung bei der ersten Verbindung. |
| -g | Deaktiviert die Dateiname-Globalisierung.  Mit **glob** können Sie das Sternchen (*) und das Fragezeichen (?) als Platzhalter Zeichen in lokalen Datei-und Pfadnamen verwenden. |
| Hymnen`<filename>` | Gibt eine Textdatei an, die **FTP** -Befehle enthält. Diese Befehle werden nach dem Start von **FTP** automatisch ausgeführt. Dieser Parameter lässt keine Leerzeichen zu. Verwenden Sie diesen Parameter anstelle der Umleitung ( `<` ). **Hinweis:** In den Betriebssystemen Windows 8 und Windows Server 2012 oder höher muss die Textdatei in UTF-8 geschrieben werden. |
| -a | Gibt an, dass beim Binden der FTP-Datenverbindung eine beliebige lokale Schnittstelle verwendet werden kann. |
| -A | Meldet sich als anonym auf dem FTP-Server an. |
| Stuben`<sendbuffer> `| Überschreibt die Standard SO_SNDBUF Größe von 8192. |
| r`<recvbuffer>` | Überschreibt die Standard SO_RCVBUF Größe von 8192. |
| b`<asyncbuffers>` | Überschreibt die standardmäßige Async-Puffer Anzahl von 3. |
| Löw`<windowssize>` | Gibt die Größe des Übertragungs Puffers an. Die Standardfenster Größe beträgt 4096 Bytes. |
| `<host>` | Gibt den Computernamen, die IP-Adresse oder die IPv6-Adresse des FTP-Servers an, mit dem eine Verbindung hergestellt werden soll. Der Hostname oder die Adresse, falls angegeben, muss der letzte Parameter in der Zeile sein. |
| -? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Bei den **FTP** -Befehlszeilen Parametern wird die Groß-/Kleinschreibung beachtet.

- Dieser Befehl ist nur verfügbar, wenn das **TCP/IP-Protokoll (Internet Protocol)** als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

- Der **FTP** -Befehl kann interaktiv verwendet werden. Nach dem Start erstellt **FTP** eine unter Umgebung, in der Sie **FTP** -Befehle verwenden können. Sie können zur Eingabeaufforderung zurückkehren, indem Sie den Befehl **Beenden** eingeben. Wenn die **FTP** -unter Umgebung ausgeführt wird, wird Sie von der `ftp >` Eingabeaufforderung angezeigt. Weitere Informationen finden Sie in den **FTP** -Befehlen.

- Der **FTP** -Befehl unterstützt die Verwendung von IPv6, wenn das IPv6-Protokoll installiert ist.

### <a name="examples"></a>Beispiele

Um sich am FTP-Server mit dem Namen anzumelden, geben Sie Folgendes ein `ftp.example.microsoft.com` :

```
ftp ftp.example.microsoft.com
```

Geben Sie Folgendes ein, um sich am FTP-Server mit dem Namen anzumelden `ftp.example.microsoft.com` und die in einer Datei namens *resync.txt*enthaltenen **FTP** -Befehle auszuführen:

```
ftp -s:resync.txt ftp.example.microsoft.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))

- [IP-Version 6](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc738636(v=ws.10))

- [IPv6-Anwendungen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc782509(v=ws.10))
