---
title: nslookup root
description: Referenz Artikel für den nslookup-Stamm Befehl, der den Standard Server auf den Server für den Stamm des Domänen Namespace der Domain Name System (DNS) ändert.
ms.topic: reference
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e3dbbdf970143ce1e82f0c817fc1f53c5b22749
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635655"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set root](nslookup-set-root.md)
