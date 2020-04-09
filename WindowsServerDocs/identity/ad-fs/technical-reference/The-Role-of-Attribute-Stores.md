---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: Rolle des Attributspeichers
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 595f0b3b11172df9bf95d3bb8aab90368bb0e77f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860193"
---
# <a name="the-role-of-attribute-stores"></a>Rolle des Attributspeichers
Active Directory-Verbunddienste (AD FS) verwendet den Begriff "Attribut Speicher", um auf Verzeichnisse oder Datenbanken zu verweisen, die in einer Organisation zum Speichern der Benutzerkonten und der zugehörigen Attributwerte verwendet werden. Nach der Konfiguration in einer Identitäts Anbieter Organisation ruft AD FS diese Attributwerte aus dem Speicher ab und erstellt Ansprüche basierend auf diesen Informationen, damit eine Webanwendung oder ein Dienst, der in einer Organisation der vertrauenden Seite gehostet wird, die entsprechenden Autorisierungs Entscheidungen treffen kann, wenn ein Verbund Benutzer einen Benutzer \(, dessen Konto in der Identitäts Anbieter Organisation gespeichert\) versucht, auf die Anwendung oder den Dienst zuzugreifen  
  
Weitere Informationen zum Generieren von Ansprüchen finden Sie unter [The Role of Claims](The-Role-of-Claims.md).  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>Auswirkungen von Attributspeichern auf Ihre AD FS-Bereitstellungsziele  
Der Speicherort des Benutzer Attribut Speicher und der Speicherort, von dem die Benutzer authentifizieren, legen fest, wie Sie AD FS zur Unterstützung der Benutzer Identitäten entwerfen. Abhängig vom Speicherort des Attribut Speicher und von dem Benutzer, auf den die Anwendung \(in einem Intranet oder im Internet\)zugreifen wird, können Sie eines der folgenden Bereitstellungs Ziele verwenden:  
  
-   [Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Ihre Active Directory Benutzer](https://technet.microsoft.com/library/dd807071.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation auf eine AD FS – gesicherte Anwendung oder einen Dienst \(entweder Ihre eigene Anwendung oder ihren eigenen Dienst oder die Anwendung oder den Dienst eines Partners\) wenn die Benutzer im Unternehmens Intranet Active Directory angemeldet sind.  
  
-   [Bereitstellen des Zugriffs auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory Benutzer](https://technet.microsoft.com/library/dd807123.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation auf eine AD FS – gesicherte Anwendung oder einen Dienst \(entweder Ihre eigene Anwendung oder ihren eigenen Dienst oder die Anwendung oder den Dienst eines Partners\) wenn die Benutzer in einem Attribut Speicher im Unternehmens Intranet angemeldet sind und sich Remote über das Internet anmelden.  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Benutzer in einer anderen Organisation](https://technet.microsoft.com/library/dd807099.aspx)– bei diesem Ziel müssen Benutzerkonten in einer anderen Organisation, die sich in einem Attribut Speicher im Unternehmens Intranet dieser Organisation befinden, auf eine AD FS gesicherte Anwendung in Ihrer Organisation zugreifen. Dieses Ziel kann auch verwendet werden, wenn Consumer\-basierte Benutzerkonten, die sich in einem Attribut Speicher im Umkreis Netzwerk Ihrer Organisation befinden, mit Zugriff auf eine AD FS – gesicherte Anwendung in Ihrer Organisation bereitgestellt werden müssen.  
  
Abhängig von der Platzierung des Attribut Speicher und anderen Anforderungen Ihrer Organisation können Sie mehrere dieser Bereitstellungs Ziele kombinieren, um den Entwurf Ihrer AD FS Bereitstellung abzuschließen.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>Von AD FS unterstützte Attributspeicher  
AD FS unterstützt eine breite Palette von Verzeichnis-und Daten Bank speichern, die Sie zum Extrahieren von Administrator\-definierten Attributwerten und Auffüllen von Ansprüchen mit diesen Werten verwenden können. AD FS unterstützt die folgenden Verzeichnisse oder Datenbanken als Attribut Speicher:  
  
-   Active Directory in Windows Server 2003, Active Directory Domain Services \(AD DS\) in Windows Server 2008, AD DS in Windows Server 2012 und 2012 R2 und Windows Server 2016. 
  
-   Alle Editionen von Microsoft SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014 und SQL Server 2016  
  
-   Benutzerdefinierte Attributspeicher  
  

