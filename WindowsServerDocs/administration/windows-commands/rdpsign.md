---
title: rdpsign
description: Informationen Sie zum Signieren der RDP-Datei.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9e35d3a3e85ed046fb658bbf5a97ab5fc5eec6d3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442014"
---
# <a name="rdpsign"></a>rdpsign

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ermöglicht Ihnen, eine Remotedesktopprotokoll (RDP)-Datei digital signiert werden.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/sha1 \<hash>|Gibt den Fingerabdruck, den Secure Hash Algorithm 1 (SHA1)-Hash des Signaturzertifikats handelt, die im Zertifikatspeicher enthalten ist.|
|/q|Stiller Modus. Keine Ausgabe, wenn der Befehl erfolgreich ausgeführt wird und die minimale Daten ausgegeben, wenn der Befehl fehlschlägt.|
|/v|Ausführlichen Modus fest. Zeigt alle Warnungen, Meldungen und Status.|
|/l|Überprüft die Ergebnisse signier- und Ausgabe, ohne tatsächlich ersetzen, den Eingabedateien.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der SHA1-Zertifikatfingerabdruck sollte es sich um eine vertrauenswürdige RDP-Datei-Herausgeber darstellen. Um den Fingerabdruck des Zertifikats zu erhalten, öffnen Sie das Zertifikate-Snap-in, und doppelklicken Sie auf das Zertifikat aus, die gewünschte (entweder im Zertifikatspeicher des lokalen Computers oder in Ihrem persönlichen Zertifikatspeicher), klicken Sie auf die **Details** Registerkarte, und klicken Sie dann in der **Feld** auf **Fingerabdruck**.

    > [!NOTE]
    > Wenn Sie den Fingerabdruck für die Verwendung mit dem Tool rdpsign.exe kopieren, müssen Sie Leerzeichen entfernen.

-   Sie müssen die RDP-Datei (oder Dateien) zu signieren, indem Sie mit dem vollständigen Namen angeben. Platzhalterzeichen werden nicht akzeptiert.
-   Die signierte Ausgabedateien überschreibt die Eingabedateien.
-   Wenn Sie die RDP-Dateien können nicht gelesen oder geschrieben werden, wird das Tool zur nächsten Datei fortgesetzt, wenn mehrere Dateien angegeben werden.

## <a name="BKMK_examples"></a>Beispiele für
- Um eine RDP-Datei signieren mit dem Namen File1.rdp, navigieren Sie zu dem Ordner, in dem Sie die RDP-Datei gespeichert, und klicken Sie dann Folgendes ein:
  ```
  rdpsign /sha1 hash file1.rdp
  ```
  > [!NOTE]
  > Die *Hash* Wert darstellt, den SHA1-Zertifikatfingerabdruck ohne Leerzeichen.
- Um zu testen, ob die digitale Signatur für eine RDP-Datei erfolgreich ist, ohne tatsächlich Signieren der Datei, geben Sie Folgendes ein:
  ```
  rdpsign /sha1 hash /l file1.rdp
  ```
- Um mehrere RDP-Dateien zu signieren, werden die Dateinamen durch Leerzeichen getrennt. Um mehrere RDP-Dateien zu signieren, die File1.rdp File2.rdp und File3.rdp benannt sind, geben Sie beispielsweise Folgendes ein:
  ```
  rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
  ```
  ## <a name="see-also"></a>Siehe auch
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
