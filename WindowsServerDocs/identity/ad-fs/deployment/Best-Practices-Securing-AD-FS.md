---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: Bewährte Methoden zum Sichern von AD FS und webanwendungsproxys
description: Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) (AD FS) und webanwendungsproxy.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bf7e2ed20a59bb021627a8a58f869ea5d94bf2b7
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868185"
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Bewährte Methoden zum Sichern von Active Directory-Verbunddienste (AD FS)


Dieses Dokument enthält bewährte Methoden für die sichere Planung und Bereitstellung von Active Directory-Verbunddienste (AD FS) (AD FS) und webanwendungsproxy.  Sie enthält Informationen über das Standardverhalten dieser Komponenten und Empfehlungen für zusätzliche Sicherheits Konfigurationen für eine Organisation mit spezifischen Anwendungsfällen und Sicherheitsanforderungen.

Dieses Dokument gilt für AD FS und WAP in Windows Server 2012 R2 und Windows Server 2016 (Vorschau).  Diese Empfehlungen können verwendet werden, unabhängig davon, ob die Infrastruktur in einem lokalen Netzwerk oder in einer in der Cloud gehosteten Umgebung wie Microsoft Azure bereitgestellt wird.

## <a name="standard-deployment-topology"></a>Standard Bereitstellungs Topologie
Für die Bereitstellung in lokalen Umgebungen wird eine Standard Bereitstellungs Topologie empfohlen, die aus einem oder mehreren AD FS Servern im internen Unternehmensnetzwerk besteht. dabei wird mindestens ein webanwendungsproxy-Server (WAP) in einem DMZ-oder Extranet-Netzwerk bereitgestellt.  Auf jeder Ebene, AD FS und WAP, wird ein Hardware-oder Software Lastenausgleich vor der Serverfarm platziert und verarbeitet das Datenverkehrs Routing.  Firewalls werden nach Bedarf vor der externen IP-Adresse des Load Balancers vor jeder (FS-und Proxy-) Farm platziert.

![AD FS Standard Topologie](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>Erforderliche Ports
Das folgende Diagramm zeigt die Firewallports, die zwischen und unter den Komponenten der AD FS-und WAP-Bereitstellung aktiviert werden müssen.  Wenn die Bereitstellung nicht Azure AD/Office 365 umfasst, können die Synchronisierungs Anforderungen ignoriert werden.

>Beachten Sie, dass Port 49443 nur erforderlich ist, wenn die Benutzerzertifikat Authentifizierung verwendet wird. Dies ist für Azure AD und Office 365 optional.

![AD FS Standard Topologie](media/Best-Practices-Securing-AD-FS/adfssec2.png)

>[!NOTE]
> Port 808 (Windows Server 2012r2) oder Port 1501 (Windows Server 2016 und höher) ist der net. TCP-Port AD FS der für den lokalen WCF-Endpunkt verwendet wird, um Konfigurationsdaten an den Dienst Prozess und PowerShell zu übertragen. Dieser Port kann durch Ausführen von Get-ADF sproperties angezeigt werden. Wählen Sie nettcpport aus. Dabei handelt es sich um einen lokalen Port, der nicht in der Firewall geöffnet werden muss, sondern in einem Portscan angezeigt wird. 

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect und Verbund Server/WAP
In dieser Tabelle werden die Ports und Protokolle beschrieben, die für die Kommunikation zwischen dem Azure AD Connect-Server und Verbund-/WAP-Servern erforderlich sind.  

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |---------
HTTP|80 (TCP/UDP)|Dient zum Herunterladen von CRLs (Zertifikat Sperr Listen) zum Überprüfen von SSL-Zertifikaten.
HTTPS|443 (TCP/UDP)|Wird für die Synchronisierung mit Azure AD verwendet.
WinRM|5985| WinRM-Listener

### <a name="wap-and-federation-servers"></a>WAP-und Verbund Server
In dieser Tabelle werden die Ports und Protokolle beschrieben, die für die Kommunikation zwischen den Verbund Servern und WAP-Servern erforderlich sind.

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |---------
HTTPS|443 (TCP/UDP)|Wird für die Authentifizierung verwendet.

### <a name="wap-and-users"></a>WAP und Benutzer
In dieser Tabelle werden die Ports und Protokolle beschrieben, die für die Kommunikation zwischen Benutzern und den WAP-Servern erforderlich sind.

Protokoll |Anschlüsse |Beschreibung
--------- | --------- |--------- |
HTTPS|443 (TCP/UDP)|Wird für die Geräte Authentifizierung verwendet.
TCP|49443 (TCP)|Wird für die Zertifikat Authentifizierung verwendet.

Weitere Informationen zu den erforderlichen Ports und Protokollen, die für Hybrid Bereitstellungen erforderlich sind, finden Sie in [diesem Dokument.](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/)

Ausführliche Informationen zu Ports und Protokollen, die für eine Bereitstellung von Azure AD und Office 365 erforderlich sind, finden Sie in [diesem Dokument.](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)

### <a name="endpoints-enabled"></a>Aktivierte Endpunkte

Wenn AD FS und WAP installiert sind, wird ein Standardsatz von AD FS Endpunkten für den Verbund Dienst und den Proxy aktiviert.  Diese Standardeinstellungen wurden basierend auf den am häufigsten benötigten und verwendeten Szenarien ausgewählt, und es ist nicht notwendig, Sie zu ändern.  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>Optionale Minimaler Satz von Endpunkten, für Azure AD/Office 365 aktiviert
Organisationen, die AD FS und WAP nur für Azure AD-und Office 365-Szenarien bereitstellen, können die Anzahl von AD FS Endpunkten, die auf dem Proxy aktiviert sind, begrenzen, um eine minimale Angriffsfläche zu erzielen.
Im folgenden finden Sie eine Liste der Endpunkte, die auf dem Proxy in folgenden Szenarien aktiviert werden müssen:

|Endpunkt|Zweck
|-----|-----
|/ADFS/ls|Browser basierte Authentifizierungs Abläufe und aktuelle Versionen von Microsoft Office verwenden Sie diesen Endpunkt für die Azure AD-und Office 365-Authentifizierung.
|/adfs/services/trust/2005/usernamemixed|Wird für Exchange Online mit Office-Clients verwendet, die älter sind als Office 2013-Update von Mai 2015.  Spätere Clients verwenden den passiven Endpunkt \adfs\ls.
|/adfs/services/trust/13/usernamemixed|Wird für Exchange Online mit Office-Clients verwendet, die älter sind als Office 2013-Update von Mai 2015.  Spätere Clients verwenden den passiven Endpunkt \adfs\ls.
|/adfs/oauth2|Diese wird für alle modernen Apps (lokal oder in der Cloud) verwendet, die Sie für die direkte Authentifizierung bei AD FS (d. h. nicht über AAD) konfiguriert haben.
|/adfs/services/trust/mex|Wird für Exchange Online mit Office-Clients verwendet, die älter sind als Office 2013-Update von Mai 2015.  Spätere Clients verwenden den passiven Endpunkt \adfs\ls.
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |Anforderung für passive Flows und von Office 365/Azure AD verwendet werden, um AD FS Zertifikate zu überprüfen


AD FS Endpunkte können mithilfe des folgenden PowerShell-Cmdlets auf dem Proxy deaktiviert werden:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

Zum Beispiel:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>Erweiterter Schutz für die Authentifizierung
Der erweiterte Schutz für die Authentifizierung ist ein Feature, das gegen man-in-the-Middle-Angriffen (MITM) abwehrt und standardmäßig mit AD FS aktiviert ist.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie die folgenden Schritte ausführen:
Die Einstellung kann mithilfe des folgenden PowerShell-Cmdlets überprüft werden.  
    
   `PS:\>Get-ADFSProperties`

Die-Eigenschaft `ExtendedProtectionTokenCheck`ist.  Die Standardeinstellung ist zulassen, sodass die Sicherheitsvorteile ohne die Kompatibilitätsprobleme mit Browsern erzielt werden können, die die Funktion nicht unterstützen.  

### <a name="congestion-control-to-protect-the-federation-service"></a>Überlastungs Steuerung zum Schutz des Verbund Dienstanbieter
Der Verbund Dienst Proxy (Teil des WAP) stellt die Überlastungs Steuerung zum Schutz des AD FS Dienstanbieter vor einer Flut von Anforderungen bereit.  Der webanwendungsproxy lehnt externe Client Authentifizierungsanforderungen ab, wenn der Verbund Server durch die Latenz zwischen dem webanwendungsproxy und dem Verbund Server erkannt wird.  Diese Funktion ist standardmäßig mit einem empfohlenen Schwellenwert für die Latenzzeit konfiguriert.

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>Um die Einstellungen zu überprüfen, können Sie die folgenden Schritte ausführen:
1.  Starten Sie auf dem webanwendungsproxy-Computer ein Befehlsfenster mit erhöhten Rechten.
2.  Navigieren Sie zum Verzeichnis ADFS unter%windir%\adfs\config.
3.  Ändern Sie die Einstellungen für die Überlastungs Steuerung von<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />den Standardwerten in "".
4.  Speichern und schließen Sie die Datei.
5.  Starten Sie den AD FS-Dienst neu, indem Sie "NET stoppt ADF" und dann "NET Start ADF" ausführen.
Hinweise zu dieser Funktion finden Sie [hier](https://msdn.microsoft.com/library/azure/dn528859.aspx ).

### <a name="standard-http-request-checks-at-the-proxy"></a>Standard-HTTP-Anforderungs Prüfungen auf dem Proxy
Der Proxy führt außerdem die folgenden Standardprüfungen für den gesamten Datenverkehr durch:

- Der FS-P selbst authentifiziert sich bei AD FS über ein kurzlebiges Zertifikat.  In einem Szenario mit einer verdächtigen Gefährdung der DMZ-Server können AD FS die Proxy Vertrauensstellung widerrufen, sodass eingehende Anforderungen von potenziell kompromittierten Proxys nicht mehr vertraut werden. Durch das Aufheben der Proxy Vertrauensstellung wird das eigene Zertifikat eines Proxys widerrufen, sodass es für keinen Zweck für den AD FS Server authentifiziert werden kann.
- FS-P beendet alle Verbindungen und erstellt eine neue HTTP-Verbindung mit dem AD FS-Dienst im internen Netzwerk. Dadurch wird ein Puffer auf Sitzungs Ebene zwischen externen Geräten und dem AD FS-Dienst bereitstellt. Das externe Gerät stellt nie eine direkte Verbindung mit dem AD FS-Dienst her.
- Der FS-P führt die HTTP-Anforderungs Überprüfung aus, die speziell HTTP-Header filtert, die nicht für AD FS-Dienst erforderlich sind.

## <a name="recommended-security-configurations"></a>Empfohlene Sicherheits Konfigurationen
Stellen Sie sicher, dass alle AD FS-und WAP-Server die aktuellsten Updates erhalten. die wichtigste Sicherheitsempfehlung für Ihre AD FS-Infrastruktur besteht darin sicherzustellen, dass Sie über eine Möglichkeit verfügen, Ihre AD FS und WAP-Server mit allen Sicherheitsupdates und den optionalen Updates, die für AD FS auf dieser Seite als wichtig festgelegt wurden.

Die empfohlene Vorgehensweise für Azure AD Kunden, ihre Infrastruktur zu überwachen und zu behalten, ist die Azure AD Connect Health für AD FS, eine Funktion Azure AD Premium.  Azure AD Connect Health enthält Monitore und Warnungen, die auslöst, wenn ein AD FS-oder WAP-Computer eines der wichtigen Updates für AD FS und WAP fehlt.

Informationen zum Installieren Azure AD Connect Health für AD FS finden Sie [hier](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/).

## <a name="additional-security-configurations"></a>Weitere Sicherheits Konfigurationen
Die folgenden zusätzlichen Funktionen können optional so konfiguriert werden, dass Sie zusätzliche Schutzmaßnahmen bieten, die in der Standard Bereitstellung angeboten werden.

### <a name="extranet-soft-lockout-protection-for-accounts"></a>Extranet "weicher" Sperrungs Schutz für Konten
Mit der extranetsperrungsfunktion in Windows Server 2012 R2 kann ein AD FS Administrator eine maximal zulässige Anzahl von Authentifizierungsanforderungen (extranetlockoutthreshold) und einen Zeit Zeitraum (extranetobservationwindow) für das Überwachungs Fenster festlegen. Wenn diese maximale Anzahl (extranetlockoutthreshold) der Authentifizierungsanforderungen erreicht ist, versucht AD FS nicht mehr, die angegebenen Konto Anmelde Informationen für den festgelegten Zeitraum (extranetobservationwindow) für AD FS zu authentifizieren. Diese Aktion schützt dieses Konto vor einer AD-Konto Sperre, d. h., er schützt dieses Konto vor dem Verlust des Zugriffs auf Unternehmensressourcen, die AD FS für die Authentifizierung des Benutzers erfordern. Diese Einstellungen gelten für alle Domänen, die der AD FS-Dienst authentifizieren kann.

Sie können den folgenden Windows PowerShell-Befehl verwenden, um die AD FS extranetsperre festzulegen (Beispiel): 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

Die öffentliche Dokumentation dieses Features finden Sie [hier](https://technet.microsoft.com/library/dn486806.aspx ). 

### <a name="disable-ws-trust-windows-endpoints-on-the-proxy-ie-from-extranet"></a>Deaktivieren von WS-Trust-Windows-Endpunkten auf dem Proxy, d. h. vom Extranet

WS-Trust-Windows-Endpunkte ( */ADFS/Services/Trust/2005/windowstransport* und */ADFS/Services/Trust/13/windowstransport*) sind nur für Intranetorientierte Endpunkte gedacht, die eine WIA-Bindung auf HTTPS verwenden. Wenn Sie Sie für das Extranet verfügbar machen, können Anforderungen an diese Endpunkte für die Umgehung von Sperrungs Schutz-Anforderungen Diese Endpunkte müssen auf dem Proxy deaktiviert werden (d. h. deaktiviert aus dem Extranet), um die AD-Konto Sperre mithilfe der folgenden PowerShell-Befehle zu schützen. Es gibt keine bekannten Auswirkungen auf Endbenutzer, indem diese Endpunkte auf dem Proxy deaktiviert werden.

    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/2005/windowstransport -Proxy $false
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/windowstransport -Proxy $false
    
### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>Unterscheiden von Zugriffsrichtlinien für Intranet-und Extranetzugriff
AD FS ist in der Lage, Zugriffsrichtlinien für Anforderungen zu unterscheiden, die aus dem lokalen Unternehmensnetzwerk und aus dem Internet über den Proxy stammen.  Dies kann pro Anwendung oder Global erfolgen.  Für Anwendungen mit hohem Geschäftswert oder Anwendungen mit sensiblen oder personenbezogenen Informationen sollten Sie die Multi-Factor Authentication benötigen.  Dies kann über das Snap-in "AD FS-Verwaltung" erfolgen.  

### <a name="require-multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA) erforderlich
AD FS kann so konfiguriert werden, dass eine strenge Authentifizierung (z. b. Multi-Factor Authentication) erforderlich ist, insbesondere für Anforderungen, die über den Proxy, für einzelne Anwendungen und für den bedingten Zugriff auf Azure AD/Office 365 und lokale Ressourcen erfolgen.  Zu den unterstützten MFA-Methoden zählen sowohl Microsoft Azure MFA als auch Drittanbieter Anbietern.  Der Benutzer wird aufgefordert, die zusätzlichen Informationen (z. b. einen SMS-Text mit einem einmaligen Code) anzugeben, und AD FS verwendet das anbieterspezifische Plug-in, um den Zugriff zuzulassen.  

Zu den unterstützten externen MFA-Anbietern zählen die auf [dieser](https://technet.microsoft.com/library/dn758113.aspx) Seite aufgeführten und HDI Global.

### <a name="hardware-security-module-hsm"></a>Hardwaresicherheitsmodul (HSM)
In der Standardkonfiguration werden von den Schlüsseln, AD FS zum Signieren von Token verwendet, die Verbund Server im Intranet nie verlassen.  Sie sind niemals in der DMZ oder auf den Proxy Computern vorhanden.  Optional können diese Schlüssel in einem Hardware Sicherheitsmodul geschützt werden, das AD FS zugeordnet ist, um zusätzlichen Schutz zu bieten.  Microsoft erzeugt kein HSM-Produkt, es gibt jedoch mehrere auf dem Markt, die AD FS unterstützen.  Um diese Empfehlung zu implementieren, befolgen Sie die Anweisungen des Herstellers, um die X509-Zertifikate für Signierung und Verschlüsselung zu erstellen. verwenden Sie dann die AD FS PowerShell-Cmdlets für die Installation, und geben Sie die benutzerdefinierten Zertifikate wie folgt an

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

Dabei gilt:


- `CertificateThumbprint`ist Ihr SSL-Zertifikat
- `SigningCertificateThumbprint`ist Ihr Signaturzertifikat (mit HSM-geschütztem Schlüssel)
- `DecryptionCertificateThumbprint`ist Ihr Verschlüsselungs Zertifikat (mit HSM-geschütztem Schlüssel)



