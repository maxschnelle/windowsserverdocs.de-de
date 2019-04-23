---
title: nslookup server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52a846b1084380d0b40d58d81c11d20dacb407bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869151"
---
# <a name="nslookup-server"></a>nslookup server

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Standardserver an der angegebenen Domäne von Domain Name System (DNS).
## <a name="syntax"></a>Syntax
```
server <DNSDomain>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<DNSDomain>|Erforderlich. Gibt die neue DNS-Domäne für den Standardserver an.|
|{help &#124; ?}|Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.|
## <a name="remarks"></a>Hinweise
-   Die **Server** Befehl verwendet den aktuellen Server, um die Informationen über die angegebenen DNS-Domäne zu suchen. Dies ist im Gegensatz zu den **Lserver** -Befehl, der den ersten Server verwendet.
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Nslookup Lserver](nslookup-lserver.md)
