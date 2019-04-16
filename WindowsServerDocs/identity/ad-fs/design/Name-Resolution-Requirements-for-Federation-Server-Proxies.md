---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: "Namensauflösungsanforderungen für Verbundserverproxys"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a94e4de181cd8794d479bbd6695a94658aba0f86
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>Namensauflösungsanforderungen für Verbundserverproxys

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Clientcomputer im Internet versuchen, eine Anwendung zugreifen, die von Active Directory Federation Services \(AD FS\) geschützt ist, müssen sie zunächst den Verbundserver authentifizieren. In den meisten Fällen ist der Verbundserver in der Regel nicht direkt aus dem Internet zugegriffen werden kann. Daher müssen internetclientcomputer zum der Verbundserverproxy stattdessen weitergeleitet. Sie können die Umleitung erreichen, indem Ihre DNS-Zone oder Zonen, die im Internet sind die entsprechenden Domain Name System \(DNS\) Einträge hinzugefügt.  
  
Die Methode, die Sie verwenden, um die Umleitung von Internetclients an der Verbundserverproxy hängt davon ab, wie Sie die DNS-Zone im Umkreisnetzwerk konfigurieren oder die Konfiguration einer DNS-Zone, die Sie steuern, auf das Internet. Verbundserverproxys sind zur Verwendung in einem Umkreisnetzwerk vorgesehen. Sie leiten Internetclientanforderungen an Verbundserver erfolgreich nur, wenn DNS ordnungsgemäß in allen möglicherweise gerichtete Zonen konfiguriert wurde, die Sie steuern. Daher ist die Konfiguration möglicherweise gerichtete Zonen – gibt an, ob Sie eine DNS-Zone für ausschließlich das Umkreisnetzwerk oder einer DNS-Zone für sowohl das Umkreisnetzwerk und Internetclients haben – wichtig ist.  
  
Dieses Thema beschreibt die Schritte, die Sie zum Konfigurieren der namensauflösung beim Platzieren eines Verbundserverproxys in Ihrem Umkreisnetzwerk ausführen können. Um festzustellen, welche Schritte erforderlich, ermitteln Sie zunächst die folgenden DNS-Szenarien am ehesten die DNS-Infrastruktur im Umkreisnetzwerk Ihrer Organisation entspricht. Befolgen Sie die Schritte für dieses Szenario.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>DNS-Zone für ausschließlich das Umkreisnetzwerk  
In diesem Fall Ihre Organisation verfügt über ein oder zwei DNS-Zonen im Umkreisnetzwerk, und Ihre Organisation DNS-Zonen im Internet nicht gesteuert. Erfolgreiche namensauflösung für einen Verbundserverproxy in der DNS-Zone, die nur das umkreisnetzwerkszenario hängt von folgenden Bedingungen ab:  
  
-   Der Verbundserverproxy benötigen Sie eine Einstellung in der "Hosts"-Datei zum Auflösen der vollständig qualifizierten Domäne den Namen \(FQDN\) von Federation Server Endpunkt-URL eine IP-Adresse eines Verbundservers oder einen Verbund-Server-Cluster.  
  
-   DNS im Umkreisnetzwerk des Kontopartners muss so konfiguriert, dass die FQDN des Federation Server-Endpunkt-URL in die IP-Adresse des Verbundserverproxys aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte zeigen, wie jede dieser Bedingungen für ein gegebenes Beispiel erreicht ist. In dieser Abbildung bietet Microsoft-Netzwerklastenausgleich \(NLB\)-Technologie eine einzelne Cluster-FQDN und eine einzelne, Cluster-IP-Adresse für einen vorhandenen Verbundserverfarm.  
  
![Name-Anforderungen](media/adfs2_deploy_single_fs.gif)  
  
Weitere Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-FQDN mit NLB finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. Konfigurieren der "Hosts"-Datei für den Verbundserverproxy  
Da DNS im Umkreisnetzwerk konfiguriert ist, um alle Anfragen für "FS.Fabrikam.com" in der Kontoverbundserverproxy aufzulösen, enthält der Konto-Partner-Verbundserverproxy einen Eintrag in der lokalen Dateien Hosts zum Auflösen von "FS.Fabrikam.com" in die IP-Adresse des tatsächlichen kontoverbundservers \ (oder Cluster-DNS-Namen für die Federation Server Farm\), die mit dem Unternehmensnetzwerk verbunden ist. Dies ermöglicht es dem Kontoverbundserverproxy auf den Host Name "FS.Fabrikam.com" in der Kontoverbundserver statt auf sich selbst zu beheben — dies passieren würde, wenn er versucht, "FS.Fabrikam.com" mithilfe des Umkreis-DNS nachzuschlagen –, damit der Verbundserverproxy mit dem Verbundserver kommunizieren kann.  
  
### <a name="2-configure-perimeter-dns"></a>2. Konfigurieren des Umkreis-DNS  
Da es ist nur ein einzelner AD FS Hostnamen, die Clientcomputer geleitet werden – gibt an, ob sie in einem Intranet oder im Internet sind – Clientcomputern im Internet, die den Umkreis-DNS-Server verwenden müssen den FQDN für das Konto Federation Server \(fs.fabrikam.com\) in die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk aufgelöst. So, dass es, wenn sie versuchen, "FS.Fabrikam.com" aufzulösen Clients an der Kontoverbundserverproxy weiterleiten kann, enthält Umkreis-DNS eine begrenzte "corp.Fabrikam.com" DNS-Zone mit einer einzelnen \(A\) Hostressourceneintrag für fs \(fs.fabrikam.com\) und die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk.  
  
Weitere Informationen zur Vorgehensweise beim Ändern der "Hosts"-Datei der Verbundserverproxys und Konfigurieren von DNS im Umkreisnetzwerk finden Sie unter [Konfigurieren der namensauflösung für einen Verbundserverproxy in einer DNS-Zone, die nur das Umkreisnetzwerk bedient](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md).  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>DNS-Zone für sowohl das Umkreisnetzwerk und Internetclients  
In diesem Szenario kontrolliert Ihre Organisation die DNS-Zone im Umkreisnetzwerk und mindestens ein DNS-Zone im Internet. Erfolgreiche namensauflösung für einen Verbundserverproxy in diesem Szenario hängt von folgenden Bedingungen ab:  
  
-   DNS in der Internetzone des Kontopartners muss so konfiguriert, dass der FQDN des Hostnamens Federation Server in die IP-Adresse des Verbundserverproxys im Umkreisnetzwerk aufgelöst wird.  
  
-   DNS im Umkreisnetzwerk des Kontopartners muss so konfiguriert, dass der FQDN des Hostnamens Federation Server in die IP-Adresse des Verbundservers im Unternehmensnetzwerk aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte zeigen, wie jede dieser Bedingungen für ein gegebenes Beispiel erreicht ist.  
  
![Name-Anforderungen](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. Konfigurieren des Umkreis-DNS  
Für dieses Szenario, da davon ausgegangen wird, dass Sie die Internet-DNS-Zone konfiguriert werden, Sie-Steuerelement auflösen anfordert, die für eine bestimmte Endpunkt-URL erfolgen \ (d. h. fs.fabrikam.com\) auf dem Verbundserverproxy im Umkreisnetzwerk, außerdem müssen Sie konfigurieren die Zone im Umkreisnetzwerk-DNS, um diese Anforderungen an den Verbundserver im Unternehmensnetzwerk weitergeleitet.  
  
Damit Clients an der Kontoverbundserver weitergeleitet werden können, wenn sie versuchen, "FS.Fabrikam.com" aufzulösen, wird mit einer einzelnen \(A\) Hostressourceneintrag für fs \(fs.fabrikam.com\) und die IP-Adresse der Kontoverbundserver im Unternehmensnetzwerk Umkreis-DNS konfiguriert. Dies ermöglicht es dem Kontoverbundserverproxy auf den Host Name "FS.Fabrikam.com" in der Kontoverbundserver statt auf sich selbst zu beheben — dies passieren würde, wenn er versucht, "FS.Fabrikam.com" mithilfe von Internet-DNS nachzuschlagen –, damit der Verbundserverproxy mit dem Verbundserver kommunizieren kann.  
  
### <a name="2-configure-internet-dns"></a>2. Konfigurieren des Internet-DNS  
Für die namensauflösung in diesem Szenario erfolgreich ausgeführt werden kann müssen alle Anforderungen von Clientcomputern im Internet an "FS.Fabrikam.com" von der Internet-DNS-Zone aufgelöst werden, zu steuern. Daher müssen Sie Ihre Internet-DNS-Zone zum Weiterleiten von Clientanforderungen für "FS.Fabrikam.com" die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk konfigurieren.  
  
Weitere Informationen dazu, wie Sie das Umkreisnetzwerk und dem Internet-DNS-Zonen ändern, finden Sie unter [Konfigurieren der namensauflösung für einen Verbundserverproxy in einer DNS-Zone, dient sowohl das Umkreisnetzwerk und Internetclients](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
