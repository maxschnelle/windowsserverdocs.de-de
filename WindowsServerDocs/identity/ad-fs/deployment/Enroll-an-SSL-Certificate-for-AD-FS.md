---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: "Registrieren eines SSL-Zertifikats für AD FS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 12f544ad0d037c4ae7a9789238186b7ded311bdf
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Registrieren eines SSL-Zertifikats für AD FS

>Gilt für: Windows Server 2016, Windows Server2012 R2

Active Directory-Verbunddienste \(AD FS\) erfordert ein Zertifikat für die Serverauthentifizierung auf jedem Verbundserver in der Verbundserverfarm Secure Socket Layer \(SSL\). Das gleiche Zertifikat kann auf jedem Verbundserver in einer Farm verwendet werden. Sie müssen das Zertifikat und seinen privaten Schlüssel zur Verfügung haben. Wenn Sie das Zertifikat und seinen privaten Schlüssel in eine PFX-Datei verfügen, können Sie z.B. die Datei direkt in den Active Directory Federation Konfigurations-Assistenten importieren. Dieses SSL-Zertifikat muss Folgendes enthalten:  
  
1.  Der Antragstellername und der alternative Antragstellername müssen den verbunddienstnamen, z.B. fs.contoso.com enthalten.  
  
2.  Der alternative Antragstellername muss den Wert enthalten **Enterpriseregistration**, gefolgt von der Benutzerprinzipalname \(UPN\) Suffix Ihrer Organisation, z.B. **enterpriseregistration.corp.contoso.com**.  
  
    > [!WARNING]  
    > Geben Sie den alternativen Antragstellernamen, wenn Sie beabsichtigen, den Geräteregistrierungsdienst \(DRS\) für den Arbeitsplatzbeitritt zu aktivieren.  
  
> [!IMPORTANT]  
> Wenn Ihre Organisation mehrere UPN-Suffixe verwendet, und Sie DRS aktivieren möchten, muss das SSL-Zertifikat für jedes Suffix einen Eintrag Antragstellernamen alternativen Namen enthalten.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

