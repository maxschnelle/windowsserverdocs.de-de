---
title: bitadmin gethelperflkenflags
description: 'Windows-Befehls Thema für **BITSAdmin gethelpertokenflags** : gibt die nutzungsflags für ein Hilfsobjekt zurück, das einem Bits-Übertragungs Auftrag zugeordnet ist.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 25d667736d5fdcd018f557b2a5565b94898f6e51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381570"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitadmin gethelperflkenflags

Gibt die nutzungsflags für ein [Hilfsobjekt](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) zurück, das einem Bits-Übertragungs Auftrag zugeordnet ist.

**Bits 3,0 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Folgende Rückgabewerte sind möglich:

- 0x0001. Das Hilfsobjekt dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.
- 0x0002. Das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block-Uploads (SMB) oder eines Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy-Abfrage für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen/SetCredentialsJob targetscheme NULL NULL aufrufen, um zuzulassen, dass die Anmelde Informationen über HTTP gesendet werden.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
