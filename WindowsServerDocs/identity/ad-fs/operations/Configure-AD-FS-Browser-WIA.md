---
title: Konfigurieren von Browsern für die Verwendung der integrierten Windows-Authentifizierung (WIA) mit AD FS
description: In diesem Dokument wird beschrieben, wie Sie Browser für die Verwendung von WIA mit AD FS konfigurieren.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 576ec407e244485441e99ed831b4ed9a0dac198c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358249"
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Konfigurieren von Browsern für die Verwendung der integrierten Windows-Authentifizierung (WIA) mit AD FS

Standardmäßig ist die integrierte Windows-Authentifizierung (WIA) in Active Directory-Verbunddienste (AD FS) (AD FS) in Windows Server 2012 R2 für Authentifizierungsanforderungen aktiviert, die im internen Netzwerk des Unternehmens (Intranet) für Anwendungen erfolgen, die eine Browser für die Authentifizierung.

AD FS 2016 verfügt jetzt über eine verbesserte Standardeinstellung, die es dem Edge-Browser ermöglicht, WIA zu tun, während er nicht gleichzeitig Windows Phone abfängt:

    =~Windows\s*NT.*Edge

Das obige bedeutet, dass Sie keine einzelnen Benutzer-Agent-Zeichen folgen mehr konfigurieren müssen, um gängige Edge-Szenarien zu unterstützen, auch wenn Sie sehr häufig aktualisiert werden.

Konfigurieren Sie für andere Browser die AD FS-Eigenschaft **wiasupporteduseragents** , um die erforderlichen Werte basierend auf den verwendeten Browsern hinzuzufügen.  Sie können die nachfolgenden Prozeduren verwenden.



### <a name="view-wiasupporteduseragent-settings"></a>Einstellungen für wiasupporteduseragent anzeigen
**Wiasupporteduseragents** definiert die Benutzer-Agents, die WIA unterstützen. AD FS analysiert die Zeichenfolge des Benutzer-Agents, wenn Anmeldungen in einem Browser-oder Browser Steuerelement durchgeführt werden.

Sie können die aktuellen Einstellungen mithilfe des folgenden PowerShell-Beispiels anzeigen:

```powershell
    Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA-Unterstützung](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>Einstellungen für wiasupporteduseragent ändern
Standardmäßig enthält eine neue AD FS Installation eine Reihe von Benutzer-Agent-Zeichen folgen, die erstellt wurden. Diese können jedoch aufgrund von Änderungen an Browsern und Geräten veraltet sein. Insbesondere Windows-Geräte verfügen über ähnliche Benutzer-Agent-Zeichen folgen mit geringfügigen Variationen in den Token. Das folgende Windows PowerShell-Beispiel bietet den besten Leitfaden für die aktuelle Gruppe von Geräten, die heute auf dem Markt sind und nahtlose WIA unterstützen:

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

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
