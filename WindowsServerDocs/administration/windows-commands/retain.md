---
title: Erhalten
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 891192c0d6b1687cf6bffea0f57d1853e023b776
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835763"
---
# <a name="retain"></a>Erhalten



Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Hinweise

-   Auf einem dynamischen Datenträger mit Master Boot Record (MBR) erstellt dieser Befehl einen Partitionseintrag im Master Boot Record.
-   Bei einem dynamischen GPT-Datenträger (GUID-Partitionstabelle) erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="additional-references"></a>Weitere Verweise

