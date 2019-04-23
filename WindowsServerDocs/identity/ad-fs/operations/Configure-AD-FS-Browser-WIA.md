---
title: Konfigurieren von Browsern, Verwendung von Windows integrierte Authentifizierung (WIA) mit AD FS
description: In diesem Dokument wird beschrieben, wie Browsern, Verwendung WIA mit AD FS konfigurieren
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f71680bb721635bd37197dca9d3ae4726099525f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845481"
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Konfigurieren von Browsern, Verwendung von Windows integrierte Authentifizierung (WIA) mit AD FS

Standardmäßig Windows integrierte Authentifizierung (WIA) aktiviert ist, in Active Directory Federation Services (AD FS) in Windows Server 2012 R2 für authentifizierungsanforderungen, die innerhalb der internen Unternehmensnetzwerk (Intranet) für jede Anwendung auftreten, die verwendet ein Browser für die Authentifizierung.

AD FS 2016 jetzt verfügt über eine verbesserte-Einstellung, die den Edge-Browser WIA zu tun, während Sie nicht auch (falsch) abfangen Windows Phone auch ermöglicht:

    =~Windows\s*NT.*Edge

Der obige Code bedeutet, die Sie müssen nicht mehr so konfigurieren Sie die einzelnen Benutzer-Agent-Zeichenfolgen zur Unterstützung allgemeiner Szenarien für Edge, obwohl sie häufig aktualisiert werden.

Konfigurieren Sie die AD FS-Eigenschaft, für andere Browser **WiaSupportedUserAgents** hinzufügen die erforderlichen Werte, die basierend auf den Browsern, die Sie verwenden.  Sie können die folgenden Verfahren verwenden.



### <a name="view-wiasupporteduseragent-settings"></a>Anzeigen von WIASupportedUserAgent-Einstellungen
Die **WIASupportedUserAgents** definiert, die Benutzer-Agents die WIA-Unterstützung. AD FS analysiert die Zeichenfolge des Benutzer-Agent beim Ausführen von Anmeldungen in einen Browser bzw. ein Webbrowser-Steuerelement.

Sie können die aktuellen Einstellungen, die mit dem folgenden PowerShell-Beispiel anzeigen:

```powershell
    $strings = Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA-Unterstützung](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent-Einstellungen ändern
Eine neue Installation von AD FS hat standardmäßig eine Reihe von Benutzer-Agent-zeichenfolgenübereinstimmungen erstellt. Allerdings können diese nicht mehr aktuell sein basierend auf Änderungen an Browsern und Geräten. Insbesondere haben Windows-Geräte ähnlich wie Benutzer-Agent-Zeichenfolgen mit geringfügigen abweichungen in den Token. Das folgende Windows PowerShell-Beispiel bietet die beste gegenwärtige für den aktuellen Satz von Geräten, die heute am Markt sind, die nahtlose WIA-Unterstützung:

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

Der obige Befehl wird sichergestellt, dass AD FS die folgenden Anwendungsfälle für WIA nur deckt:

Benutzer-Agents|Anwendungsfälle|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0; Windows NT|Internet Explorer 7, Internet Explorer, in der Intranetzone. Das Fragment "Windows NT" wird von desktop-Betriebssystem gesendet.|
MSIE 8.0|Internet Explorer 8.0 (keine Geräte senden, daher müssen Sie spezifischere)|
MSIE 9.0|Internet Explorer 9.0 (keine Geräte senden, damit keine müssen Sie diese spezifische)|
MSIE 10.0; Windows NT 6|Internet Explorer 10.0 für Windows XP und neuere Versionen von desktop-Betriebssystem</br></br>Windows Phone 8.0-Geräte (mit bevorzugen, legen Sie für die mobile) werden ausgeschlossen, da sie senden</br></br>Benutzer-Agent: Mozilla/5.0 (kompatibel; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 920)|
Windows NT 6.3; Trident/7.0</br></br>Windows NT 6.3; Win64; x64; Trident/7.0</br></br>Windows NT 6.3; WOW64; Trident/7.0| Windows 8.1-desktop-Betriebssystem, verschiedene Plattformen|
Windows NT 6.2; Trident/7.0</br></br>Windows NT 6.2; Win64; x64; Trident/7.0</br></br>Windows NT 6.2; WOW64; Trident/7.0|Windows 8 desktop-Betriebssystem, verschiedene Plattformen|
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; Win64; x64; Trident/7.0</br></br>Windows NT 6.1; WOW64; Trident/7.0|Windows 7 desktop-Betriebssystem, verschiedene Plattformen|
MSIPC| Microsoft Information Protection und Steuerelement|
Windows Rights Management-Client|Windows Rights Management-Client|
