---
title: Erweiterte Features von Always On VPN
description: Über das Bereitstellungsszenario, die in dieser Bereitstellung bereitgestellt wird können Sie andere erweiterte VPN-Features zur Verbesserung der Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung hinzufügen.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 5f43d64dc7642ef67da03fec989909bc4f2f14ae
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263025"
---
# <a name="advanced-features-of-always-on-vpn"></a>Erweiterte Features von Always On-VPN-

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Erfahren Sie mehr über die Always On-VPN-Technologie](../always-on-vpn-technology-overview.md)
- [**nächster:** Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

Über die Bereitstellungsszenarien bereitgestellt wird können Sie andere erweiterte VPN-Features zur Verbesserung der Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung hinzufügen. Beispielsweise können solche Komponenten sichergestellt, dass der verbindende Client fehlerfrei ist, bevor Sie eine Verbindung zulassen.

## <a name="high-availability"></a>Hohe Verfügbarkeit

Es folgen weitere Optionen für hohe Verfügbarkeit.

|Option  |Beschreibung  |
|---------|---------|
|Server-resilienz und Lastenausgleich     |In Umgebungen, die eine hohe Verfügbarkeit bzw. die Unterstützung zahlreicher Anforderungen erfordern, können Sie erhöhen die Leistung und Stabilität des Remotezugriffs mit Lastenausgleich zwischen mehreren Servern, die ausgeführt wird (Network Policy Server, NPS) und Remoteaktivierung Access-Server-clustering.<p>Verwandte Dokumente:<ul><li>[NPS-Proxy-Server den Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Bereitstellen des Remotezugriffs in einem Cluster](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|Geografische standortsicherheit     |Für die IP-basierte Geolocation können Sie Global Traffic Manager mit DNS in Windows Server 2016. Stabilere geografischen Lastenausgleich können Sie globale Lastenausgleich zwischen für Server-Lösungen, wie z. B. Microsoft Azure Traffic Manager verwenden.<p>Verwandte Dokumente:<ul><li>[Was ist Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>Erweiterte Authentifizierung

Es folgen weitere Optionen für die Authentifizierung.

|Option  |Beschreibung  |
|---------|---------|
|Windows Hello for Business     |Unter Windows 10 werden Kennwörter von Windows Hello for Business durch eine sichere zweistufige Authentifizierung auf Computern und mobilen Geräten ersetzt. Diese Authentifizierung besteht aus einen neuen Typ von Anmeldeinformationen des Benutzers, der an ein Gerät gebunden ist, und verwendet ein biometrisches Merkmal oder Anzahl PIN (Personal Identification).<p>Der Windows 10-VPN-Client ist kompatibel mit Windows Hello for Business. Nachdem der Benutzer mit einer Geste anmeldet, verwendet die VPN-Verbindung die Windows Hello für Business-Zertifikat für die zertifikatbasierte Authentifizierung.<p>Verwandte Dokumente:<ul><li>[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Technische Fallstudie: [Aktivieren des Remotezugriffs mit Windows Hello für Unternehmen in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-Factor Authentication (MFA)     |Azure MFA verfügt über die Cloud und lokalen Versionen, die Sie in der Windows-VPN-Authentifizierungsmechanismus integrieren können.<p>Weitere Informationen dazu, wie dieser Mechanismus funktioniert, finden Sie unter [Integration der RADIUS-Authentifizierung mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

## <a name="advanced-vpn-features"></a>Erweiterte VPN-Funktionen

Im folgenden sind zusätzliche Optionen für die erweiterte Funktionen.

|Option  |Beschreibung  |
|---------|---------|
|Filtern von Datenverkehr     |Wenn Sie erzwingen, welche Anwendungen-VPN-Clients zugreifen können müssen, können Sie VPN-IP-Filter aktivieren.<p>Weitere Informationen finden Sie unter [VPN-Sicherheitsfunktionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features).         |
|Durch Apps ausgelöstes VPN     |Sie können VPN-Profilen die Verbindung automatisch beim Starten von bestimmten Anwendungen oder die Arten von Anwendungen konfigurieren.<p>Weitere Informationen zu diesen und anderen auslösenden Optionen finden Sie unter [VPN-Profil automatisch ausgelöste Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|Bedingter Zugriff für VPN   |Für bedingten Zugriff und die Geräte-Compliance kann verlangen, dass verwaltete Geräte Standards zu erfüllen, bevor sie mit dem VPN verbinden können. Eine der erweiterten Funktionen für den bedingten Zugriff für VPN-können Sie die VPN-Verbindungen auf jene einzuschränken, von denen das Clientauthentifizierungszertifikat "AAD für den bedingten Zugriff OID des" 1.3.6.1.4.1.311.87"enthält.<p>Um den VPN-Verbindungen zu beschränken, müssen Sie:<ol><li>Öffnen Sie auf dem NPS-Server die **Netzwerkrichtlinienserver** -Snap-in.</li><li>Erweitern Sie **Richtlinien** > **Netzwerkrichtlinien**.</li><li>Mit der rechten Maustaste die **virtuelles privates Netzwerk (VPN) Verbindungen** Netzwerkrichtlinie, und wählen **Eigenschaften**.</li><li>Wählen Sie die **Einstellungen** Registerkarte.</li><li>Wählen Sie **Hersteller bestimmte** , und wählen Sie **hinzufügen**.</li><li>Wählen Sie die **zulässige-Zertifikat-OID** aus, und wählen Sie dann **hinzufügen**.</li><li>Fügen Sie die AAD für bedingten Zugriff OID des **1.3.6.1.4.1.311.87** als Attributwert aus, und wählen Sie dann **OK** zweimal.</li><li>Wählen Sie **schließen** und dann **anwenden**.<p>Wenn VPN-Clients versuchen, die Verbindung mit einem beliebigen Zertifikat als das kurzlebige Cloud-Zertifikat, wird jetzt die Verbindung fehl.</li></ol>Weitere Informationen zum bedingten Zugriff finden Sie unter [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access).   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>Blockieren von VPN-Clients, die gesperrte Zertifikate zu verwenden
  
Nach der Installation von Updates der RRAS-Server kann das Sperren von Zertifikaten für VPNs, die Verwendung von IKEv2 erzwingen und Computerzertifikate für die Authentifizierung, z. B. Gerät Tunneln AlwaysOn-VPNs. Dies bedeutet, dass für diese VPNs, der RRAS-Server-VPN-Verbindungen für Clients, die versuchen verweigern kann, eine Liste gesperrter Zertifikate zu verwenden.

**Verfügbarkeit**

Die folgende Tabelle enthält die ungefähre Veröffentlichungstermine Updates, die für jede Version von Windows.

|Version des Betriebssystems |Release-Datum * |
|---------|---------|
|Windows Server, version 1903  |Q2, 2019  |
|Windows Server 2019<br />Windows Server, Version 1809  |3\. QUARTAL 2019  |
|Windows Server, Version 1803  |3\. QUARTAL 2019  |
|Windows Server, Version 1709  |3\. QUARTAL 2019  |
|Windows Server 2016 Version 1607  |Q2, 2019  |
  
\* Alle Datumsangaben für Veröffentlichungen werden in Kalenderquartale aufgeführt. Datumsangaben sind ungefähre Werte und können ohne vorherige Ankündigung ändern.

**Vorgehensweise: Konfigurieren der Voraussetzungen** 

1. Installieren Sie die Windows-Updates, sobald diese verfügbar werden.
1. Stellen Sie sicher, dass alle VPN-Client und RRAS-Server-Zertifikate, die Sie verwenden die CDP-Einträge aufweisen, und der RRAS-Server die entsprechenden CRLs erreichen kann.
1. Verwenden Sie auf dem RRAS-Server die **Set-VpnAuthProtocol** PowerShell-Cmdlet zum Konfigurieren der **RootCertificateNameToAccept** Parameter.<br /><br />
   Im folgende Beispiel werden die Befehle zu diesem Zweck aufgelistet. Im Beispiel **CN = Contoso Stammzertifikate von Zertifizierungsstellen** stellt den distinguished Name des der Stammzertifizierungsstelle. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority,*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**Vorgehensweise: konfigurieren den RRAS-Server, um das Sperren von Zertifikaten für VPN-Verbindungen zu erzwingen, die IKEv2-Computerzertifikate basieren**

1. Führen Sie in einem Eingabeaufforderungsfenster den folgenden Befehl ein: 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. Neustart der **Routing- und RAS** Service.
  
Um das Sperren von Zertifikaten für diese VPN-Verbindungen zu deaktivieren, legen **CertAuthFlags = 2** oder entfernen Sie die **CertAuthFlags** Wert ein, und wiederholen Sie die **Routing- und RAS**Service. 

**Vorgehensweise zum Widerrufen des VPN-Clientzertifikat für eine VPN-Verbindung, die basierend auf einer IKEv2-Computerzertifikat**
1. VPN-Clientzertifikat aus der Zertifizierungsstelle gesperrt.
1. Veröffentlichen Sie eine neue Sperrliste der Zertifizierungsstelle.
1. Klicken Sie auf dem RRAS-Server öffnen Sie eine administrative Eingabeaufforderung, und führen Sie die folgenden Befehle:
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**Gewusst wie: Überprüfen Sie, ob dieser das Sperren von Zertifikaten für IKEv2 Computer Zertifikat-basierte VPN-Verbindungen funktioniert.**  
>[!Note]  
> Bevor Sie dieses Verfahren verwenden, stellen Sie sicher, dass Sie das CAPI2-operational-Ereignisprotokoll aktivieren.
1. Führen Sie die vorherigen Schritte, um ein VPN-Clientzertifikat widerrufen.
1. Versuchen Sie es, mithilfe von ein Client, der das gesperrte Zertifikat verfügt über eine Verbindung mit dem VPN herstellen. RRAS-Servers sollten die Verbindung verweigert, und eine Meldung angezeigt, wie z. B. "IKE-Authentifizierungsinformationen sind nicht akzeptabel."
1. Klicken Sie auf dem RRAS-Server-Ereignisanzeige zu öffnen, und navigieren Sie zu **Applications and Services Logs/Microsoft/Windows/CAPI2**. 
1. Suchen Sie nach der ein Ereignis, das die folgenden Informationen enthält:
   * Protokollname: **Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational**
   * Ereignis-ID: **41** 
   * Das Ereignis enthält den folgenden Text: **Subject = "*Client FQDN*"** (*Client FQDN* den vollständig qualifizierten Domänennamen des Clients, die die gesperrten darstellt das Zertifikat.) 

   Die **<Result>** Feld der Daten für das Ereignis aufzunehmen **wird das Zertifikat widerrufen**. Beispielsweise sehen Sie die folgenden Auszüge aus einem Ereignis:
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
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
## <a name="additional-protection"></a>Zusätzlichen Schutz

### <a name="trusted-platform-module-tpm-key-attestation"></a>Trusted Platform Module (TPM)-Schlüsselnachweis

Ein Zertifikat mit einem Schlüssel mit TPM-Verwendung der attested bietet höhere Sicherheit, gesichert durch nicht-Exportierbarkeit, Anti-hammering und Isolation von Schlüsseln, die vom TPM bereitgestellt.

Weitere Informationen zu TPM-schlüsselnachweis unter Windows 10, finden Sie unter [TPM-Schlüsselnachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation).

## <a name="next-step"></a>Nächster Schritt

[Planen der Bereitstellung von Always On-VPN-](always-on-vpn-deploy-planning.md): Bevor Sie die Remotezugriffs-Serverrolle auf dem Computer, die Sie zur Verwendung als VPN-Server planen installieren, werden führen Sie die folgenden Aufgaben aus. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  

## <a name="related-topics"></a>Verwandte Themen
- [NPS-Proxy den Serverlastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): Remote Authentication Dial-in User Service (RADIUS)-Clients, die Netzwerkzugriffsserver, z. B. virtuelles privates Netzwerk (VPN)-Servern und drahtlose Zugriffspunkte sind, erstellen die Weiterleitung von verbindungsanforderungen und senden sie, wie z. B. NPS RADIUS-Server. In einigen Fällen ein NPS-Server zu viele Anforderungen von Verbindungen gleichzeitig ausführen möchten, möglicherweise zu Leistungseinbußen oder eine Überladung.

- [Was ist Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): Dieses Thema enthält einen Übersicht über die von Azure Traffic Manager, dem Sie die Verteilung von Benutzerdatenverkehr für Dienstendpunkte steuern können. Traffic Manager verwendet das Domain Name System (DNS), um Clientanforderungen auf der Grundlage einer datenverkehrsrouting Methode und die Integrität der Endpunkte am besten geeigneten Endpunkt weiterzuleiten. 

- [Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): Dieses Thema enthält die erforderlichen Komponenten, z. B. nur cloudbereitstellungen oder hybridbereitstellungen durchführen.  Dieses Thema enthält auch häufig gestellte Fragen zu Windows Hello for Business.

- [Technische Fallstudie: Aktivieren des Remotezugriffs mit Windows Hello für Unternehmen in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx): In diese Technische Fallstudie erfahren Sie, wie Microsoft RAS in Windows Hello für Unternehmen implementiert.  Windows Hello for Business ist eine privaten/öffentlichen Schlüsseln oder die zertifikatbasierte authentifizierungsansatz für Unternehmen und Verbraucher, die von Kennwörtern hinausgeht. Diese Form der Authentifizierung werden Schlüsselpaar-Anmeldeinformationen, die Kennwörter ersetzen können und Verstößen, resistent und Phishing gegenüber basiert. 

- [Integrieren der RADIUS-Authentifizierung mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): Dieses Thema führt Sie durch das Hinzufügen und konfigurieren eine RADIUS-Client-Authentifizierung mit Azure Multi-Factor Authentication-Server. RADIUS ist ein Standardprotokoll zum Annehmen und Verarbeiten von Authentifizierungsanforderungen. Azure Multi-Factor Authentication-Server kann als RADIUS-Server fungieren. 

- [VPN-Sicherheitsfunktionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): Dieses Thema enthält Sie VPN-Sicherheitsrichtlinien für LockDown-VPN, Integration von Windows Information Protection (WIP) mit VPN- und Datenverkehrsfilter. 

- [VPN-Profil automatisch ausgelöste Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): Dieses Thema enthält Sie die VPN-Profil automatisch ausgelöste Optionen wie app-Trigger, einen Namen-basierte Trigger und Always On.

- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Dieses Thema bietet einen Überblick über die Cloud-basierten bedingten Zugriffsplattform, eine Geräte-Compliance-Option für Clients bereitgestellt werden. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

- [TPM-Schlüsselnachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): Dieses Thema bietet einen Überblick über die Trusted Platform Module (TPM) und Schritte zum Bereitstellen der TPM-schlüsselnachweise. Sie erhalten auch bei der Problembehandlung Informationen und Schritte, um Probleme zu beheben.
