---
title: Schritt 2 Planen der RADIUS-Server Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9c0d5adbf2096bbfcf4ea3aaa8b4e735e6594dcc
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965242"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>Schritt 2 Planen der RADIUS-Server Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Planen Sie nach der Bereitstellung eines einzelnen RAS-Servers den einmal Kennwort (One-time password, OTP)-Authentifizierungsserver ein.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2,1 Planen des RADIUS-Servers|Für den OTP-Authentifizierungsserver unterstützt der Remote Zugriff in Windows Server 2016 und Windows Server 2012 alle RADIUS-fähigen OTP-Server, die das Kennwort Authentication Protocol (PAP) unterstützen.|  
  
## <a name="21-plan-the-radius-server"></a><a name="BKMK_1.1"></a>2,1 Planen des RADIUS-Servers  
Beachten Sie Folgendes, wenn Sie einen RADIUS-Server für die OTP-Authentifizierung planen:  
  
-   Für die meisten Arten von OTP-bereit Stellungen müssen Sie den RAS-Server als RADIUS-Agent konfigurieren. Weitere Informationen finden Sie in der Dokumentation des OTP-Herstellers.  
  
-   Für alle OTP-bereit Stellungen müssen Sie Ihre Active Directory Benutzer mit dem RADIUS-Server synchronisieren.  
  
-   Der RADIUS-Server muss kein Domänen Mitglied sein.  
  
-   Wenn Sie den RADIUS-Server bereitstellen, konfigurieren Sie einen gemeinsamen geheimen Schlüssel und die Portnummer für RADIUS-Datenverkehr. Notieren Sie sich diese Details. Sie sind erforderlich, wenn Sie den Remote Zugriffs Server konfigurieren.  
  
Ein Beispiel für eine Test Umgebungs Anleitung zum Einrichten der OTP-Authentifizierung mit einem RSA SecurID-Server finden Sie in der [Test Umgebungs Anleitung: demonstrieren von DirectAccess mit OTP-Authentifizierung und RSA SecurID](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md).  
  
  
  
