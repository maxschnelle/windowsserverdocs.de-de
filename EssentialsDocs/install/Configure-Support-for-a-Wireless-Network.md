---
title: "Konfigurieren der Unterstützung für ein Drahtlosnetzwerk"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d7020d4-fd46-4858-a406-de5c0f21ea06
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c5c98727b81bf37fdb3f90c612270462a51908c8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-support-for-a-wireless-network"></a>Konfigurieren der Unterstützung für ein Drahtlosnetzwerk

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können das Betriebssystem zur Unterstützung eines Funknetzwerks konfigurieren. Die folgenden Anforderungen müssen erfüllt sein, um Unterstützung für Funknetzwerke auf dem Server zu aktivieren:  
  
-   Der Server muss einen Adapter für Kabelnetzwerke installiert haben.  
  
-   Wenn der Netzwerkadapter vom Betriebssystem nicht unterstützt wird, muss die richtige Treiber für den Drahtlosnetzwerkadapter vorinstalliert werden.  
  
-   Die Möglichkeit zum Aktivieren und deaktivieren den Adapter muss zur Verfügung gestellt. Methoden für die auf diese Weise können eine physische Taste auf dem Server oder eine benutzerdefinierte Benutzeroberfläche im Dashboard enthalten. Das Produkthandbuch sollte die Schritte zum Aktivieren und deaktivieren den Adapter enthalten.  
  
-   Die Möglichkeit, ein Funknetzwerk auszuwählen und eine Verbindung herstellen, muss zur Verfügung gestellt. Dies sollte erfolgen, indem Sie eine benutzerdefinierte Benutzeroberfläche im Dashboard hinzufügen. Im Produkthandbuch sollten die Schritte zum auswählen und Herstellen einer Verbindung mit einem drahtlosen Netzwerk bereitstellen.  
  
-   Wenn die Unterstützung für eine drahtlose Ad-hoc-Netzwerk erforderlich ist, muss eine erweiterte Benutzeroberfläche im Dashboard bereitgestellt werden. Die Benutzeroberfläche möglich, eine Schaltfläche oder einen Link, der das Einrichten eines drahtlosen Ad-hoc-Netzwerk-Assistenten in der Systemsteuerung in Windows Server 2008 R2 gestartet wird.  
  
## <a name="additional-considerations"></a>Weitere Überlegungen  
 Die folgende Informationen sollten ebenfalls berücksichtigt werden, wenn Sie Unterstützung für ein drahtloses Netzwerk konfigurieren:  
  
-   Der Server muss über ein Kabel zum Ausführen von Setup mit dem Netzwerk verbunden sein.  
  
-   Ein Netzwerkcomputer, auf dem eine bare-Metal-Recovery ausgeführt wird, muss über ein Kabel mit dem Netzwerk verbunden werden.  
  
-   Der Server muss über ein Kabel eine bare-Metal-Wiederherstellung des Servers mit dem Netzwerk verbunden sein.  
  
-   Wenn ein Ad-hoc-Netzwerk auf dem Server erstellt wird, ist den Adapter für das Ad-hoc-Netzwerk vorgesehen, damit der Benutzer immer das Netzwerkkabel in den Server erhalten Sie eine Internetverbindung schließen muss.  
  
> [!NOTE]
>  Weitere Informationen zum Konfigurieren von Netzwerkverbindungen finden Sie unter [Vorkonfigurieren eines Routers](Preconfiguring-a-Router.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)