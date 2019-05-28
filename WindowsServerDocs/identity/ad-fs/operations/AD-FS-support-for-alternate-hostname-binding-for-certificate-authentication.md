---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: AD FS-Unterstützung für alternative Hostnamenbindung für Zertifikatauthentifizierung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e3d1e5d86afbef2fdabd211047f513d31a40300
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190324"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS-Unterstützung für alternative Hostnamenbindung für Zertifikatauthentifizierung

In vielen Netzwerken können die lokale Firewall-Richtlinien kein Datenverkehr über nicht standardmäßige Ports, z. B. 49443 zulässig. Dies wurde ein Problem beim Versuch, eine zertifikatbasierte Authentifizierung mit AD FS vor der AD FS unter Windows Server 2016 zu erreichen. Dies ist, da Sie unterschiedliche Bindungen für die Geräteauthentifizierung und Authentifizierung mit Benutzerzertifikat nicht auf demselben Host haben. Der Standardport 443 gebunden ist, um Zertifikate für Geräte zu erhalten und kann nicht geändert werden, um mehrere Bindung in den gleichen Kanal zu unterstützen. Die Ergebnisse waren, dass die Smartcard-Authentifizierung funktioniert nicht, und Benutzer konnten keine Kenntnis von Was passiert, da es keinen Hinweis gibt von was tatsächlich passiert ist.  
  
Mit AD FS unter Windows Server 2016 kann dies erreicht, werden.
  
In AD FS unter Windows Server 2016 wurde dies geändert werden. Nachdem wir zwei Modi zu unterstützen, verwendet die erste den gleichen Host (z.B. "ADFS.contoso.com") mit unterschiedlichen Ports (443, 49443 verwendet). Die zweite verwendet verschiedene Hosts ("ADFS.contoso.com" und certauth.adfs.contoso.com) mit den gleichen Port (443). Dies erfordert ein SSL-Zertifikat zur Unterstützung von "Certauth. < AD FS-Service-Name >" als eine alternative Antragstellernamen aus. Dies kann zum Zeitpunkt der Erstellung der Farm oder einem späteren Zeitpunkt mithilfe von PowerShell erfolgen.  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>Vorgehensweise: Konfigurieren Sie alternative Hostnamen-Bindungen für die zertifikatbasierte Authentifizierung  
Es gibt zwei Möglichkeiten, dass Sie die alternative Hostnamen-Bindungen für die zertifikatbasierte Authentifizierung hinzufügen können. Die erste ist beim Einrichten einer neuen AD FS-Farm mit AD FS für WindowsServer 2016, wenn das Zertifikat ein alternativen Antragstellernamens (SAN), enthält, wird er automatisch, die zweite Methode, die oben genannten verwenden kann. D.h., wird es automatisch zwei unterschiedlichen Hosts ("STS.contoso.com" und certauth.sts.contoso.com mit den gleichen Port. eingerichtet Wenn das Zertifikat nicht über ein SAN enthält, dann sehen Sie eine Warnung besagt, dass es sich bei den alternativen zertifikatantragstellernamen certauth.* nicht unterstützt. Finden Sie unter den folgenden Screenshots. Der erste Screenshot zeigt eine Installation, in dem das Zertifikat verfügt, ein SAN und das zweite Beispiel zeigt ein Zertifikat, das nicht der Fall.  
  
![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
Nach der Bereitstellung mit AD FS unter Windows Server 2016 können Sie ebenso das PowerShell-Cmdlet verwenden: Set-AdfsAlternateTlsClientBinding.
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

Wenn Sie aufgefordert werden, klicken Sie auf "Ja", um zu bestätigen.  Und dies sollte es sein.

![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>Weitere Verweise

* [Verwalten von SSL-Zertifikaten in AD FS und WAP unter WindowsServer 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
