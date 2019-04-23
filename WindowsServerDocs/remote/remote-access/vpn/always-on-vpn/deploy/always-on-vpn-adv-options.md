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
ms.openlocfilehash: a544ac3c1a121874170a2fc78a34bd401b8bebe1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885081"
---
# <a name="advanced-features-of-always-on-vpn"></a>Erweiterte Features von Always On-VPN-

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**Vorherige:** Erfahren Sie mehr über die Always On-VPN-Technologie](../always-on-vpn-technology-overview.md)<br>
&#187; [ **Next:** Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

Über die Bereitstellungsszenarien bereitgestellt wird können Sie andere erweiterte VPN-Features zur Verbesserung der Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung hinzufügen. Beispielsweise können solche Komponenten sichergestellt, dass der verbindende Client fehlerfrei ist, bevor Sie eine Verbindung zulassen.


## <a name="high-availability"></a>Hohe Verfügbarkeit

Es folgen weitere Optionen für hohe Verfügbarkeit.


|Option  |Beschreibung  |
|---------|---------|
|Server-resilienz und Lastenausgleich     |In Umgebungen, die eine hohe Verfügbarkeit bzw. die Unterstützung zahlreicher Anforderungen erfordern, können Sie erhöhen die Leistung und Stabilität des Remotezugriffs mit Lastenausgleich zwischen mehreren Servern, die ausgeführt wird (Network Policy Server, NPS) und Remoteaktivierung Access-Server-clustering.<p>Verwandte Dokumente:<ul><li>[NPS-Proxy-Server den Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Bereitstellen des Remotezugriffs in einem Cluster](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|Geografische standortsicherheit     |Für die IP-basierte Geolocation können Sie Global Traffic Manager mit DNS in Windows Server 2016. Stabilere geografischen Lastenausgleich können Sie globale Lastenausgleich zwischen für Server-Lösungen, wie z. B. Microsoft Azure Traffic Manager verwenden.<p>Verwandte Dokumente:<ul><li>[Was ist Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

---

## <a name="advanced-authentication"></a>Erweiterte Authentifizierung

Es folgen weitere Optionen für die Authentifizierung.


|Option  |Beschreibung  |
|---------|---------|
|Windows Hello for Business     |Unter Windows 10 werden Kennwörter von Windows Hello for Business durch eine sichere zweistufige Authentifizierung auf Computern und mobilen Geräten ersetzt. Diese Authentifizierung besteht aus einen neuen Typ von Anmeldeinformationen des Benutzers, der an ein Gerät gebunden ist, und verwendet ein biometrisches Merkmal oder Anzahl PIN (Personal Identification).<p>Der Windows 10-VPN-Client ist kompatibel mit Windows Hello for Business. Nachdem der Benutzer mit einer Geste anmeldet, verwendet die VPN-Verbindung die Windows Hello für Business-Zertifikat für die zertifikatbasierte Authentifizierung.<p>Verwandte Dokumente:<ul><li>[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Technische Fallstudie: [Aktivieren des Remotezugriffs mit Windows Hello für Unternehmen in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-Factor Authentication (MFA)     |Azure MFA verfügt über die Cloud und lokalen Versionen, die Sie in der Windows-VPN-Authentifizierungsmechanismus integrieren können.<p>Weitere Informationen dazu, wie dieser Mechanismus funktioniert, finden Sie unter [Integration der RADIUS-Authentifizierung mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

---

## <a name="advanced-vpn-features"></a>Erweiterte VPN-Funktionen

Folgendes sind zusätzliche Optionen für die erweiterte Funktionen.


|Option  |Beschreibung  |
|---------|---------|
|Filtern von Datenverkehr     |Wenn Sie erzwingen, welche Anwendungen-VPN-Clients zugreifen können müssen, können Sie VPN-IP-Filter aktivieren.<p>Weitere Informationen finden Sie unter [VPN-Sicherheitsfunktionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features).         |
|Durch Apps ausgelöstes VPN     |Sie können VPN-Profilen die Verbindung automatisch beim Starten von bestimmten Anwendungen oder die Arten von Anwendungen konfigurieren.<p>Weitere Informationen zu diesen und anderen auslösenden Optionen finden Sie unter [VPN-Profil automatisch ausgelöste Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|Bedingter Zugriff für VPN   |Für bedingten Zugriff und die Geräte-Compliance kann verlangen, dass verwaltete Geräte Standards zu erfüllen, bevor sie mit dem VPN verbinden können. Eine der erweiterten Funktionen für den bedingten Zugriff für VPN-können Sie die VPN-Verbindungen auf jene einzuschränken, von denen das Clientauthentifizierungszertifikat "AAD für den bedingten Zugriff OID des" 1.3.6.1.4.1.311.87"enthält.<p>Um den VPN-Verbindungen zu beschränken, müssen Sie:<ol><li>Öffnen Sie auf dem NPS-Server die **Netzwerkrichtlinienserver** -Snap-in.</li><li>Erweitern Sie **Richtlinien** > **Netzwerkrichtlinien**.</li><li>Mit der rechten Maustaste die **virtuelles privates Netzwerk (VPN) Verbindungen** Netzwerkrichtlinie, und wählen **Eigenschaften**.</li><li>Wählen Sie die **Einstellungen** Registerkarte.</li><li>Wählen Sie **Hersteller bestimmte** , und klicken Sie auf **hinzufügen**.</li><li>Wählen Sie die **zulässige-Zertifikat-OID** aus, und klicken Sie dann auf **hinzufügen**.</li><li>Fügen Sie die AAD für bedingten Zugriff OID des **1.3.6.1.4.1.311.87** als Attributwert ein, und klicken Sie dann auf **OK** zweimal.</li><li>Klicken Sie auf **schließen** und dann **anwenden**.<p>Wenn VPN-Clients versuchen, die Verbindung mit einem beliebigen Zertifikat als das kurzlebige Cloud-Zertifikat, wird jetzt die Verbindung fehl.</li></ol>Weitere Informationen zum bedingten Zugriff finden Sie unter [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access).   |

---


## <a name="additional-protection"></a>Zusätzlichen Schutz

**Trusted Platform Module (TPM)-Schlüsselnachweis**<p>
Ein Zertifikat mit einem Schlüssel mit TPM-Verwendung der attested bietet höhere Sicherheit, gesichert durch nicht-Exportierbarkeit, Anti-hammering und Isolation von Schlüsseln, die vom TPM bereitgestellt.

Weitere Informationen zu TPM-schlüsselnachweis unter Windows 10, finden Sie unter [TPM-Schlüsselnachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation).

## <a name="next-step"></a>Nächster Schritt
[Planen der Bereitstellung von Always On-VPN-](always-on-vpn-deploy-planning.md): Bevor Sie die Remotezugriffs-Serverrolle auf dem Computer, die Sie zur Verwendung als VPN-Server planen installieren, werden führen Sie die folgenden Aufgaben aus. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  

---

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

---