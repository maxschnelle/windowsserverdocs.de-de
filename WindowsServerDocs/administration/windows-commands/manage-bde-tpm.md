---
title: manage-bde TPM
description: Referenz Thema für den Befehl manage-bde TPM, mit dem die Trusted Platform Module des Computers (TPM) konfiguriert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3aa597dbd871c64efc7e718ef70ed0c69b256ab9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222143"
---
# <a name="manage-bde-tpm"></a>manage-bde TPM

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert den Trusted Platform Module des Computers (TPM).

## <a name="syntax"></a>Syntax

```
manage-bde -tpm [-turnon] [-takeownership <ownerpassword>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -turnon | Aktiviert und aktiviert das TPM, sodass das TPM-Besitzer Kennwort festgelegt werden kann. Sie können auch **-t** als abgekürzte Version dieses Befehls verwenden. |
| -Take Ownership | Übernimmt den Besitz des TPM durch Festlegen eines Besitzer Kennworts. Sie können **-o** auch als abgekürzte Version dieses Befehls verwenden. |
| `<ownerpassword>` | Stellt das Besitzer Kennwort dar, das Sie für das TPM angeben. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [TPM-Verwaltungs-Cmdlets für Windows PowerShell](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)

- [Befehl "Manage-BDE"](manage-bde.md)
