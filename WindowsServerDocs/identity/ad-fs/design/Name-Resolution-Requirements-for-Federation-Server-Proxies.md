---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: Namensauflösungsanforderungen für Verbundserverproxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 540b58c6fe150e5d8781b1d23e97a3efcdf6c43d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959802"
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>Namensauflösungsanforderungen für Verbundserverproxys

Wenn Client Computer im Internet versuchen, auf eine Anwendung zuzugreifen, die durch Active Directory-Verbunddienste (AD FS) AD FS gesichert ist \( \) , müssen Sie sich zuerst beim Verbund Server authentifizieren. In den meisten Fällen ist der Verbund Server in der Regel nicht direkt über das Internet zugänglich. Daher müssen Internet Client Computer stattdessen an den Verbund Server Proxy umgeleitet werden. Sie können eine erfolgreiche Umleitung erreichen, indem Sie die entsprechenden Domain Name System \( DNS- \) Einträge zu Ihrer DNS-Zone oder ihren Zonen hinzufügen, die dem Internet überstehen.  
  
Die Methode, die Sie zum Umleiten von Internet Clients an den Verbund Server Proxy verwenden, hängt davon ab, wie Sie die DNS-Zone in Ihrem Umkreis Netzwerk konfigurieren, oder wie Sie eine DNS-Zone konfigurieren, die Sie im Internet steuern. Verbundserverproxys sind zur Verwendung in einem Umkreisnetzwerk vorgesehen. Sie leiten Internet Client Anforderungen nur dann erfolgreich an Verbund Server weiter, wenn DNS in allen von Ihnen kontrollierten Zonen mit Internet Zugriff ordnungsgemäß konfiguriert wurde \- . Daher ist die Konfiguration Ihrer Zonen mit Internet Zugriff – unabhängig davon, \- ob Sie über eine DNS-Zone verfügen, die nur das Umkreis Netzwerk oder eine DNS-Zone für das Umkreis Netzwerk und Internet Clients bedient – wichtig.  
  
In diesem Thema werden die Schritte beschrieben, die Sie ausführen können, um die Namensauflösung zu konfigurieren, wenn Sie einen Verbund Server Proxy in Ihrem Umkreis Netzwerk platzieren. Um die erforderlichen Schritte zu bestimmen, ermitteln Sie zunächst, welches der folgenden DNS-Szenarien am ehesten der DNS-Infrastruktur im Umkreisnetzwerk Ihrer Organisation entspricht. Befolgen Sie dann die Schritte für das jeweilige Szenario.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>DNS-Zone nur für das Umkreisnetzwerk  
In diesem Szenario verfügt Ihre Organisation über ein oder zwei DNS-Zonen im Umkreisnetzwerk, ohne dass Ihre Organisation DNS-Zonen im Internet kontrolliert. Die erfolgreiche Namensauflösung für einen Verbund Server Proxy in der DNS-Zone, die nur dem Umkreis Netzwerkszenario dient, hängt von den folgenden Bedingungen ab:  
  
-   Der Verbund Server Proxy muss über eine Einstellung in der Hosts-Datei verfügen, um den voll qualifizierten Domänen Namen- \( FQDN \) der Verbund Server-Endpunkt-URL in eine IP-Adresse eines Verbund Servers oder eines Verbund Server Clusters aufzulösen.  
  
-   Das DNS im Umkreis Netzwerk des Konto Partners muss so konfiguriert werden, dass der FQDN der Verbund Server-Endpunkt-URL in die IP-Adresse des Verbund Server Proxys aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird. In dieser Abbildung stellt die NLB-Technologie des Microsoft-Netzwerk Lastenausgleichs \( \) einen einzelnen Cluster-voll qualifizierten Namen und eine einzelne Cluster-IP-Adresse für eine vorhandene Verbund Serverfarm bereit.  
  
![namens Anforderungen](media/adfs2_deploy_single_fs.gif)  
  
Weitere Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-voll qualifizierten Daten Controllers mithilfe von NLB finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. Konfigurieren der "Hosts"-Datei für den Verbundserverproxy  
Da DNS im Umkreis Netzwerk so konfiguriert ist, dass alle Anforderungen von FS.fabrikam.com an den Konto Verbund Server Proxy aufgelöst werden, verfügt der Verbund Server Proxy des Konto Partners über einen Eintrag in der lokalen Hosts-Datei, um FS.fabrikam.com auf die IP-Adresse des tatsächlichen Konto Verbund Servers \( oder des DNS-Cluster namens für die Verbund Serverfarm zu beheben, die \) mit dem Unternehmensnetzwerk verbunden ist. Dies ermöglicht es dem Konto Verbund Server Proxy, den Hostnamen fs.fabrikam.com auf den Konto Verbund Server und nicht in sich selbst zu lösen – wie beim Versuch, FS.fabrikam.com mithilfe des Umkreis-DNS – zu suchen, sodass der Verbund Server Proxy mit dem Verbund Server kommunizieren kann.  
  
### <a name="2-configure-perimeter-dns"></a>2. Konfigurieren des Umkreis-DNS  
Da es nur einen einzigen AD FS Hostnamen gibt, zu dem Client Computer geleitet werden – ob Sie sich in einem Intranet oder Internet befinden – müssen Client Computer im Internet, die den Umkreis-DNS-Server verwenden, den FQDN für den Konto \( Verbund Server FS.fabrikam.com \) in die IP-Adresse des Konto Verbund Server Proxys im Umkreis Netzwerk auflösen. Damit Clients beim Auflösen von FS.fabrikam.com an den Konto Verbund Server Proxy weiterleiten können, enthält der Umkreis-DNS eine eingeschränkte Corp.fabrikam.com-DNS-Zone mit einem einzelnen Host \( einen \) Ressourcen Daten Satz für FS \( FS.fabrikam.com \) und die IP-Adresse des Konto Verbund Server Proxys im Umkreis Netzwerk.  
  
Weitere Informationen zum Ändern der Hosts-Datei des Verbund Server Proxys und Konfigurieren von DNS im Umkreis Netzwerk finden Sie unter [Konfigurieren der Namensauflösung für einen Verbund Server Proxy in einer DNS-Zone, die nur dem Umkreis Netzwerk dient](../deployment/configure-name-resolution-for-federation-server-proxy-in-dns-zone-serving-only-perimeter-network.md).  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>DNS-Zone für das Umkreisnetzwerk und Internetclients  
In diesem Szenario kontrolliert Ihre Organisation die DNS-Zone im Umkreisnetzwerk und mindestens eine DNS-Zone im Internet. Die erfolgreiche Namensauflösung eines Verbund Server Proxys in diesem Szenario hängt von den folgenden Bedingungen ab:  
  
-   DNS in der Internet Zone des Konto Partners muss so konfiguriert werden, dass der FQDN des Verbund Server-Host namens in die IP-Adresse des Verbund Server Proxys im Umkreis Netzwerk aufgelöst wird.  
  
-   Das DNS im Umkreis Netzwerk des Konto Partners muss so konfiguriert werden, dass der FQDN des Verbund Server-Host namens in die IP-Adresse des Verbund Servers im Unternehmensnetzwerk aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird.  
  
![namens Anforderungen](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. Konfigurieren des Umkreis-DNS  
In diesem Szenario wird davon ausgegangen, dass Sie die Internet-DNS-Zone konfigurieren, die Sie für die Auflösung von Anforderungen konfigurieren, die für eine bestimmte Endpunkt-URL ( \( FS.fabrikam.com \) to the Federation Server Proxy im Umkreis Netzwerk) erfolgt sind. Außerdem müssen Sie die Zone im Umkreis Netzwerk konfigurieren, um diese Anforderungen an den Verbund Server im Unternehmensnetzwerk weiterzuleiten.  
  
Damit Clients an den Konto Verbund Server weitergeleitet werden können, wenn Sie versuchen, FS.fabrikam.com aufzulösen, wird Umkreis-DNS mit einem einzelnen Host \( a \) -Ressourcen Daten Satz für FS \( FS.fabrikam.com \) und der IP-Adresse des Konto Verbund Servers im Unternehmensnetzwerk konfiguriert. Dies ermöglicht es dem Konto Verbund Server Proxy, den Hostnamen fs.fabrikam.com auf den Konto Verbund Server und nicht in sich selbst zu lösen – wie bei der Suche nach FS.fabrikam.com mithilfe von Internet DNS –, damit der Verbund Server Proxy mit dem Verbund Server kommunizieren kann.  
  
### <a name="2-configure-internet-dns"></a>2. Konfigurieren von Internet-DNS  
Damit die Namensauflösung in diesem Szenario erfolgreich ist, müssen alle Anforderungen von Clientcomputern im Internet an "fs.fabrikam.com" von der von Ihnen kontrollierten Internet-DNS-Zone aufgelöst werden. Folglich müssen Sie die Internet-DNS-Zone so konfigurieren, dass Client Anforderungen für FS.fabrikam.com an die IP-Adresse des Konto-Verbund Server Proxys im Umkreis Netzwerk weiterleiten werden.  
  
Weitere Informationen zum Ändern des Umkreis Netzwerks und der Internet-DNS-Zonen finden Sie unter [Konfigurieren der Namensauflösung für einen Verbund Server Proxy in einer DNS-Zone, die sowohl das Umkreis Netzwerk als auch Internet Clients bedient](../deployment/configure-name-resolution-for-federation-server-proxy-in-dns-zone-serving-only-perimeter-network.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
