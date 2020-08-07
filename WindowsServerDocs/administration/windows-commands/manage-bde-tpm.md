---
title: manage-bde TPM
description: Referenz Artikel für den Befehl manage-bde TPM, der die Trusted Platform Module des Computers (TPM) konfiguriert.
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5a41ccff889fc729ce812523d64b9404378d32c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886657"
---
# <a name="manage-bde-tpm"></a>manage-bde TPM

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert den Trusted Platform Module des Computers (TPM).

## <a name="syntax"></a>Syntax

```
manage-bde -tpm [-turnon] [-takeownership <ownerpassword>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -turnon | Aktiviert und aktiviert das TPM, sodass das TPM-Besitzer Kennwort festgelegt werden kann. Sie können auch **-t** als abgekürzte Version dieses Befehls verwenden. |
| -Take Ownership | Übernimmt den Besitz des TPM durch Festlegen eines Besitzer Kennworts. Sie können **-o** auch als abgekürzte Version dieses Befehls verwenden. |
| `<ownerpassword>` | Stellt das Besitzer Kennwort dar, das Sie für das TPM angeben. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das TPM zu aktivieren:

```
manage-bde  tpm -turnon
```

Um den Besitz des TPM zu übernehmen und das Besitzer Kennwort auf festzulegen, geben Sie Folgendes ein *0wnerP@ss* :

```
manage-bde  tpm  takeownership 0wnerP@ss
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [TPM-Verwaltungs-Cmdlets für Windows PowerShell](/powershell/module/trustedplatformmodule/)

- [Befehl "Manage-BDE"](manage-bde.md)
