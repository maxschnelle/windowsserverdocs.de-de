---
title: Konfigurieren von Browser, um Windows integrierte Authentifizierung (WIA) mit AD FS verwenden
description: "Dieses Dokument enthält Informationen zum Konfigurieren von Browser, um WIA-Unterstützung mit AD FS verwenden"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f7d43931d1fe4958a539ff1b728e4cc154d06248
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Konfigurieren von Browser, um Windows integrierte Authentifizierung (WIA) mit AD FS verwenden

Standardmäßig ist Windows integrierte Authentifizierung (WIA) in Active Directory-Verbunddienste (AD FS) in Windows Server2012 R2 für die Authentifizierung aktiviert, die innerhalb der Organisation internen Netzwerks (Intranet) für jede Anwendung auftreten, die einen Browser für die Authentifizierung verwendet.

AD FS 2016 jetzt verfügt über eine verbesserte Standardeinstellung, mit der Edge-Browser WIA tun, während Sie nicht auch (falsch) Abfangen von Windows Phone als auch kann:

    =~Windows\s*NT.*Edge

Die oben genannten Fall können Sie nicht mehr so konfigurieren Sie einzelne Benutzer-Agent-Zeichenfolgen in gängigen Edge-Szenarien zu unterstützen, obwohl sie häufig aktualisiert werden.

Konfigurieren Sie die AD FS-Eigenschaft für andere Browser **WiaSupportedUserAgents** hinzufügen die erforderlichen Werte basierend auf den Browsern, die Sie verwenden.  Sie können die folgenden Verfahren verwenden.



### <a name="view-wiasupporteduseragent-settings"></a>WIASupportedUserAgent Einstellungen anzeigen
Die **WIASupportedUserAgents** definiert, die Benutzeragents die WIA-Unterstützung. AD FS analysiert die Zeichenfolge des Benutzer-Agent beim Ausführen von Benutzernamen in einem Browser oder ein Webbrowser-Steuerelement.

Sie können die aktuellen Einstellungen entsprechend dem folgenden PowerShell-Beispiel anzeigen:

```powershell
    $strings = Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA-Unterstützung](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent-Einstellungen ändern
Standardmäßig hat eine neue AD FS-Installation eine Reihe von Benutzer-Agent-Zeichenfolge Übereinstimmungen erstellt. Jedoch können diese veraltet sein basierend auf Änderungen an Browsern und Geräten. Windows-Geräte haben besonders, ähnlich wie Zeichenfolgen des Benutzer-Agent geringfügige Unterschiede auf in die Token. Das folgende Windows PowerShell-Beispiel bietet die beste Richtlinien für den aktuellen Satz von Geräten, die auf dem Markt erhältlichen sind, die eine nahtlose WIA-Unterstützung:

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

Die oben genannten Befehl stellt sicher, dass AD FS nur die folgenden Anwendungsfälle für WIA behandelt:

Benutzer-Agents|Anwendungsfälle|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0; Windows NT|Internet Explorer7, Internet Explorer in der Zone des Intranets. Die "Windows NT"-Fragment wird von Desktop-Betriebssystem gesendet.|
MSIE 8.0|Internet Explorer8.0 (keine Geräte senden diese, daher müssen Sie spezielle)|
MSIE 9.0|Internet Explorer9.0 (keine Geräte senden, nicht zum spezifischere hierdurch müssen)|
MSIE 10.0; Windows NT 6|Internet Explorer10.0 für Windows XP und neuere Versionen von Desktop-Betriebssystem</br></br>Windows Phone8.0-Geräte (mit Satz an mobiles Voreinstellungen) sind ausgeschlossen, da sie senden</br></br>Benutzer-Agent: Mozilla/5.0 (Compatible; MSIE 10.0; Windows Phone8.0; Trident/6.0; IEMobile/10.0; ARM; Tippen Sie auf; NOKIA; Lumia 920)|
Windows NT 6.3; Trident/7.0</br></br>Windows NT 6.3; Win64; x64; Trident/7.0</br></br>Windows NT 6.3; WOW64; Trident/7.0| Windows8.1-Desktop-Betriebssystem, unterschiedliche Plattformen|
Windows NT 6.2; Trident/7.0</br></br>Windows NT 6.2; Win64; x64; Trident/7.0</br></br>Windows NT 6.2; WOW64; Trident/7.0|Windows8 Desktop-Betriebssystem, unterschiedliche Plattformen|
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; Win64; x64; Trident/7.0</br></br>Windows NT 6.1; WOW64; Trident/7.0|Windows7 Desktop-Betriebssystem, verschiedene platoforms|
MSIPC| Microsoft Information Protection und -Steuerungsclient|
Windows Rights Management-Client|Windows Rights Management-Client|
