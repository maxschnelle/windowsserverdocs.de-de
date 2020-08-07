---
title: Auswählen eines BranchCache-Entwurfs
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f64d27f3ef36c587e2ec5c08f51723942ba6a28c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937509"
---
# <a name="choosing-a-branchcache-design"></a>Auswählen eines BranchCache-Entwurfs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie mehr über die BranchCache-Modi und die Auswahl der besten Modi für die Bereitstellung.

Sie können dieses Handbuch verwenden, um BranchCache in den folgenden Modi und im Modus bereitzustellen.

-   Alle Zweigstellen sind für den Modus "verteilter Cache" konfiguriert.

-   Alle Zweigstellen sind für den gehosteten Cache Modus konfiguriert und verfügen über einen gehosteten Cache Server an einem Standort.

-   Einige Zweigstellen sind für den Modus "verteilter Cache" konfiguriert, und einige Zweigstellen verfügen über einen gehosteten Cache Server an einem Standort und sind für den gehosteten Cache Modus konfiguriert.

In der folgenden Abbildung wird eine Installation im Dual-Modus dargestellt, wobei eine Zweigstelle für den Modus für verteilte Caches und eine für den Modus für gehostete Caches konfigurierte Zweigstellen

![Auswählen eines BranchCache-Entwurfs](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)

Wählen Sie vor der Bereitstellung von BranchCache den gewünschten Modus für jede Zweigstelle in Ihrer Organisation aus.



