---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: Dienstkommunikationszertifikate
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 377b6f9053a5805f6a13f6a865185da6965f9966
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972077"
---
# <a name="service-communications-certificates"></a>Dienstkommunikationszertifikate

Ein Verbund Server erfordert die Verwendung von Dienst Kommunikations Zertifikaten für Szenarien, in denen die WCF-Nachrichten Sicherheit verwendet wird.

## <a name="service-communication-certificate-requirements"></a>Zertifikat Anforderungen für die Dienst Kommunikation
Dienst Kommunikations Zertifikate müssen die folgenden Anforderungen erfüllen, um mit AD FS arbeiten zu können:

-   Das Dienst Kommunikations Zertifikat muss die erweiterte Schlüssel Verwendung-EKU-Erweiterung der Server Authentifizierung enthalten \( \) .

-   Der Zertifikat Sperr Listen-Sperr Listen \( \) muss für alle Zertifikate in der Kette vom Dienst Kommunikations Zertifikat bis zum Stamm Zertifikat der Zertifizierungsstelle zugänglich sein. Die Stamm Zertifizierungsstelle muss auch von allen Verbund Server Proxys und Webservern, die diesem Verbund Server Vertrauen, als vertrauenswürdig eingestuft werden.

-   Der Antragsteller Name, der im Dienst Kommunikations Zertifikat verwendet wird, muss mit dem Verbunddienst Namen in den Eigenschaften des Verbunddienst identisch sein.

## <a name="deployment-considerations-for-service-communication-certificates"></a>Überlegungen zur Bereitstellung für Dienst Kommunikations Zertifikate
Konfigurieren Sie Dienst Kommunikations Zertifikate, sodass alle Verbund Server das gleiche Zertifikat verwenden. Wenn Sie den Verbund- \- SSO-Entwurf für einmaliges Anmelden bereitstellen \- \( \) , wird empfohlen, dass das Dienst Kommunikations Zertifikat von einer öffentlichen Zertifizierungsstelle ausgestellt wird. Sie können diese Zertifikate über das IIS-Manager-Snap-in anfordern und installieren \- .

Sie können selbst \- signierte Dienst Kommunikations Zertifikate erfolgreich auf Verbund Servern in einer Testumgebung verwenden. Für eine Produktionsumgebung wird jedoch empfohlen, dass Sie Dienst Kommunikations Zertifikate von einer öffentlichen Zertifizierungsstelle abrufen. Aus folgenden Gründen sollten Sie keine selbst \- signierten Dienst Kommunikations Zertifikate für eine Live Bereitstellung verwenden:

-   Ein selbst \- signiertes SSL-Zertifikat muss dem vertrauenswürdigen Stamm Speicher auf jedem der Verbund Server in der Ressourcen Partnerorganisation hinzugefügt werden. Dies bedeutet, dass ein Angreifer nicht in der Lage ist, einen Ressourcen Verbund Server zu kompromittieren. das Vertrauen \- von selbst signierten Zertifikaten erhöht die Angriffsfläche eines Computers und kann zu Sicherheitsrisiken führen, wenn der Zertifikat Signatur Geber nicht vertrauenswürdig ist.

-   Dadurch entsteht eine schlechte Benutzer Leistung. Wenn Sie versuchen, auf Verbund Ressourcen zuzugreifen, die die folgende Meldung anzeigen, erhalten die Clients Sicherheitswarnungen: "das Sicherheitszertifikat wurde von einem Unternehmen ausgestellt, das Sie nicht als vertrauenswürdig eingestuft haben." Dies ist das erwartete Verhalten, da das selbst \- signierte Zertifikat nicht vertrauenswürdig ist.

    > [!NOTE]
    > Bei Bedarf können Sie diese Bedingung umgehen, indem Sie Gruppenrichtlinie verwenden, um das selbst \- signierte Zertifikat manuell in den vertrauenswürdigen Stamm Speicher auf jedem Client Computer zu überführen, der versucht, auf einen AD FS-Standort zuzugreifen.

-   CAS bieten zusätzliche Zertifikat \- basierte Features, wie z. b. private Schlüssel Archivierung, Erneuerung und Sperrung, die nicht von selbst \- signierten Zertifikaten bereitgestellt werden.


