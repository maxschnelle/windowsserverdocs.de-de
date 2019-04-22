---
title: Bitsadmin sethelpertokenflags
description: Windows-Befehle Thema **Bitsadmin Sethelpertokenflags** -legt die Usage-Flags für ein Hilfsprogramm-Token, das einen BITS-Übertragungsauftrag zugeordnet ist.
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
ms.openlocfilehash: cc9652afe73476041aa42e64671885bfc1af9628
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813861"
---
# <a name="bitsadmin-sethelpertokenflags"></a>Bitsadmin sethelpertokenflags

Legt die Usage-Flags für eine [Helper-Token](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) , einen BITS-Übertragungsauftrag zugeordnet ist.

**BITS 3.0 und früheren**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Auftrags Anzeigenamen oder die GUID.|
|Flags|Mögliche Werte sind die folgenden. 0 x 0001&mdash;das Hilfsprogramm-Token wird verwendet, zum Öffnen der lokalen Datei von einem Uploadauftrag, zum Erstellen oder benennen Sie die temporäre Datei eines Auftrags herunterladen oder zum Erstellen oder benennen Sie die Antwortdatei von einem Upload-Antwort-Auftrag. 0 x 0002&mdash;der Hilfsprogramm-Token wird verwendet, um die remote-Datei über einen Upload von Server Message Block (SMB) zu öffnen oder Downloadauftrag oder als Reaktion auf eine HTTP-Server oder Proxy-Herausforderung, für die implizite NTLM oder Kerberos-Anmeldeinformationen. Rufen Sie `/SetCredentialsJob TargetScheme NULL NULL` können die Anmeldeinformationen, die über HTTP gesendet werden.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
