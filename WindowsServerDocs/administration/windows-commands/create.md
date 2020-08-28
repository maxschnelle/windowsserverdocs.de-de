---
title: create
description: Referenz Artikel für den CREATE-Befehl, mit dem eine Partition oder eine Schatten Partition auf einem Datenträger, ein Volume auf einem oder mehreren Datenträgern oder eine virtuelle Festplatte (VHD) erstellt wird.
ms.topic: reference
ms.assetid: b45acde1-8f4f-4ec3-b905-d8188f884af8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0aefdccf2a9d2a560ce95cd7224a940beec51f7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033068"
---
# <a name="create"></a>create

Erstellt eine Partition oder einen Schatten auf einem Datenträger, einem Volume auf einem oder mehreren Datenträgern oder einer virtuellen Festplatte (VHD). Wenn Sie diesen Befehl verwenden, um ein Volume auf dem Schatten Datenträger zu erstellen, müssen Sie bereits über mindestens ein Volume im Schattenkopiesatz verfügen.

## <a name="syntax"></a>Syntax

```
create partition
create volume
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| [create partition primary-Befehl](create-partition-primary.md) | Erstellt eine primäre Partition auf dem Basis Datenträger mit dem Fokus. |
| [Create Partition (EFI-Befehl)](create-partition-efi.md) | Erstellt eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) auf Itanium-basierten Computern. |
| [Befehl "erweiterte Partition erstellen"](create-partition-extended.md) | Erstellt eine erweiterte Partition auf dem Datenträger mit dem Fokus. |
| [Create Partition (logischer Befehl)](create-partition-logical.md) | Erstellt eine logische Partition in einer vorhandenen erweiterten Partition. |
| [Create Partition (MSR-Befehl)](create-partition-msr.md) | Erstellt eine reservierte Microsoft-Partition (MSR) auf einem GPT-Datenträger (GUID-Partitionstabelle). |
| [Create Volume Simple-Befehl](create-volume-simple.md) | Erstellt ein einfaches Volume auf dem angegebenen dynamischen Datenträger. |
| [volumespiegelungs-Befehl erstellen](create-volume-mirror.md) | Erstellt eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger. |
| [Create Volume-RAID-Befehl](create-volume-raid.md) | Erstellt ein RAID-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern. |
| [Create Volume Stripe-Befehl](create-volume-stripe.md) | Erstellt ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
