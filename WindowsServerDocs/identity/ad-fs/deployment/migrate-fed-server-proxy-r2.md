---
title: Migrieren der AD FS 2.0-Verbundserver-Proxyservers
description: Enthält Informationen zur Migration von AD FS-Proxy-Server zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a2eb6c670e704564bed49486b8950dab96da8a80
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444568"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Migrieren von Active Directory Federation Services-Proxy-Server zu Windows Server 2012 R2

In Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2 erfolgt die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy. In Windows Server 2012 R2 können Sie zum Aktivieren von AD FS für Zugriff von außerhalb des Unternehmensnetzwerks, eine oder mehrere Webanwendungsproxys bereitstellen. Jedoch können kein Verbundserverproxys unter Windows Server 2008 R2 oder Windows Server 2012 auf einem Webanwendungsproxy unter Windows Server 2012 R2 migriert werden.  
  
> [!IMPORTANT]
>  Die Migration eines Verbundserverproxys unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 auf einem Webanwendungsproxy unter Windows Server 2012 R2 wird nicht unterstützt.  
  
Wenn Sie AD FS in einer migrierten Windows Server 2012 R2-Farm für den Extranetzugriff zu konfigurieren möchten, müssen Sie eine neue Bereitstellung der einen oder mehrere Webanwendungsproxy-Computer als Teil der AD FS-Infrastruktur ausführen.  
  
Wenn Sie die Bereitstellung eines Webanwendungsproxys planen, lesen Sie die Informationen in den folgenden Themen:  
  
- [Planen der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383648.aspx)  
  
- [Planen Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
  Sie können zum Bereitstellen eines Webanwendungsproxys die Schritte in den folgenden Themen ausführen:  
  
- [Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383644.aspx)  
  
- [Installieren Sie und konfigurieren Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx)  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services für Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)    
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)

