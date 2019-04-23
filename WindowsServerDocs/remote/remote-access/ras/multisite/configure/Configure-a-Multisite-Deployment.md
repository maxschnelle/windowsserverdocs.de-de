---
title: Konfigurieren einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b602855db271348ac48ee0a5691424a7321c7370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849751"
---
# <a name="configure-a-multisite-deployment"></a>Konfigurieren einer Bereitstellung mit mehreren Standorten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Windows Server 2016 werden DirectAccess "und" Remote Access Service (RAS) VPN in einer einzigen remotezugriffsrolle zusammengefasst. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte zum Bereitstellen von einer einzelnen Windows Server 2016 oder Windows Server 2012-Remotezugriff für mehrere Standorte Bereitstellung erforderlich sind.  
  
-   Schritt 1: [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings). Installieren Sie und konfigurieren Sie einer RAS-Servers. Die Bereitstellung für mehrere Standorte müssen Sie einen einzelnen Server zu installieren, bevor Sie eine Bereitstellung für mehrere Standorte zu konfigurieren.  
  
-   [Schritt 2: Konfigurieren der Infrastruktur für mehrere Standorte](Step-2-Configure-the-Multisite-Infrastructure.md). Für eine Bereitstellung für mehrere Standorte müssen Sie zusätzliche Active Directory-Standorte und Domänencontroller konfigurieren. Zusätzliche von Sicherheitsgruppen und Gruppenrichtlinienobjekte (GPOs) sind auch erforderlich, wenn Sie nicht automatisch konfigurierte Gruppenrichtlinienobjekte verwenden.  
  
-   [Schritt 3: Konfigurieren Sie die Bereitstellung für mehrere Standorte](Step-3-Configure-the-Multisite-Deployment.md)– installieren Sie die remotezugriffsrolle auf zusätzliche RAS-Server, die Bereitstellung für mehrere Standorte zu aktivieren und konfigurieren Sie die zusätzlichen Server als Einstiegspunkte für die Bereitstellung.  
  
-   [Schritt 4: Überprüfen Sie die Bereitstellung für mehrere Standorte](Step-4-Verify-the-Multisite-Deployment.md) 
  


