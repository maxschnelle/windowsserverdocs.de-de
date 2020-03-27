---
title: Konfigurieren einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4a0229d5605271876f89e8e0ae75f8612e3f5762
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314015"
---
# <a name="configure-a-multisite-deployment"></a>Konfigurieren einer Bereitstellung mit mehreren Standorten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 kombiniert DirectAccess-und RAS-VPN (RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte, die erforderlich sind, um eine einzelne Bereitstellung von Windows Server 2016 oder Windows Server 2012 Remote Access für mehrere Standorte bereitzustellen.  
  
-   Schritt 1: bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings) Installieren und konfigurieren Sie einen einzelnen Remote Zugriffs Server. Die Bereitstellung für mehrere Standorte erfordert, dass Sie einen einzelnen Server installieren, bevor Sie eine Bereitstellung für mehrere Standorte konfigurieren.  
  
-   [Schritt 2: Konfigurieren der Infrastruktur für mehrere Standorte](Step-2-Configure-the-Multisite-Infrastructure.md) Für eine Bereitstellung mit mehreren Standorten müssen Sie zusätzliche Active Directory Standorte und Domänen Controller konfigurieren. Weitere Sicherheitsgruppen und Gruppenrichtlinie Objekte (GPOs) sind ebenfalls erforderlich, wenn Sie nicht automatisch konfigurierte Gruppenrichtlinien Objekte verwenden.  
  
-   [Schritt 3: Konfigurieren der Bereitstellung für mehrere Standorte:](Step-3-Configure-the-Multisite-Deployment.md)installieren Sie die Remote Zugriffs Rolle auf zusätzlichen Remote Zugriffs Servern, aktivieren Sie die Bereitstellung für mehrere Standorte, und konfigurieren Sie die zusätzlichen Server als Einstiegspunkte für die Bereitstellung.  
  
-   [Schritt 4: Überprüfen der Bereitstellung für mehrere Standorte](Step-4-Verify-the-Multisite-Deployment.md) 
  


