---
title: Planen einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6a0679ba548aabd9ea83f886e5e8db79480c819e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958712"
---
# <a name="plan-a-multisite-deployment"></a>Planen einer Bereitstellung mit mehreren Standorten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016, Windows Server 2012 kombinieren DirectAccess-und RRAS-VPN (Routing and Remote Access Service, Routing-und RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Diese Übersicht bietet eine Einführung in die erforderlichen Planungsschritte für die Bereitstellung von Windows Server 2016 oder Windows Server 2012 Remote Access in einer Konfiguration mit mehreren Standorten.  
  
1.  Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831436(v=ws.11))bereit. Dieser Schritt umfasst die Planung der Infrastruktur, die für die Bereitstellung eines einzelnen Servers erforderlich ist. Dazu gehört die Planung von Netzwerk-und Servereinstellungen, Zertifikat Anforderungen, DNS-Einstellungen, Bereitstellung des Netzwerkadressen Servers, DirectAccess-Verwaltungs Servern, Active Directory Einstellungen und Gruppenrichtlinie Objekte (GPOs).  
  
2.  [Schritt 2: Planen der Infrastruktur für mehrere Standorte](Step-2-Plan-the-Multisite-Infrastructure.md). Dieser Schritt umfasst Active Directory-und GPO-Planung und DNS-Konfiguration.  
  
3.  [Schritt 3: Planen der Bereitstellung für mehrere Standorte](Step-3-Plan-the-Multisite-Deployment.md). Dieser Schritt umfasst die Planung von Zertifikat Einstellungen, die Netzwerkadressen Server-Konfiguration, Einstellungen für Client Einstiegspunkte, IPv6-Präfix Einstellungen und optional globale Einstellungen für den Lastenausgleich.  
  
> [!NOTE]  
> Notieren Sie Ihre Planungsentscheidungen für die erweiterte Remote Zugriffs Bereitstellung. Dieser Datensatz kann als Arbeitshilfe für die Personen verwendet werden, die in den Abschluss der Bereitstellungsschritte involviert sind.  
  
Nachdem Sie diese Planungsschritte abgeschlossen haben, finden Sie weitere Informationen unter [Konfigurieren einer Bereitstellung für mehrere Standorte](../configure/Configure-a-Multisite-Deployment.md).  
  
