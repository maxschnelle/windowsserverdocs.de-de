---
title: convert
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c1e22f67768bbe2f37f3627ca69b162cae96f2d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379079"
---
# <a name="convert"></a>convert



Konvertiert Dateizuordnungs-und FAT32-Volumes in das NTFS-Dateisystem, sodass vorhandene Dateien und Verzeichnisse intakt bleiben. Volumes, die in das NTFS-Dateisystem konvertiert werden, können nicht zurück in FAT oder FAT32 konvertiert werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
convert [<Volume>] /fs:ntfs [/v] [/cvtarea:<FileName>] [/nosecurity] [/x]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<volume >|Gibt den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt), einen Einstellungspunkt oder einen Volumenamen an, der in NTFS konvertiert werden soll.|
|/FS: NTFS|Erforderlich. Konvertiert das Volume in NTFS.|
|/v|Führt **Convert** im ausführlichen Modus aus, in dem während des Konvertierungs Vorgangs alle Meldungen angezeigt werden.|
|/CvtArea: \<filename >|Gibt an, dass die Master Dateitabelle (MFT) und andere NTFS-Metadatendateien in eine vorhandene, zusammenhängende Platzhalter Datei geschrieben werden. Diese Datei muss sich im Stammverzeichnis des Dateisystems befinden, das konvertiert werden soll. Die Verwendung des **/Cvtarea** -Parameters kann nach der Konvertierung zu einem weniger fragmentierten Dateisystem führen. Um optimale Ergebnisse zu erzielen, sollte die Größe dieser Datei 1 KB multipliziert mit der Anzahl der Dateien und Verzeichnisse im Dateisystem betragen, obwohl das **Convert** Utility Dateien beliebiger Größe akzeptiert.</br>Wichtig: Sie müssen die Platzhalter Datei erstellen, indem Sie den Befehl **fsutil file atenew** vor dem Ausführen von **Convert**verwenden. **Convert** erstellt diese Datei nicht für Sie. **Convert** überschreibt diese Datei mit NTFS-Metadaten. Nach der Konvertierung wird der nicht verwendete Speicherplatz in dieser Datei freigegeben.|
|/nosecurity|Gibt an, dass die Sicherheitseinstellungen für die konvertierten Dateien und Verzeichnisse den Zugriff durch alle Benutzer zulassen.|
|/x|Hebt die Bereitstellung des Volumes bei Bedarf vor der Konvertierung auf. Alle geöffneten Handles zum Volume sind nicht mehr gültig.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn **Convert** das Laufwerk nicht sperren kann (z. b. wenn das Laufwerk das System Volume oder das aktuelle Laufwerk ist), haben Sie die Möglichkeit, das Laufwerk beim nächsten Neustart des Computers zu konvertieren. Wenn Sie den Computer nicht sofort neu starten können, um die Konvertierung abzuschließen, planen Sie einen Neustart des Computers ein, und lassen Sie zusätzliche Zeit für den Abschluss des Konvertierungs Vorgangs zu.
-   Für Volumes, die von FAT oder FAT32 in NTFS konvertiert werden:

    Aufgrund der vorhandenen Datenträger Verwendung wird die MFT an einem anderen Speicherort als auf einem Volume erstellt, das ursprünglich mit NTFS formatiert wurde, sodass die Volumeleistung möglicherweise nicht so gut ist wie bei Volumes, die ursprünglich mit NTFS formatiert wurden. Um eine optimale Leistung zu erzielen, sollten Sie diese Volumes neu erstellen und mit dem NTFS-Dateisystem formatieren.

    Bei der Volumekonvertierung von FAT oder FAT32 zu NTFS bleiben die Dateien intakt, aber das Volume kann im Vergleich zu den ursprünglich mit NTFS formatierten Volumes einige Leistungsvorteile mit sich bringen. Beispielsweise kann die MFT auf konvertierten Volumes fragmentiert werden. Außerdem wendet **Convert** auf konvertierten Start Volumes die gleiche Standard Sicherheit an, die während Windows Setup angewendet wird.

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie das Volume auf Laufwerk E in NTFS konvertieren und während des Konvertierungs Vorgangs alle Meldungen anzeigen möchten, geben Sie Folgendes ein:
```
convert e: /fs:ntfs /v
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)