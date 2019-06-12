---
title: ftp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3639626962e295a54c9068c9731f1d30754a9472
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438371"
---
# <a name="ftp"></a>ftp

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überträgt Dateien in und aus einem Computer mit einer Server-Dienst mit File Transfer Protocol (ftp). **FTP** kann interaktiv oder im Modus "Batch" verwendet werden, durch die Verarbeitung von ASCII-Textdateien. 
## <a name="syntax"></a>Syntax
```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<FileName>] [-a] [-A] [-x:<SendBuffer>] [-r:<RecvBuffer>] [-b:<AsyncBuffers>][-w:<WindowsSize>]  [-?] [<Host>]
```
### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                                                                      Beschreibung                                                                                                                                                      |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        -v         |                                                                                                                                    Unterdrückt die Anzeige der Remoteserver-Antworten.                                                                                                                                     |
|        -d         |                                                                                                               Ermöglicht das Debuggen und Anzeigen von allen Befehlen, die zwischen dem FTP-Client und dem FTP-Server übergeben.                                                                                                                |
|        -i         |                                                                                                                            Deaktiviert die interaktive Aufforderung während der Übertragung von mehreren Dateien.                                                                                                                             |
|        -n         |                                                                                                                                    Unterdrückt die automatische Anmeldung bei der ersten Verbindung.                                                                                                                                     |
|        -g         |                                         Deaktiviert die Namen von Platzhaltern.  **Glob** erlaubt die Verwendung des Sternchens (\*) und ein Fragezeichen (?) als Platzhalterzeichen in lokalen Dateinamen und Pfad. Weitere Informationen finden Sie unter [zusätzliche Verweise](ftp.md#BKMK_additionalRef).                                          |
|   -s:<FileName>   | Gibt an, eine Textdatei mit **ftp** Befehle. Automatisch nach dem Ausführen dieser Befehle **ftp** beginnt. Dieser Parameter ermöglicht keine Leerzeichen enthalten. Verwenden Sie diesen Parameter anstelle von Umleitung ( **<** ). **Hinweis**: In Windows 8 und Windows Server 2012 oder höher muss die Textdatei in UTF-8 geschrieben werden. |
|        -a         |                                                                                                                 Gibt an, dass es sich bei eine lokale Schnittstelle verwendet werden kann, wenn die ftp-Datenverbindung gebunden.                                                                                                                  |
|        -A         |                                                                                                                                        Die Protokolle auf dem ftp-Server als anonymes.                                                                                                                                         |
|  -x:<SendBuffer>  |                                                                                                                                     Überschreibt die Standardgröße der SO_SNDBUF 8192 Zeichen.                                                                                                                                     |
|  -r:.<RecvBuffer>  |                                                                                                                                     Überschreibt die Standardgröße der SO_RCVBUF 8192 Zeichen.                                                                                                                                     |
| -b:<AsyncBuffers> |                                                                                                                                    Überschreibt die standardmäßige asynchrone Pufferanzahl 3.                                                                                                                                     |
| -w:<WindowsSize>  |                                                                                                                   Gibt die Größe des Übertragungspuffers. Die Standardgröße ist 4096 Bytes.                                                                                                                   |
|        -?         |                                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                          |
|      <host>       |                                                                    Gibt an, der Computername, IP-Adresse oder IPv6-Adresse des FTP-Servers, auf dem eine Verbindung herstellen. Den Hostnamen oder die Adresse muss angegeben werden, der letzte Parameter in der Zeile sein.                                                                    |

## <a name="remarks"></a>Hinweise
- Weitere Informationen zu **ftp** Befehle in Windows Server 2003 finden Sie unter [ftp](https://technet.microsoft.com/library/cc756013(v=ws.10).aspx).
- **FTP** -Befehlszeilenparametern wird Groß-/Kleinschreibung beachtet.
- Mit diesem Befehl steht nur, wenn die **Internetprotokoll (TCP/IP)** Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.
- **FTP** können interaktiv verwendet werden. Nachdem sie gestartet wurde, **ftp** erstellt eine untergeordnete Umgebung, in denen Sie verwenden können **ftp** Befehle. Sie können zur Eingabeaufforderung zurückkehren, durch Eingabe der **beenden** Befehl. Wenn die **ftp** untergeordnete Umgebung ausgeführt wird, es wird angegeben, indem die **ftp >** Eingabeaufforderung. Weitere Informationen finden Sie unter den **ftp** Befehle.
- **FTP** die Verwendung von IPv6 unterstützt, wenn das IPv6-Protokoll installiert ist. Weitere Informationen finden Sie unter [zusätzliche Verweise](ftp.md#BKMK_additionalRef).
  ## <a name="BKMK_Examples"></a>Beispiele für
  Zum Anmelden am FTP-Server mit dem Namen ftp.example.microsoft.com, geben Sie Folgendes ein:
  ```
  ftp ftp.example.microsoft.com
  ```
  Melden Sie sich bei dem ftp-Server mit dem Namen ftp.example.microsoft.com, und führen Sie die **ftp** enthalten sind, in einer Datei namens resync.txt, Typ:
  ```
  ftp -s:resync.txt ftp.example.microsoft.com
  ```
  ## <a name="BKMK_additionalRef"></a>Zusätzliche Referenzen
- [Internetprotokoll, Version 6](https://technet.microsoft.com/library/cc738636(v=ws.10).aspx)
- [IPv6-Anwendungen](https://technet.microsoft.com/library/cc782509(v=ws.10).aspx)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
