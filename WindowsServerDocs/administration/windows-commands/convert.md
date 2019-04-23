---
title: convert
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 96e437c0-1aa3-46ab-9078-a7b8cdaf3792
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9fcb7b2190c3359b78145a2ef79a28e30639a89c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873161"
---
# <a name="convert"></a>convert



Konvertiert die Datei FAT (Allocation Table) und FAT32-Volumes auf dem NTFS-Dateisystem beibehalten vorhandener Dateien und Verzeichnisse. Volumes in NTFS-Dateisystem konvertiert darf nicht FAT oder FAT32 an konvertiert werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
convert [<Volume>] /fs:ntfs [/v] [/cvtarea:<FileName>] [/nosecurity] [/x]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Volume >|Gibt den Laufwerkbuchstaben (gefolgt von einem Doppelpunkt), Bereitstellungspunkt oder Name des Volumes in NTFS konvertieren.|
|/fs:ntfs|Erforderlich. Das Volume konvertiert in NTFS.|
|/v|Ausführungen **konvertieren** im ausführlichen Modus, woraufhin alle Nachrichten während der Konvertierung.|
|/cvtarea:\<FileName>|Gibt an, dass die Masterdateitabelle (MFT) und andere NTFS-Metadatendateien in eine vorhandene zusammenhängend Platzhalterdatei geschrieben werden. Diese Datei muss sich im Stammverzeichnis des Dateisystems, konvertiert werden soll. Verwenden der **CvtArea** Parameter kann dazu führen, einen weniger Fragmentierung des Dateisystems nach der Konvertierung. Für optimale Ergebnisse die Größe dieser Datei muss 1 KB, die multipliziert der Anzahl der Dateien und Verzeichnisse im Dateisystem, obwohl die **konvertieren** Hilfsprogramm akzeptiert, Dateien beliebiger Größe.</br>Wichtig: Sie müssen die Platzhalterdatei erstellen, mit der **Fsutil Datei Createnew** Befehl vor der Ausführung **konvertieren**. **Konvertieren von** erstellt diese Datei nicht für Sie. **Konvertieren von** überschreibt diese Datei mit dem NTFS-Metadaten. Nach der Konvertierung wird ungenutzter Speicherplatz in dieser Datei freigegeben.|
|/nosecurity|Gibt an, dass die Sicherheitseinstellungen für die konvertierten Dateien und Verzeichnisse Zugriff durch alle Benutzer zulassen.|
|/x|Die Volumebereitstellung, falls erforderlich, bevor er konvertiert wird. Alle geöffneten Handles zum Volume sind nicht mehr gültig.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn **konvertieren** das Laufwerk kann nicht gesperrt werden kann (z. B. das Laufwerk ist das System- oder das aktuelle Laufwerk), erhalten Sie die Option zum Konvertieren des Laufwerks beim nächsten des Computers Neustart. Wenn den Computer direkt, um die Konvertierung abzuschließen kann nicht gestartet werden, Planen Sie eine Zeit in den Computer neu starten und zusätzliche Zeit für den Konvertierungsprozess abgeschlossen.
-   Für Volumes nach NTFS konvertiert von FAT oder FAT32:

    Aufgrund der bestehende Datenträgerverwendung wird die MFT an einem anderen Speicherort erstellt, als auf einem Volume, das ursprünglich mit NTFS formatiert, also Volume Leistung nicht so gut wie auf Volumes, die ursprünglich mit NTFS formatiert sein kann. Sollten Sie um eine optimale Leistung diese Volumes neu zu erstellen und diese mit dem NTFS-Dateisystem formatiert werden.

    Volumekonvertierung von FAT oder FAT32 in NTFS bleiben die Dateien erhalten, das Volume fehlen jedoch möglicherweise einige Leistungsvorteile im Vergleich zu Volumes, die anfänglich mit NTFS formatiert. Z. B. die MFT möglicherweise auf konvertierte Datenträger fragmentiert werden. Darüber hinaus auf konvertierte Startvolumes **konvertieren** gilt die gleiche Standardsicherheit, die während des Setups von Windows angewendet wird.

## <a name="BKMK_examples"></a>Beispiele für

Um das Volume auf dem Laufwerk E: in NTFS konvertieren, und zeigen alle Nachrichten während der Konvertierung, geben Sie Folgendes ein:
```
convert e: /fs:ntfs /v
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)