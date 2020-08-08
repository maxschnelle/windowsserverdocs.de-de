---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: Namensauflösungsanforderungen für Verbundserver
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d40e574526380da158261f8fe45ce226ced2bf03
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945183"
---
# <a name="name-resolution-requirements-for-federation-servers"></a>Namensauflösungsanforderungen für Verbundserver

Wenn Client Computer im Unternehmensnetzwerk versuchen, auf eine Anwendung oder einen Webdienst zuzugreifen, der durch Active Directory-Verbunddienste (AD FS) \( AD FS geschützt ist \) , müssen Sie sich zunächst bei einem Verbund Server authentifizieren. Eine Möglichkeit, sich zu authentifizieren, besteht darin, dass die Unternehmensnetzwerk Clients über die integrierte Windows-Authentifizierung auf einen lokalen Verbund Server zugreifen.

## <a name="configure-corporate-dns"></a>Konfigurieren des Unternehmens-DNS
Damit eine erfolgreiche Namensauflösung durch die integrierte Windows-Authentifizierung auf lokalen Verbund Servern auftreten kann \( , \) muss Domain Name System DNS im Unternehmensnetzwerk des Konto Partners für einen neuen Host \( ein Ressourcen Daten Satz konfiguriert werden, \) der den voll qualifizierten Domänen Namen- \( FQDN \) -Hostnamen des Verbund Servers in die IP-Adresse des Verbund Server Clusters auflöst.

In der folgenden Abbildung sehen Sie, wie diese Aufgabe für ein bestimmtes Szenario durchgeführt wird. In diesem Szenario stellt der Microsoft-Netzwerk Lastenausgleich \( -NLB \) einen einzelnen Cluster-voll qualifizierten Namen und eine einzelne Cluster-IP-Adresse für eine vorhandene Verbund Serverfarm bereit.

![namens Anforderungen](media/adfs2_deploy_single_fs.gif)

Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-FQDN mithilfe von NLB finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkId=75282).

Informationen zum Konfigurieren des Unternehmens-DNS für einen Verbund Server finden [Sie unter Hinzufügen eines Hosts &#40;einem&#41;-Ressourcen Daten Satz zu einem Unternehmens-DNS für einen Verbund Server](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).

Informationen zum Konfigurieren von Verbund Server Proxys im Umkreis Netzwerk finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.


## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
