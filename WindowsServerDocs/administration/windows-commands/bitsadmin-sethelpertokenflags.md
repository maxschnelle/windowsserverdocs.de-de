---
title: bitsadmin sethelpertokenflags
description: Referenz Artikel zum Befehl "BITSAdmin sethelpertokenflags", mit dem die nutzungsflags für ein Hilfsobjekt festgelegt werden, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: d5fc4c1d78fdf7ea6a6bb67cf435c8e71d5a9cbc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927770"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

Legt die nutzungsflags für ein [Hilfsobjekt](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)fest   , das einem Bits-Übertragungs Auftrag zugeordnet ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| flags | Mögliche hilfstokenwerte, einschließlich:<ul><li>**0x0001.** Dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.</li><li>**0x0002.** Wird verwendet, um die Remote Datei eines Server Message Block-Uploads (SMB) zum Hochladen oder herunterladen oder als Reaktion auf eine HTTP-Server-oder Proxy Aufforderung für implizite NTLM-oder Kerberos-Anmelde Informationen zu öffnen.</li></ul>Sie müssen anrufen  `/setcredentialsjob targetscheme null null`   , um die Anmelde Informationen über HTTP zu senden. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
