---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: Dienstkommunikationszertifikate
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b781d6fe99864b13d6e7f8ab65f3a14d205c2aa6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190805"
---
# <a name="service-communications-certificates"></a>Dienstkommunikationszertifikate

Ein Verbundserver erfordert die Verwendung von dienstkommunikationszertifikate für Szenarien, in denen WCF-nachrichtensicherheit verwendet wird.  
  
## <a name="service-communication-certificate-requirements"></a>Zertifikatanforderungen für Dienst-Kommunikation  
Dienstkommunikationszertifikate müssen zur Verwendung von AD FS die folgenden Anforderungen erfüllen:  
  
-   Das dienstkommunikationszertifikat, muss der Server Authentifizierung, die erweiterte Schlüsselverwendung enthalten \(EKU\) Erweiterung.  
  
-   Der Zertifikatssperrlisten \(CRLs\) Zugriff für alle Zertifikate in der Kette aus das dienstkommunikationszertifikat auf das Stamm-CA-Zertifikat sein muss. Die Stamm-CA muss auch durch alle Verbundserverproxys und eine Web-Server, die dieser Verbundserver zu vertrauen, vertrauenswürdig sein.  
  
-   Der Name des Antragstellers, das in das dienstkommunikationszertifikat verwendet wird, muss den Namen des Verbunddiensts in den Eigenschaften des Verbunddiensts übereinstimmen.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>Bereitstellungsüberlegungen für dienstkommunikationszertifikate  
Konfigurieren Sie dienstkommunikationszertifikate so, dass alle Verbundserver dasselbe Zertifikat verwenden. Wenn Sie einzelne für Federated Web bereitstellen\-anmelden\-auf \(SSO\) Design, es wird empfohlen, Ihre dienstkommunikationszertifikat von einer öffentlichen Zertifizierungsstelle ausgestellt werden. Sie können anfordern und installieren Sie diese Zertifikate über das IIS-Manager-Snap-\-in.  
  
Sie können Self-Service\-angemeldet, Dienstzertifikate Kommunikation erfolgreich auf dem Verbundserver in einer testumgebung auszuführen. Für eine produktionsumgebung empfehlen wir jedoch, dass Sie von einer öffentlichen Zertifizierungsstelle dienstkommunikationszertifikate abrufen. Im folgenden werden die Gründe, warum Sie nicht selbst verwenden\-angemeldet, Dienstzertifikate Kommunikation für eine live-Bereitstellung:  
  
-   Ein selbstsigniertes\-angemeldet, SSL-Zertifikat muss hinzugefügt werden dem vertrauenswürdigen Stammspeicher auf jedem Verbundserver in der Ressourcenpartnerorganisation. Obwohl dies einen Angreifer einen Ressourcenverbundserver zu gefährden allein nicht aktiviert ist, vertrauen Sie Self-Service\-selbstsignierte Zertifikate wird vergrößert die Angriffsfläche eines Computers, und es kann zu Sicherheitsrisiken führen, der Signaturgeber Zertifikat ist nicht vertrauenswürdig ist.  
  
-   Erstellt einen Benutzer negatives Erlebnis. Clients erhalten Sicherheitshinweis Anweisungen aus, wenn sie versuchen, verbundene Ressourcen zugreifen, die die folgende Meldung angezeigt: "Das Sicherheitszertifikat wurde von einem Unternehmen, die Sie nicht vertrauenswürdig eingestuften ausgestellt." Dieses Verhalten wird erwartet, da der eigenen\-signiertes Zertifikat ist nicht vertrauenswürdig.  
  
    > [!NOTE]  
    > Wenn erforderlich, Sie das Problem umgehen können mithilfe der Gruppenrichtlinie manuell übertragen Sie die Self\-selbstsignierten Zertifikats im vertrauenswürdigen Stammspeicher auf jedem Clientcomputer, die versuchen, eine AD FS-Website zugreifen.  
  
-   Zertifizierungsstellen geben Sie zusätzliches Zertifikat\-basierend Features wie private Schlüssel Archiv-, Erneuerung und Sperrung, die nicht von Self-Service bereitgestellt werden\-selbstsignierten Zertifikaten.  
  

