---
title: Vorkonfigurieren eines Routers
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7dc66c8a439552c2087d0348b0115adba04027ee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433499"
---
# <a name="preconfiguring-a-router"></a>Vorkonfigurieren eines Routers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Normalerweise erfordert eine neue Installation des Betriebssystems einen internetfähigen Router und eine Firewall, um das interne Netzwerk des Kunden mit dem Internet zu verbinden. Wenn Sie zusätzlich zu einem Router einen vorkonfigurierten Server zur Verfügung stellen, können Sie weitere Schritte ausführen, um den Router benutzerfreundlicher zu konfigurieren.  
  
 Auf dem Router sollte DHCP aktiviert sein. Dem Server sollte eine statische IP-Adresse zugewiesen sein. Dazu können Sie eine DHCP-Reservierung einer IP-Adresse verwenden oder eine IP-Adresse zuweisen, die nicht im DHCP-Adressbereich liegt.  
  
 Sie sollten auf dem Router auch die Einstellungen für die Portweiterleitung vorkonfigurieren, um bestimmte Ports von der externen Schnittstelle des Routers an die Adresse des Servers im internen Netzwerk weiterzuleiten. Die folgende Tabelle listet die empfohlene Konfiguration auf.  
  
|Konfigurationseinstellung|Details|  
|---------------------------|-------------|  
|DHCP|On|  
|Portweiterleitung|Sie sollten die folgenden Ports an die Adresse des Servers weiterleiten:<br /><br /> -80 (für gehosteten Konfiguration ausschließlich 443)<br />-   443|  
|UPnP-Unterstützung|Sie sollten UPnP™-Support, um die einfachste Routerkonfiguration für den Kunden und die bestmögliche kundenerfahrung zu sorgen während der Installation angeben aktivieren.<br /><br /> **Warnung:** Die UPnP-Architektur kann ein Sicherheitsrisiko darstellen, wenn sie aktiviert bleibt.|  
  
 Neben den grundlegenden Einstellungen für die Routervorkonfiguration können Sie die folgenden Aufgaben ausführen, um das Verwalten des Routers benutzerfreundlicher zu gestalten:  
  
-   Erweitern Sie das Dashboard, indem Sie auf dem Server ein Add-In bereitstellen, mit dem die Benutzer den Router über eine angepasste Benutzeroberfläche verwalten können.  
  
-   Erweitern Sie die Integritätswarnungen, damit alle Warnungen vom Router in der Meldungsanzeige angezeigt werden.  
  
-   Wenn der Router mehrere Subnetze unterstützt, muss die IP-Adresse des Servers als ein DNS-Server über DHCP ausgegeben werden.  
  
-   Wenn der Router eine integrierte Zugriffssteuerungsfunktion für Active DirectoryÂ®-Domänendienste verfügt, können Sie die Active Directory-Integration während der Erstkonfiguration des Servers automatisieren. Sie sollten diese Funktion auch über das Add-In für die Routerverwaltung im Dashboard verfügbar machen.  
  
> [!NOTE]
>  Weitere Informationen zum Konfigurieren von Funkverbindungen finden Sie unter [Configure Support for a Wireless Network](Configure-Support-for-a-Wireless-Network.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)