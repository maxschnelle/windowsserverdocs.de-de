---
title: bitsadmin gethelpertokenflags
description: Referenz Thema für den BITSAdmin gethelpertokenflags-Befehl, der die nutzungsflags für ein Hilfsobjekt zurückgibt, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 23e93ca71915fc369a940a21ce856b14deced004
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717908"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

Gibt die nutzungsflags für ein Hilfsobjekt [helper token](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) zurück, das einem Bits-Übertragungs Auftrag zugeordnet ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

### <a name="remarks"></a>Bemerkungen

Mögliche Rückgabewerte, einschließlich:

- **0x0001.** Das Hilfsobjekt dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.

- **0x0002.** Das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block-Uploads (SMB) oder eines Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy-Abfrage für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen anrufen `/SetCredentialsJob TargetScheme NULL NULL` , um zuzulassen, dass die Anmelde Informationen über HTTP gesendet werden.
  
## <a name="examples"></a>Beispiele

So rufen Sie die nutzungsflags für ein Hilfstoken ab, das einem Bits-Übertragungs Auftrag mit dem Namen *mydownloadjob*zugeordnet ist

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
