---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: AD FS-Unterstützung für alternative Hostnamenbindung für zertifikatbasierte Authentifizierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0b361c99486f61a3aee4651a743eb83ab4127e40
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947393"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS-Unterstützung für alternative Hostnamenbindung für zertifikatbasierte Authentifizierung

In vielen Netzwerken können die lokalen Firewallrichtlinien keinen Datenverkehr über nicht standardmäßige Ports wie 49443 zulassen. Dies ist ein Problem beim Versuch, die Zertifikat Authentifizierung mit AD FS vor dem AD FS in Windows Server 2016 auszuführen. Dies liegt daran, dass für die Geräte Authentifizierung und Benutzerzertifikat Authentifizierung auf dem gleichen Host keine unterschiedlichen Bindungen vorhanden sein konnten. Der Standardport 443 ist an den Empfang von Geräte Zertifikaten gebunden und kann nicht geändert werden, um mehrere Bindungen im gleichen Kanal zu unterstützen. Dies hat zur Folge, dass die Smartcard-Authentifizierung nicht funktioniert, und dass die Benutzer nicht wissen, was passiert ist, da nicht angegeben wird, was tatsächlich passiert ist.

Mit AD FS in Windows Server 2016 kann dies erreicht werden.

In AD FS unter Windows Server 2016 hat sich diese Änderung geändert. Wir unterstützen nun zwei Modi. der erste verwendet den gleichen Host (d.h. ADFS.contoso.com) mit unterschiedlichen Ports (443, 49443). Die zweite verwendete andere Hosts (ADFS.contoso.com und certauth.ADFS.contoso.com) mit demselben Port (443). Hierfür ist ein SSL-Zertifikat erforderlich, damit "certauth. <ADFS-Service-Name>" als alternativer Antragsteller Name unterstützt wird. Dies kann zum Zeitpunkt der Erstellung der Farm oder später über PowerShell erfolgen.

## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>Konfigurieren alternativer Hostnamen Bindungen für die Zertifikat Authentifizierung
Es gibt zwei Möglichkeiten, wie Sie die Alternative Host Namen Bindung für die Zertifikat Authentifizierung hinzufügen können. Der erste Schritt ist das Einrichten einer neuen AD FS Farm mit AD FS für Windows Server 2016, wenn das Zertifikat einen alternativen Antragsteller Namen (Subject Alternative Name, San) enthält, wird es automatisch so eingerichtet, dass es die oben genannte zweite Methode verwendet. Das heißt, es werden automatisch zwei verschiedene Hosts (STS.contoso.com und certauth.STS.contoso.com mit demselben Port) eingerichtet. Wenn das Zertifikat kein San enthält, wird eine Warnung angezeigt, die besagt, dass die alternativen Antragsteller Namen des Zertifikats "certauth. *" nicht unterstützen. Sehen Sie sich die folgenden Screenshots an. Der erste zeigt eine Installation, bei der das Zertifikat über ein San und das zweite ein Zertifikat anzeigt, das nicht.

![Alternative Host Namen Bindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)

![Alternative Host Namen Bindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)

Entsprechend können Sie das PowerShell-Cmdlet Set-ADF salternatetlsclientbinding verwenden, nachdem AD FS in Windows Server 2016 bereitgestellt wurde.

```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

Wenn Sie dazu aufgefordert werden, klicken Sie zur Bestätigung auf Ja  Und das sollte der Fall sein.

![Alternative Host Namen Bindung](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>Weitere Verweise

* [Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016](./manage-ssl-certificates-ad-fs-wap.md)
