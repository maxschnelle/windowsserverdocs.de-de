---
title: rdpsign
description: Erfahren Sie, wie Sie eine RDP-Datei digital signieren.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a6fa8ce-3d32-49a5-b056-bcc1a23391f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 406563a07d3760c2846c201410f3a7b8f1c2829b
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588055"
---
# <a name="rdpsign"></a>rdpsign

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das digitale Signieren einer Remotedesktopprotokoll Datei (. RDP).
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/SHA1 \<Hash >|Gibt den Fingerabdruck an. Hierbei handelt es sich um den Secure-Hash-Algorithmus 1 (SHA1)-Hash des Signatur Zertifikats, das im Zertifikat Speicher enthalten ist. Wird in Windows Server 2012 R2 und älteren Versionen verwendet.|
|/SHA256 \<Hash >|Gibt den Fingerabdruck an, bei dem es sich um den Secure Hash Algorithmus 256 (SHA256)-Hash des Signatur Zertifikats handelt, das im Zertifikat Speicher enthalten ist. Ersetzt/SHA1 in Windows Server 2016 und höher.|
|/q|Stiller Modus. Keine Ausgabe, wenn der Befehl erfolgreich ausgeführt wird, und minimale Ausgabe, wenn der Befehl fehlschlägt.|
|/v|Ausführliche-Modus. Zeigt alle Warnungen, Meldungen und den Status an.|
|/l|Testet die Signierungs-und Ausgabe Ergebnisse, ohne tatsächlich eine der Eingabedateien zu ersetzen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der SHA1-oder SHA256-Zertifikat Fingerabdruck sollte einen vertrauenswürdigen RDP-Datei Herausgeber darstellen. Öffnen Sie zum Abrufen des Zertifikat Fingerabdrucks das Zertifikate-Snap-in, und doppelklicken Sie auf das Zertifikat, das Sie verwenden möchten (entweder im Zertifikat Speicher des lokalen Computers oder in Ihrem persönlichen Zertifikat Speicher), klicken Sie auf die Registerkarte **Details** , und klicken Sie dann in der **Feldliste** auf Finger **Abdruck**.

    > [!NOTE]
    > Wenn Sie den Fingerabdruck für die Verwendung mit dem Tool rdpsign. exe kopieren, müssen Sie Leerzeichen entfernen.

-   Sie müssen die RDP-Datei (oder Dateien) angeben, die mit dem vollständigen Dateinamen signiert werden soll. Platzhalter Zeichen werden nicht akzeptiert.
-   Die signierten Ausgabedateien überschreiben die Eingabedateien.
-   Wenn eine der RDP-Dateien nicht gelesen oder geschrieben werden kann, wird das Tool mit der nächsten Datei fortgesetzt, wenn mehrere Dateien angegeben sind.

## <a name="BKMK_examples"></a>Beispiele
- Zum Signieren einer RDP-Datei mit dem Namen file1. RDP navigieren Sie zu dem Ordner, in dem Sie die RDP-Datei gespeichert haben, und geben Sie dann Folgendes ein:
  ```
  rdpsign /sha1 hash file1.rdp
  ```
  > [!NOTE]
  > Der *Hashwert* stellt den SHA1-Zertifikat Fingerabdruck ohne Leerzeichen dar.
- Geben Sie Folgendes ein, um zu testen, ob die digitale Signierung für eine RDP-Datei erfolgreich ist, ohne die Datei tatsächlich zu signieren:
  ```
  rdpsign /sha1 hash /l file1.rdp
  ```
- Zum Signieren mehrerer RDP-Dateien trennen Sie die Dateinamen mithilfe von Leerzeichen. Wenn Sie z. b. mehrere RDP-Dateien mit den Namen file1. RDP, file2. RDP und datei3. RDP signieren möchten, geben Sie Folgendes ein:
  ```
  rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
  ```
  ## <a name="see-also"></a>Weitere Informationen
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste &#40;Terminal Dienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
