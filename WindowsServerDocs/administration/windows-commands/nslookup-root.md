---
title: nslookup root
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 3eb3375df3a109685fc8dc5d23f0c5008339d09e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373388"
---
# <a name="nslookup-root"></a>nslookup root

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Standard Server für den Stamm Domain Name System des DNS-Domänen Namen-Speicherplatzes auf den Server.
## <a name="syntax"></a>Syntax
```
root 
```
## <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
| {Help &#124; ?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Hinweise
- Derzeit wird der NS.nic.DDN.mil Nameserver verwendet. Dieser Befehl ist ein Synonym für lserver NS.nic.DDN.mil. Sie können den Namen des Stamm Servers mit dem Befehl " **root festlegen** " ändern.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup](nslookup-set-root.md) -Stammgruppe
