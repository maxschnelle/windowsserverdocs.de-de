---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: Konfigurieren der formularbasierten Intranetauthentifizierung für Geräte, die ohne WIA-Unterstützung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c79524a011336d676fa2e80936e1254a8d2dd6b2
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189692"
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>Konfigurieren der formularbasierten Intranetauthentifizierung für Geräte, die ohne WIA-Unterstützung


Standardmäßig Windows integrierte Authentifizierung (WIA) aktiviert ist, in Active Directory Federation Services (AD FS) in Windows Server 2012 R2 für authentifizierungsanforderungen, die innerhalb der internen Unternehmensnetzwerk (Intranet) für jede Anwendung auftreten, die verwendet ein Browser für die Authentifizierung. Diese können beispielsweise sein, browserbasierte Anwendungen, die WS-Verbund verwenden oder SAML-Protokolle und Rich-Anwendungen, die das OAuth-Protokoll verwenden. WIA bietet Endbenutzern nahtlose Anmeldung auf die Anwendungen ohne Manuelles Eingeben ihrer Anmeldeinformationen. Allerdings einige Geräte und Browser nicht WIA unterstützen und daher Fehlschlagen von authentifizierungsanforderungen von diesen Geräten. Darüber hinaus ist die Oberfläche auf bestimmte Browser, die auf NTLM auszuhandeln nicht wünschenswert. Der empfohlene Ansatz ist auf die formularbasierte Authentifizierung für solche Geräte und Browser.

AD FS unter Windows Server 2016 und Windows Server 2012 R2 bietet Administratoren die Möglichkeit, die die Liste der Benutzer-Agents zu konfigurieren, dass das Fallback auf formularbasierte Authentifizierung unterstützen. Das Fallback wird durch zwei Konfigurationen ermöglicht:


- Die **WIASupportedUserAgentStrings** Eigenschaft der `Set-ADFSProperties` Cmdlet
- Die **WindowsIntegratedFallbackEnabled** Eigenschaft der `Set-AdfsGlobalAuthenticationPolicy` Cmdlet

Die **WIASupportedUserAgentStrings** definiert, die Benutzer-Agents die WIA-Unterstützung. AD FS analysiert die Zeichenfolge des Benutzer-Agent beim Ausführen von Anmeldungen in einen Browser bzw. ein Webbrowser-Steuerelement. Wenn der Anteil der Zeichenfolge des Benutzer-Agent nicht die Komponenten, die Benutzer-Agent-Zeichenfolgen übereinstimmen, die in konfiguriert werden **WIASupportedUserAgentStrings** -Eigenschaft, AD FS wird ein Fallback auf formularbasierte die Authentifizierung bereitstellt, vorausgesetzt, dass die **WindowsIntegratedFallbackEnabled** Flag auf "true" festgelegt ist.

Eine neue Installation von AD FS hat standardmäßig eine Reihe von Benutzer-Agent-zeichenfolgenübereinstimmungen erstellt. Allerdings können diese nicht mehr aktuell sein basierend auf Änderungen an Browsern und Geräten. Insbesondere haben Windows-Geräte ähnlich wie Benutzer-Agent-Zeichenfolgen mit geringfügigen abweichungen in den Token. Das folgende Windows PowerShell-Beispiel bietet die beste gegenwärtige für den aktuellen Satz von Geräten, die heute am Markt sind, die nahtlose WIA-Unterstützung:

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

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

Um Fallback auf formularbasiert-Authentifizierung für Benutzer-Agents als den oben in der Zeichenfolge WIASupportedUserAgents zu ermöglichen, festlegen Sie das WindowsIntegratedFallbackEnabled-Flag auf "true"

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

Stellen Sie außerdem sicher, dass die formularbasierte Authentifizierung für Intranet aktiviert ist.

## <a name="configuring-wia-for-chrome"></a>Konfigurieren der WIA für Chrome
Sie können Chrome oder andere Benutzeragents auf dem AD FS-Konfiguration hinzufügen, die WIA unterstützt. Dies ermöglicht die nahtlose Anmeldung bei Anwendungen, ohne Anmeldeinformationen manuell eingeben, wenn Sie von AD FS geschützte Ressourcen zugreifen. Gehen Sie folgendermaßen vor, um WIA in Chrome zu aktivieren:

Fügen Sie eine Zeichenfolge des Benutzer-Agenten für Chrome hinzu, in der AD FS-Konfiguration

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + “Chrome”)
    
Vergewissern Sie sich, dass die Zeichenfolge des Benutzer-Agenten für Chrome jetzt in den Eigenschaften des AD FS festgelegt ist

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

![Konfigurieren der Authentifizierung](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> Wenn neue Browser und Geräte veröffentlicht werden, empfiehlt es sich, dass Sie die Funktionen des die Benutzeragents abstimmen und die AD FS-Konfiguration entsprechend aktualisieren, um das Benutzererlebnis bei der Authentifizierung zu optimieren, wenn Sie mithilfe von Browser und Geräte als bezeichnet. Genauer gesagt, es wird empfohlen, dass Sie erneut die **WIASupportedUserAgents** in AD FS festlegen, wenn es sich bei Ihrer Support-Matrix für WIA einen neuen Typ von Gerät bzw. Ihren Browser hinzugefügt.


