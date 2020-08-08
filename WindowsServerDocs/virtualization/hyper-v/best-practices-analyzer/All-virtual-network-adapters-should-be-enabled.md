---
title: Alle virtuellen Netzwerkadapter sollten aktiviert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 286a0dc099eb6350fe7f5adef925a2d38d99a3ca
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946096"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>Alle virtuellen Netzwerkadapter sollten aktiviert sein.

>Gilt für: Windows Server 2016



|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Mindestens ein virtueller Netzwerkadapter, der einem physischen Netzwerkadapter zugeordnet ist, wird im Verwaltungs Betriebssystem deaktiviert.*

## <a name="impact"></a>Auswirkung

*Die Konfiguration dieses Servers ist nicht optimal.*

Das Verwaltungs Betriebssystem kann keine Verbindung mit einem physischen (externen) Netzwerk über einen der physischen Netzwerkadapter auf diesem Computer herstellen, da er einem deaktivierten virtuellen Netzwerkadapter zugeordnet ist.

## <a name="resolution"></a>Lösung

*Verwenden Sie die Netzwerk-& Internet Einstellungen, um den virtuellen Netzwerkadapter zu aktivieren. Alternativ können Sie mit dem Manager für virtuelle Switches den externen virtuellen Switch so konfigurieren, dass er nicht mit dem Verwaltungs Betriebssystem gemeinsam verwendet wird.*



