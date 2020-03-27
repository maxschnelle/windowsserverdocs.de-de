---
title: Auswählen eines BranchCache-Entwurfs
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca605589d28811f96296f2ff865e8ae6923304c3
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319116"
---
# <a name="choosing-a-branchcache-design"></a>Auswählen eines BranchCache-Entwurfs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die BranchCache-Modi und die Auswahl der besten Modi für die Bereitstellung.  
  
Sie können dieses Handbuch verwenden, um BranchCache in den folgenden Modi und im Modus bereitzustellen.  
  
-   Alle Zweigstellen sind für den Modus "verteilter Cache" konfiguriert.  
  
-   Alle Zweigstellen sind für den gehosteten Cache Modus konfiguriert und verfügen über einen gehosteten Cache Server an einem Standort.  
  
-   Einige Zweigstellen sind für den Modus "verteilter Cache" konfiguriert, und einige Zweigstellen verfügen über einen gehosteten Cache Server an einem Standort und sind für den gehosteten Cache Modus konfiguriert.  
  
In der folgenden Abbildung wird eine Installation im Dual-Modus dargestellt, wobei eine Zweigstelle für den Modus für verteilte Caches und eine für den Modus für gehostete Caches konfigurierte Zweigstellen  
  
![Auswählen eines BranchCache-Entwurfs](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
Wählen Sie vor der Bereitstellung von BranchCache den gewünschten Modus für jede Zweigstelle in Ihrer Organisation aus.  
  


