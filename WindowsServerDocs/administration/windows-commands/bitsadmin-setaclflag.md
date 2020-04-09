---
title: bitsadmin setaclflag
description: Windows-Befehls Thema für BITSAdmin setaclflag, mit dem die weitergabesteuerungsflags für Zugriffs Steuerungs Listen festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ac47e554dde6a555e891d89668cd12fec3179d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849673"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Legt die weitergabesteuerungsflags für die Zugriffs Steuerungs Liste (ACL) für den Auftrag fest. Die Flags geben an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Um z. b. den Besitzer und die Gruppe mit der Datei beizubehalten, legen Sie **Flags** auf `OG`fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetAclFlags <Job> <Flags>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Flags|Geben Sie mindestens einen der folgenden Flagwerte an:</br>-O: Besitzer Informationen in Datei kopieren.</br>-G: Kopieren von Gruppeninformationen mit der Datei.</br>-D: DACL-Informationen werden mit der Datei kopiert.</br>-S: Kopieren Sie SACL-Informationen mit der Datei.|

## <a name="remarks"></a>Hinweise

Der Schalter "staclflags" wird verwendet, um Besitzer-und Zugriffs Steuerungs Listen-Informationen beizubehalten, wenn ein Auftrag Daten aus einer Windows-Freigabe (SMB) herunterlädt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag *mydownloadjob* festgelegt, um die Besitzer-und Gruppeninformationen mit den heruntergeladenen Dateien beizubehalten.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)