---
title: nslookup root
description: Referenz Thema für den nslookup-Stamm Befehl, mit dem der Standard Server für den Stamm des Domänen Namespace der Domain Name System (DNS) auf den Server geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f1f2bbe3b71660d079a0b7c87f5be487e0ff437
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721653"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set root](nslookup-set-root.md)
