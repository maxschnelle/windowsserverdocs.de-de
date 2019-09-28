---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: Konfigurieren der Formular basierten intranetauthentifizierung für Geräte, die WIA nicht unterstützen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9b74c57059346e87c5091c83d648b034f4cd049e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358079"
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>Konfigurieren der Formular basierten intranetauthentifizierung für Geräte, die WIA nicht unterstützen


Standardmäßig ist die integrierte Windows-Authentifizierung (WIA) in Active Directory-Verbunddienste (AD FS) (AD FS) in Windows Server 2012 R2 für Authentifizierungsanforderungen aktiviert, die im internen Netzwerk des Unternehmens (Intranet) für Anwendungen erfolgen, die eine Browser für die Authentifizierung. Dies können beispielsweise browserbasierte Anwendungen sein, die WS-Verbund-oder SAML-Protokolle und umfangreiche Anwendungen verwenden, die das OAuth-Protokoll verwenden. WIA bietet Endbenutzern eine nahtlose Anmeldung bei den Anwendungen, ohne dass Ihre Anmelde Informationen manuell eingegeben werden müssen. Allerdings sind einige Geräte und Browser nicht in der Lage, WIA zu unterstützen, und das Ergebnis ist, dass Authentifizierungsanforderungen von diesen Geräten fehlschlagen. Außerdem ist das Verhalten für bestimmte Browser, die in NTLM aushandeln, nicht wünschenswert. Die empfohlene Vorgehensweise ist ein Fall Back auf Formular basierte Authentifizierung für solche Geräte und Browser.

AD FS in Windows Server 2016 und Windows Server 2012 R2 bietet Administratoren die Möglichkeit, die Liste der Benutzer-Agents zu konfigurieren, die den Fall Back auf Formular basierte Authentifizierung unterstützen. Der Fall Back wird durch zwei Konfigurationen ermöglicht:


- Die **wiasupporteduseragentstrings** -Eigenschaft des `Set-ADFSProperties` Commandlets
- Die **windowsintegratedfallbackaktivierte** Eigenschaft des `Set-AdfsGlobalAuthenticationPolicy` Commandlets

**Wiasupporteduseragentstrings** definiert die Benutzer-Agents, die WIA unterstützen. AD FS analysiert die Zeichenfolge des Benutzer-Agents, wenn Anmeldungen in einem Browser-oder Browser Steuerelement durchgeführt werden. Wenn die Komponente der Zeichenfolge des Benutzer-Agents keiner der Komponenten der Zeichen Folgen des Benutzer-Agents entspricht, die in der **wiasupporteduseragentstrings** -Eigenschaft konfiguriert sind, wird AD FS auf die Formular basierte Authentifizierung zurückgreifen, vorausgesetzt, dass die  **Das Flag "windowsintegratedfallbackaktivierte** " ist auf "true" festgelegt.

Standardmäßig enthält eine neue AD FS Installation eine Reihe von Benutzer-Agent-Zeichen folgen, die erstellt wurden. Diese können jedoch aufgrund von Änderungen an Browsern und Geräten veraltet sein. Insbesondere Windows-Geräte verfügen über ähnliche Benutzer-Agent-Zeichen folgen mit geringfügigen Variationen in den Token. Das folgende Windows PowerShell-Beispiel bietet den besten Leitfaden für die aktuelle Gruppe von Geräten, die heute auf dem Markt sind und nahtlose WIA unterstützen:

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

Mit dem obigen Befehl wird sichergestellt, dass AD FS nur die folgenden Anwendungsfälle für WIA abdeckt:

Benutzer-Agents|Anwendungsfälle|
-----|-----|
MSIE 6,0|IE 6,0|
MSIE 7,0; Windows NT|IE 7, IE in der Intranetzone. Das Fragment "Windows NT" wird vom Desktop Betriebssystem gesendet.|
MSIE 8,0|IE 8,0 (keine Geräte senden dies, deshalb müssen Sie spezifischere festlegen)|
MSIE 9,0|IE 9,0 (keine Geräte senden dies, sodass Sie dies nicht spezifischere machen müssen)|
MSIE 10,0; Windows NT 6|IE 10,0 für Windows XP und neuere Versionen des Desktop Betriebssystems</br></br>Windows Phone 8,0-Geräte (mit der Einstellung Mobile) werden ausgeschlossen, da Sie</br></br>Benutzer-Agent: Mozilla/5.0 (kompatibel; MSIE 10,0; Windows Phone 8,0; Einzug/6.0; Iemobile/10.0; Harm Ansprechen Heftig Lumia 920)|
Windows NT 6,3; Einzug/7.0</br></br>Windows NT 6,3; Win64 x64 Einzug/7.0</br></br>Windows NT 6,3; WOW64 Einzug/7.0| Windows 8.1 Desktop Betriebssystem, unterschiedliche Plattformen|
Windows NT 6,2; Einzug/7.0</br></br>Windows NT 6,2; Win64 x64 Einzug/7.0</br></br>Windows NT 6,2; WOW64 Einzug/7.0|Windows 8 Desktop-Betriebssystem, unterschiedliche Plattformen|
Windows NT 6,1; Einzug/7.0</br></br>Windows NT 6,1; Win64 x64 Einzug/7.0</br></br>Windows NT 6,1; WOW64 Einzug/7.0|Windows 7 Desktop-Betriebssystem, unterschiedliche Plattformen|
MSIPC| Microsoft Information Protection and Control-Client|
Windows Rights Management-Client|Windows Rights Management-Client|

Um das Fall Back auf eine Formular basierte Authentifizierung für Benutzer-Agents zu aktivieren, die nicht in der Zeichenfolge wiasupporteduseragents erwähnt werden, legen Sie das Flag windowsintegratedfallbackenable auf true fest.

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

Stellen Sie außerdem sicher, dass die Formular basierte Authentifizierung für das Intranet aktiviert ist.

## <a name="configuring-wia-for-chrome"></a>Konfigurieren von WIA für Chrome
Sie können Chrome oder andere Benutzer-Agents der AD FS Konfiguration hinzufügen, die WIA unterstützt. Dies ermöglicht eine nahtlose Anmeldung bei Anwendungen, ohne dass Sie manuell Anmelde Informationen eingeben müssen, wenn Sie auf durch AD FS geschützte Ressourcen zugreifen. Führen Sie die folgenden Schritte aus, um WIA in Chrome zu aktivieren:

Fügen Sie in AD FS Konfiguration eine Benutzer-Agent-Zeichenfolge für Chrome auf Windows-basierten Plattformen hinzu:

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Windows NT")

Fügen Sie die folgende Benutzer-Agent-Zeichenfolge für Chrome auf Apple macOS der AD FS Konfiguration hinzu:

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Macintosh; Intel Mac OS X")

Vergewissern Sie sich, dass die Benutzer-Agent-Zeichenfolge für Chrome nun in den AD FS Eigenschaften festgelegt ist:

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

(Sie benötigen hier einen neuen Screenshot) ![Konfigurieren der Authentifizierung](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> Wenn neue Browser und Geräte veröffentlicht werden, wird empfohlen, dass Sie die Funktionen dieser Benutzer-Agents abstimmen und die AD FS Konfiguration entsprechend aktualisieren, um die Authentifizierung des Benutzers bei der Verwendung von Gesagten Browsern und Geräten zu optimieren. Genauer gesagt wird empfohlen, dass Sie die **wiasupporteduseragents** -Einstellung in AD FS neu auswerten, wenn Sie Ihrer Unterstützungs Matrix für WIA ein neues Gerät oder einen Browsertyp hinzufügen.


