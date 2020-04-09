---
title: Detail Festplatte
description: Windows-Befehls Thema für Detail Datenträger, der die Eigenschaften des ausgewählten Datenträgers und die Volumes auf diesem Datenträger anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d0768d45c0f56ba549ff54064c4e74ae3048e41
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846453"
---
# <a name="detail-disk"></a>Detail Festplatte

Zeigt die Eigenschaften des ausgewählten Datenträgers und der Volumes auf dem Datenträger an.

## <a name="syntax"></a>Syntax

```
detail disk
```

## <a name="remarks"></a>Hinweise

-   Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.
-   Wenn es sich bei der ausgewählten Festplatte um eine virtuelle Festplatte (VHD) handelt, meldet der **Detail** Datenträger den Bustyp des Datenträgers als virtuell

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Eigenschaften des ausgewählten Datenträgers und Informationen zu den Volumes auf dem Datenträger anzuzeigen:
```
detail disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

