---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: Namensauflösungsanforderungen für Verbundserver
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2776cc29b8c9ede884a6b304cd541f700f516ca
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191260"
---
# <a name="name-resolution-requirements-for-federation-servers"></a>Namensauflösungsanforderungen für Verbundserver

Wenn Clientcomputer im Unternehmensnetzwerk versuchen, Zugriff auf eine Anwendung oder einen Webdienst, der durch Active Directory Federation Services geschützt ist \(AD FS\), sie müssen sich zunächst bei einem Verbundserver authentifizieren. Eine Möglichkeit zur Authentifizierung ist der Unternehmensnetzwerk-Clients, die einen lokalen Verbundserver über die integrierte Windows-Authentifizierung Zugriff haben.  
  
## <a name="configure-corporate-dns"></a>Konfigurieren des Unternehmens-DNS  
Damit eine erfolgreiche namensauflösung über die integrierte Windows-Authentifizierung auf den lokalen Verbundserver auftreten können, Domain Name System \(DNS\) im Unternehmensnetzwerk des Kontos Partner konfiguriert werden muss, für einen neuen Host \(Ein\) -Ressourceneintrag, die den vollqualifizierten Domänennamen aufgelöst werden \(FQDN\) Hostnamen des Verbundservers der IP-Adresse des Verbund-Server-Clusters.  
  
In der folgenden Abbildung sehen Sie, wie diese Aufgabe für ein bestimmtes Szenario durchgeführt wird. In diesem Szenario wird die Microsoft-Netzwerklastenausgleich \(NLB\) enthält einen einzelnen FQDN-Clusternamen und einen einzelnen Cluster-IP-Adresse für einer vorhandenen Verbundserverfarm.  
  
![Anforderungen an den](media/adfs2_deploy_single_fs.gif)  
  
Informationen zum Konfigurieren einer Cluster-IP-Adresse oder FQDN mit NLB-cluster finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
Informationen über das Unternehmens-DNS für einen Verbundserver zu konfigurieren, finden Sie unter [Hinzufügen eines Hosts &#40;ein&#41; -Ressourceneintrag auf Unternehmens-DNS für einen Verbundserver](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
Informationen zum Konfigurieren von Verbundserverproxys im Umkreisnetzwerk finden Sie unter [Namensauflösungsanforderungen für Verbundserverproxys](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
