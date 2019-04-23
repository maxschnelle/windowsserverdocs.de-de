---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: Rolle des Attributspeichers
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 730411ed7efbb9cf0db3d7e94a486cec4c363849
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860411"
---
 >Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-attribute-stores"></a>Rolle des Attributspeichers
Active Directory Federation Services verwendet den Begriff "Attributspeicher" zum Verweisen auf Verzeichnisse und Datenbanken, in denen eine Organisation ihre Benutzerkonten und deren zugeordnete Attributwerte zu speichern. Sobald er in einer identitätsanbieterorganisation konfiguriert ist, wird AD FS diese Attributwerte aus dem Speicher abruft und erstellt basierend auf diesen Informationen, damit eine Webanwendung oder Dienst, der in der Organisation einer vertrauenden Seite gehostet wird die entsprechende kann Ansprüche Autorisierung Entscheidungen zu treffen, wenn ein Verbundbenutzer \(eines Benutzers, dessen Konto sich in der identitätsanbieterorganisation befindet\) versucht, auf die Anwendung oder den Dienst zuzugreifen.  
  
Weitere Informationen zum Generieren von Ansprüchen finden Sie unter [The Role of Claims](The-Role-of-Claims.md).  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>Auswirkungen von Attributspeichern auf Ihre AD FS-Bereitstellungsziele  
Den Speicherort des benutzerattributspeichers und den Speicherort, der von der Authentifizierung von Benutzern bestimmen, wie Sie AD FS zur Unterstützung der Benutzeridentitäten entwerfen. Je nachdem, wo sich der Attributspeicher befindet und, in dem Benutzer die Anwendung zugreifen \(in einem Intranet oder im Internet\), können Sie eine der folgenden Bereitstellungsziele verwenden:  
  
-   [Geben Sie Ihre Active Directory Users Access auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](https://technet.microsoft.com/library/dd807071.aspx)– bei diesem Ziel Benutzer in Ihrer Organisation Zugriff auf eine AD FS-gesicherte Anwendung oder ein Dienst \(entweder Ihre eigene Anwendung oder Ihren Dienst oder ein Anwendung oder ein Dienst des Partners\) Wenn der Benutzer angemeldet sind in Active Directory im Unternehmensintranet.  
  
-   [Geben Sie auf die Anwendungen und Dienste von anderen Organisationen Ihrer Active Directory Users Access](https://technet.microsoft.com/library/dd807123.aspx)– bei diesem Ziel Benutzer in Ihrer Organisation Zugriff auf eine AD FS-gesicherte Anwendung oder ein Dienst \(entweder Ihre eigene Anwendung oder Ihren Dienst oder ein Anwendung oder ein Dienst des Partners\) Wenn der Benutzer angemeldet sind einem Attributspeicher im Unternehmensintranet und wenn sie sich Remote über das Internet anmelden.  
  
-   [Geben Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](https://technet.microsoft.com/library/dd807099.aspx)– bei diesem Ziel Benutzerkonten in einer anderen Organisation, die in einem Attributspeicher im Unternehmensintranet dieser Organisation befinden müssen Zugriff auf eine AD FS: gesicherte Anwendung in Ihrer Organisation. Dieses Ziel kann auch beim Consumer\-basierend Benutzerkonten, die in einem Attributspeicher im Umkreisnetzwerk Ihrer Organisation befinden müssen mit Zugriff auf einer AD FS-gesicherte Anwendung in Ihrer Organisation bereitgestellt werden.  
  
Abhängig von der Platzierung und andere Anforderungen Ihrer Organisation können Sie mehrere dieser Bereitstellungsziele, um den Entwurf von AD FS-Bereitstellung abzuschließen kombinieren.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>Von AD FS unterstützte Attributspeicher  
AD FS unterstützt eine Vielzahl von Verzeichnis und die Datenbank werden gespeichert, Sie verwenden können, für das Extrahieren von Administrator\-definierten Attributwerten und Auffüllen von Ansprüchen mit diesen Werten. AD FS unterstützt die folgenden Verzeichnisse oder Datenbanken als Attributspeicher:  
  
-   Active Directory unter WindowsServer 2003 Active Directory-Domänendienste \(AD DS\) in WindowsServer 2008, AD DS unter Windows Server 2012 und 2012 R2 und WindowsServer 2016. 
  
-   Alle Editionen von Microsoft SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014 und SQL Server 2016  
  
-   Benutzerdefinierte Attributspeicher  
  

