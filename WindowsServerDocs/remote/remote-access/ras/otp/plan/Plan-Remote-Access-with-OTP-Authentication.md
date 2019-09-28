---
title: Planen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 69127ef86e1e14620f8cbb29322e930c6d921702
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404356"
---
# <a name="plan-remote-access-with-otp-authentication"></a>Planen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess-und RRAS-VPN (Routing and Remote Access Service, Routing-und RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte, die erforderlich sind, um eine einzelne Bereitstellung von Windows Server 2016 oder Windows Server 2012 Remote Access für mehrere Standorte bereitzustellen.  
  
  
-  Schritt 1: Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)bereit. Dieser Schritt umfasst die Planung der Infrastruktur, die für die Bereitstellung eines einzelnen Servers erforderlich ist. Dazu gehört die Planung von Netzwerk-und Servereinstellungen, Zertifikat Anforderungen, DNS-Einstellungen, Bereitstellung des Netzwerkadressen Servers, DirectAccess-Verwaltungs Servern, Active Directory Einstellungen und Gruppenrichtlinie Objekte (GPOs).  
  
-   [Schritt 2: Planen der RADIUS-Server Bereitstellung @ no__t-0  
  
-   [Schritt 3: Planen der OTP-Zertifikat Bereitstellung @ no__t-0  
  
-   [Schritt 4: Planen von OTP auf dem Remote Zugriffs Server @ no__t-0  
  
Nachdem Sie diese Planungsschritte abgeschlossen haben, finden Sie weitere Informationen unter [Konfigurieren des Remote Zugriffs mit OTP-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication). Informationen zum Konfigurieren einer Bereitstellung für mehrere Standorte als Proof of Concept in einer Lab-Umgebung finden Sie unter [test Lab Guide: Veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID @ no__t-0.  
  


