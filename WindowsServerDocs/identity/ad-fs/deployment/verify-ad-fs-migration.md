---
title: Migrieren des AD FS 2,0-Verbund Servers
description: Bietet Informationen zum Migrieren eines AD FS Servers zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 024f7a586c58dcf5f0d6f9c3aa291e6bef8d838b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408185"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>Überprüfen der Migration von AD FS 2,0 zu Windows Server 2012 R2

Nachdem Sie die gleiche Servermigration Ihrer Active Directory Verbunddienst (AD FS)-Farm zu Windows Server 2012 R2 durchgeführt haben, können Sie das folgende Verfahren verwenden, um zu überprüfen, ob die Verbund Server in der Farm betriebsbereit sind. Das heißt, dass jeder Client im gleichen Netzwerk Ihre Verbund Server erreichen kann.  
  
Zum Abschließen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Benutzer**, **Sicherungs-Operatoren**, **Hauptbenutzer**, **Administratoren** oder in einer anderen entsprechenden Gruppe auf dem lokalen Computer erforderlich.
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Öffnen Sie ein Browserfenster, geben Sie in der Adressleiste den Namen der Verbund Server ein, und fügen Sie ihn dann mit `federationmetadata/2007-06/federationmetadata.xml` an, um zum Endpunkt der Verbund Dienst Metadaten zu navigieren. Beispielsweise `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml`.  
  
Werden im Browserfenster die Verbundservermetadaten ohne SSL-Fehler oder -Warnungen angezeigt, ist der Verbundserver betriebsbereit.  
  
2. Sie können auch zur AD FS-Anmeldeseite (Ihr Verbunddienstname, an den `adfs/ls/idpinitiatedsignon.htm` angehängt wird, z. B. `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`) navigieren.  Dadurch wird die AD FS-Anmeldeseite angezeigt, auf der Sie sich mit Domänenadministrator-Anmeldeinformationen anmelden können.  
  
> [!IMPORTANT]
>  Stellen Sie sicher, dass Sie die Browsereinstellungen so konfigurieren, dass Sie der Verbund Server Rolle Vertrauen, indem Sie Ihren Verbund Dienstnamen (z. b. `https://fs.contoso.com`) der lokalen Intranetzone des Browsers hinzufügen.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren Active Directory-Verbunddienste (AD FS) Rollen Dienste zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS Verbund Servers](prepare-migrate-ad-fs-server-r2.md)  
 [Migrieren des AD FS Verbund Servers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS Verbund Server Proxys](migrate-fed-server-proxy-r2.md)   
