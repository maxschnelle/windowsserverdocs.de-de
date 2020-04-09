---
title: bitsadmin getnotifyflags
description: Windows-Befehls Thema für **bitadmin getnotifyflags**, das die Benachrichtigungs Flags für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3138baea05f793cfb587d3f8fb669d446daea6b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850583"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

Ruft die Benachrichtigungs Flags für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Hinweise

Der Auftrag kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten:

| Flag | Beschreibung |
| ----- | ----- |
| 0x001 | Generiert ein Ereignis, wenn alle Dateien im Auftrag übertragen wurden. |
| 0x002 | Generiert ein Ereignis, wenn ein Fehler auftritt. |
| 0x004 | Deaktivieren Sie Benachrichtigungen. |
| 0x008 | Generieren Sie ein Ereignis, wenn der Auftrag geändert oder der Übertragungs Fortschritt durchgeführt wird. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Benachrichtigungs Flags für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)