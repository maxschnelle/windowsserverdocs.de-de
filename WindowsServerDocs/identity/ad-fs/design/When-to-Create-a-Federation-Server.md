---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Wann sollte ein Verbundserver erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8013764b88a1061cfcaa3a507466c111bfd59aad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864811"
---
# <a name="when-to-create-a-federation-server"></a>Wann sollte ein Verbundserver erstellt werden?

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie einen Verbund Serversin Active Directory Federation Services erstellen \(AD FS\), Sie bieten eine Möglichkeit, die mit dem Ihre Organisation kann:  
  
-   Interaktion mit Web Single\-anmelden\-auf \(SSO\)–-basierter Kommunikation mit einer anderen Organisation \(verfügt, die auch über mindestens einen Verbundserver\) und, falls notwendig, mit der Mitarbeiter in Ihrer eigenen Organisation \(, die Zugriff über das Internet benötigen\).  
  
-   Aktivieren Sie die Front-End-Dienste, um Benutzer mithilfe von Identitätsdelegierung bei Infrastrukturdiensten anzumelden. Weitere Informationen finden Sie unter [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).  
  
In den folgenden Abschnitten werden einige der wichtigsten Entscheidungen zur Bestimmung, wann und wo Sie eine oder mehrere Verbundserver zu erstellen.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>Bestimmen der Organisationsrollen für den Verbundserver  
Damit wird eine fundierte Entscheidung in Bezug auf einen neuen Verbundserver zu erstellen, müssen Sie zunächst ermitteln, in welcher Organisation der Server gespeichert werden soll. Die Rolle, die ein Verbundserver in einer Organisation spielt, hängt davon ab, ob Sie den Verbundserver in der Kontopartnerorganisation oder in der Ressourcenpartnerorganisation platzieren.  
  
Wenn der Verbundserver im Unternehmensnetzwerk des Kontopartners platziert wird, werden seine Rolle die Anmeldeinformationen des Browsers, Webdienst oder identitätsauswahlclients zu authentifizieren und Senden von Sicherheitstoken an die Clients. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
Wenn der Verbundserver im Unternehmensnetzwerk des Ressourcenpartners platziert wird, seine Rolle darin, authentifizieren Benutzer basierend auf der ein Sicherheitstoken, das durch einen Verbundserver in der Ressourcenpartnerorganisation ausgestellt wird, oder seine Rolle darin, tokenanfragen von umleiten konfigurierten Webanwendungen oder Webdiensten der Kontopartnerorganisation, die der Client angehört. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>Ermitteln des AD FS-Entwurfs für die Bereitstellung  
Sie erstellen Verbundserver in Ihrer Organisation, wenn Sie die folgenden AD FS-Entwürfe bereitstellen möchten:  
  
-   [Web-SSO-Entwurf](Web-SSO-Design.md)  
  
-   [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)  
  
Bei Bedarf kann eine Organisation, die einen Federated-Web-SSO-Entwurf bereitstellt ein einzelnen Verbundservers konfigurieren, sodass in sowohl die kontopartnerrolle und in der Ressourcenpartnerrolle fungiert. In diesem Fall kann der Verbundserver Security Assertion Markup Language generieren \(SAML\) Grundlage, dass die Token, die basierend auf Benutzerkonten in ihrem eigenen Unternehmen, oder er leitet tokenanforderungen für die Organisation, in denen die Benutzerkonten befinden .  
  
> [!NOTE]  
> Für den Federated-Web-SSO-Entwurf muss mindestens einen Verbundserver in der Kontopartner und mindestens ein Verbundserver im Ressourcenpartner vorhanden sein.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Unterschiede zwischen einem Verbundserver und einem Verbundserverproxy  
Ein Verbundserver dienen Webseiten für die Anmeldung\-in Richtlinien, Authentifizierung und Ermittlung in die gleiche Weise wie ein Verbundserverproxy. Die wichtigsten Unterschiede zwischen einem Verbundserver und einem Verbundserverproxy müssen Verbindung mit Vorgängen einen Verbund-Server kann, führen Sie ein Verbundserverproxy kann nicht durchführen.  
  
Es folgen die Vorgänge, die nur ein Verbundserver ausführen können:  
  
-   Der Verbundserver führt die kryptografischen Vorgänge, die das Token zu erzeugen. Obwohl Verbundserverproxys Token erzeugen können, können sie verwendet werden, weitergeleitet oder die Token für Clients, und, bei Bedarf zurück an den Verbundserver umleiten. Weitere Informationen zur Verwendung von Verbundservern, finden Sie unter [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md).  
  
-   Verbundserver unterstützen die Verwendung der integrierten Windows-Authentifizierung für Clients im Unternehmensnetzwerk. Verbundserverproxys nicht der Fall ist. Weitere Informationen zur Verwendung der integrierten Windows-Authentifizierung mit Verbundserver finden Sie unter [When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md).  
  
> [!CAUTION]  
> Die Integrität und Vertraulichkeit der Kommunikation zwischen Verbundservern und SQL Server-Konfigurationsdatenbanken, SQL Server-Attributspeichern, Domänencontrollern und AD LDS-Instanzen ist standardmäßig nicht geschützt. Um dieses Problem zu minimieren, sollten Sie den Kommunikationskanal zwischen diesen Servern mit IPsec oder mithilfe einer sicheren physischen Verbindung zwischen all diesen Servern schützen. Für die Kommunikation zwischen Verbundservern und SQL Server sollten Sie in Erwägung ziehen, SSL-Schutz in der Verbindungszeichenfolge zu verwenden. Für Verbindungen zwischen Verbundservern und Domänencontrollern sollten Sie Kerberos-Signaturen und -Verschlüsselung in Betracht ziehen. LDAP und LDAP\/S werden nicht für AD LDS unterstützt\/AD DS.  
  
## <a name="how-to-create-a-federation-server"></a>Wie wird ein Verbundserver erstellt?  
Sie können einen Verbundserver unter Verwendung der AD FS Konfigurations-Assistenten oder den Befehl Fsconfig.exe erstellen\-Tools "Linie". Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihres Verbundservers auswählen.  
  
-   Erstellen Sie einen eigenständigen\-allein Verbundserver  
  
    Weitere Informationen dazu, wie Sie einen eigenständigen einrichten\-allein Verbundserver finden Sie unter [Erstellen eines eigenständigen Verbundservers](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md).  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
    Weitere Informationen zum Einrichten des ersten Verbundservers oder zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Create the First Federation Server in a Federation Server Farm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
    Weitere Informationen zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).  
  
Ausführlichere Informationen zur Funktionsweise der einzelnen Optionen finden Sie unter [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
Weitere Informationen über das Einrichten der erforderlichen Komponenten zum Bereitstellen eines Verbundservers finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

