---
title: Auswählen eines BranchCache-Entwurfs
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 330dcbee26f52ff69cd85ef8dc78d2e161b943d1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811911"
---
# <a name="choosing-a-branchcache-design"></a>Auswählen eines BranchCache-Entwurfs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema können Informationen zu BranchCache-Modi und die beste Modi für die Bereitstellung auswählen.  
  
Sie können dieses Handbuch zum Bereitstellen von BranchCache in der folgenden Modi und sicherheitsmoduskombinationen verwenden.  
  
-   Alle Zweigstellen sind für Modus "verteilter Cache" konfiguriert.  
  
-   Alle Zweigstellen für Modus "gehosteter Cache" konfiguriert sind und über einen gehosteten Cacheserver für Website verfügen.  
  
-   Einigen Zweigstellen für Modus "verteilter Cache" konfiguriert sind, und einigen Zweigstellen über einen gehosteten Cacheserver für Website und für den Modus "gehosteter Cache" konfiguriert sind.  
  
Die folgende Abbildung zeigt eine dual-Modus-Installation mit einer Zweigstelle, die für den Modus "verteilter Cache" konfiguriert und eine Filiale, die für den Modus "gehosteter Cache" konfiguriert.  
  
![Auswählen eines BranchCache-Entwurfs](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
Bevor Sie BranchCache bereitgestellt haben, wählen Sie den Modus, die, den Sie für jede Zweigstelle in Ihrer Organisation zu bevorzugen.  
  


