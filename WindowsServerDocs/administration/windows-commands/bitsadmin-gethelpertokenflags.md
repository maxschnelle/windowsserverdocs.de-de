---
title: bitsadmin gethelpertokenflags
description: Referenz Artikel für den BITSAdmin gethelpertokenflags-Befehl, der die nutzungsflags für ein Hilfsobjekt zurückgibt, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: d49a2aef829b3e443ad5e1fd3e70d8c260f59ec8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894243"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

Gibt die nutzungsflags für ein [Hilfsobjekt](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)zurück   , das einem Bits-Übertragungs Auftrag zugeordnet ist.

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

- **0x0002.** Das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block-Uploads (SMB) oder eines Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy-Abfrage für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen anrufen  `/SetCredentialsJob TargetScheme NULL NULL`   , um zuzulassen, dass die Anmelde Informationen über HTTP gesendet werden.

## <a name="examples"></a>Beispiele

So rufen Sie die nutzungsflags für ein Hilfstoken ab, das einem Bits-Übertragungs Auftrag mit dem Namen *mydownloadjob*zugeordnet ist

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
