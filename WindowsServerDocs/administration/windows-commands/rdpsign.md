---
title: rdpsign
description: Referenz Artikel zum rdpsign-Befehl, mit dem Sie eine Remotedesktopprotokoll Datei (. RDP) digital signieren können.
ms.topic: reference
ms.assetid: 4a6fa8ce-3d32-49a5-b056-bcc1a23391f5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: a98619c468ce26e7af3406512be54937c8aa799d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637341"
---
# <a name="rdpsign"></a>rdpsign

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das digitale Signieren einer Remotedesktopprotokoll Datei (. RDP).

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /sha1 `<hash>` | Gibt den Fingerabdruck an. Hierbei handelt es sich um den Secure-Hash-Algorithmus 1 (SHA1)-Hash des Signatur Zertifikats, das im Zertifikat Speicher enthalten ist. Wird in Windows Server 2012 R2 und älteren Versionen verwendet. |
| /sha256 `<hash>` | Gibt den Fingerabdruck an, bei dem es sich um den Secure Hash Algorithmus 256 (SHA256)-Hash des Signatur Zertifikats handelt, das im Zertifikat Speicher enthalten ist. Ersetzt/SHA1 in Windows Server 2016 und höher. |
| /q | Stiller Modus. Keine Ausgabe, wenn der Befehl erfolgreich ausgeführt wird, und minimale Ausgabe, wenn der Befehl fehlschlägt. |
| /v | Ausführliche-Modus. Zeigt alle Warnungen, Meldungen und den Status an. |
| /l | Testet die Signierungs-und Ausgabe Ergebnisse, ohne tatsächlich eine der Eingabedateien zu ersetzen. |
| `<file_name.rdp>` | Der Name der RDP-Datei. Sie müssen die RDP-Datei (oder Dateien) angeben, die mit dem vollständigen Dateinamen signiert werden soll. Platzhalter Zeichen werden nicht akzeptiert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der SHA1-oder SHA256-Zertifikat Fingerabdruck sollte einen vertrauenswürdigen RDP-Datei Herausgeber darstellen. Öffnen Sie zum Abrufen des Zertifikat Fingerabdrucks das **Zertifikate** -Snap-in, und doppelklicken Sie auf das Zertifikat, das Sie verwenden möchten (entweder im Zertifikat Speicher des lokalen Computers oder in Ihrem persönlichen Zertifikat Speicher), klicken Sie auf die Registerkarte **Details** , und klicken Sie dann in der **Feldliste** auf Finger **Abdruck**.

    > [!NOTE]
    > Wenn Sie den Fingerabdruck für die Verwendung mit dem rdpsign.exe Tool kopieren, müssen Sie Leerzeichen entfernen.

- Die signierten Ausgabedateien überschreiben die Eingabedateien.

- Wenn mehrere Dateien angegeben sind und eine der RDP-Dateien nicht gelesen oder geschrieben werden kann, wird das Tool mit der nächsten Datei fortgesetzt.

### <a name="examples"></a>Beispiele

Zum Signieren einer RDP-Datei mit dem Namen *File1. RDP*navigieren Sie zu dem Ordner, in dem Sie die RDP-Datei gespeichert haben, und geben Sie dann Folgendes ein:

```
rdpsign /sha1 hash file1.rdp
```

> [!NOTE]
> Der *Hashwert* stellt den SHA1-Zertifikat Fingerabdruck ohne Leerzeichen dar.

Geben Sie Folgendes ein, um zu testen, ob die digitale Signatur für eine RDP-Datei erfolgreich ist, ohne die Datei tatsächlich zu signieren

```
rdpsign /sha1 hash /l file1.rdp
```

Zum Signieren mehrerer RDP-Dateien mit den Namen *File1. RDP*, *File2. RDP*und *datei3. RDP*geben Sie (einschließlich der Leerzeichen zwischen den Dateinamen) Folgendes ein:

```
rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
```

## <a name="see-also"></a>Weitere Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
