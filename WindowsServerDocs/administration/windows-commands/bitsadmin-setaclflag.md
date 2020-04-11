---
title: bitsadmin setaclflag
description: Windows-Befehls Thema für **BITSAdmin setaclflag**, mit dem die Zugriffs Steuerungs Listen-Weitergabeflags festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0aae550e94d04db518edccafb1d6bcf46d0320b
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123063"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Legt die weitergabesteuerungsflags für die Zugriffs Steuerungs Liste (ACL) für den Auftrag fest. Die Flags geben an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Um z. b. den Besitzer und die Gruppe mit der Datei beizubehalten, legen Sie den **Flags** -Parameter auf `og`fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setaclflag <job> <flags>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| flags | Geben Sie einen oder mehrere der Werte an, einschließlich:<ul><li>**o** -Besitzer Informationen mit Datei kopieren.</li><li>**g** -Gruppeninformationen in Datei kopieren.</li><li>**d** : Kopieren Sie die DACL-Informationen ("-Zugriffs Steuerungs Liste") mit der Datei.</li><li>**s** -Informationen zur System Zugriffs Steuerungs Liste (SACL) mit Datei kopieren.</li></ul> |

## <a name="remarks"></a>Hinweise

Der Schalter/setaclflag wird verwendet, um Besitzer-und Zugriffs Steuerungs Listen-Informationen beizubehalten, wenn ein Auftrag Daten aus einer Windows-Freigabe (SMB) herunterlädt.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag *mydownloadjob* festgelegt, um die Besitzer-und Gruppeninformationen mit den heruntergeladenen Dateien beizubehalten.

```
C:\>bitsadmin /setaclflags myDownloadJob og
```

## <a name="additional-references"></a>Weitere Verweise

[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)&reg;'    