---
title: Detail Festplatte
description: Referenz Thema für Detail Datenträger, auf dem die Eigenschaften des ausgewählten Datenträgers und die Volumes auf diesem Datenträger angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a746506d6c9609e3214dbd48e5fa91f52d16ab4d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710520"
---
# <a name="detail-disk"></a>Detail Festplatte

Zeigt die Eigenschaften des ausgewählten Datenträgers und der Volumes auf dem Datenträger an.

## <a name="syntax"></a>Syntax

```
detail disk
```

## <a name="remarks"></a>Bemerkungen

-   Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.
-   Wenn es sich bei der ausgewählten Festplatte um eine virtuelle Festplatte (VHD) handelt, meldet der **Detail** Datenträger den Bustyp des Datenträgers als virtuell

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Eigenschaften des ausgewählten Datenträgers und Informationen zu den Volumes auf dem Datenträger anzuzeigen:
```
detail disk
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

