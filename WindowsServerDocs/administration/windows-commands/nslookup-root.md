---
title: nslookup root
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d11179ff3cd22acd9df67261e7ab752aa159201a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838643"
---
# <a name="nslookup-root"></a>nslookup root

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Standard Server für den Stamm Domain Name System des DNS-Domänen Namen-Speicherplatzes auf den Server.
## <a name="syntax"></a>Syntax
```
root 
```
### <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
| {Help &#124; ?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Hinweise
- Derzeit wird der NS.nic.DDN.mil Nameserver verwendet. Dieser Befehl ist ein Synonym für lserver NS.nic.DDN.mil. Sie können den Namen des Stamm Servers mit dem Befehl " **root festlegen** " ändern.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup](nslookup-set-root.md) -Stammgruppe
