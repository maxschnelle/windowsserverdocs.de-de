---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: Namensauflösungsanforderungen für Verbundserver
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 88ec418bd72a6389856deb1abd85641d8782bc30
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408048"
---
# <a name="name-resolution-requirements-for-federation-servers"></a>Namensauflösungsanforderungen für Verbundserver

Wenn Client Computer im Unternehmensnetzwerk versuchen, auf eine Anwendung oder einen Webdienst zuzugreifen, der durch Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 geschützt ist, müssen Sie sich zunächst bei einem Verbund Server authentifizieren. Eine Möglichkeit, sich zu authentifizieren, besteht darin, dass die Unternehmensnetzwerk Clients über die integrierte Windows-Authentifizierung auf einen lokalen Verbund Server zugreifen.  
  
## <a name="configure-corporate-dns"></a>Konfigurieren des Unternehmens-DNS  
Damit eine erfolgreiche Namensauflösung durch die integrierte Windows-Authentifizierung auf lokalen Verbund Servern auftreten kann, muss Domain Name System \(dns @ no__t-1 im Unternehmensnetzwerk des Konto Partners für einen neuen Host \(a @ no__t-3 konfiguriert werden. Ressourcen Daten Satz, der den voll qualifizierten Domänen Namen \(fqdn @ no__t-5 Hostname des Verbund Servers in die IP-Adresse des Verbund Server Clusters auflöst.  
  
In der folgenden Abbildung sehen Sie, wie diese Aufgabe für ein bestimmtes Szenario durchgeführt wird. In diesem Szenario stellt der Microsoft-Netzwerk Lastenausgleich \(nlb @ no__t-1 einen einzelnen Cluster-voll qualifizierten Namen und eine einzelne Cluster-IP-Adresse für eine vorhandene Verbund Serverfarm bereit.  
  
![namens Anforderungen](media/adfs2_deploy_single_fs.gif)  
  
Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-FQDN mithilfe von NLB finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
Weitere Informationen zum Konfigurieren des Unternehmens-DNS für einen Verbund Server finden [Sie unter hinzu &#40;fügen&#41; eines Host-a-Ressourceneinsatzes zu einem Unternehmens-DNS für einen Verbund Server](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
Informationen zum Konfigurieren von Verbund Server Proxys im Umkreis Netzwerk finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
