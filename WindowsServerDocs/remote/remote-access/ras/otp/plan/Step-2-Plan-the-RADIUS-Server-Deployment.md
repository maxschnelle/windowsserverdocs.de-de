---
title: Schritt 2 Planen der Bereitstellung des RADIUS-Servers
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: pashort
author: shortpatti
ms.openlocfilehash: faf3f0b7c691edfb2c41e7b568e0791a3cad76b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859211"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>Schritt 2 Planen der Bereitstellung des RADIUS-Servers

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Planen Sie nach dem Bereitstellen eines einzelnen Remotezugriffsservers an, für das Einmalkennwort (OTP) Authentication-Server.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2.1 Planen des RADIUS-Servers|Für den Server OTP-Authentifizierung unterstützt den Remotezugriff in Windows Server 2016 und Windows Server 2012 einen RADIUS-aktivierte OTP-Server, der Password Authentication Protokoll (PAP) unterstützt.|  
  
## <a name="BKMK_1.1"></a>2.1 Planen des RADIUS-Servers  
Beachten Sie Folgendes ein, wenn Sie einen RADIUS-Server für die OTP-Authentifizierung zu planen:  
  
-   Für die meisten Arten von OTP-Bereitstellungen können, müssen Sie die RAS-Server als RADIUS-Agent konfigurieren. Weitere Informationen finden Sie in der Dokumentation des Herstellers OTP.  
  
-   Für alle Bereitstellungen für OTP müssen Sie Active Directory-Benutzer mit dem RADIUS-Server synchronisieren.  
  
-   Der RADIUS-Server muss nicht Mitglied einer Domäne sein.  
  
-   Wenn Sie den RADIUS-Server bereitstellen, konfigurieren Sie einen gemeinsamen geheimen Schlüssel und die Portnummer für RADIUS-Datenverkehr. Notieren Sie sich diese Details; Sie sind erforderlich, wenn Sie die RAS-Server konfigurieren.  
  
Sehen Sie ein Beispiel für Test Lab-Handbuch, mit dem OTP-Authentifizierung mit einem RSA SecurID-Server in eingerichtet [Test Lab Guide: Vorführen von DirectAccess mit OTP-Authentifizierung und RSA SecurID](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid).  
  
  
  


