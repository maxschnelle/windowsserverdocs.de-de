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
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 25c0ce5d62268f64113ebc39345b2d50867bebf7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367122"
---
# <a name="configure-a-multisite-deployment"></a>Konfigurieren einer Bereitstellung mit mehreren Standorten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016 kombiniert DirectAccess-und RAS-VPN (RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte, die erforderlich sind, um eine einzelne Bereitstellung von Windows Server 2016 oder Windows Server 2012 Remote Access für mehrere Standorte bereitzustellen.  
  
-   Schritt 1: Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)bereit. Installieren und konfigurieren Sie einen einzelnen Remote Zugriffs Server. Die Bereitstellung für mehrere Standorte erfordert, dass Sie einen einzelnen Server installieren, bevor Sie eine Bereitstellung für mehrere Standorte konfigurieren.  
  
-   [Schritt 2: Konfigurieren Sie die Infrastruktur für mehrere Standorte @ no__t-0. Für eine Bereitstellung mit mehreren Standorten müssen Sie zusätzliche Active Directory Standorte und Domänen Controller konfigurieren. Weitere Sicherheitsgruppen und Gruppenrichtlinie Objekte (GPOs) sind ebenfalls erforderlich, wenn Sie nicht automatisch konfigurierte Gruppenrichtlinien Objekte verwenden.  
  
-   [Schritt 3: Konfigurieren der Bereitstellung für mehrere Standorte @ no__t-0-installieren Sie die Remote Zugriffs Rolle auf zusätzlichen Remote Zugriffs Servern, aktivieren Sie die Bereitstellung für mehrere Standorte, und konfigurieren Sie die zusätzlichen Server als Einstiegspunkte für die Bereitstellung.  
  
-   [Schritt 4: Überprüfen der Bereitstellung für mehrere Standorte @ no__t-0 
  


