---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: "Konfigurieren des Intranet formularbasierte Authentifizierung für Geräte, die ohne WIA-Unterstützung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c78dc702cbff8eab487c6c077dfe57b0f0663342
ms.sourcegitcommit: 5012c078b410f59261edf0cc917393467243a5c7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>Konfigurieren des Intranet formularbasierte Authentifizierung für Geräte, die ohne WIA-Unterstützung

>Gilt für: Windows Server 2016, Windows Server2012 R2

Standardmäßig ist Windows integrierte Authentifizierung (WIA) in Active Directory-Verbunddienste (AD FS) in Windows Server2012 R2 für die Authentifizierung aktiviert, die innerhalb der Organisation internen Netzwerks (Intranet) für jede Anwendung auftreten, die einen Browser für die Authentifizierung verwendet. Beispielsweise kann diese browserbasierte Anwendungen, die WS-Federation verwenden oder SAML-Protokolle und Rich-Anwendungen, die das OAuth-Protokoll verwenden. WIA bietet Endbenutzern eine nahtlose Anmeldung auf die Anwendungen ohne manuelle Eingabe ihrer Anmeldeinformationen. Allerdings einigen Geräten und Browsern sind nicht WIA unterstützen und daher authentifizierungsanforderungen von diesen Geräten nicht ausgeführt. Darüber hinaus ist das Verhalten auf bestimmte Browser, die auf NTLM auszuhandeln nicht wünschenswert. Es wird empfohlen, einen Fallback auf formularbasierte Authentifizierung für diese Geräte und Browsern.

AD FS unter Windows Server 2016 und Windows Server 2012 R2 bietet die Administratoren die Möglichkeit, die Liste der Benutzer-Agents konfigurieren, die die Fallback auf formularbasierte Authentifizierung unterstützen. Das Fallback wird durch zwei Konfigurationen möglich:


- Die **WIASupportedUserAgentStrings** Eigenschaft der `Set-ADFSProperties` Cmdlet
- Die **WindowsIntegratedFallbackEnabled** Eigenschaft der `Set-AdfsGlobalAuthenticationPolicy` Commmandlet

Die **WIASupportedUserAgentStrings** definiert, die Benutzeragents die WIA-Unterstützung. AD FS analysiert die Zeichenfolge des Benutzer-Agent beim Ausführen von Benutzernamen in einem Browser oder ein Webbrowser-Steuerelement. Entspricht die Komponente der Zeichenfolge des Benutzer-Agent keine Komponenten von Zeichenfolgen des Benutzer-Agenten, die in konfiguriert sind **WIASupportedUserAgentStrings** Eigenschaft AD FS wird ein Fallback auf formularbasierte Authentifizierung, bereitgestellt, die die **WindowsIntegratedFallbackEnabled** Flag auf "true" festgelegt ist.

Standardmäßig hat eine neue AD FS-Installation eine Reihe von Benutzer-Agent-Zeichenfolge Übereinstimmungen erstellt. Jedoch können diese veraltet sein basierend auf Änderungen an Browsern und Geräten. Windows-Geräte haben besonders, ähnlich wie Zeichenfolgen des Benutzer-Agent geringfügige Unterschiede auf in die Token. Das folgende Windows PowerShell-Beispiel bietet die beste Richtlinien für den aktuellen Satz von Geräten, die auf dem Markt erhältlichen sind, die eine nahtlose WIA-Unterstützung:

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

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
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; Win64; x64; Trident/7.0</br></br>Windows NT 6.1; WOW64; Trident/7.0|Windows7 Desktop-Betriebssystem, unterschiedliche Plattformen|
MSIPC| Microsoft Information Protection und -Steuerungsclient|
Windows Rights Management-Client|Windows Rights Management-Client|

Um Fallback auf formularbasiert Authentifizierung für Benutzer-Agents nicht in der Zeichenfolge WIASupportedUserAgents zu aktivieren, legen Sie das Flag WindowsIntegratedFallbackEnabled auf "true"

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

Stellen Sie außerdem sicher, dass die formularbasierte Authentifizierung für Intranet aktiviert ist.

## <a name="configuring-wia-for-chrome"></a>Konfigurieren von WIA für Chrome
Sie können Chrome oder andere Benutzer-Agents für die AD FS-Konfiguration hinzufügen, die WIA unterstützt. Dies ermöglicht eine nahtlose Anmeldung für Anwendungen ohne manuelle Eingabe der Anmeldeinformationen Zugriff auf Ressourcen, die von AD FS geschützte. Gehen Sie folgendermaßen vor, um WIA auf Chrome zu aktivieren:

Fügen Sie eine Zeichenfolge des Benutzer-Agent für Chrome in AD FS-Konfiguration

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + “Chrome”)
    
Stellen Sie sicher, dass die Benutzer-Agent-Zeichenfolge für Chrome jetzt in den AD FS-Eigenschaften festgelegt ist

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

![Konfigurieren Sie die Authentifizierung](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> Wenn neue Browser und Geräte freigegeben werden, empfiehlt es sich, dass Sie die Funktionen der diese Benutzer-Agents abstimmen und die AD FS-Konfiguration entsprechend aktualisieren, um die Authentifizierung Erfahrung des Benutzers zu optimieren, wenn mithilfe von Browser und Geräte sind so. Genauer gesagt, es empfiehlt sich, dass Sie neu bewerten der **WIASupportedUserAgents** in AD FS festlegen, wenn Sie eine neue Art von Gerät oder den Browser Ihrer Unterstützungsmatrix für WIA hinzufügen.


