---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: "AD FS-Unterstützung für alternative hostnamenbindung für zertifikatbasierte Authentifizierung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 553ff059693c7b0c0e6f0364d82c1adbca661097
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS-Unterstützung für alternative hostnamenbindung für zertifikatbasierte Authentifizierung

>Gilt für: Windows Server 2016

Auf viele Netzwerke möglicherweise lokale Firewall-Richtlinien kein Datenverkehr über nicht standardmäßigen Ports wie 49443 zulässig. Dies wurde behoben, wenn zertifikatbasierte Authentifizierung mit AD FS vor der AD FS unter Windows Server 2016 ausführen möchten. Dies ist, da Sie unterschiedliche Bindungen für Geräte und Benutzerauthentifizierung Zertifikat auf dem gleichen Host kein konnte. Der Standardport 443 Gerätezertifikate empfangen gebunden ist, und es kann nicht geändert werden, um mehrere Bindung in denselben Kanal zu unterstützen. Die Ergebnisse wurden, dass die Smartcard-Authentifizierung funktioniert nicht, und Benutzer konnten nicht bewusst was passiert ist, da es ist kein Hinweis was wirklich passiert ist.  
  
Mit AD FS unter Windows Server 2016 kann dadurch erfolgen.
  
In AD FS unter Windows Server 2016 wurde dies geändert. Nun zwei Modi unterstützt wird, verwendet die erste den gleichen Host (d. h. adfs.contoso.com) mit unterschiedliche Ports (443, 49443). Die zweite verwendet verschiedene Hosts (adfs.contoso.com und certauth.adfs.contoso.com) mit den gleichen Port (443). Dies ist ein SSL-Zertifikat zur Unterstützung von "Certauth. < AD FS-Dienst-Name >" als einen alternativen Antragstellernamen erforderlich. Dies kann zum Zeitpunkt der Erstellung der Farm oder später über PowerShell erfolgen.  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>Konfigurieren von alternativen Namen Bindung die zertifikatbasierte Authentifizierung  
Es gibt zwei Möglichkeiten, dass Sie die alternativen Namen Bindung für die Zertifikatauthentifizierung hinzufügen können. Die erste ist beim Einrichten einer neuen AD FS-Farm mit AD FS für WindowsServer 2016, wenn das Zertifikat einen alternativen Antragstellernamen (SAN), enthält, wird er automatisch Setup die zweite Methode, die oben genannten verwenden kann. Es wird automatisch zwei unterschiedlichen Hosts (sts.contoso.com und certauth.sts.contoso.com mit den gleichen Port. einrichten Wenn das Zertifikat nicht über ein SAN enthält, dann sehen Sie eine Warnung besagt, dass das Zertifikat alternativen Antragstellernamen certauth.* nicht unterstützt. Finden Sie unter den folgenden Screenshots. Als erster zeigt eine Installation, in dem das Zertifikat hat ein SAN und das zweite Beispiel zeigt ein Zertifikat, das nicht der Fall.  
  
![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
Entsprechend wird nach der Bereitstellung von AD FS unter Windows Server 2016 können das PowerShell-Cmdlet: Set-AdfsAlternateTlsClientBinding.
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

Wenn Sie aufgefordert werden, klicken Sie auf "Ja", um zu bestätigen.  Und es sollten werden.

![Alternative hostnamenbindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>Weitere Verweise

* [Verwalten von SSL-Zertifikaten in AD FS und WAP in WindowsServer 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
