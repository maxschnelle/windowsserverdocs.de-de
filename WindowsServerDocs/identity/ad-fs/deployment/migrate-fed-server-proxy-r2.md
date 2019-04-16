---
title: Migrieren der AD FS 2.0-Verbundserver-Proxyserver
description: "Enthält Informationen zur Migration von eines AD FS-Proxyservers zu Windows Server 2012 R2."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 33ab29fd5efdb0bdd1fe25580e3f4434071e1c7d
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2017
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Migrieren Sie die Active Directory Federation Services Proxyserver zu Windows Server 2012 R2

In Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2 wird die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy behandelt. In Windows Server 2012 R2 können Sie zum Aktivieren von AD FS ermöglichen den Zugriff von außerhalb des Unternehmensnetzwerks eine oder mehrere Webanwendungsproxys bereitstellen. Sie können jedoch kein Verbundserverproxys unter Windows Server 2008 R2 oder Windows Server 2012 zu einem Webanwendungsproxy unter Windows Server 2012 R2 migrieren.  
  
> [!IMPORTANT]
>  Die Migration eines Verbundserverproxys unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 zu einem Webanwendungsproxy unter Windows Server 2012 R2 wird nicht unterstützt.  
  
Wenn Sie AD FS in einer migrierten Windows Server 2012 R2-Farm für extranet-Zugriff konfigurieren möchten, müssen Sie mindestens ein Webanwendungsproxy-Computer als Teil der AD FS-Infrastruktur neu bereitgestellt ausführen.  
  
Um die Bereitstellung eines Webanwendungsproxys planen, können Sie die Informationen in den folgenden Themen überprüfen:  
  
-   [Planen der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/en-us/library/dn383648.aspx)  
  
-   [Planen der Webanwendungsproxy-Servers](https://technet.microsoft.com/en-us/library/dn383647.aspx)  
  
 Zum Bereitstellen von Web Application Proxy führen Sie die Verfahren in den folgenden Themen:  
  
-   [Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/en-us/library/dn383644.aspx)  
  
-   [Installieren Sie und konfigurieren Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/en-us/library/dn383662.aspx)  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)    
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)

