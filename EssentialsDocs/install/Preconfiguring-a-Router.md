---
title: Vorkonfigurieren eines Routers
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="preconfiguring-a-router"></a>Vorkonfigurieren eines Routers

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Normalerweise erfordert eine Neuinstallation des Betriebssystems einen internetfähigen Router und Firewalls, um das interne Netzwerk des Kunden mit dem Internet herstellen. Wenn Sie einen Router einen vorkonfigurierten Server als einen zusätzlichen Wert bieten, können Sie zur konfigurieren Sie des Routers eine bessere Benutzererfahrung bieten zusätzliche Schritteerforderlich.  
  
 Der Router sollte DHCP aktiviert haben. Der Server sollte eine statische IP-Adresse zugewiesen werden. Sie erreichen dies, DHCP-Reservierung einer IP-Adresse oder eine IP-Adresse, die außerhalb des Bereichs der DHCP-Adresse zuweisen.  
  
 Sie sollten auch die Einstellungen des Routers zum Weiterleiten von bestimmte Ports von der externen Schnittstelle des Routers an die Adresse des Servers, auf dem internen Netzwerk für die portweiterleitung vorkonfigurieren. Die folgende Tabelle enthält die empfohlene Konfiguration.  
  
|Einstellung für die Konfiguration|Detail|  
|---------------------------|-------------|  
|DHCP|Auf|  
|Portweiterleitung|Sie sollten die folgenden Ports an die Adresse des Servers weiterleiten:<br /><br /> -80 (für gehosteten Konfiguration ausschließlich 443)<br />-   443|  
|UPnP-Unterstützung|Aktivieren Sie UPnP-Unterstützung, ¢ Konfiguration für den Kunden und die optimale Benutzerfreundlichkeit bei der Installation bereitstellen.<br /><br /> **Warnung:** die UPnP-Architektur kann stellen ein Sicherheitsrisiko dar, wenn es aktiviert ist.|  
  
 Zusätzlich zu den Einstellungen für die Vorkonfiguration grundlegende Router können Sie die folgenden Aufgaben aus, um eine besser integrierte Benutzeroberfläche zum Verwalten des Routers bereitzustellen ausführen:  
  
-   Erweitern Sie das Dashboard, indem Sie ein Add-In bereitstellen, auf dem Server, der Benutzer den Router über eine angepasste Benutzeroberfläche verwalten kann.  
  
-   Erweitern Sie die Warnungen, sodass alle Warnungen vom Router in der Meldungsanzeige angezeigt werden können.  
  
-   Wenn der Router mehrere Subnetze unterstützt, muss die IP-Adresse des Servers als ein DNS-Server über DHCP ausgegeben werden.  
  
-   Wenn der Router über eine integrierte Zugriffssteuerungsfunktion für Active DirectoryÂ®-Domänendienste verfügt, können Sie die Active Directory-Integration während der Erstkonfiguration des Servers automatisieren. Sie sollten auch diese Funktion über das Router Management Add-In im Dashboard verfügbar machen.  
  
> [!NOTE]
>  Weitere Informationen zum Konfigurieren von Funkverbindungen finden Sie unter [Unterstützung für ein Drahtlosnetzwerk konfigurieren](Configure-Support-for-a-Wireless-Network.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)