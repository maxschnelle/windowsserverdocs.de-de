---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: Registrieren eines SSL-Zertifikats für AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6f7af40f23c3fa3bd0a31ecb74b11013133a4b32
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855433"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Registrieren eines SSL-Zertifikats für AD FS

Active Directory-Verbunddienste (AD FS) \(AD FS\) erfordert auf jedem Verbund Server in der Verbund Serverfarm ein Zertifikat für Secure Socket Layer \(SSL\) Server-Authentifizierung. Das gleiche Zertifikat kann auf jedem Verbund Server in einer Farm verwendet werden. Das Zertifikat und sein privater Schlüssel müssen verfügbar sein. Wenn Sie beispielsweise über eine PFX-Datei mit dem Zertifikat und dem privaten Schlüssel verfügen, können Sie die Datei direkt in den Konfigurations-Assistenten für Active Directory-Verbunddienste importieren. Dieses SSL-Zertifikat muss Folgendes enthalten:  
  
1.  Der Antragsteller Name und der alternative Antragsteller Name müssen ihren Verbund Dienstnamen enthalten, z. b. fs.contoso.com.  
  
2.  Der alternative Antragsteller Name muss den Wert **enterpriseregistration** enthalten, auf den der Benutzer Prinzipal Name \(UPN\) Suffix Ihrer Organisation folgt, z. b. **enterpriseregistration.Corp.contoso.com**.  
  
    > [!WARNING]  
    > Geben Sie den alternativen Antragsteller Namen an, wenn Sie planen, den Geräte Registrierungsdienst \(DRS\) für Workplace Join zu aktivieren.  
  
> [!IMPORTANT]  
> Wenn Ihre Organisation mehrere UPN-Suffixe verwendet und Sie beabsichtigen, das DRS zu aktivieren, muss das SSL-Zertifikat einen alternativen Antragsteller Namen für jedes Suffix enthalten.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

