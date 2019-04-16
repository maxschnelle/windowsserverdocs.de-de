---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: Die Rolle des Attributspeichers
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 730411ed7efbb9cf0db3d7e94a486cec4c363849
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
 >Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-attribute-stores"></a>Die Rolle des Attributspeichers
Active Directory Federation Services verwendet den Begriff "Attributspeicher" bezieht sich auf Verzeichnisse oder Datenbanken, die eine Organisation verwendet werden, um ihre Benutzerkonten und deren zugeordnete Attributwerte zu speichern. Nach der Konfiguration in einer identitätsanbieterorganisation ruft diese Attributwerte aus dem Store und erstellt Ansprüche basierend auf diese Informationen, sodass eine Anwendung oder einen Dienst, der in einer Organisation der vertrauenden Seite gehostet wird der entsprechende Autorisierungsentscheidungen treffen, wenn ein Verbundbenutzer kann AD FS \ (ein Benutzer, dessen Konto befindet sich in der Organization\ Identity Provider) auf die Anwendung oder den Dienst zuzugreifen versucht.  
  
Weitere Informationen zum Generieren von Ansprüchen finden Sie unter [The Role of Claims](The-Role-of-Claims.md).  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>Wie attributspeichern der AD FS-Bereitstellungsziele  
Der Speicherort des benutzerattributspeichers und der Speicherort, von dem Benutzer authentifizieren sich, bestimmen, wie Sie AD FS zur Unterstützung der Benutzeridentitäten entwerfen. Je nachdem, wo sich die Attributspeicher befindet und, in denen Benutzer die Anwendung zugreifen \ (in einem Intranet oder auf der möglicherweise), können Sie eine der folgenden Bereitstellungsziele verwenden:  
  
-   [Ermöglichen der Active Directory Users Access Your Claims-Aware Applications and Services](https://technet.microsoft.com/library/dd807071.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation Zugriff auf eine AD FS-gesicherte Anwendung oder ein Dienst \ (eigene Anwendung oder Dienst oder eines Partners Anwendung oder Dienst eines Drittanbieters\) Wenn der Benutzer angemeldet sind auf in Active Directory im Unternehmensintranet.  
  
-   [Bereitstellen der Active Directory Users Access auf die Anwendungen und Dienste von anderen Organisationen](https://technet.microsoft.com/library/dd807123.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation Zugriff auf eine AD FS-gesicherte Anwendung oder ein Dienst \ (eigene Anwendung oder Dienst oder eines Partners Anwendung oder Dienst eines Drittanbieters\) Wenn die Benutzer bei einem Attributspeicher im Unternehmensintranet und wenn sie sich Remote über das Internet anmelden angemeldet sind.  
  
-   [Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](https://technet.microsoft.com/library/dd807099.aspx)– bei diesem Ziel müssen Benutzerkonten in einer anderen Organisation, die in einem Attributspeicher im Unternehmensintranet dieser Organisation befinden, eine AD FS-gesicherte Anwendung in Ihrer Organisation zugreifen. Dieses Ziel funktioniert auch, wenn Consumer\-basierte Benutzerkonten, die sich in einem Attributspeicher im Umkreisnetzwerk Ihrer Organisation befinden Zugriff für einer AD FS-gesicherte Anwendung in Ihrer Organisation bereitgestellt werden müssen.  
  
Je nach Attribut Platzierung und anderen Anforderungen Ihrer Organisation können Sie mehrere dieser Bereitstellungsziele Entwurfs Ihrer AD FS-Bereitstellung kombinieren.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>Attributspeicher, die von AD FS unterstützt werden  
AD FS unterstützt eine Vielzahl von Directory und Datenbank speichert, können Sie zum Extrahieren von Administrator\ definierten Attributwerte und zum Auffüllen der Ansprüche mit diesen Werten verwenden. AD FS unterstützt die folgenden Verzeichnisse oder Datenbanken als Attributspeicher:  
  
-   Active Directory in Windows Server 2003, Active Directory Domain Services \(AD DS\) in Windows Server 2008, AD DS in Windows Server2012 und 2012 R2 und Windows Server 2016. 
  
-   Alle Editionen von Microsoft SQL Server2005, SQL Server2008, SQL Server2012, SQL Server2014 und SQL Server2016  
  
-   Benutzerdefinierte Attributspeicher  
  

