---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: Namensauflösungsanforderungen für Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a94e4de181cd8794d479bbd6695a94658aba0f86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855021"
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>Namensauflösungsanforderungen für Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Clientcomputer im Internet versuchen, auf eine Anwendung zuzugreifen, die von Active Directory Federation Services gesichert ist \(AD FS\), sie müssen sich zunächst an den Verbundserver authentifizieren. In den meisten Fällen ist der Verbundserver in der Regel nicht direkt über das Internet zugegriffen werden. Internetclientcomputer müssen daher stattdessen an den Verbundserverproxy umgeleitet werden. Sie können die Umleitung erreichen, durch Hinzufügen der entsprechenden Domain Name System \(DNS\) Datensätze zu Ihrer DNS-Zone oder Zonen, die das Internet auftreten.  
  
Die Methode, die Sie verwenden, um Internetclients an den Verbundserverproxy umzuleiten hängt davon ab, wie Sie die DNS-Zone in Ihrem Umkreisnetzwerk konfigurieren oder der Konfiguration einer DNS-Zone, die Sie steuern, auf das Internet. Verbundserverproxys sind zur Verwendung in einem Umkreisnetzwerk vorgesehen. Sie leiten Internetclientanforderungen für Verbundserver erfolgreich nur dann, wenn DNS ordnungsgemäß in alle im Internet konfiguriert wurde,\-mit Zonen, die Sie steuern. Daher ist die Konfiguration Ihres Internet\-für Zonen – gibt an, ob Sie über eine DNS-Zone für ausschließlich das Umkreisnetzwerk oder einer DNS-Zone für sowohl Umkreisnetzwerk und Internetclients verfügen, ist wichtig.  
  
Dieses Thema beschreibt die Schritte, die Sie ergreifen können, um die Konfiguration der namensauflösung, wenn Sie einen Verbundserverproxy in Ihrem Umkreisnetzwerk platzieren. Um die erforderlichen Schritte zu bestimmen, ermitteln Sie zunächst, welches der folgenden DNS-Szenarien am ehesten der DNS-Infrastruktur im Umkreisnetzwerk Ihrer Organisation entspricht. Befolgen Sie dann die Schritte für das jeweilige Szenario.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>DNS-Zone nur für das Umkreisnetzwerk  
In diesem Szenario verfügt Ihre Organisation über ein oder zwei DNS-Zonen im Umkreisnetzwerk, ohne dass Ihre Organisation DNS-Zonen im Internet kontrolliert. Erfolgreiche namensauflösung für einen Verbundserverproxy in der DNS-Zone, die nur das umkreisnetzwerkszenario hängt von folgenden Bedingungen ab:  
  
-   Der Verbundserverproxy müssen eine Einstellung in der Datei "Hosts" auf den vollqualifizierten Domänennamen auflösen \(FQDN\) von Verbund-Serverendpunkt-URL, IP-Adresse eines Verbundservers oder einen Verbund-Server-Cluster.  
  
-   DNS im Umkreisnetzwerk des Kontopartners muss konfiguriert werden, sodass die FQDN des der Verbund-Serverendpunkt-URL in die IP-Adresse des Verbundserverproxys aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird. In dieser Abbildung ist die Microsoft-Netzwerklastenausgleich \(NLB\) -Technologie bietet eine einzelne Cluster-FQDN und eine einzelne IP-Adresse für einen vorhandenen Verbundserverfarm.  
  
![Anforderungen an den](media/adfs2_deploy_single_fs.gif)  
  
Weitere Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-FQDN mit NLB finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. Konfigurieren der "Hosts"-Datei für den Verbundserverproxy  
Da DNS im Umkreisnetzwerk konfiguriert ist, um alle Anforderungen für "FS.Fabrikam.com" in der Konto-Verbundserverproxy aufzulösen, enthält der Konto-Partner-Verbundserverproxy einen Eintrag in die lokale Hosts-Datei zum Auflösen von "FS.Fabrikam.com" in die IP-Adresse der tatsächliche Kontoverbundserver \(oder DNS-Namen für die Verbundserverfarm\) , mit dem Unternehmensnetzwerk verbunden ist. Dadurch kann für die Konto-Verbundserverproxy, den Host Name "FS.Fabrikam.com" zu der Kontoverbundserver anstatt in sich selbst zu beheben, würde passieren, wenn es versucht, "FS.Fabrikam.com" mithilfe des Umkreis-DNS nachzuschlagen –, damit der Verbund Server-Proxy kann mit der Verbundserver kommunizieren.  
  
### <a name="2-configure-perimeter-dns"></a>2. Konfigurieren des Umkreis-DNS  
Da ist es nur ein einzelner AD FS Hostnamen an, an die Clientcomputer geleitet werden, gibt an, ob sie in einem Intranet oder im Internet sind –-Clientcomputern im Internet, die den Umkreis-DNS-Server verwenden, müssen den FQDN der Kontoverbundserver aufgelöst\("FS.Fabrikam.com"\) auf die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk. Damit es beim Versuch, "FS.Fabrikam.com" aufzulösen Clients an die Kontoverbundserverproxy weiterleiten kann, enthält das Umkreis-DNS eine begrenzte "corp.Fabrikam.com" DNS-Zone mit einem einzelnen Host \(ein\) -Ressourceneintrag für die fs \("FS.Fabrikam.com"\) und die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk.  
  
Weitere Informationen zum Ändern der Hosts-Datei der Verbundserverproxys und Konfigurieren von DNS im Umkreisnetzwerk finden Sie unter [Konfigurieren der namensauflösung für a Federation Server Proxy in einer DNS-Zone, die ausschließlich das Umkreisnetzwerkdient.](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md).  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>DNS-Zone für das Umkreisnetzwerk und Internetclients  
In diesem Szenario kontrolliert Ihre Organisation die DNS-Zone im Umkreisnetzwerk und mindestens eine DNS-Zone im Internet. Erfolgreiche namensauflösung für einen Verbundserverproxy in diesem Szenario hängt von folgenden Bedingungen ab:  
  
-   DNS in der Internetzone des Kontopartners muss konfiguriert sein, sodass der FQDN des Hostnamens Federation Server in die IP-Adresse des Verbundserverproxys im Umkreisnetzwerk aufgelöst wird.  
  
-   DNS im Umkreisnetzwerk des Kontopartners muss konfiguriert werden, damit der FQDN des Hostnamens Federation Server in die IP-Adresse des Verbundservers im Unternehmensnetzwerk aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird.  
  
![Anforderungen an den](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. Konfigurieren des Umkreis-DNS  
Für dieses Szenario, da davon ausgegangen wird, wird die Internet-DNS-Zone zu konfigurieren, Sie-Steuerelement zum Auflösen anfordert, die für einen bestimmten Endpunkt-URL hergestellt werden \(, also "FS.Fabrikam.com"\) auf dem Verbundserverproxy in der Umkreisnetzwerk, müssen Sie auch die Zone im Umkreisnetzwerk-DNS zum Weiterleiten dieser Anforderungen an den Verbundserver im Unternehmensnetzwerk konfigurieren.  
  
Damit Clients an der Kontoverbundserver weitergeleitet werden können, wenn sie versuchen, "FS.Fabrikam.com" aufzulösen, ist der Umkreis-DNS mit einem einzelnen Host konfiguriert \(ein\) -Ressourceneintrag für die fs \("FS.Fabrikam.com"\) und die IP-Adresse der Kontoverbundserver mit dem Unternehmensnetzwerk verbunden. Dies ermöglicht es der Konto-Verbundserverproxy, den Host Name "FS.Fabrikam.com" zu der Kontoverbundserver anstatt in sich selbst zu beheben, würde passieren, wenn es versucht, "FS.Fabrikam.com" mithilfe von Internet-DNS nachzuschlagen –, damit der Verbundserver Proxy kann mit dem Verbundserver kommunizieren.  
  
### <a name="2-configure-internet-dns"></a>2. Konfigurieren von Internet-DNS  
Damit die Namensauflösung in diesem Szenario erfolgreich ist, müssen alle Anforderungen von Clientcomputern im Internet an "fs.fabrikam.com" von der von Ihnen kontrollierten Internet-DNS-Zone aufgelöst werden. Daher müssen Sie Ihre Internet-DNS-Zone zum Weiterleiten von Clientanforderungen für "FS.Fabrikam.com" an die IP-Adresse des Kontos Verbundserverproxys im Umkreisnetzwerk konfigurieren.  
  
Weitere Informationen dazu, wie Sie das Umkreisnetzwerk und der Internet-DNS-Zonen ändern, finden Sie unter [Konfigurieren der namensauflösung für einen Verbundserverproxy in einer DNS-Zone, dient sowohl Umkreisnetzwerk und Internetclients](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
