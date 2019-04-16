---
title: Migrieren des AD FS 2.0-Verbundservers
description: "Enthält Informationen zum Migrieren eines AD FS-Servers zu Windows Server 2012 R2."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a3e8e444f715fe2ae0f0ccd858d90e8664be00c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2017
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>Überprüfen Sie die AD FS 2.0-Migration zu Windows Server 2012 R2

Nachdem Sie dieselbe Servermigration der Active Directory-Verbunddienste (AD FS) Farm zu Windows Server 2012 R2 abgeschlossen haben, können Sie das folgende Verfahren, um sicherzustellen, dass der Verbundserver in Ihrer Farm betriebsbereit sind; d. h., dass alle Clients im gleichen Netzwerk Ihre Federtation Server erreichen kann.  
  
Mitgliedschaft in **Benutzer**, **Sicherungsoperatoren**, **Hauptbenutzer**, **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer ist mindestens erforderlich, um dieses Verfahren ausführen.
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>Um sicherzustellen, dass ein Verbundserver betriebsbereit ist  
  
1.  Öffnen Sie ein Browserfenster und geben Sie in der Adressleiste den Namen des Federation Server fügen sie `federationmetadata/2007-06/federationmetadata.xml` um zum Endpunkt verbunddienstmetadaten zu navigieren. Z. B. `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` .  
  
Wenn Sie im Browserfenster die verbundservermetadaten ohne SSL-Fehler oder Warnungen sehen, ist der Verbundserver betriebsbereit.  
  
2.  Sie können auch suchen, um die AD FS-Anmeldeseite (Ihr verbunddienstname mit der angehängten `adfs/ls/idpinitiatedsignon.htm`, z. B. `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`).  Hiermit wird der AD FS-Anmeldeseite, in dem Sie sich mit Domänenadministrator-Anmeldeinformationen anmelden können.  
  
> [!IMPORTANT]
>  Achten Sie darauf, konfigurieren Sie die Browsereinstellungen der verbundserverrolle vertraut wird den verbunddienstnamen (z. B. `https://fs.contoso.com`) im Browser auf die lokale Intranetzone.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)  
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
