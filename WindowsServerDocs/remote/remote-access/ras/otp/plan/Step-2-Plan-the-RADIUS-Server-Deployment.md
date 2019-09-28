---
title: Schritt 2 Planen der RADIUS-Server Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a991b312a0938a3809acd2b94c00aa678f5b41da
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404401"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>Schritt 2 Planen der RADIUS-Server Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Planen Sie nach der Bereitstellung eines einzelnen RAS-Servers den einmal Kennwort (One-time password, OTP)-Authentifizierungsserver ein.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2,1 Planen des RADIUS-Servers|Für den OTP-Authentifizierungsserver unterstützt der Remote Zugriff in Windows Server 2016 und Windows Server 2012 alle RADIUS-fähigen OTP-Server, die das Kennwort Authentication Protocol (PAP) unterstützen.|  
  
## <a name="BKMK_1.1"></a>2,1 Planen des RADIUS-Servers  
Beachten Sie Folgendes, wenn Sie einen RADIUS-Server für die OTP-Authentifizierung planen:  
  
-   Für die meisten Arten von OTP-bereit Stellungen müssen Sie den RAS-Server als RADIUS-Agent konfigurieren. Weitere Informationen finden Sie in der Dokumentation des OTP-Herstellers.  
  
-   Für alle OTP-bereit Stellungen müssen Sie Ihre Active Directory Benutzer mit dem RADIUS-Server synchronisieren.  
  
-   Der RADIUS-Server muss kein Domänen Mitglied sein.  
  
-   Wenn Sie den RADIUS-Server bereitstellen, konfigurieren Sie einen gemeinsamen geheimen Schlüssel und die Portnummer für RADIUS-Datenverkehr. Notieren Sie sich diese Details. Sie sind erforderlich, wenn Sie den Remote Zugriffs Server konfigurieren.  
  
Ein Beispiel für eine Test Umgebungs Anleitung, die die OTP-Authentifizierung mit einem RSA SecurID-Server festlegt, finden Sie im [test Lab Guide: Veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID @ no__t-0.  
  
  
  


