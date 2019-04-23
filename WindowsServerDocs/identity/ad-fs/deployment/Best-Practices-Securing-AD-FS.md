---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: Bewährte Methoden zum Schützen von AD FS und Webanwendungsproxy
description: Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) und Web Application Proxy.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 38de2bca413ce7f8aeda2af4392f9a616641b189
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873071"
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Bewährte Methoden zum Schützen von Active Directory Federation Services

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) und Web Application Proxy.  Es enthält Informationen über das Standardverhalten dieser Komponenten und Empfehlungen für zusätzliche Sicherheitskonfigurationen für eine Organisation spezifische Anwendungsfälle und sicherheitsanforderungen.

Dieses Dokument gilt für AD FS und WAP in Windows Server 2012 R2 und Windows Server 2016 (Vorschau).  Diese Empfehlungen können verwendet werden, ob die Infrastruktur in einem lokalen Netzwerk oder in einer gehosteten Cloudumgebung wie Microsoft Azure bereitgestellt wird.

## <a name="standard-deployment-topology"></a>Standard-Bereitstellungstopologie
Für die Bereitstellung in lokalen Umgebungen empfehlen wir eine standardbereitstellung-Topologie, die eine oder mehrere AD FS-Server auf dem internen Unternehmensnetzwerk mit einem oder mehreren Webanwendungsproxy (WAP)-Servern in einer DMZ oder extranet-Netzwerk bestehend aus.  Auf jeder Ebene, die AD FS und WAP, wird ein Hardware oder Software Load Balancer vor der Serverfarm und verarbeitet das datenverkehrsrouting.  Firewalls, werden als erforderlich ist, der die externe IP-Adresse des Load Balancers im Vordergrund vor jede Farm (FS und Proxys) platziert.

![AD FS-Standard-Topologie](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>Erforderliche Ports
Das folgende Diagramm zeigt die Firewallports, die zwischen und für die Komponenten von der AD FS und WAP-Bereitstellung aktiviert werden müssen.  Enthält die Bereitstellung keinen Azure AD / Office 365, die Anforderungen an die verzeichnissynchronisierung ignoriert werden kann.

>Beachten Sie, dass Port 49443 verwendet nur erforderlich, wenn die Authentifizierung mit Benutzerzertifikat der Einsatz ist optional für Azure AD verwendet wird, und Office 365.

![AD FS-Standard-Topologie](media/Best-Practices-Securing-AD-FS/adfssec2.png)

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect und Verbund/WAP-Server
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen Azure AD Connect-Server und Verbund-/WAP-Servern erforderlich sind.  

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |---------
HTTP|80 (TCP/UDP)|Zum Herunterladen von Zertifikatsperrlisten (Certificate Revocation Lists) zu überprüfen, ob SSL-Zertifikate verwendet.
HTTPS|443(TCP/UDP)|Verwendet, um mit Azure AD zu synchronisieren.
WinRM|5985| WinRM-Listener

### <a name="wap-and-federation-servers"></a>WAP- und Verbundserver
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen den Verbundservern und WAP-Servern erforderlich sind.

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |---------
HTTPS|443(TCP/UDP)|Für die Authentifizierung verwendet.

### <a name="wap-and-users"></a>WAP und Benutzer
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen Benutzern und den WAP-Servern erforderlich sind.

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|Für die Geräteauthentifizierung verwendet.
TCP|49443 (TCP)|Für die zertifikatbasierte Authentifizierung verwendet.

Weitere Informationen zu den erforderlichen Ports und Protokolle, die erforderlich sind, Hybrid-Bereitstellungen finden Sie in das Dokument [hier](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/).

Ausführliche Informationen zu Ports und Protokollen, die erforderliche für ein Azure AD und Office 365-Bereitstellung, finden Sie in das Dokument [hier](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).

### <a name="endpoints-enabled"></a>Endpunkte aktiviert

Bei der Installation von AD FS und WAP ein Standardsatz von AD FS-Endpunkte sind aktiviert für den Verbunddienst und für den Proxy.  Diese Standardwerte wurden ausgewählt, basierend auf die am häufigsten erforderlichen und verwendeten Szenarien, und es ist nicht erforderlich, diese zu ändern.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[Optional] Min-Satz von Endpunkten Proxy aktiviert für Azure AD / Office 365
Organisationen, die Bereitstellung von AD FS und WAP nur für Azure AD und Office 365-Szenarien können sogar noch weiter begrenzen die Anzahl der AD FS-Endpunkte, die auf dem Proxy aktiviert werden, um eine weitere minimale Angriffsfläche zu erzielen.
Im folgenden finden Sie die Liste der Endpunkte, die für den Proxy in diesen Szenarien aktiviert werden muss:

|Endpunkt|Zweck
|-----|-----
|/adfs/ls|Browserbasierte authentifizierungsflüsse und die aktuelle Versionen von Microsoft Office verwenden Sie diesen Endpunkt für Azure AD und Office 365-Authentifizierung
|/adfs/services/trust/2005/usernamemixed|Für Exchange Online verwendet mit Office-Clients, die älter sind als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/adfs/services/trust/13/usernamemixed|Für Exchange Online verwendet mit Office-Clients, die älter sind als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/adfs/oauth2|Dieser wird verwendet, für alle modernen apps (lokal oder in der Cloud) auf, die Sie direkt in AD FS (d. h. nicht über AAD) Authentifizierung konfiguriert haben
|/adfs/services/trust/mex|Für Exchange Online verwendet mit Office-Clients, die älter sind als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |Anforderung für alle passive Abläufe und von Office 365 / Azure AD zum Überprüfen der AD FS-Zertifikaten verwendet


AD FS-Endpunkte können für den Proxy mit dem folgenden PowerShell-Cmdlet deaktiviert werden:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

Zum Beispiel:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>Erweiterter Schutz für Authentifizierung
Erweiterter Schutz für die Authentifizierung ist ein Feature, das für Man-in-middle (MITM)-Angriffe verringert und werden standardmäßig mit AD FS aktiviert ist.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie die folgenden Schritte ausführen:
Die Einstellung kann überprüft werden, mit dem folgenden PowerShell-Cmdlet.  
    
   `PS:\>Get-ADFSProperties`

Die Eigenschaft ist `ExtendedProtectionTokenCheck`.  Die Standardeinstellung ist die zulassen, damit die Sicherheitsvorteile, ohne die Probleme mit der Anwendungskompatibilität mit Browsern erreicht werden können, die die Funktion nicht unterstützen.  

### <a name="congestion-control-to-protect-the-federation-service"></a>Überlastungssteuerung, um den Verbunddienst zu schützen.
Der Verbunddienstproxy (Teil der WAP) stellt die überlastungssteuerung zum Schutz von AD FS-Diensts aus einer Flut von Anforderungen bereit.  Der Webanwendungsproxy lehnt externe clientauthentifizierungsanforderungen aus, wenn der Verbundserver überlastet ist, wie durch die Latenz zwischen dem Webanwendungsproxy und dem Verbundserver erkannt wurde.  Diese Funktion wird standardmäßig mit einem empfohlenen Schwellenwert festgelegten latenzzeitebene konfiguriert.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie die folgenden Schritte ausführen:
1.  Starten Sie auf dem Webanwendungsproxy-Computer ein Fenster mit erhöhten Rechten aus.
2.  Navigieren Sie zum ADFS-Verzeichnis % WINDIR%\adfs\config.
3.  Ändern Sie die Standardwerte, die Einstellungen für die überlastungssteuerung "<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />".
4.  Speichern und schließen Sie die Datei.
5.  Starten Sie den AD FS-Dienst durch Ausführen von "net Stop Adfssrv", und klicken Sie dann "net Start Adfssrv" neu.
Zur Referenz, Hinweise zu dieser Funktion finden Sie [hier](https://msdn.microsoft.com/en-us/library/azure/dn528859.aspx ).

### <a name="standard-http-request-checks-at-the-proxy"></a>Standard-HTTP-Anforderung überprüft werden, auf dem proxy
Der Proxy führt auch die folgenden standard-Prüfungen für den gesamten Datenverkehr an:

- Die FS-P selbst wird für AD FS über ein kurzlebiges Zertifikat authentifiziert.  In einem Szenario der mutmaßlicher Verlust des dmz-Server kompromittiert AD FS "proxyvertrauensstellung können widerrufen", damit es ohne mehr alle eingehenden Anforderungen von möglicherweise als vertrauenswürdig eingestuft Proxys. Aufheben der proxyvertrauensstellung widerruft jedes Zertifikat des Proxys, damit sie für beliebige Zwecke der AD FS-Server erfolgreich authentifizieren kann
- Die FS-P beendet alle Verbindungen und erstellt eine neue HTTP-Verbindung mit der AD FS-Dienst auf dem internen Netzwerk. Dies bietet einen Puffer auf Sitzungsebene zwischen externen Geräte und AD FS-Diensts. Das externe Gerät verbindet sich nie direkt mit der AD FS-Dienst.
- Die FS-P überprüft die HTTP-Anforderung, insbesondere bei der HTTP-Header herausgefiltert, die nicht von AD FS-Dienst erforderlich sind.

## <a name="recommended-security-configurations"></a>Empfohlenen Sicherheitskonfigurationen
Stellen Sie sicher, dass alle AD FS und WAP-Server der meisten aktuellen Updates erhalten, die die wichtigsten sicherheitsempfehlung für AD FS-Infrastruktur wird sichergestellt, dass Sie eine Möglichkeit zur Ihrer AD FS und WAP-Server mit allen Sicherheitsupdates als auch die optionale aktualisieren verfügen Updates, die als wichtig für AD FS auf dieser Seite angegeben werden.

Die empfohlene Vorgehensweise für Azure AD-Kunden zum Überwachen und zu den neuesten Stand ist ihre Infrastruktur über Azure AD Connect Health für AD FS ist ein Feature von Azure AD Premium.  Azure AD Connect Health enthält Überwachungen und Warnungen, die auslösen, wenn auf ein AD FS oder WAP-Computer eines der wichtigen Updates speziell für AD FS und WAP fehlt.

Informationen zum Installieren von Azure AD Connect Health für AD FS finden [hier](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/).

## <a name="additional-security-configurations"></a>Zusätzliche Sicherheitskonfigurationen
Optional können die folgenden zusätzlichen Funktionen konfiguriert werden, um zusätzlichen Schutz zu derjenigen, die in der standardbereitstellung zu ermöglichen.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>"Soft" extranetsperrschutz für Konten
Ein AD FS-Administrator kann mit dem extranetsperre-Feature in Windows Server 2012 R2 können maximal zulässige Anzahl von fehlgeschlagene Authentifizierungsanfragen (ExtranetLockoutThreshold) festlegen und ein "Beobachtung des Fensters Zeitraum (ExtranetObservationWindow). Wenn diese maximale Anzahl (ExtranetLockoutThreshold) von authentifizierungsanforderungen erreicht wird, beendet AD FS mit dem Versuch, die die angegebenen Anmeldeinformationen für AD FS für den festgelegten Zeitraum (ExtranetObservationWindow) zu authentifizieren. Diese Aktion schützt dieses Konto von einem AD-kontosperrungen, in anderen Worten, dieses Konto vor Verlust des Zugriffs auf Unternehmensressourcen zugreifen, die auf AD FS für die Authentifizierung des Benutzers basieren geschützt ist. Diese Einstellungen gelten für alle Domänen, die der AD FS-Dienst authentifiziert werden kann.

Folgende Windows PowerShell-Befehle können die AD FS extranet Lockout (z. B.) festlegen: 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

Zu Referenzzwecken den öffentliche Dokumentation zu dieser Funktion ist [hier](https://technet.microsoft.com/library/dn486806.aspx ). 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>Unterscheiden von Zugriffsrichtlinien für Intranet- und extranet-Zugriff
AD FS hat die Möglichkeit, Richtlinien für den Zugriff für Anforderungen zu unterscheiden, die in den lokalen, Unternehmens-Netzwerk-Vs-Anforderungen stammen, die aus dem Internet über den Proxy stammen.  Dies kann pro Anwendung oder global erfolgen.  Erwägen Sie für geschäftskritische Anwendungen oder Anwendungen mit sensible oder personenbezogene Informationen erfordern von Multi-Factor Authentication aus.  Dies kann über die AD FS-Verwaltungs-Snap-in erfolgen.  

### <a name="require-multi-factor-authentication-mfa"></a>Erfordern von Multi-Factor Authentication (MFA)
AD FS kann konfiguriert werden, dass strenge Authentifizierung (z. B. Multi-Factor Authentication) erforderlich sind, speziell für Anforderungen eingehen, über den Proxy, für einzelne Anwendungen und für den bedingten Zugriff auf beide Azure AD / Office 365 und lokale Ressourcen.  Unterstützte Verfahren zum MFA umfassen sowohl Microsoft Azure MFA und Drittanbieter-Anbieter.  Der Benutzer wird aufgefordert, die zusätzliche Informationen bereitzustellen (z. B. ein SMS-Text, enthält eine Uhrzeit Code), und AD FS funktioniert, mit dem anbieterspezifischen-Plug-in, um Zugriff zu ermöglichen.  

Unterstützte externe MFA-Anbieter sind in aufgeführten [dies](https://technet.microsoft.com/library/dn758113.aspx) Seite als auch globale HDI.

### <a name="hardware-security-module-hsm"></a>Hardwaresicherheitsmodul (HSM)
In der Standardkonfiguration lassen verwendet der AD FS-Schlüssel zum Signieren von Token nie die Verbundservern im Intranet.  Sie sind nicht vorhanden, in der DMZ oder auf die Proxycomputer.  Um zusätzlichen Schutz bieten, können diese Schlüssel optional in einem Hardwaresicherheitsmodul, das mit AD FS verbunden geschützt werden.  Microsoft führt nicht zu einem HSM-Produkt, es gibt jedoch mehrere auf dem Markt, die AD FS-Unterstützung.  Um diese Empfehlung zu implementieren, führen Sie in der Vendor-Anleitung zum Erstellen der X509 Zertifikate für Signierung und Verschlüsselung, verwenden Sie dann die AD FS-Installation Powershell-Cmdlets, die benutzerdefinierte Zertifikate wie folgt angeben:

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

Dabei gilt Folgendes:


- `CertificateThumbprint` ist das SSL-Zertifikat
- `SigningCertificateThumbprint` ist Ihr Signaturzertifikat (mit den HSM geschützten Schlüssels)
- `DecryptionCertificateThumbprint` ist Ihr Verschlüsselungszertifikat (mit den HSM geschützten Schlüssels)



