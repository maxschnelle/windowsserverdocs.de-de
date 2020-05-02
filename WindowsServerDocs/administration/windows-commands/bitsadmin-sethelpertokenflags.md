---
title: bitsadmin sethelpertokenflags
description: Referenz Thema für den BITSAdmin sethelpertokenflags-Befehl, mit dem die nutzungsflags für ein Hilfsobjekt festgelegt werden, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2bb93664d88c0f346e2926102f97287ac8fc35de
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719371"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

Legt die nutzungsflags für ein Hilfsobjekt [helper token](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) fest, das einem Bits-Übertragungs Auftrag zugeordnet ist.

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
| flags | Mögliche hilfstokenwerte, einschließlich:<ul><li>**0x0001.** Dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.</li><li>**0x0002.** Wird verwendet, um die Remote Datei eines Server Message Block-Uploads (SMB) zum Hochladen oder herunterladen oder als Reaktion auf eine HTTP-Server-oder Proxy Aufforderung für implizite NTLM-oder Kerberos-Anmelde Informationen zu öffnen.</li></ul>Sie müssen anrufen `/setcredentialsjob targetscheme null null` , um die Anmelde Informationen über HTTP zu senden. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
