---
title: inactive
description: Referenz Thema für den inaktiven Befehl, der die Systempartition oder Start Partition mit dem Fokus auf grundlegenden Master Boot Record-Datenträgern (MBR) als inaktiv markiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9861a54c284002e53b0a8fc354aa883d80fff0e7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818440"
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

- [Erweiterte Problembehandlung für Windows-Startprobleme](https://docs.microsoft.com/windows/client-management/advanced-troubleshooting-boot-problems)
