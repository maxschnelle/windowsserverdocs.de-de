---
title: nslookup root
description: Referenz Artikel für den nslookup-Stamm Befehl, der den Standard Server auf den Server für den Stamm des Domänen Namespace der Domain Name System (DNS) ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 07dbfcf401314145cb0e7553d71480072da4b574
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936286"
---
# <a name="nslookup-root"></a>nslookup root

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server für den Stamm Domain Name System des DNS-Domänen Namen-Speicherplatzes auf den Server. Derzeit wird der NS.nic.DDN.mil Nameserver verwendet. Sie können den Namen des Stamm Servers mithilfe des Befehls [nslookup Set root](nslookup-set-root.md) ändern.

> [!NOTE]
> Dieser Befehl ist mit identisch `lserver ns.nic.ddn.mil` .

## <a name="syntax"></a>Syntax

```
root
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set root](nslookup-set-root.md)
