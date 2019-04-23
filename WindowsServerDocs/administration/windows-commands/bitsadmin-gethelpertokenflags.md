---
title: Bitsadmin gethelpertokenflags
description: Windows-Befehle Thema **Bitsadmin Gethelpertokenflags** -gibt die Optionen für die Verwendung für ein Hilfsprogramm-Token, das einen BITS-Übertragungsauftrag zugeordnet ist.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: e5665ed4670891dcbecd56215342f3d94e1ed753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885791"
---
# <a name="bitsadmin-gethelpertokenflags"></a>Bitsadmin gethelpertokenflags

Gibt die Optionen für die Nutzung für eine [Helper-Token](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) , einen BITS-Übertragungsauftrag zugeordnet ist.

**BITS 3.0 und früheren**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Folgende: Mögliche Rückgabewerte

- 0x0001. Das Hilfsprogramm-Token wird verwendet, um die lokale Datei von einem Uploadauftrag, zum Erstellen oder benennen Sie die temporäre Datei eines Auftrags herunterladen oder zum Erstellen und benennen Sie die Antwortdatei von einem Upload-Antwort-Auftrag zu öffnen.
- 0x0002. Das Hilfsprogramm-Token wird verwendet, um die remote-Datei über einen Upload von Server Message Block (SMB) zu öffnen oder Downloadauftrag oder als Reaktion auf eine HTTP-Server oder Proxy-Herausforderung, für die implizite NTLM oder Kerberos-Anmeldeinformationen. Sie müssen SetCredentialsJob TargetScheme NULL NULL an, um die Anmeldeinformationen, die über HTTP gesendet werden können aufrufen.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
