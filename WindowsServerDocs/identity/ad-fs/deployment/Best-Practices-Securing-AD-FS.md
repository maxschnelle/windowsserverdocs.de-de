---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: "Bewährte Methoden zum Sichern von AD FS und Web Application Proxy"
description: "Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) und Web Application Proxy."
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6026246228b22fdea6001528ab7621a1704f1983
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Bewährte Methoden zum Schützen von Active Directory-Verbunddienste

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) und Web Application Proxy.  Es enthält Informationen über das Standardverhalten für diese Komponenten und Empfehlungen für die zusätzliche Sicherheitskonfigurationen für ein Unternehmen mit bestimmten Anwendungsfälle und sicherheitsanforderungen.

Dieses Dokument gilt für AD FS und WAP in Windows Server 2012 R2 und Windows Server 2016 (Vorschau).  Diese Empfehlungen können verwendet werden, ob die Infrastruktur in einer im lokalen Netzwerk oder in einer gehosteten Cloudumgebung, z. B. Microsoft Azure bereitgestellt wird.

## <a name="standard-deployment-topology"></a>Standard-Bereitstellungstopologie
Für die Bereitstellung in einer lokalen Umgebung empfehlen wir eine standard-Bereitstellungstopologie bestehend aus einem oder mehreren AD FS-Server im internen Unternehmensnetzwerk mit einem oder mehreren Web Application Proxy (WAP)-Servern in einem Umkreisnetzwerk oder extranet-Netzwerk.  Auf jeder Ebene, die AD FS und WAP, wird ein Lastenausgleich Hardware oder Software vor der Serverfarm und Weiterleitung von Datenverkehr verarbeitet.  Firewalls werden je nach Bedarf im Vordergrund der externen IP-Adresse des Lastenausgleichs vor jede Farm (FS und webanwendungsproxy) platziert.

![AD FS-Standard-Topologie](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>Benötigten Ports
Das folgende Diagramm zeigt die Firewall-Ports, die zwischen und einzelnen Komponenten der AD FS und WAP-Bereitstellung aktiviert werden müssen.  Enthält die Bereitstellung keinen Azure AD / Office 365, die Synchronisierung Anforderungen ignoriert werden kann.

>Beachten Sie, dass Port 49443 verwendet nur erforderlich, wenn benutzerzertifikatauthentifizierung ist optional für Azure AD verwendet wird, und Office 365.

![AD FS-Standard-Topologie](media/Best-Practices-Securing-AD-FS/adfssec2.png)

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD verbinden und Federation Server/WAP
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen dem Azure AD Connect-Server und Verbund/WAP-Servern erforderlich sind.  

Protokoll |Ports |Beschreibung
--------- | --------- |---------
HTTP|80 (TCP/UDP)|Zum Herunterladen von Zertifikatsperrlisten (Certificate Revocation Lists) so überprüfen Sie die SSL-Zertifikate verwendet.
HTTPS|443(TCP/UDP)|Zum Synchronisieren mit Azure AD verwendet.
WinRM|5985| WinRM-Listener

### <a name="wap-and-federation-servers"></a>WAP und Verbundserver
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen Verbundservern und WAP-Servern erforderlich sind.

Protokoll |Ports |Beschreibung
--------- | --------- |---------
HTTPS|443(TCP/UDP)|Für die Authentifizierung verwendet.

### <a name="wap-and-users"></a>WAP und Benutzer
Diese Tabelle beschreibt die Ports und Protokolle, die für die Kommunikation zwischen Benutzern und den WAP-Servern erforderlich sind.

Protokoll |Ports |Beschreibung
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|Für die Geräteauthentifizierung verwendet.
TCP|49443 (TCP)|Für die Zertifikatauthentifizierung verwendet.

Weitere Informationen zu erforderlichen Ports und Protokolle, die erforderlichen hybridbereitstellungen finden Sie in das Dokument [hier](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-ports/).

Ausführliche Informationen zu Ports und Protokolle für ein Azure AD erforderlich und Office 365-Bereitstellung finden Sie in das Dokument [hier](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).

### <a name="endpoints-enabled"></a>Endpunkte aktiviert

Wenn AD FS und WAP installiert sind, ein Standardsatz von AD FS-Endpunkte werden aktiviert auf den Verbunddienst und dem Proxy.  Diese Standardwerte wurden ausgewählt basierend auf den am häufigsten Szenarien für erforderlich sind und verwendet, und es ist nicht erforderlich, sie zu ändern.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[Optional] Min Satz von Endpunkten Proxy aktiviert für Azure AD / Office 365
Organisationen, die Bereitstellung von AD FS und WAP nur für Azure AD und Office 365-Szenarien können sogar noch weiter die Anzahl der AD FS-Endpunkte, die auf dem Proxy aktiviert, um eine weitere minimale Angriffsfläche zu erzielen.
Nachfolgend finden Sie die Liste der Endpunkte, die auf dem Proxy in diesen Szenarien aktiviert werden müssen:

|Endpunkt|Zweck
|-----|-----
|/ Adfs/ls|Browserbasierte authentifizierungsflüssen und aktuelle Versionen von Microsoft Office verwenden diesen Endpunkt für Azure AD und Office 365-Authentifizierung
|/ADFS/Services/Trust/2005/usernamemixed|Für Exchange Online verwendet mit Office-Clients, die älter als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/ADFS/Services/trust/13/usernamemixed|Für Exchange Online verwendet mit Office-Clients, die älter als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/ Adfs/oauth2|Diese wird verwendet, für alle modernen apps (auf lokale oder in der Cloud), die Sie für die Authentifizierung von direkt an AD FS (d. h. nicht durch eine AAD) konfiguriert haben
|/ADFS/Services/trust/mex|Für Exchange Online verwendet mit Office-Clients, die älter als Update für Office 2013 Mai 2015.  Neuere Clients verwenden den passiven \adfs\ls-Endpunkt.
|/ADFS/ls/FederationMetadata/2007-06/FederationMetadata.Xml |Anforderung für eine beliebige passive Abläufe; vom Office 365 / Azure AD So überprüfen Sie die AD FS-Zertifikaten verwendet


AD FS-Endpunkte können für den Proxy mit dem folgenden PowerShell-Cmdlet deaktiviert werden:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

Zum Beispiel:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>Erweiterter Schutz für Authentifizierung
Der erweiterte Schutz für die Authentifizierung ist ein Feature, das vor Man-in-Angriffe (MITM) reduziert und ist standardmäßig mit AD FS aktiviert.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie Folgendes tun:
Die Einstellung kann überprüft werden, mit dem folgenden PowerShell-Cmdlet.  
    
   `PS:\>Get-ADFSProperties`

Die Eigenschaft ist `ExtendedProtectionTokenCheck`.  Die Standardeinstellung ist zulassen, damit die Sicherheitsvorteile ohne der Kompatibilitätsprobleme mit Browsern erreicht werden können, die die Funktion nicht unterstützen.  

### <a name="congestion-control-to-protect-the-federation-service"></a>Überlastung-Steuerelement, um den Verbunddienst zu schützen.
Der Verbunddienstproxy (Teil der WAP) bietet Überlastung-Steuerelement, um den AD FS-Dienst von einer Flut von Anfragen zu schützen.  Wenn der Verbundserver überlastet ist, wie durch die Wartezeit zwischen dem Web Application Proxy und dem Verbundserver erkannt the Web Application Proxy externe Clientanforderungen für Authentifizierung abgelehnt.  Dieses Feature ist standardmäßig mit einen Schwellenwert für die empfohlenen Wartezeit konfiguriert.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie Folgendes tun:
1.  Starten Sie auf Ihrem Computer Web Application Proxy ein Befehlsfenster mit erhöhten Rechten.
2.  Navigieren Sie zu dem AD FS-Verzeichnis, % WINDIR%\adfs\config.
3.  Ändern Sie die Überlastung Kontrolle über seine Standardwerte auf '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />'.
4.  Speichern Sie und schließen Sie die Datei.
5.  Mit "net Stop Adfssrv", und klicken Sie dann 'net Start Adfssrv', um den AD FS-Dienst neu zu starten.
Für den Verweis auf diese Funktion können werden Ratschläge [hier](https://msdn.microsoft.com/en-us/library/azure/dn528859.aspx ).

### <a name="standard-http-request-checks-at-the-proxy"></a>Standard-HTTP-Anforderung überprüft wird, auf dem proxy
Der Proxy führt auch die folgenden standardmäßigen überprüft vor der gesamte Datenverkehr:

- AD FS über ein kurzlebiges Zertifikat authentifiziert FS-P selbst.  In einem Szenario der mutmaßlicher Verlust dmz-Server gefährdet AD FS "proxyvertrauensstellung revoke können", damit sie alle eingehenden Anforderung aus nicht mehr potenziell vertraut Proxys. Sperren der proxyvertrauensstellung sperrt jedes Zertifikat des Proxys, damit sie erfolgreich zu beliebigen Zwecken zu AD FS-Server authentifizieren kann
- Die FS-P beendet alle Verbindungen und erstellt eine neue HTTP-Verbindung mit der AD FS-Dienst auf dem internen Netzwerk. Dadurch wird einen Anwendungsebene Puffer zwischen externe Geräte und dem AD FS-Dienst. Externe Gerät verbindet sich nie direkt mit der AD FS-Dienst.
- FS-P führt die Überprüfung der HTTP-Anforderung, die speziell HTTP-Header herausfiltert, die nicht von AD FS-Dienst erforderlich sind.

## <a name="recommended-security-configurations"></a>Empfohlene Sicherheitskonfiguration
Alle AD FS sicherzustellen und WAP-Server empfangen die aktuellsten Updates die wichtigste Sicherheit Empfehlung für AD FS-Infrastruktur besteht darin, sicherzustellen, dass Sie eine Möglichkeit, alle Sicherheitsupdates als auch die optionalen Updates, die als wichtig für AD FS auf dieser Seite angegebenen Aktualität der AD FS und WAP-Server verfügen.

Die empfohlene Methode für Azure AD-Kunden zu überwachen und Stand ist ihre Infrastruktur über Azure AD Connect Health für AD FS, ein Feature des Azure AD Premium.  Azure AD Connect Health enthält Überwachungen und Warnungen, die ausgelöst werden, wenn ein AD FS oder WAP-Computer eine wichtige Updates speziell für AD FS und WAP fehlt.

Informationen zum Installieren von Azure AD Connect Health für AD FS finden [hier](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-health-agent-install/).

## <a name="additional-security-configurations"></a>Zusätzliche Sicherheitskonfigurationen
Die folgenden zusätzlichen Funktionen können optional konfiguriert werden, um zusätzlichen Schutz, denen in der Standard-Bereitstellung bereitstellen.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>Extranet "soft" Sperre Schutz für Konten
Mit dem extranet sperrungsfeature in Windows Server 2012 R2 ein AD FS-Administrator kann maximal zulässige Anzahl von fehlgeschlagenen authentifizierungsanforderungen (ExtranetLockoutThreshold) festgelegt und ein ' des Fensters Beobachtung Zeitraum (ExtranetObservationWindow). Wenn diese maximal (ExtranetLockoutThreshold) authentifizierungsanforderungen erreicht ist, versucht AD FS die angegebenen Kontoanmeldeinformationen für AD FS für den festgelegten Zeitraum (ExtranetObservationWindow) zu authentifizieren. Diese Aktion schützt dieses Konto aus einer Kontosperre AD, in anderen Worten: dieses Konto vor Verlust des Zugriffs auf Unternehmensressourcen, die von AD FS für die Authentifizierung des Benutzers abhängen geschützt. Diese Einstellungen gelten für alle Domänen, die der AD FS-Dienst authentifiziert werden kann.

Die folgenden Windows PowerShell-Befehl können Sie die AD FS-extranet-Sperre (Beispiel) festgelegt: 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

Referenz die öffentliche Dokumentation für dieses Feature ist [hier](https://technet.microsoft.com/en-us/library/dn486806.aspx ). 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>Unterscheiden von Zugriffsrichtlinien für Intranet- und extranet-Zugriff
AD FS hat die Möglichkeit, Richtlinien für Anforderungen unterscheiden, die in der lokalen, corporate Vs netzwerkanforderungen, die über den Proxy aus dem Internet stammen stammen,.  Dies kann pro Anwendung oder global erfolgen.  Hoher Wert Geschäftsanwendungen oder Anwendungen mit persönlichen oder sensiblen Informationen umgehen sollten Sie die Multi-Factor Authentication erfordern.  Dies kann über die AD FS-Verwaltungs-Snap-in erfolgen.  

### <a name="require-multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA) erfordern
AD FS kann so konfiguriert werden, dass strenge Authentifizierung (z. B. Multi-Factor Authentication) speziell für Anfragen über den Proxy, für die einzelnen Anwendungen und für den bedingten Zugriff auf Azure AD-erfordern / Office 365 und lokale Ressourcen.  Unterstützte Methoden MFA umfassen Microsoft Azure MFA und Drittanbieter-Anbieter.  Der Benutzer wird aufgefordert, zusätzliche Informationen bereitstellen (z. B. eine SMS-Text, enthält eine Zeit Code), und AD FS ist mit spezifischen Anbieter-Plug-in, um Zugriff zu ermöglichen.  

Unterstützte externe MFA-Anbieter enthalten den Angaben unter [dies](https://technet.microsoft.com/en-us/library/dn758113.aspx) Seite sowie globale HDI.

### <a name="hardware-security-module-hsm"></a>Hardwaresicherheitsmodul (HSM)
In der Standardkonfiguration lassen verwendet die AD FS-Schlüssel zum Signieren von Token niemals die Verbundservern im Intranet.  Sie sind nicht vorhanden, in dem Umkreisnetzwerk oder auf die Proxycomputer.  Um zusätzlichen Schutz zu bieten, können diese Schlüssel optional in einem Hardwaresicherheitsmodul an der AD FS geschützt werden.  Microsoft wird kein HSM-Produkt erstellt, es gibt jedoch mehrere auf dem Markt, die AD FS-Unterstützung.  Um diese Empfehlung zu implementieren, führen Sie die Anbieter-Anleitung zum Erstellen der X509 Zertifikate für Signierung und Verschlüsselung, verwenden Sie dann die AD FS-Installation Powershell-Cmdlets, die benutzerdefinierte Zertifikate wie folgt angeben:

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

Dabei gilt:


- `CertificateThumbprint` ist das SSL-Zertifikat
- `SigningCertificateThumbprint` ist Ihr Signaturzertifikat (mit HSM-geschützten Schlüssel)
- `DecryptionCertificateThumbprint` ist das Verschlüsselungszertifikat (mit HSM-geschützten Schlüssel)



