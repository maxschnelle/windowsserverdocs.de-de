---
title: bitadmin gethelperflkenflags
description: Windows-Befehls Thema für **BITSAdmin gethelpertokenflags**, das die nutzungsflags für ein Hilfsobjekt zurückgibt, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 37e40ea1f71795e0c975988169577deb205c3335
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850663"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitadmin gethelperflkenflags

Gibt die nutzungsflags für ein [Hilfsobjekt](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) zurück, das einem Bits-Übertragungs Auftrag zugeordnet ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Hinweise

Mögliche Rückgabewerte, einschließlich:

- **0x0001.** Das Hilfsobjekt dient zum Öffnen der lokalen Datei eines uploadauftrags, zum Erstellen oder Umbenennen der temporären Datei eines Download Auftrags oder zum Erstellen oder Umbenennen der Antwortdatei eines Upload-Antwort-Auftrags.

- **0x0002.** Das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block-Uploads (SMB) oder eines Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy-Abfrage für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen/SetCredentialsJob targetscheme NULL NULL aufrufen, um zuzulassen, dass die Anmelde Informationen über HTTP gesendet werden.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
