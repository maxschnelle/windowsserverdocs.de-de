---
title: Erweiterte Features von Always On VPN
description: Neben dem Bereitstellungs Szenario in dieser Bereitstellung können Sie weitere erweiterte VPN-Features hinzufügen, um die Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung zu verbessern.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/24/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: fd3ebf1acada5de1ed3f4b14ddeca761728ffa75
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965542"
---
# <a name="advanced-features-of-always-on-vpn"></a>Erweiterte Features von Always On VPN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Erfahren Sie mehr über die Always on VPN-Technologie](../always-on-vpn-technology-overview.md)
- [**Weiter:** Beginnen der Planung der Always on-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

Neben den bereitgestellten Bereitstellungs Szenarien können Sie weitere erweiterte VPN-Features hinzufügen, um die Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung zu verbessern. Beispielsweise kann der VPN-Server diese Features verwenden, um sicherzustellen, dass der Verbindungs Client fehlerfrei ist, bevor er eine Verbindung zulässt.

## <a name="high-availability"></a>Hochverfügbarkeit

Im folgenden finden Sie zusätzliche Optionen für hohe Verfügbarkeit.

|Option  |Beschreibung  |
|---------|---------|
|Server Resilienz und Lastenausgleich     |In Umgebungen, die Hochverfügbarkeit erfordern oder eine große Anzahl von Anforderungen unterstützen, können Sie die Leistung und Resilienz des Remote Zugriffs steigern, indem Sie den Lastenausgleich zwischen mehreren Servern verwenden, auf denen ein Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, und die Aktivierung des RAS-Server Clustering<p>Verwandte Dokumente:<ul><li>[NPS-Proxy Server-Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Bereitstellen des Remotezugriffs in einem Cluster](../../../ras/cluster/deploy-remote-access-in-cluster.md)</li></ul>        |
|Stabilität des geografischen Standorts     |Für die IP-basierte geolozierung können Sie globale Traffic Manager mit DNS in Windows Server 2016 verwenden. Um einen stabileren geografischen Lastenausgleich zu erreichen, können Sie Lösungen für den Lastenausgleich auf globaler Server wie Microsoft Azure Traffic Manager verwenden.<p>Verwandte Dokumente:<ul><li>[Was ist Traffic Manager?](/azure/traffic-manager/traffic-manager-overview)</li><li>[Was ist Traffic Manager?](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>Erweiterte Authentifizierung

Im folgenden finden Sie zusätzliche Authentifizierungs Optionen.

|Option  |Beschreibung  |
|---------|---------|
|Windows Hello for Business     |In Windows 10 ersetzt Windows Hello for Business Kenn Wörter durch eine starke zweistufige Authentifizierung auf PCs und mobilen Geräten. Diese Authentifizierung besteht aus einem neuen Typ von Benutzer Anmelde Informationen, der an ein Gerät gebunden ist und eine biometrische oder persönliche Identifikationsnummer (PIN) verwendet.<p>Der Windows 10-VPN-Client ist kompatibel mit Windows Hello for Business. Nachdem sich der Benutzer mit einer Geste anmeldet, verwendet die VPN-Verbindung das Windows Hello for Business-Zertifikat für die Zertifikat basierte Authentifizierung.<p>Verwandte Dokumente:<ul><li>[Windows Hello for Business](/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Technische Fallstudie: [Aktivieren des Remote Zugriffs mit Windows Hello for Business in Windows 10](/previous-versions//mt728163(v=technet.10))</li></ul>         |
|Azure Multi-Factor Authentication (MFA)     |Azure MFA verfügt über Cloud-und lokale Versionen, die Sie in den Windows-VPN-Authentifizierungsmechanismus integrieren können.<p>Weitere Informationen zur Funktionsweise dieses Mechanismus finden Sie unter [integrieren der RADIUS-Authentifizierung in Azure Multi-Factor Authentication-Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

## <a name="advanced-vpn-features"></a>Erweiterte VPN-Features

Im folgenden finden Sie zusätzliche Optionen für erweiterte Funktionen.

|Option  |Beschreibung  |
|---------|---------|
|Filtern von Datenverkehr     |Wenn Sie die Auswahl der Anwendungen erzwingen müssen, auf die VPN-Clients zugreifen können, können Sie VPN-Datenverkehrs Filter aktivieren.<p>Weitere Informationen finden Sie unter [VPN-Sicherheitsfeatures](/windows/access-protection/vpn/vpn-security-features).         |
|Durch Apps ausgelöstes VPN     |Sie können VPN-Profile so konfigurieren, dass Sie automatisch eine Verbindung herstellen, wenn bestimmte Anwendungen oder Anwendungs Typen gestartet werden.<p>Weitere Informationen zu dieser und anderen auslösenden Optionen finden Sie unter von [automatisch ausgelöste VPN-Profil Optionen](/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|Bedingter VPN-Zugriff   |Bedingter Zugriff und Geräte Konformität können von verwalteten Geräten verlangt werden, dass Sie die Standards erfüllen, bevor Sie eine Verbindung mit dem VPN herstellen können. Eine der erweiterten Features für den bedingten VPN-Zugriff ermöglicht es Ihnen, die VPN-Verbindungen auf solche einzuschränken, auf denen das Client Authentifizierungszertifikat die OID "Aad Conditional Access" von **1.3.6.1.4.1.311.87**enthält.<p>Um die VPN-Verbindungen einzuschränken, müssen Sie die folgenden Schritte ausführen:<ol><li>Öffnen Sie auf dem NPS-Server das Snap-in " **Netzwerk Richtlinien Server** ".</li><li>Erweitern Sie **Richtlinien**  >  **Netzwerk Richtlinien**.</li><li>Klicken Sie mit der rechten Maustaste auf die Netzwerk Richtlinie **VPN-Verbindungen (virtuelles privates Netzwerk)** , und wählen Sie **Eigenschaften**.</li><li>Wählen Sie die Registerkarte **Einstellungen** aus.</li><li>Wählen Sie **Hersteller spezifisch**aus, und klicken Sie dann auf **Hinzufügen**.</li><li>Wählen Sie die Option **Allowed-Certificate-OID** aus, und klicken Sie dann auf **Hinzufügen**.</li><li>Fügen Sie die Aad Conditional Access OID of **1.3.6.1.4.1.311.87** als Attribut Wert ein, und wählen Sie dann zweimal **OK** aus.</li><li>Wählen Sie **Schließen**aus, und klicken Sie dann auf **anwenden**.<p>Nachdem Sie diese Schritte ausgeführt haben, schlägt die Verbindung fehl, wenn VPN-Clients versuchen, eine Verbindung mit einem anderen Zertifikat als dem kurzlebigen cloudzertifikat herzustellen.</li></ol>Weitere Informationen zum bedingten Zugriff finden Sie unter [VPN und bedingter Zugriff](/windows/access-protection/vpn/vpn-conditional-access).   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>Blockieren von VPN-Clients, die widerrufene Zertifikate verwenden
  
Nachdem Sie Updates installiert haben, kann der RRAS-Server die Zertifikat Sperrung für VPNs erzwingen, die IKEv2-und Computer Zertifikate für die Authentifizierung verwenden, z. b. Geräte Tunnel-Always-on-VPNs. Dies bedeutet, dass der RRAS-Server für solche VPNs VPN-Verbindungen zu Clients verweigern kann, die versuchen, ein gesperrtes Zertifikat zu verwenden.

**Verfügbarkeit**

In der folgenden Tabelle sind die Versionen aufgeführt, die die Fixes für jede Windows-Version enthalten.

|Betriebssystemversion |Release  |
|---------|---------|
|Windows Server, Version 1903  |[KB4501375](https://support.microsoft.com/help/4501375/windows-10-update-kb4501375) |
|Windows Server 2019<br />Windows Server, Version 1809  |[KB4505658](https://support.microsoft.com/help/4505658/windows-10-update-kb4505658)  |
|Windows Server Version 1803  |[KB4507466](https://support.microsoft.com/help/4507466/windows-10-update-kb4507466)  |
|Windows Server, Version 1709  |[KB4507465](https://support.microsoft.com/help/4507465/windows-10-update-kb4507465)  |
|Windows Server 2016, Version 1607  |[KB4503294](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) |

**Vorgehensweise beim Konfigurieren der Voraussetzungen** 

1. Installieren Sie die Windows-Updates, sobald Sie verfügbar werden.
1. Stellen Sie sicher, dass alle VPN-Client-und RRAS-Server Zertifikate, die Sie verwenden, über CDP-Einträge verfügen und dass der RRAS-Server die entsprechenden CRLs erreichen kann.
1. Verwenden Sie auf dem RRAS-Server das PowerShell-Cmdlet **Set-vpnauthprotocol** , um den Parameter **rootcertificatenametoaccept** zu konfigurieren.<p>
   Im folgenden Beispiel werden die zu diesem Zweck aufgeführten Befehle aufgelistet. Im Beispiel stellt CN = die Stamm Zertifizierungsstelle von " **CN =** " den Distinguished Name der Stamm Zertifizierungsstelle dar. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**Konfigurieren des RRAS-Servers, um die Zertifikat Sperrung für VPN-Verbindungen zu erzwingen, die auf IKEv2-Computer Zertifikaten basieren**

1. Führen Sie in einem Eingabe Aufforderungs Fenster den folgenden Befehl aus: 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. Starten Sie den **Routing-und RAS-** Dienst neu.
  
Um die Zertifikat Sperrung für diese VPN-Verbindungen zu deaktivieren, legen Sie **certauthflags = 2** fest, oder entfernen Sie den Wert **certauthflags** , und starten Sie dann den **Routing-und** RAS-Dienst neu. 

**Widerrufen eines VPN-Client Zertifikats für eine VPN-Verbindung, die auf einem IKEv2-Computer Zertifikat basiert**
1. Widerrufen Sie das VPN-Client Zertifikat von der Zertifizierungsstelle.
1. Veröffentlichen Sie eine neue CRL von der Zertifizierungsstelle.
1. Öffnen Sie auf dem RRAS-Server ein Administrator Eingabe Aufforderungs Fenster, und führen Sie dann die folgenden Befehle aus:
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**Überprüfen, ob die Zertifikat Sperrung für Zertifikat basierte VPN-Verbindungen auf IKEv2-Computern funktioniert**  
>[!Note]  
> Bevor Sie dieses Verfahren verwenden, stellen Sie sicher, dass Sie das Betriebs Ereignisprotokoll CAPI2 aktivieren.
1. Führen Sie die vorherigen Schritte aus, um ein VPN-Client Zertifikat aufzuheben.
1. Versuchen Sie, mithilfe eines Clients, der über das gesperrte Zertifikat verfügt, eine Verbindung mit dem VPN herzustellen. Der RRAS-Server sollte die Verbindung ablehnen und eine Meldung wie "die Anmelde Informationen für die IKE-Authentifizierung sind nicht zulässig" anzeigen.
1. Öffnen Sie auf dem RRAS-Server Ereignisanzeige, und navigieren Sie zu **Anwendungs-und Dienst Protokolle/Microsoft/Windows/CAPI2**. 
1. Suchen Sie nach einem Ereignis, das die folgenden Informationen enthält:
   * Protokoll Name: **Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational**
   * Ereignis-ID: **41** 
   * Das Ereignis enthält den folgenden Text: **Subject = "*Client FQDN*"** (*Client-FQDN* steht für den voll qualifizierten Domänen Namen des Clients, der über das gesperrte Zertifikat verfügt). 

   Das- **<Result>** Feld der Ereignisdaten sollte einschließen, dass **das Zertifikat gesperrt ist**. Sehen Sie sich beispielsweise die folgenden Ausschnitte eines Ereignisses an:
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="https://schemas.microsoft.com/win/2004/08/events/event">
    <UserData>  
     <CertVerifyRevocation>  
      <Certificate fileRef="C97AE73E9823E8179903E81107E089497C77A720.cer" subjectName="client01.corp.contoso.com" />  
      <IssuerCertificate fileRef="34B1AE2BD868FE4F8BFDCA96E47C87C12BC01E3A.cer" subjectName="Contoso Root Certification Authority" />
      ...
      <Result value="80092010">The certificate is revoked.</Result>
     </CertVerifyRevocation>
    </UserData>
   </Event>
   ```

---
## <a name="additional-protection"></a>Zusätzlicher Schutz

### <a name="trusted-platform-module-tpm-key-attestation"></a>TPM-Schlüssel Nachweis (Trusted Platform Module)

Ein Benutzerzertifikat, das über einen TPM-geprüften Schlüssel verfügt, bietet eine höhere Sicherheitsgarantie, die durch nicht Exportierbarkeit, Anti-hammerung und Isolation der von TPM bereitgestellten Schlüssel gesichert wird.

Weitere Informationen zum TPM-Schlüssel Nachweis in Windows 10 finden Sie unter [TPM Key Nachweis](../../../../../identity/ad-ds/manage/component-updates/tpm-key-attestation.md).

## <a name="next-step"></a>Nächster Schritt

[Planen der Always on-VPN-Bereitstellung](always-on-vpn-deploy-planning.md): führen Sie vor der Installation der Remote Zugriffs-Server Rolle auf dem Computer, den Sie als VPN-Server verwenden möchten, die folgenden Aufgaben aus. Nach der entsprechenden Planung können Sie Always on VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mithilfe Azure AD konfigurieren.  

## <a name="related-topics"></a>Zugehörige Themen
- [NPS-Proxy Server-Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): Remote Authentication Dial-in User Service (RADIUS)-Clients, bei denen es sich um Netzwerk Zugriffs Server wie VPN-Server (virtuelles privates Netzwerk) und drahtlos Zugriffspunkte handelt, erstellen Sie Verbindungsanforderungen und senden diese an RADIUS-Server wie z. b. NPS. In einigen Fällen kann ein NPS-Server zu viele Verbindungsanforderungen gleichzeitig empfangen, was zu einer Beeinträchtigung der Leistung oder einer Überlastung führt.

- [Übersicht über Traffic Manager](/azure/traffic-manager/traffic-manager-overview): dieses Thema bietet einen Überblick über Azure Traffic Manager, mit dem Sie die Verteilung von Benutzer Datenverkehr für Dienst Endpunkte steuern können. Traffic Manager verwendet das Domain Name System (DNS), um Clientanforderungen auf der Grundlage einer Datenverkehrsrouting-Methode und der Integrität der Endpunkte an den optimalen Endpunkt weiterzuleiten. 

- [Windows Hello for Business](/windows/access-protection/hello-for-business/hello-identity-verification): dieses Thema enthält die Voraussetzungen, wie z. b. reine Cloud-bereit Stellungen und Hybrid Bereitstellungen.  Außerdem werden in diesem Thema häufig gestellte Fragen zu Windows Hello for Business aufgeführt.

- [Technische Fallstudie: Aktivieren des Remote Zugriffs mit Windows Hello for Business in Windows 10](/previous-versions//mt728163(v=technet.10)): in dieser technischen Fallstudie erfahren Sie, wie Microsoft den Remote Zugriff mit Windows Hello for Business implementiert.  Windows Hello for Business ist ein Authentifizierungsansatz für Unternehmen und Endkunden, der auf privaten/öffentlichen Schlüsseln oder Zertifikaten basiert und weit über den Gebrauch von Kennwörtern hinausgeht. Bei dieser Form der Authentifizierung werden Schlüsselpaar-Anmeldeinformationen verwendet, die Kennwörter ersetzen können und Verstößen, Diebstahl und Phishing gegenüber resistent sind. 

- [Integrieren der RADIUS-Authentifizierung in Azure Multi-Factor Authentication-Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): in diesem Thema wird schrittweise erläutert, wie Sie eine RADIUS-Client Authentifizierung mit Azure Multi-Factor Authentication-Server hinzufügen und konfigurieren. RADIUS ist ein Standardprotokoll, um Authentifizierungsanforderungen zu akzeptieren und diese Anforderungen zu verarbeiten. Der Azure Multi-Factor Authentication-Server kann als RADIUS-Server fungieren. 

- [VPN-Sicherheitsfeatures](/windows/access-protection/vpn/vpn-security-features): in diesem Thema finden Sie VPN-Sicherheitsrichtlinien für das Sperren von VPN, die WIP-Integration (Windows Information Protection) mit VPN und Datenverkehrs Filter. 

- [Automatisch ausgelöste VPN-Profil Optionen](/windows/access-protection/vpn/vpn-auto-trigger-profile): dieses Thema bietet Ihnen automatisch ausgelöste VPN-Profil Optionen, z. b. app-Trigger, namensbasierte Trigger und Always on.

- [VPN und bedingter Zugriff](/windows/access-protection/vpn/vpn-conditional-access): in diesem Thema erhalten Sie einen Überblick über die cloudbasierte Plattform für den bedingten Zugriff, die eine Geräte Kompatibilitäts Option für Remote Clients bereitstellt. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

- [TPM-Schlüssel](../../../../../identity/ad-ds/manage/component-updates/tpm-key-attestation.md)Nachweis: in diesem Thema erhalten Sie einen Überblick über Trusted Platform Module (TPM) und die Schritte zum Bereitstellen von TPM-Schlüssel Nachweis. Außerdem finden Sie Informationen zur Problembehandlung und zu den Schritten, um Probleme zu beheben.
