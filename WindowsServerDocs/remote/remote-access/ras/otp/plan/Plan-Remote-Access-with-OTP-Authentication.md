---
title: Planen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ddcfa2898f4b90bf724a547bb16244cfad4ab3ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858193"
---
# <a name="plan-remote-access-with-otp-authentication"></a>Planen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess-und RRAS-VPN (Routing and Remote Access Service, Routing-und RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Diese Übersicht bietet eine Einführung in die Konfigurationsschritte, die erforderlich sind, um eine einzelne Bereitstellung von Windows Server 2016 oder Windows Server 2012 Remote Access für mehrere Standorte bereitzustellen.  
  
  
-  Schritt 1: bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings) Dieser Schritt umfasst die Planung der Infrastruktur, die für die Bereitstellung eines einzelnen Servers erforderlich ist. Dazu gehört die Planung von Netzwerk-und Servereinstellungen, Zertifikat Anforderungen, DNS-Einstellungen, Bereitstellung des Netzwerkadressen Servers, DirectAccess-Verwaltungs Servern, Active Directory Einstellungen und Gruppenrichtlinie Objekte (GPOs).  
  
-   [Schritt 2: Planen der RADIUS-Server Bereitstellung](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [Schritt 3: Planen der OTP-Zertifikat Bereitstellung](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [Schritt 4: Planen von OTP auf dem Remote Zugriffs Server](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
Nachdem Sie diese Planungsschritte abgeschlossen haben, finden Sie weitere Informationen unter [Konfigurieren des Remote Zugriffs mit OTP-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication). Informationen zum Konfigurieren einer Bereitstellung für mehrere Standorte als Proof of Concept in einer Lab-Umgebung finden Sie unter [Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid).  
  


