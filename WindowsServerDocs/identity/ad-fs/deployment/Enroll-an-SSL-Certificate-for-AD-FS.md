---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: Registrieren eines SSL-Zertifikats für AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 2d24e5593af2d12359d4e2acd5fc93df334730b8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962824"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Registrieren eines SSL-Zertifikats für AD FS

Active Directory-Verbunddienste (AD FS) \( AD FS \) erfordert ein Zertifikat für \( die SSL-Server Authentifizierung Secure Socket Layer \) auf jedem Verbund Server in der Verbund Serverfarm. Das gleiche Zertifikat kann auf jedem Verbund Server in einer Farm verwendet werden. Sie müssen sowohl über das Zertifikat als auch den dazugehörigen privaten Schlüssel verfügen. Wenn Sie beispielsweise über eine PFX-Datei mit dem Zertifikat und dem privaten Schlüssel verfügen, können Sie die Datei direkt in den Konfigurations-Assistenten für Active Directory-Verbunddienste importieren. Dieses SSL-Zertifikat muss Folgendes enthalten:

1.  Der Antragsteller Name und der alternative Antragsteller Name müssen ihren Verbund Dienstnamen enthalten, z. b. fs.contoso.com.

2.  Der alternative Antragsteller Name muss den Wert **enterpriseregistration** enthalten, gefolgt vom UPN-Suffix des Benutzer Prinzipal namens \( \) Ihrer Organisation, z. b. **enterpriseregistration.Corp.contoso.com**.

    > [!WARNING]
    > Geben Sie den alternativen Antragsteller Namen an, wenn Sie beabsichtigen, den Geräte Registrierungsdienst \( DRS \) für Workplace Join zu aktivieren.

> [!IMPORTANT]
> Wenn Ihre Organisation mehrere UPN-Suffixe verwendet und Sie beabsichtigen, das DRS zu aktivieren, muss das SSL-Zertifikat einen alternativen Antragsteller Namen für jedes Suffix enthalten.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)

[Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)



