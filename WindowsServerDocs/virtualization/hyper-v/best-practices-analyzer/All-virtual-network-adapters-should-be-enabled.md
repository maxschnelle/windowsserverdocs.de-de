---
title: Alle virtuellen Netzwerkadapter sollten aktiviert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
ms.date: 8/16/2016
ms.openlocfilehash: 48417108f780c8b145613b110bb51681bd69bdc6
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746305"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>Alle virtuellen Netzwerkadapter sollten aktiviert sein.

>Gilt für: Windows Server 2016



|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Mindestens ein virtueller Netzwerkadapter, der einem physischen Netzwerkadapter zugeordnet ist, wird im Verwaltungs Betriebssystem deaktiviert.*

## <a name="impact"></a>Auswirkung

*Die Konfiguration dieses Servers ist nicht optimal.*

Das Verwaltungs Betriebssystem kann keine Verbindung mit einem physischen (externen) Netzwerk über einen der physischen Netzwerkadapter auf diesem Computer herstellen, da er einem deaktivierten virtuellen Netzwerkadapter zugeordnet ist.

## <a name="resolution"></a>Lösung

*Verwenden Sie die Netzwerk-& Internet Einstellungen, um den virtuellen Netzwerkadapter zu aktivieren. Alternativ können Sie mit dem Manager für virtuelle Switches den externen virtuellen Switch so konfigurieren, dass er nicht mit dem Verwaltungs Betriebssystem gemeinsam verwendet wird.*



