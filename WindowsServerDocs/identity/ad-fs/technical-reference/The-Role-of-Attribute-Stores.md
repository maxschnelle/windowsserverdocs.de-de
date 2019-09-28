---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: Rolle des Attributspeichers
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0a1543f2c935c2ef76ea014567b18bfc778c7401
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407380"
---
# <a name="the-role-of-attribute-stores"></a>Rolle des Attributspeichers
Active Directory-Verbunddienste (AD FS) verwendet den Begriff "Attribut Speicher", um auf Verzeichnisse oder Datenbanken zu verweisen, die in einer Organisation zum Speichern der Benutzerkonten und der zugehörigen Attributwerte verwendet werden. Nach der Konfiguration in einer Identitäts Anbieter Organisation ruft AD FS diese Attributwerte aus dem Speicher ab und erstellt Ansprüche basierend auf diesen Informationen, damit eine Webanwendung oder ein Dienst, der in einer Organisation der vertrauenden Seite gehostet wird, das entsprechende Autorisierungs Entscheidungen, wenn ein Verbund \(Benutzer ein Benutzer ist, dessen Konto in der Identitäts Anbieter\) Organisation gespeichert ist, versucht, auf die Anwendung oder den Dienst zuzugreifen.  
  
Weitere Informationen zum Generieren von Ansprüchen finden Sie unter [The Role of Claims](The-Role-of-Claims.md).  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>Auswirkungen von Attributspeichern auf Ihre AD FS-Bereitstellungsziele  
Der Speicherort des Benutzer Attribut Speicher und der Speicherort, von dem die Benutzer authentifizieren, legen fest, wie Sie AD FS zur Unterstützung der Benutzer Identitäten entwerfen. Abhängig vom Speicherort des Attribut Speicher und von dem Benutzer, der in einem \(Intranet oder im Internet\)auf die Anwendung zugreift, können Sie eines der folgenden Bereitstellungs Ziele verwenden:  
  
-   [Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Ihre Active Directory-Benutzer](https://technet.microsoft.com/library/dd807071.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation auf eine AD FS – \(gesicherte Anwendung zu oder bedienen entweder Ihre eigene Anwendung oder ihren eigenen Dienst oder den Anwendung oder Dienst\) , wenn die Benutzer im Unternehmens Intranet bei Active Directory angemeldet sind.  
  
-   [Bereitstellen des Zugriffs auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory Benutzer](https://technet.microsoft.com/library/dd807123.aspx)– bei diesem Ziel greifen Benutzer in Ihrer Organisation auf eine AD FS – gesicherte Anwendung \(zu oder bedienen entweder Ihre eigene Anwendung oder ihren eigenen Dienst oder einen die Anwendung oder der Dienst\) des Partners, wenn die Benutzer an einem Attribut Speicher im Unternehmens Intranet angemeldet sind und sich Remote über das Internet anmelden.  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Benutzer in einer anderen Organisation](https://technet.microsoft.com/library/dd807099.aspx)– bei diesem Ziel müssen Benutzerkonten in einer anderen Organisation, die sich in einem Attribut Speicher im Unternehmens Intranet dieser Organisation befinden, auf eine AD FS zugreifen – gesicherte Anwendung in Ihrer Organisation. Dieses Ziel kann auch verwendet werden\-, wenn consumerbasierte Benutzerkonten, die sich in einem Attribut Speicher im Umkreis Netzwerk Ihrer Organisation befinden, mit Zugriff auf eine AD FS – gesicherte Anwendung in Ihrer Organisation bereitgestellt werden müssen.  
  
Abhängig von der Platzierung des Attribut Speicher und anderen Anforderungen Ihrer Organisation können Sie mehrere dieser Bereitstellungs Ziele kombinieren, um den Entwurf Ihrer AD FS Bereitstellung abzuschließen.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>Von AD FS unterstützte Attributspeicher  
AD FS unterstützt eine breite Palette an Verzeichnis-und Daten Bank speichern, die Sie zum\-Extrahieren von durch den Administrator definierten Attributwerten und Auffüllen von Ansprüchen mit diesen Werten verwenden können. AD FS unterstützt die folgenden Verzeichnisse oder Datenbanken als Attribut Speicher:  
  
-   Active Directory in Windows Server 2003, Active Directory Domain Services \(AD DS\) in Windows Server 2008, AD DS in Windows Server 2012 und 2012 R2 und Windows Server 2016. 
  
-   Alle Editionen von Microsoft SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014 und SQL Server 2016  
  
-   Benutzerdefinierte Attributspeicher  
  

