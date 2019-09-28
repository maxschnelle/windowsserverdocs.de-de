---
title: VSTE
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ce91b6a024c165e3aa63148b9ad6dfcc4db7a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375375"
---
# <a name="inactive"></a>VSTE



In den MBR-Datenträgern (Basic Master Boot Record) kennzeichnet die Systempartition oder Start Partition mit dem Fokus als inaktiv.

## <a name="syntax"></a>Syntax

```
inactive
```

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Ihr Computer wird möglicherweise nicht ohne eine aktive Partition gestartet. Markieren Sie ein System oder eine Start Partition nur dann als inaktiv, wenn Sie ein erfahrener Benutzer sind, der über ein umfassendes Verständnis der Windows-Betriebssystem Familie verfügt.</br>> Wenn Sie den Computer nicht starten können, nachdem Sie das System oder die Start Partition als inaktiv gekennzeichnet haben, legen Sie die Windows Setup CD in das CD-ROM-Laufwerk ein, starten Sie den Computer neu, und reparieren Sie dann die Partition mithilfe der Befehle **fixmbr** und **fixboot** im Wiederherstellungskonsole.
> -   Nachdem Sie die Systempartition oder Start Partition als inaktiv markiert haben, startet der Computer mit der nächsten im BIOS angegebenen Option, z. b. dem CD-ROM-Laufwerk oder einer Pre-Boot Execution Environment (PXE).
> -   Ein aktives System oder eine Start Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Partition auswählen** die aktive Partition aus, und verschieben Sie den Fokus auf die Partition.

## <a name="BKMK_examples"></a>Beispiele

```
inactive
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

