---
title: nslookup root
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47a26be99a5eee510970d3eee6b486331a98b159
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436905"
---
# <a name="nslookup-root"></a>nslookup root

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Standardserver an den Server für den Stamm des Domänennamespace Domain Name System (DNS).
## <a name="syntax"></a>Syntax
```
root 
```
## <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
| {help &#124; ?} | Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle. |

## <a name="remarks"></a>Hinweise
- Derzeit wird die Namenserver "NS.NIC.ddn.mil" verwendet. Dieser Befehl ist ein Synonym für Lserver ns.nic.ddn.mil. Sie können den Namen des Servers mit Stamm Ändern der **Satz Stamm** Befehl.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Nslookup Stamm festlegen](nslookup-set-root.md)
