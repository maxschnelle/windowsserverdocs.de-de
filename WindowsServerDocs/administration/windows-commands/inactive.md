---
title: inactive
description: Referenz Artikel für den inaktiven Befehl, der die Systempartition oder Start Partition mit dem Fokus als inaktiv auf grundlegenden Master Boot Record (MBR) kennzeichnet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7e9679dee2bb8a75da14e1d7ee6c75b80bb1ef1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957132"
---
# <a name="inactive"></a>inactive

Markiert die Systempartition oder Start Partition, deren Fokus auf grundlegenden Master Boot Record-Datenträgern (MBR) liegt.

Ein aktives System oder eine Start Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl [Partitions Befehl auswählen](select-partition.md) die aktive Partition aus, und verschieben Sie den Fokus auf die Partition.

> [!CAUTION]
> Ihr Computer wird möglicherweise nicht ohne eine aktive Partition gestartet. Markieren Sie ein System oder eine Start Partition nur dann als inaktiv, wenn Sie ein erfahrener Benutzer sind, der über ein umfassendes Verständnis der Windows-Betriebssystem Familie verfügt.<p>Wenn Sie den Computer nicht starten können, nachdem Sie das System oder die Start Partition als inaktiv gekennzeichnet haben, legen Sie die Windows Setup CD in das CD-ROM-Laufwerk ein, starten Sie den Computer neu, und reparieren Sie dann die Partition mithilfe der Befehle **fixmbr** und **fixboot** in der Wiederherstellungskonsole.
>
> Nachdem Sie die Systempartition oder Start Partition als inaktiv markiert haben, startet der Computer mit der nächsten im BIOS angegebenen Option, z. b. dem CD-ROM-Laufwerk oder einer Pre-Boot Execution Environment (PXE).

## <a name="syntax"></a>Syntax

```
inactive
```

### <a name="examples"></a>Beispiele

```
inactive
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Partitions Befehl auswählen](select-partition.md)

- [Erweiterte Problembehandlung für Windows-Startprobleme](/windows/client-management/advanced-troubleshooting-boot-problems)
