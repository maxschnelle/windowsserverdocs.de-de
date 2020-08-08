---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms:topic: include
ms.openlocfilehash: f07840220dbbe955a47879b3090ddd340c8c514f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952834"
---
Mit Dynamic werden ausgehende Lasten basierend auf einem Hash der TCP-Ports und IP-Adressen verteilt. Der dynamische Modus gleicht Ladevorgänge auch in Echtzeit aus, sodass ein angegebener ausgehender Flow zwischen den Teammitgliedern hin und her verschoben werden kann. Eingehende Lasten werden hingegen auf die gleiche Weise wie der Hyper-V-Port verteilt. Kurz gesagt, verwendet der dynamische Modus die besten Aspekte von Address Hash und Hyper-V-Port und ist der Lasten Ausgleichs Modus mit der höchsten Leistung.

