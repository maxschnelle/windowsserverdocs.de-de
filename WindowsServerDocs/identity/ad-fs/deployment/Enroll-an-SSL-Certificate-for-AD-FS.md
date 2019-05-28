---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: Registrieren eines SSL-Zertifikats für AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e80927f2670614d2949f4e67cc158319f05c5fa0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192152"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Registrieren eines SSL-Zertifikats für AD FS

Active Directory-Verbunddienste \(AD FS\) erfordert ein Zertifikat für Secure Socket Layer \(SSL\) Serverauthentifizierung auf jedem Verbundserver in Ihrer Verbundserverfarm. Das gleiche Zertifikat kann auf jedem Verbundserver in einer Farm verwendet werden. Sie müssen sowohl über das Zertifikat als auch den dazugehörigen privaten Schlüssel verfügen. Wenn Sie beispielsweise über eine PFX-Datei mit dem Zertifikat und dem privaten Schlüssel verfügen, können Sie die Datei direkt in den Konfigurations-Assistenten für Active Directory-Verbunddienste importieren. Dieses SSL-Zertifikat muss Folgendes enthalten:  
  
1.  Der Antragstellername und der alternative Antragstellername müssen den verbunddienstnamen, z. B. "FS.contoso.com" enthalten.  
  
2.  Der alternative Antragstellername muss den Wert enthalten **Enterpriseregistration** folgt den Benutzerprinzipalnamen \(UPN\) Suffix Ihrer Organisation, z. B.  **enterpriseregistration.corp.contoso.com**.  
  
    > [!WARNING]  
    > Geben Sie den alternativen Antragstellernamen aus, wenn Sie beabsichtigen, den Geräteregistrierungsdienst aktivieren \(DRS\) für Arbeitsplatzhinzufügung hinzu.  
  
> [!IMPORTANT]  
> Wenn es sich bei Ihrer Organisation mehrere UPN-Suffixe verwendet werden, und Sie DRS aktivieren möchten, muss das SSL-Zertifikat für jedes Suffix einen Eintrag Antragstellernamen alternativen Namen enthalten.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

