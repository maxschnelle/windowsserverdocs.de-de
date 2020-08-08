---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Wann sollte ein Verbundserver erstellt werden?
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 908a3ced3934ce078e4be424ec9ba33210905066
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962714"
---
# <a name="when-to-create-a-federation-server"></a>Wann sollte ein Verbundserver erstellt werden?

Wenn Sie Active Directory-Verbunddienste (AD FS) AD FS einen Verbund Server erstellen \( \) , können Sie Folgendes tun:

-   Setzen Sie einmaliges Anmelden für einmaliges \- Anmelden ( \- SSO) \( \) – die Kommunikation mit einer anderen Organisation ein \( , die auch über mindestens einen Verbund Server verfügt \) , und bei Bedarf mit den Mitarbeitern in Ihrer Organisation, \( die Zugriff über das Internet benötigen \) .

-   Aktivieren Sie die Front-End-Dienste, um Benutzer mithilfe von Identitätsdelegierung bei Infrastrukturdiensten anzumelden. Weitere Informationen finden Sie unter [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).

In den folgenden Abschnitten werden einige der wichtigsten Entscheidungen beschrieben, die bestimmen, wann und wo mindestens ein Verbund Server erstellt werden soll.

## <a name="determine-the-organizational-role-for-the-federation-server"></a>Bestimmen der Organisationsrollen für den Verbundserver
Um eine fundierte Entscheidung darüber zu treffen, wann ein neuer Verbund Server erstellt werden soll, müssen Sie zuerst feststellen, in welcher Organisation der Server gespeichert werden soll. Die Rolle, die ein Verbund Server in einer Organisation spielt, hängt davon ab, ob Sie den Verbund Server in der Konto Partnerorganisation oder in der Ressourcen Partnerorganisation platzieren.

Wenn ein Verbund Server im Unternehmensnetzwerk des Konto Partners platziert wird, besteht seine Rolle darin, die Benutzer Anmelde Informationen des Browsers, des Webdiensts oder der Identitäts Auswahl Clients zu authentifizieren und Sicherheits Token an Clients zu senden. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).

Wenn ein Verbund Server im Unternehmensnetzwerk des Ressourcen Partners platziert wird, besteht seine Rolle darin, Benutzer basierend auf einem Sicherheits Token zu authentifizieren, das von einem Verbund Server in der Ressourcen Partnerorganisation ausgestellt wird, oder die Rolle besteht darin, Tokenanforderungen von konfigurierten Webanwendungen oder Webdiensten an die Konto Partnerorganisation zu leiten, der der Client angehört. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).

## <a name="determine-which-ad-fs-design-to-deploy"></a>Ermitteln des AD FS-Entwurfs für die Bereitstellung
Sie erstellen Verbund Server in Ihrer Organisation, wenn Sie einen der folgenden AD FS Entwürfe bereitstellen möchten:

-   [Web-SSO-Entwurf](Web-SSO-Design.md)

-   [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)

Bei Bedarf kann eine Organisation, die einen Federated-Web-SSO-Entwurf bereitstellt, einen einzelnen Verbund Server so konfigurieren, dass er sowohl in der Konto Partner Rolle als auch in der Ressourcen Partner Rolle fungiert. In diesem Fall kann der Verbund Server Security Assertion Markup Language \( SAML- \) Token basierend auf Benutzerkonten in seiner eigenen Organisation oder Tokenanforderungen an die Organisation weiterleiten, je nachdem, wo sich die Benutzerkonten befinden.

> [!NOTE]
> Für den Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Konto Partner und mindestens ein Verbund Server im Ressourcen Partner vorhanden sein.

## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Unterschiede zwischen einem Verbundserver und einem Verbundserverproxy
Ein Verbund Server kann Webseiten zur Anmeldung \- , Richtlinie, Authentifizierung und Ermittlung auf die gleiche Weise wie ein Verbund Server Proxy bereitstellen. Die Hauptunterschiede zwischen einem Verbund Server und einem Verbund Server Proxy müssen mit den Vorgängen, die ein Verbund Server ausführen kann, die von einem Verbund Server Proxy nicht durchgeführt werden können, durchgeführt werden.

Im folgenden sind die Vorgänge aufgeführt, die nur von einem Verbund Server durchgeführt werden können:

-   Der Verbund Server führt die kryptografischen Vorgänge aus, durch die das Token erzeugt wird. Obwohl Verbund Server Proxys keine Token entwickeln können, können Sie zum Weiterleiten oder Umleiten der Token an Clients und ggf. zurück an den Verbund Server verwendet werden. Weitere Informationen zur Verwendung von Verbund Servern finden Sie unter [Erstellen eines Verbund Server Proxys](When-to-Create-a-Federation-Server-Proxy.md).

-   Verbund Server unterstützen die Verwendung der integrierten Windows-Authentifizierung für Clients im Unternehmensnetzwerk. Verbund Server Proxys. Weitere Informationen zur Verwendung der integrierten Windows-Authentifizierung mit dem Verbund Server finden Sie unter [When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md).

> [!CAUTION]
> Die Integrität und Vertraulichkeit der Kommunikation zwischen Verbundservern und SQL Server-Konfigurationsdatenbanken, SQL Server-Attributspeichern, Domänencontrollern und AD LDS-Instanzen ist standardmäßig nicht geschützt.Um dieses Problem zu minimieren, sollten Sie den Kommunikationskanal zwischen diesen Servern mit IPsec oder mithilfe einer sicheren physischen Verbindung zwischen all diesen Servern schützen.Für die Kommunikation zwischen Verbundservern und SQL Server sollten Sie in Erwägung ziehen, SSL-Schutz in der Verbindungszeichenfolge zu verwenden.Für Verbindungen zwischen Verbundservern und Domänencontrollern sollten Sie Kerberos-Signaturen und -Verschlüsselung in Betracht ziehen.LDAP \/ S wird für AD LDS AD DS nicht unterstützt \/ .

## <a name="how-to-create-a-federation-server"></a>Wie wird ein Verbundserver erstellt?
Sie können einen Verbund Server mithilfe des Konfigurations-Assistenten für den AD FS-Verbund Server oder des Befehls \- Zeilen Tools Fsconfig.exe erstellen. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihres Verbundservers auswählen.

-   Erstellen eines eigen \- ständigen Verbund Servers

    Weitere Informationen zum Einrichten eines eigen \- ständigen Verbund Servers finden Sie unter [Erstellen eines eigenständigen Verbund Servers](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md).

-   Erstellen des ersten Verbundservers in einer Verbundserverfarm

    Weitere Informationen zum Einrichten des ersten Verbundservers oder zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Create the First Federation Server in a Federation Server Farm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).

-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm

    Weitere Informationen zum Hinzufügen eines Verbundservers zu einer Farm finden Sie unter [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).

Ausführlichere Informationen zur Funktionsweise der einzelnen Optionen finden Sie unter [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).

Weitere Informationen zum Einrichten der erforderlichen Komponenten zum Bereitstellen eines Verbundservers finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

