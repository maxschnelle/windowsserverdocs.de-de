---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Wann sollte ein Verbundserver erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 91c260dad1bd260a7dad7320fecd15e6472c50a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407886"
---
# <a name="when-to-create-a-federation-server"></a>Wann sollte ein Verbundserver erstellt werden?

Wenn Sie einen Verbund Server in Active Directory-Verbunddienste (AD FS) \(AD FS\)erstellen, können Sie Folgendes tun:  
  
-   Melden Sie sich mit Web Single\-Sign\-on \(SSO\)– based communication with another organization \(, die auch mindestens einen Verbund Server hat\) und bei Bedarf mit den Mitarbeitern in ihrer eigenen Organisation \(, die Zugriff über das Internet\)benötigen.  
  
-   Aktivieren Sie die Front-End-Dienste, um Benutzer mithilfe von Identitätsdelegierung bei Infrastrukturdiensten anzumelden. Weitere Informationen finden Sie unter [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).  
  
In den folgenden Abschnitten werden einige der wichtigsten Entscheidungen beschrieben, die bestimmen, wann und wo mindestens ein Verbund Server erstellt werden soll.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>Bestimmen der Organisationsrollen für den Verbundserver  
Um eine fundierte Entscheidung darüber zu treffen, wann ein neuer Verbund Server erstellt werden soll, müssen Sie zuerst feststellen, in welcher Organisation der Server gespeichert werden soll. Die Rolle, die ein Verbund Server in einer Organisation spielt, hängt davon ab, ob Sie den Verbund Server in der Konto Partnerorganisation oder in der Ressourcen Partnerorganisation platzieren.  
  
Wenn ein Verbund Server im Unternehmensnetzwerk des Konto Partners platziert wird, besteht seine Rolle darin, die Benutzer Anmelde Informationen des Browsers, des Webdiensts oder der Identitäts Auswahl Clients zu authentifizieren und Sicherheits Token an Clients zu senden. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
Wenn ein Verbund Server im Unternehmensnetzwerk des Ressourcen Partners platziert wird, besteht seine Rolle darin, Benutzer basierend auf einem Sicherheits Token zu authentifizieren, das von einem Verbund Server in der Ressourcen Partnerorganisation ausgestellt wird, oder die Rolle besteht darin, Tokenanforderungen von Konfigurieren von Webanwendungen oder Webdiensten für die Konto Partnerorganisation, zu der der Client gehört. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>Ermitteln des AD FS-Entwurfs für die Bereitstellung  
Sie erstellen Verbund Server in Ihrer Organisation, wenn Sie einen der folgenden AD FS Entwürfe bereitstellen möchten:  
  
-   [Web-SSO-Entwurf](Web-SSO-Design.md)  
  
-   [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)  
  
Bei Bedarf kann eine Organisation, die einen Federated-Web-SSO-Entwurf bereitstellt, einen einzelnen Verbund Server so konfigurieren, dass er sowohl in der Konto Partner Rolle als auch in der Ressourcen Partner Rolle fungiert. In diesem Fall kann der Verbund Server Security Assertion Markup Language \(SAML-\) Token basierend auf Benutzerkonten in seiner eigenen Organisation oder Tokenanforderungen an die Organisation basierend auf dem Speicherort der Benutzerkonten weiterleiten.  
  
> [!NOTE]  
> Für den Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Konto Partner und mindestens ein Verbund Server im Ressourcen Partner vorhanden sein.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Unterschiede zwischen einem Verbundserver und einem Verbundserverproxy  
Ein Verbund Server kann Webseiten für das SIG\-Nieren von Anmeldungen, Richtlinien, Authentifizierung und Ermittlung auf die gleiche Weise wie ein Verbund Server Proxy bereitstellen. Die Hauptunterschiede zwischen einem Verbund Server und einem Verbund Server Proxy müssen mit den Vorgängen, die ein Verbund Server ausführen kann, die von einem Verbund Server Proxy nicht durchgeführt werden können, durchgeführt werden.  
  
Im folgenden sind die Vorgänge aufgeführt, die nur von einem Verbund Server durchgeführt werden können:  
  
-   Der Verbund Server führt die kryptografischen Vorgänge aus, durch die das Token erzeugt wird. Obwohl Verbund Server Proxys keine Token entwickeln können, können Sie zum Weiterleiten oder Umleiten der Token an Clients und ggf. zurück an den Verbund Server verwendet werden. Weitere Informationen zur Verwendung von Verbund Servern finden Sie unter [Erstellen eines Verbund Server Proxys](When-to-Create-a-Federation-Server-Proxy.md).  
  
-   Verbund Server unterstützen die Verwendung der integrierten Windows-Authentifizierung für Clients im Unternehmensnetzwerk. Verbund Server Proxys. Weitere Informationen zur Verwendung der integrierten Windows-Authentifizierung mit dem Verbund Server finden Sie unter [When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md).  
  
> [!CAUTION]  
> Die Integrität und Vertraulichkeit der Kommunikation zwischen Verbundservern und SQL Server-Konfigurationsdatenbanken, SQL Server-Attributspeichern, Domänencontrollern und AD LDS-Instanzen ist standardmäßig nicht geschützt. Um dies zu verhindern, sollten Sie den Kommunikationskanal zwischen diesen Servern mithilfe von IPSec oder einer physisch sicheren Verbindung zwischen allen diesen Servern schützen. Für die Kommunikation zwischen Verbund Servern und SQL-Servern sollten Sie SSL-Schutz in der Verbindungs Zeichenfolge verwenden. Für Verbindungen zwischen Verbund Servern und Domänen Controllern sollten Sie die Kerberos-Signierung und-Verschlüsselung aktivieren. LDAP-\/S werden für AD LDS\/AD DS nicht unterstützt.  
  
## <a name="how-to-create-a-federation-server"></a>Wie wird ein Verbundserver erstellt?  
Sie können einen Verbund Server mithilfe des Konfigurations-Assistenten für den AD FS-Verbund Servers oder mithilfe des Befehls\-Zeilen Tools "fsconfig. exe" erstellen. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihres Verbundservers auswählen.  
  
-   Erstellen eines eigenständigen\-Verbund Servers  
  
    Weitere Informationen zum Einrichten eines eigenständigen\-Verbund Servers finden Sie unter [Erstellen eines eigenständigen Verbund Servers](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md).  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
    Weitere Informationen zum Einrichten des ersten Verbundservers oder zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Erstellen des ersten Verbundservers in einer Verbundserverfarm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
    Weitere Informationen zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).  
  
Ausführlichere Informationen zur Funktionsweise der einzelnen Optionen finden Sie unter [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
Weitere Informationen zum Einrichten der erforderlichen Komponenten zum Bereitstellen eines Verbundservers finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

