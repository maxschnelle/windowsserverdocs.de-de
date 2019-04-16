---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Wann sollte ein Verbundserver erstellt
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8013764b88a1061cfcaa3a507466c111bfd59aad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server"></a>Wann sollte ein Verbundserver erstellt

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie einen Verbundserverproxy Serversin Active Directory Federation Services \(AD FS\) erstellen, bieten Sie eine Möglichkeit, die mit dem Ihrer Organisation kann:  
  
-   Interaktion mit Web Singlethread-Standardparameter auf \ (SSO\) – Kommunikation mit einer anderen Organisation \ (die auch verfügt über mindestens einen Verbundserver Server\) und, falls notwendig, mit der Mitarbeiter in Ihrer Organisation \ (benötigen Zugriff über die möglicherweise).  
  
-   Aktivieren Sie front-End-Dienste für den Identitätswechsel von Benutzern mithilfe von identitätsdelegierung. Weitere Informationen finden Sie unter [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).  
  
In den folgenden Abschnitten werden einige der wichtigsten Entscheidungen zur Bestimmung, wann und wo Sie erstellen eine oder mehrere Verbundserver beschrieben.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>Bestimmen Sie die Organisations-Rolle für den Verbundserver  
Wenn Sie eine fundierte Entscheidung in Bezug auf einen neuen Verbundserver erstellen möchten, müssen Sie zunächst bestimmen, in welcher Organisation der Server befinden wird. Die Rolle, die ein Verbundserver in einer Organisation spielt, hängt davon ab, ob Sie den Verbundserver in der Kontopartnerorganisation oder in der Ressourcenpartnerorganisation platzieren.  
  
Wenn ein Verbundserver im Unternehmensnetzwerk des Kontopartners platziert wird, wird seine Rolle Benutzeranmeldeinformationen im Browser, Webdienst oder identitätsauswahlclients zu authentifizieren und Sicherheitstoken an Clients zu senden. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
Wenn Verbundserver im Unternehmensnetzwerk des Ressourcenpartners platziert wird, wird seine Rolle darin, authentifiziert Benutzer basierend auf einem Sicherheitstoken, die durch einen Verbundserver in der Ressourcenpartnerorganisation ausgestellt wird, oder seine Rolle darin, tokenanfragen von konfigurierten Webanwendungen oder Webdiensten an die Kontopartnerorganisation zu leiten, der der Client angehört. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Ressourcenpartner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>Ermitteln Sie die AD FS-Entwurfs für die Bereitstellung  
Sie erstellen Verbundserver in Ihrer Organisation, wenn Sie die folgenden AD FS-Entwürfe bereitstellen möchten:  
  
-   [Web-SSO-Entwurf](Web-SSO-Design.md)  
  
-   [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)  
  
Bei Bedarf kann eine Organisation, die einen Federated-Web-SSO-Entwurf bereitgestellt wird ein einzelnen Verbundservers konfigurieren, sodass es in sowohl den Kontopartner- und in der Ressourcenpartnerrolle fungiert. In diesem Fall des Verbundservers erzeugen Security Assertion Markup Language \(SAML\) Token, basierend auf Benutzerkonten in der eigenen Organisation oder umleiten Token anfordert, für die Organisation basierend auf dem sich die Benutzerkonten befinden.  
  
> [!NOTE]  
> Für den Federated-Web-SSO-Entwurf muss mindestens einen Verbundserver in der Kontopartner und mindestens ein Verbundserver im Ressourcenpartner vorhanden sein.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Unterschiede zwischen einem Verbundserver und eines Verbundserverproxys  
Verbundserver kann Webseiten für Standardparameter in, Gruppenrichtlinie, Authentifizierung und Ermittlung auf die gleiche Weise dienen, die ein Verbundserverproxy ist. Die wichtigsten Unterschiede zwischen einem Verbundserver und einem Verbundserverproxy mit Vorgängen ein Verbund, müssen Server möglich, dass ein Verbundserverproxys ausführen kann.  
  
Im folgenden sind die Vorgänge, die nur ein Verbundserver ausführen können:  
  
-   Der Verbundserver führt die kryptografischen Vorgänge, die das Token zu erzeugen. Obwohl Verbundserverproxys Token erzeugen können, können sie verwendet werden, weiterzuleiten oder die Token an Clients und bei Bedarf wieder an den Verbundserver umgeleitet werden. Weitere Informationen zur Verwendung von Verbundservern, finden Sie unter [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md).  
  
-   Verbundserver unterstützen die Verwendung der integrierten Windows-Authentifizierung für Clients im Unternehmensnetzwerk. Verbundserverproxys nicht. Weitere Informationen zur Verwendung der integrierten Windows-Authentifizierung mit Verbundserver finden Sie unter [When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md).  
  
> [!CAUTION]  
> Kommunikation zwischen Verbundservern und SQL Server-Konfigurationsdatenbanken, SQL Server-attributspeichern, Domänencontrollern und AD LDS-Instanzen ist nicht die Integrität und Vertraulichkeit standardmäßig geschützt. Um dieses Problem zu minimieren, sollten Sie in den Kommunikationskanal zwischen diesen Servern mit IPSEC oder mithilfe einer sicheren physischen Verbindungs zwischen all diesen Servern schützen. Für die Kommunikation zwischen Verbundservern und SQL Server sollten Sie in Erwägung ziehen, SSL-Schutz in der Verbindungszeichenfolge zu verwenden. Verbindungen zwischen Verbundservern und Domänencontrollern sollten Sie die Kerberos-Signierung und Verschlüsselung aktivieren. Für LDAP ist LDAP\/S für AD LDS\/AD DS nicht unterstützt.  
  
## <a name="how-to-create-a-federation-server"></a>Vorgehensweise beim Erstellen eines Verbundservers  
Sie können einen Verbundserver mit AD FS Federation Server-Konfigurations-Assistenten oder das Befehlszeilentool Fsconfig.exe erstellen. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen eines Verbundservers auswählen.  
  
-   Erstellen Sie einen eigenständige Verbundserver  
  
    Weitere Informationen dazu, wie Sie eine eigenständige Verbundserver einrichten, finden Sie unter [Erstellen eines eigenständigen Verbundservers](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md).  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
    Weitere Informationen zur Vorgehensweise beim Einrichten des ersten Verbundservers oder zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Erstellen des ersten Verbundservers in einer Verbundserverfarm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
    Weitere Informationen zur Vorgehensweise beim Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).  
  
Ausführlichere Informationen wie jede dieser Lösungen funktioniert, finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
Weitere Informationen zur Vorgehensweise beim Einrichten der Voraussetzungen zum Bereitstellen eines Verbundservers finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

