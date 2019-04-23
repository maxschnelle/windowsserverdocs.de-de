---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: Verbundserverfarm mit WID
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bb4e5f88f3d62511b185a2b4317416169717c860
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851401"
---
# <a name="federation-server-farm-using-wid"></a>Verbundserverfarm mit WID

>Gilt für: Windows Server 2012

Die Standardtopologie für Active Directory Federation Services \(AD FS\) eine Verbundserverfarm unter Verwendung der internen Windows-Datenbank ist \(WID\), bestehen, die bis zu fünf Verbundserver Hosten Ihrer Verbunddienst der Organisation. In dieser Topologie verwendet die AD FS WID als Speicher für die AD FS-Konfigurationsdatenbank für alle Verbundserver, die mit der betreffenden Farm verbunden sind. Die Verbunddienstdaten in der Konfigurationsdatenbank werden von der Farm auf alle Server der Farm repliziert und dort verwaltet.  
  
Beim Erstellen des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt. Bei Verwendung von WID für die AD FS-Konfigurationsdatenbank des ersten Verbundservers, die Sie in der Farm zu erstellen als bezeichnet die *primärer Verbundserver*. Dies bedeutet, dass dieser Computer, mit der ein Lesevorgang konfiguriert ist\/Kopie der AD FS-Konfigurationsdatenbank zu schreiben.  
  
Alle anderen Verbundserver, die Sie für diese Farm zu konfigurieren, werden als bezeichnet *sekundäre Verbundserver* , da sie keine Änderungen repliziert werden müssen, die auf dem primären Verbundserver für die Lese-vorgenommen werden\-nur Kopien der AD FS-Konfigurationsdatenbank, die sie lokal speichern.  
  
> [!NOTE]  
> Wir empfehlen die Verwendung von mindestens zwei Verbundserver in einem Auslastungstestszenario\-ausgeglichene Konfiguration.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnitt beschreibt verschiedene Überlegungen zu den Zielgruppe, Vorteile und Einschränkungen, die mit dieser Bereitstellungstopologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die zum Bereitstellen ihrer internen Benutzer benötigen \(auf den Computern, die physisch mit dem Unternehmensnetzwerk verbunden sind, protokolliert\) mit Einmaliger Anmeldung\-auf \(SSO\) Zugriff auf verbundanwendungen oder-Dienste  
  
-   Organisationen, die internen Benutzer SSO-Zugriff auf Microsoft Online Services oder Microsoft Office 365 ermöglichen möchten  
  
-   Kleinere Organisationen, die redundante, skalierbare Dienste erfordern  
  
> [!NOTE]  
> Organisationen mit größeren Datenbanken sollten mit den [Federation Server Farm mithilfe von SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Bereitstellungstopologie, die später in diesem Abschnitt beschrieben wird. Organisationen mit Benutzern, die sich von außerhalb des Netzwerks sollten entweder die [Federation Server Farm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md) Topologie oder [Federation Server Farm mithilfe von SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Topologie.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Bietet SSO-Zugriff auf interne Benutzer  
  
-   Daten und der Verbunddienst Redundanz \(jedes Verbundservers Änderungen repliziert werden, an andere Verbundserver in der gleichen Farm\)  
  
-   Die Farm kann horizontal hochskaliert werden, indem Sie bis zu fünf Verbundserver hinzufügen  
  
-   WID ist in Windows enthalten. aus diesem Grund nicht erforderlich, die SQL Server zu erwerben  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Einschränkungen bei der Verwendung dieser Topologie?  
  
-   Eine WID-Farm verfügt über maximal fünf Verbundserver. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md).  
  
-   Eine WID-Farm unterstützt keine token-Replay-Erkennung oder Artefakt Auflösung \(Teil der Security Assertion Markup Language \(SAML\) Protokoll\).  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Server Platzierung und Netzwerk-Layout-Empfehlungen  
Wenn Sie die Startzeit der Bereitstellung dieser Topologie in Ihrem Netzwerk bereit sind, sollten Sie auf das Platzieren aller von den Verbundservern im Unternehmensnetzwerk hinter einem Netzwerklastenausgleich \(NLB\) Host, der für einen NLB-Cluster konfiguriert werden kann mit dediziertem Cluster Domain Name System \(DNS\) und Cluster-IP-Adresse.  
  
> [!NOTE]  
> Dieser DNS-Clustername muss den Namen des Verbunddiensts, z. B. "FS.Fabrikam.com" übereinstimmen.  
  
Der NLB-Host können die Einstellungen, die in diesem NLB-Cluster auf Clientanforderungen an den einzelnen Verbundservern zugeordnet definiert sind. Die folgende Abbildung zeigt, wie das fiktive Unternehmen Fabrikam, Inc. die erste Phase der Bereitstellung über ein einrichtet\-Computer Verbundserverfarm \(fs1 und fs2\) mit WID und die Positionierung eines DNS-Servers und eines einzelnen NLB-Hosts, das mit dem Unternehmensnetzwerk verbunden ist.  
  
![Serverfarm mit WID](media/FarmWID.gif)  
  
> [!NOTE]  
> Wenn ein Fehler auf dieses einzelnen NLB-Hosts vorhanden ist, werden Benutzer nicht auf verbundanwendungen oder-Dienste zugreifen. Fügen Sie weitere NLB-Hosts hinzu, wenn Ihre Geschäftsanforderungen eine einzelne Fehlerquelle nicht zulassen.  
  
Weitere Informationen dazu, wie Sie Ihre Netzwerkumgebung für die Verwendung mit dem Verbundserver konfigurieren zu können, finden Sie unter [Namensauflösungsanforderungen für Verbundserver](Name-Resolution-Requirements-for-Federation-Servers.md) in AD FS-Entwurfshandbuch.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
