---
title: bitsadmin sethelpertokenflags
description: Referenz Artikel zum Befehl "BITSAdmin sethelpertokenflags", mit dem die nutzungsflags für ein Hilfsobjekt festgelegt werden, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 1d3fee2b69ba498e3eae771b4be42848b1d88065
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893127"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

Legt die nutzungsflags für ein [Hilfsobjekt](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)fest   , das einem Bits-Übertragungs Auftrag zugeordnet ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| flags | Mögliche hilfstokenwerte, einschließlich:<ul><li>**0x0001.** Dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.</li><li>**0x0002.** Wird verwendet, um die Remote Datei eines Server Message Block-Uploads (SMB) zum Hochladen oder herunterladen oder als Reaktion auf eine HTTP-Server-oder Proxy Aufforderung für implizite NTLM-oder Kerberos-Anmelde Informationen zu öffnen.</li></ul>Sie müssen anrufen  `/setcredentialsjob targetscheme null null`   , um die Anmelde Informationen über HTTP zu senden. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
