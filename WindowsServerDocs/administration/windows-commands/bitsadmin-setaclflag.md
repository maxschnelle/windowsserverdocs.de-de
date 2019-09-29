---
title: bitsadmin setaclflag
description: 'Windows-Befehls Thema für **BITSAdmin setaclflag** : legt die weitergabesteuerungsflags für die Zugriffs Steuerungs Liste fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fbdb12c29af7b4db8b25846d43ee1c93b2454ff2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380758"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Legt die weitergabesteuerungsflags für die Zugriffs Steuerungs Liste (ACL) für den Auftrag fest. Die Flags geben an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Um z. b. den Besitzer und die Gruppe mit der Datei beizubehalten, legen Sie **Flags** Auf `OG` fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Flags|Geben Sie mindestens einen der folgenden Flagwerte an:</br>' Besitzer Informationen in Datei kopieren.</br>SELBST Kopieren Sie Gruppeninformationen mit der Datei.</br>D Kopieren Sie DACL-Informationen mit der Datei.</br>-S: Kopieren Sie SACL-Informationen mit der Datei.|

## <a name="remarks"></a>Hinweise

Der Schalter "staclflags" wird verwendet, um Besitzer-und Zugriffs Steuerungs Listen-Informationen beizubehalten, wenn ein Auftrag Daten aus einer Windows-Freigabe (SMB) herunterlädt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag *mydownloadjob* festgelegt, um die Besitzer-und Gruppeninformationen mit den heruntergeladenen Dateien beizubehalten.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)