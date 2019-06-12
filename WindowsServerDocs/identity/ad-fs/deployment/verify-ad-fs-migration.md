---
title: Migrieren der AD FS 2.0-Verbundservers
description: Enthält Informationen zur Migration von AD FS-Server zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 38e44ab2f803d8ec8940dbba7574a9f37389112a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444463"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>Überprüfen Sie die AD FS 2.0-Migration zu Windows Server 2012 R2

Nachdem Sie dieselbe Servermigration der Active Directory-Verbunddienst (AD FS) für Windows Server 2012 R2-Farm abgeschlossen haben, können Sie das folgende Verfahren, um sicherzustellen, dass der Verbundserver in Ihrer Farm betriebsbereit sind; d. h., dass Ihre Server Federtation für jeden Client im selben Netzwerk erreichbar.  
  
Zum Abschließen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Benutzer**, **Sicherungs-Operatoren**, **Hauptbenutzer**, **Administratoren** oder in einer anderen entsprechenden Gruppe auf dem lokalen Computer erforderlich.
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>So überprüfen Sie, ob ein Verbundserver betriebsbereit ist  
  
1.  Öffnen Sie ein Browserfenster und geben Sie in der Adressleiste den Namen der Verbund-Server und fügen sie `federationmetadata/2007-06/federationmetadata.xml` um zum Endpunkt verbunddienstmetadaten zu navigieren. Z. B. `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` .  
  
Werden im Browserfenster die Verbundservermetadaten ohne SSL-Fehler oder -Warnungen angezeigt, ist der Verbundserver betriebsbereit.  
  
2. Sie können auch zur AD FS-Anmeldeseite (Ihr Verbunddienstname, an den `adfs/ls/idpinitiatedsignon.htm` angehängt wird, z. B. `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`) navigieren.  Dadurch wird die AD FS-Anmeldeseite angezeigt, auf der Sie sich mit Domänenadministrator-Anmeldeinformationen anmelden können.  
  
> [!IMPORTANT]
>  Die Browsereinstellungen müssen so konfiguriert werden, dass der Verbundserverrolle vertraut wird. Fügen Sie dazu der Zone %%amp;quot;Lokales Intranet%%amp;quot; des Browsers den Verbunddienstnamen (z. B. `https://fs.contoso.com`) hinzu.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services für Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)  
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
