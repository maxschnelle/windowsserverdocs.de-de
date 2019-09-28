---
title: ftp
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b64e6831fcf8930c62b2a3f04022dc49d5297683
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375861"
---
# <a name="ftp"></a>ftp

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überträgt Dateien an einen und von einem Computer, auf dem ein Dateiübertragungsprotokoll (FTP)-Server Dienst ausgeführt wird. **FTP** kann interaktiv oder im Batch Modus durch Verarbeitung von ASCII-Textdateien verwendet werden. 
## <a name="syntax"></a>Syntax
```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<FileName>] [-a] [-A] [-x:<SendBuffer>] [-r:<RecvBuffer>] [-b:<AsyncBuffers>][-w:<WindowsSize>]  [-?] [<Host>]
```
### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                                                                      Beschreibung                                                                                                                                                      |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        -v         |                                                                                                                                    Unterdrückt die Anzeige von Remote Server Antworten.                                                                                                                                     |
|        -d         |                                                                                                               Aktiviert das Debuggen und zeigt alle Befehle an, die zwischen dem FTP-Client und dem FTP-Server                                                                                                                |
|        -i         |                                                                                                                            Deaktiviert die interaktive Eingabeaufforderung während mehrerer Dateiübertragungen.                                                                                                                             |
|        -n         |                                                                                                                                    Unterdrückt die automatische Anmeldung bei der ersten Verbindung.                                                                                                                                     |
|        -g         |                                         Deaktiviert die Dateiname-Globalisierung.  Mit **glob** können Sie das Sternchen (\*) und das Fragezeichen (?) als Platzhalter Zeichen in lokalen Datei-und Pfadnamen verwenden. Weitere Informationen finden Sie unter [Zusätzliche Verweise](ftp.md#BKMK_additionalRef).                                          |
|   -s: <FileName>   | Gibt eine Textdatei an, die **FTP** -Befehle enthält. Diese Befehle werden nach dem Start von **FTP** automatisch ausgeführt. Dieser Parameter lässt keine Leerzeichen zu. Verwenden Sie diesen Parameter anstelle der Umleitung ( **<** ). **Hinweis**: In den Betriebssystemen Windows 8 und Windows Server 2012 oder höher muss die Textdatei in UTF-8 geschrieben werden. |
|        -a         |                                                                                                                 Gibt an, dass beim Binden der FTP-Datenverbindung eine beliebige lokale Schnittstelle verwendet werden kann.                                                                                                                  |
|        -A         |                                                                                                                                        Meldet sich als anonym auf dem FTP-Server an.                                                                                                                                         |
|  -x: <SendBuffer>  |                                                                                                                                     Überschreibt die SO_SNDBUF-Standardgröße von 8192.                                                                                                                                     |
|  -r: <RecvBuffer>  |                                                                                                                                     Überschreibt die SO_RCVBUF-Standardgröße von 8192.                                                                                                                                     |
| -b: <AsyncBuffers> |                                                                                                                                    Überschreibt die standardmäßige Async-Puffer Anzahl von 3.                                                                                                                                     |
| -w: <WindowsSize>  |                                                                                                                   Gibt die Größe des Übertragungs Puffers an. Die Standardfenster Größe beträgt 4096 Bytes.                                                                                                                   |
|        -?         |                                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                          |
|      <host>       |                                                                    Gibt den Computernamen, die IP-Adresse oder die IPv6-Adresse des FTP-Servers an, mit dem eine Verbindung hergestellt werden soll. Der Hostname oder die Adresse, falls angegeben, muss der letzte Parameter in der Zeile sein.                                                                    |

## <a name="remarks"></a>Hinweise
- Weitere Informationen zu **FTP** -Befehlen unter Windows Server 2003 finden Sie unter [FTP](https://technet.microsoft.com/library/cc756013(v=ws.10).aspx).
- bei **FTP** -Befehlszeilen Parametern wird die Groß-/Kleinschreibung beachtet.
- Dieser Befehl ist nur verfügbar, wenn das **TCP/IP-Protokoll (Internet Protocol)** als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.
- **FTP** kann interaktiv verwendet werden. Nach dem Start erstellt **FTP** eine unter Umgebung, in der Sie **FTP** -Befehle verwenden können. Sie können zur Eingabeaufforderung zurückkehren, indem Sie den Befehl **Beenden** eingeben. Wenn die **FTP** -unter Umgebung ausgeführt wird, wird Sie von der **FTP->** Eingabeaufforderung angezeigt. Weitere Informationen finden Sie in den **FTP** -Befehlen.
- **FTP** unterstützt die Verwendung von IPv6, wenn das IPv6-Protokoll installiert ist. Weitere Informationen finden Sie unter [Zusätzliche Verweise](ftp.md#BKMK_additionalRef).
  ## <a name="BKMK_Examples"></a>Beispiele
  Um sich am FTP-Server mit dem Namen ftp.example.Microsoft.com anzumelden, geben Sie Folgendes ein:
  ```
  ftp ftp.example.microsoft.com
  ```
  Geben Sie Folgendes ein, um sich am FTP-Server mit dem Namen ftp.example.Microsoft.com anzumelden und die **FTP** -Befehle auszuführen, die in einer Datei namens Resync. txt enthalten sind:
  ```
  ftp -s:resync.txt ftp.example.microsoft.com
  ```
  ## <a name="BKMK_additionalRef"></a>Weitere Verweise
- [IP-Version 6](https://technet.microsoft.com/library/cc738636(v=ws.10).aspx)
- [IPv6-Anwendungen](https://technet.microsoft.com/library/cc782509(v=ws.10).aspx)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
