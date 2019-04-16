---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: Dienstkommunikationszertifikate
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 32e60f2c2d9e4fced04061ace44882b792e1a3bc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="service-communications-certificates"></a>Dienstkommunikationszertifikate

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Ein Verbundserver erfordert die Verwendung von dienstkommunikationszertifikate für Szenarien, die in denen WCF-nachrichtensicherheit verwendet wird.  
  
## <a name="service-communication-certificate-requirements"></a>Zertifikatanforderungen für Service-Kommunikation  
Dienstkommunikationszertifikate müssen mit AD FS funktioniert die folgenden Anforderungen erfüllen:  
  
-   Das dienstkommunikationszertifikat muss die Server Authentifizierung, die erweiterte Schlüsselverwendung \(EKU\) Erweiterung enthalten.  
  
-   Das Zertifikat Revocation Lists \(CRLs\) müssen für alle Zertifikate in der Kette von das dienstkommunikationszertifikat Zertifikat der Stammzertifizierungsstelle zugänglich. Die Stamm-CA muss auch von allen Verbundserverproxys und Webservern, die diese Verbundserver vertrauen vertrauenswürdig sein.  
  
-   Der Name des Antragstellers, der in das dienstkommunikationszertifikat verwendet wird, muss den Namen des Verbunddiensts in den Eigenschaften des Verbunddiensts übereinstimmen.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>Bereitstellungsüberlegungen für dienstkommunikationszertifikate  
Konfigurieren Sie dienstkommunikationszertifikate so, dass alle Verbundserver dasselbe Zertifikat verwenden. Wenn Sie das Design für Federated-Web-Single\-Sign\-On \(SSO\) bereitstellen, wird empfohlen, dass Ihre dienstkommunikationszertifikat von einer öffentlichen Zertifizierungsstelle ausgestellt werden. Sie können Zertifikate anfordern und installieren diese über das IIS-Manager-Snap-In.  
  
Sie können deren Hilfe signiert, die Kommunikation zwischen der Zertifikate erfolgreich auf dem Verbundserver in einer Testumgebung. Für eine Produktionsumgebung wird jedoch empfohlen, dass Sie von einer öffentlichen Zertifizierungsstelle dienstkommunikationszertifikate abrufen. Im folgenden sind die Gründe, warum Sie nicht mit deren Hilfe signiert, dienstkommunikationszertifikate für eine Live-Bereitstellung sollten:  
  
-   Ein deren Hilfe signiert, SSL-Zertifikat muss hinzugefügt werden dem vertrauenswürdigen Stammspeicher auf jedem Verbundserver in der Ressourcenpartnerorganisation. Während ein Angreifer einen Ressourcenverbundserver manipulieren allein nicht aktiviert ist, deren Hilfe signierte Zertifikate vertrauen steigt die Angriffsfläche eines Computers, und es kann zu Sicherheitsrisiken führen, wenn dem signierenden Zertifikat nicht als vertrauenswürdig angesehen wird.  
  
-   Es wird eine schlechte Benutzeroberfläche erstellt. Clients erhalten Sicherheitshinweis Aufforderung, wenn sie versuchen, federated Ressourcen zugreifen, die die folgende Meldung angezeigt: "das Sicherheitszertifikat wurde ausgestellt, von einem Unternehmen, die Sie nicht vertrauen möchten." Dies ist erwartet, da das Zertifikat mit deren Hilfe-Signatur nicht vertrauenswürdig ist.  
  
    > [!NOTE]  
    > Bei Bedarf können Sie umgehen, diese Bedingung mithilfe von Gruppenrichtlinien manuell nach unten das Zertifikat signierte mit deren Hilfe dem vertrauenswürdigen Stammspeicher auf jedem Client Push auf, bei denen versucht wird, auf eine AD FS-Website zuzugreifen.  
  
-   Zertifizierungsstellen werden zusätzliche Certificate\-basierte Funktionen, z.B. private Schlüssel archivieren, Erneuerung und Sperrung, die nicht von deren Hilfe signierte Zertifikate bereitgestellt werden.  
  

