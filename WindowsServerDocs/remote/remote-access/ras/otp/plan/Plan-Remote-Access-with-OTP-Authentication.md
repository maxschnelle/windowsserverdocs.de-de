---
title: Planen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 328e092dff23495203ee21fccbace1f7f36918d2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280815"
---
# <a name="plan-remote-access-with-otp-authentication"></a>Planen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Windows Server 2016 und Windows Server 2012 werden DirectAccess und Routing- und RAS-Dienst (RRAS) VPN in einer einzigen remotezugriffsrolle kombinieren. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte zum Bereitstellen von einer einzelnen Windows Server 2016 oder Windows Server 2012-Remotezugriff für mehrere Standorte Bereitstellung erforderlich sind.  
  
  
-  Schritt 1: [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings). Dieser Schritt umfasst die Planung der Infrastruktur erforderlich, um die Bereitstellung eines einzelnen Servers. Dazu gehört die Planung für das Netzwerk und servereinstellungen, zertifikatanforderungen, DNS-Einstellungen, Network Location Server-Bereitstellung, DirectAccess-Verwaltungsserver, Active Directory-Einstellungen und Gruppenrichtlinienobjekte (GPOs).  
  
-   [Schritt 2: Planen der Bereitstellung des RADIUS-server](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [Schritt 3: Planen von OTP-zertifikatbereitstellung](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [Schritt 4: Planen von OTP auf dem RAS-server](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
Nachdem Sie diese Planungsschritte abgeschlossen haben, finden Sie unter [Konfigurieren des Remotezugriffs mit OTP-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication). Informationen zum Konfigurieren einer Bereitstellung für mehrere Standorte als Proof of Concept in einer Lab-Umgebung finden Sie unter [Test Lab Guide: Vorführen von DirectAccess mit OTP-Authentifizierung und RSA SecurID](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid).  
  


