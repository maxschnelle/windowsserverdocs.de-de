---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: Dienstkommunikationszertifikate
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 624d2e26bc0277129e44eee3fdce7c7396b735a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407906"
---
# <a name="service-communications-certificates"></a>Dienstkommunikationszertifikate

Ein Verbund Server erfordert die Verwendung von Dienst Kommunikations Zertifikaten für Szenarien, in denen die WCF-Nachrichten Sicherheit verwendet wird.  
  
## <a name="service-communication-certificate-requirements"></a>Zertifikat Anforderungen für die Dienst Kommunikation  
Dienst Kommunikations Zertifikate müssen die folgenden Anforderungen erfüllen, um mit AD FS arbeiten zu können:  
  
-   Das Dienst Kommunikations Zertifikat muss die erweiterte Schlüssel Verwendung der Server Authentifizierung \(eku @ no__t-1-Erweiterung enthalten.  
  
-   Die Zertifikat Sperr Listen \(crls @ no__t-1 müssen für alle Zertifikate in der Kette vom Dienst Kommunikations Zertifikat zum Zertifikat der Stamm Zertifizierungsstelle zugänglich sein. Die Stamm Zertifizierungsstelle muss auch von allen Verbund Server Proxys und Webservern, die diesem Verbund Server Vertrauen, als vertrauenswürdig eingestuft werden.  
  
-   Der Antragsteller Name, der im Dienst Kommunikations Zertifikat verwendet wird, muss mit dem Verbunddienst Namen in den Eigenschaften des Verbunddienst identisch sein.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>Überlegungen zur Bereitstellung für Dienst Kommunikations Zertifikate  
Konfigurieren Sie Dienst Kommunikations Zertifikate, sodass alle Verbund Server das gleiche Zertifikat verwenden. Wenn Sie das Federated Web Single @ no__t-0sign @ no__t-1On \(sso @ no__t-3 Design bereitstellen, wird empfohlen, dass das Dienst Kommunikations Zertifikat von einer öffentlichen Zertifizierungsstelle ausgestellt wird. Sie können diese Zertifikate über den IIS-Manager-Snap @ no__t-0in anfordern und installieren.  
  
Sie können selbst @ no__t-0signierte Dienst Kommunikations Zertifikate erfolgreich auf Verbund Servern in einer Testumgebung verwenden. Für eine Produktionsumgebung wird jedoch empfohlen, dass Sie Dienst Kommunikations Zertifikate von einer öffentlichen Zertifizierungsstelle abrufen. Im folgenden finden Sie Gründe, warum Sie selbst @ no__t-0signierte Dienst Kommunikations Zertifikate nicht für eine Live Bereitstellung verwenden sollten:  
  
-   Dem vertrauenswürdigen Stamm Speicher auf jedem der Verbund Server in der Ressourcen Partnerorganisation muss ein selbst @ no__t-0signiertes SSL-Zertifikat hinzugefügt werden. Dies bedeutet, dass ein Angreifer nicht in der Lage ist, einen Ressourcen Verbund Server zu kompromittieren. durch vertrauende selbst @ no__t-0signierte Zertifikate wird die Angriffsfläche eines Computers vergrößert, und er kann zu Sicherheitsrisiken führen, wenn der Zertifikat Signatur Geber nicht zuverlässigen.  
  
-   Dadurch entsteht eine schlechte Benutzer Leistung. Wenn Sie versuchen, auf Verbund Ressourcen zuzugreifen, in denen die folgende Meldung angezeigt wird, erhalten die Clients Sicherheitswarnungen: "Das Sicherheitszertifikat wurde von einem Unternehmen ausgestellt, das Sie nicht als vertrauenswürdig eingestuft haben." Dies ist das erwartete Verhalten, da das selbst @ no__t-0 signierte Zertifikat nicht vertrauenswürdig ist.  
  
    > [!NOTE]  
    > Falls erforderlich, können Sie diese Bedingung umgehen, indem Sie Gruppenrichtlinie verwenden, um das selbst @ no__t-0 signierte Zertifikat manuell in den vertrauenswürdigen Stamm Speicher auf jedem Client Computer zu überführen, der versucht, auf einen AD FS-Standort zuzugreifen.  
  
-   CAS stellen zusätzliche @ no__t-0based-Funktionen bereit, die nicht von selbst @ no__t-1 signierten Zertifikaten bereitgestellt werden, z. b. die Archivierung von privaten Schlüsseln, die Erneuerung und die Sperrung.  
  

