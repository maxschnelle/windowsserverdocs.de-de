---
title: manage-bde forcerecovery
description: Referenz Thema für den Befehl manage-bde forcerecovery, der beim Neustart ein durch BitLocker geschütztes Laufwerk in den Wiederherstellungs Modus erzwingt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e152a18137925bd197e672531ccef47e7b2a7119
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222892"
---
# <a name="manage-bde-forcerecovery"></a>manage-bde forcerecovery

Erzwingt ein durch BitLocker geschütztes Laufwerk beim Neustart in den Wiederherstellungs Modus. Dieser Befehl löscht alle Trusted Platform Module (TPM)-bezogenen Schlüssel Schutzvorrichtungen vom Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungs Kennwort oder ein Wiederherstellungs Schlüssel verwendet werden, um das Laufwerk zu entsperren.

## <a name="syntax"></a>Syntax

```
manage-bde –forcerecovery <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Um BitLocker im Wiederherstellungs Modus auf Laufwerk C zu starten, geben Sie Folgendes ein:

```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
