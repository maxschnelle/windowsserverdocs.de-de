---
title: autoconv
description: Windows-Befehls Thema für **Autov**, das Datei Zuordnungs Tabellen-und FAT32-Volumes in das NTFS-Dateisystem konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe0e388a1d4fd79567ef0562197e3181bbbc46f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851113"
---
# <a name="autoconv"></a>autoconv

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konvertiert Dateizuordnungs-und FAT32-Volumes in das NTFS-Dateisystem, wobei vorhandene Dateien und Verzeichnisse beim Start nach der Ausführung von **Autochk** intakt bleiben. Volumes, die in das NTFS-Dateisystem konvertiert werden, können nicht zurück in FAT oder FAT32 konvertiert werden.

## <a name="remarks"></a>Hinweise

**Autov** kann nicht in der Befehlszeile ausgeführt werden. Diese wird nur beim Start ausgeführt, wenn Sie durch **Convert. exe**festgelegt wird.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [autochk](autochk.md)

- [convert](convert.md)

- [Arbeiten mit Dateisystemen](https://go.microsoft.com/fwlink/?LinkId=4509)
