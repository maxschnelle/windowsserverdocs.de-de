---
title: inactive
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38a4f731bef9515a387b0343eaf4cb06142e6620
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842123"
---
# <a name="inactive"></a>inactive



In den MBR-Datenträgern (Basic Master Boot Record) kennzeichnet die Systempartition oder Start Partition mit dem Fokus als inaktiv.

## <a name="syntax"></a>Syntax

```
inactive
```

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Ihr Computer wird möglicherweise nicht ohne eine aktive Partition gestartet. Markieren Sie ein System oder eine Start Partition nur dann als inaktiv, wenn Sie ein erfahrener Benutzer sind, der über ein umfassendes Verständnis der Windows-Betriebssystem Familie verfügt.</br>> Wenn Sie den Computer nicht starten können, nachdem Sie das System oder die Start Partition als inaktiv gekennzeichnet haben, legen Sie die Windows Setup-CD in das CD-ROM-Laufwerk ein, starten Sie den Computer neu, und reparieren Sie dann die Partition mithilfe der Befehle **fixmbr** und **fixboot** in der Wiederherstellungskonsole.
> -   Nachdem Sie die Systempartition oder Start Partition als inaktiv markiert haben, startet der Computer mit der nächsten im BIOS angegebenen Option, z. b. dem CD-ROM-Laufwerk oder einer Pre-Boot Execution Environment (PXE).
> -   Ein aktives System oder eine Start Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Partition auswählen** die aktive Partition aus, und verschieben Sie den Fokus auf die Partition.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

```
inactive
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

