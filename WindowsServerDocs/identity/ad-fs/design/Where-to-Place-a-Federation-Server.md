---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: Platzieren eines Verbundservers
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d459ca354a462912c6343d6d6397222fa483b45a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962654"
---
# <a name="where-to-place-a-federation-server"></a>Platzieren eines Verbundservers

Aus Sicherheitsgründen wird empfohlen, Active Directory-Verbunddienste (AD FS) \( AD FS \) Verbund Server hinter einer Firewall zu platzieren und Sie mit Ihrem Unternehmensnetzwerk zu verbinden, um eine Gefährdung im Internet zu verhindern. Dies ist wichtig, da Verbund Server über eine vollständige Autorisierung zum Erteilen von Sicherheits Token verfügen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Wenn ein Verbund Server kompromittiert ist, kann ein böswilliger Benutzer voll Zugriffs Token für alle Webanwendungen und Verbund Server ausstellen, die durch Active Directory-Verbunddienste (AD FS) \( AD FS \) in allen Ressourcen Partnerorganisationen geschützt werden.

> [!NOTE]
> Aus Sicherheitsgründen sollten Sie vermeiden, dass auf Ihre Verbund Server direkt über das Internet zugegriffen werden kann. Es empfiehlt sich, den Verbund Servern nur dann direkten Internet Zugriff zu gewähren, wenn Sie eine Testumgebung einrichten oder wenn Ihre Organisation über kein Umkreis Netzwerk verfügt.

Bei typischen Unternehmensnetzwerken wird eine Firewall mit Intranetzugriff \- zwischen dem Unternehmensnetzwerk und dem Umkreis Netzwerk eingerichtet, und eine \- Firewall mit Internet Zugriff wird häufig zwischen dem Umkreis Netzwerk und dem Internet eingerichtet. In diesem Fall befindet sich der Verbund Server innerhalb des Unternehmensnetzwerks und ist nicht direkt für Internet Clients zugänglich.

> [!NOTE]
> Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, können über die integrierte Windows-Authentifizierung direkt mit dem Verbund Server kommunizieren.

Ein Verbund Server Proxy sollte im Umkreis Netzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren. Weitere Informationen hierzu finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md) (Platzieren eines Verbundserverproxys).

## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>Konfigurieren der Firewallserver für einen Verbundserver
Damit die Verbund Server direkt mit Verbund Server Proxys kommunizieren können, muss der Intranetfirewallserver so konfiguriert werden, dass HTTPS-Datenverkehr des Secure Hypertext Transfer-Protokolls \( \) vom Verbund Server Proxy an den Verbund Server zugelassen wird. Dies ist eine Anforderung, da der Intranetfirewallserver den Verbund Server mithilfe von Port 443 veröffentlichen muss, damit der Verbund Server Proxy im Umkreis Netzwerk auf den Verbund Server zugreifen kann.

Darüber hinaus verwendet der Firewallserver mit Intranetzugriff, z. b. \- ein Server, auf dem Internet Security und Acceleration \( ISA \) Server ausgeführt wird, einen als Server Veröffentlichung bezeichneten Prozess, um Internet-Client Anforderungen an die entsprechenden Unternehmensverbund Server zu verteilen. Dies bedeutet, dass Sie manuell eine Server Veröffentlichungs Regel auf dem Intranetserver mit ISA Server erstellen müssen, der die gruppierte Verbund Server-URL veröffentlicht, z. b. http: \/ \/ FS.fabrikam.com.

Weitere Informationen zum Konfigurieren der Serververöffentlichung in einem Umkreisnetzwerk finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md). Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webpublishing Regel](https://go.microsoft.com/fwlink/?LinkId=75182).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
