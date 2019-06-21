---
title: Planen einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ba813fc5da53e9635e9ef1363f1a559a29419312
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282602"
---
# <a name="plan-a-multisite-deployment"></a>Planen einer Bereitstellung mit mehreren Standorten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Windows Server 2016, Windows Server 2012 werden DirectAccess und Routing- und RAS-Dienst (RRAS) VPN in einer einzigen remotezugriffsrolle kombinieren. Diese Übersicht bietet eine Einführung in die Planungsschritte, die zur Bereitstellung von Windows Server 2016 oder Windows Server 2012-Remotezugriff in einer Konfiguration mit mehreren Standorten erforderlich.  
  
1.  [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx). Dieser Schritt umfasst die Planung der Infrastruktur erforderlich, um die Bereitstellung eines einzelnen Servers. Dazu gehört die Planung für das Netzwerk und servereinstellungen, zertifikatanforderungen, DNS-Einstellungen, Network Location Server-Bereitstellung, DirectAccess-Verwaltungsserver, Active Directory-Einstellungen und Gruppenrichtlinienobjekte (GPOs).  
  
2.  [Schritt 2 Planen der Infrastruktur für mehrere Standorte](Step-2-Plan-the-Multisite-Infrastructure.md). Dieser Schritt umfasst die Active Directory und GPO-Planung und DNS-Konfiguration.  
  
3.  [Schritt 3 Planen der Bereitstellung für mehrere Standorte](Step-3-Plan-the-Multisite-Deployment.md). Dieser Schritt umfasst das Planen der zertifikateinstellungen, Network Location Server-Konfiguration, Einstellungen für Client-Eintrag, Einstellungen für die IPv6-Präfix und optional auch Globale Einstellungen für den Lastenausgleich.  
  
> [!NOTE]  
> Notieren Sie Ihre planungsentscheidungen für erweiterte Bereitstellung. Dieser Datensatz kann als Arbeitshilfe für die Personen verwendet werden, die in den Abschluss der Bereitstellungsschritte involviert sind.  
  
Nachdem Sie diese Planungsschritte abgeschlossen haben, finden Sie unter [Konfigurieren einer Bereitstellung für mehrere Standorte](../configure/Configure-a-Multisite-Deployment.md).  
  


