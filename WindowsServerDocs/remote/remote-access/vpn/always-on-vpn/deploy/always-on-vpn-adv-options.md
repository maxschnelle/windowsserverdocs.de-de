---
title: Erweiterte Features von Always On VPN
description: Über das Bereitstellungsszenario in dieser Bereitstellung bereitgestellt wird können Sie andere erweiterte VPN-Features zur Verbesserung der Sicherheit und Verfügbarkeit der VPN-Verbindung hinzufügen.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067431"
---
# Erweiterte Features von Always On VPN

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherige:** erfahren Sie mehr über die Always On VPN-Technologie](../always-on-vpn-technology-overview.md)<br>
& #187; [ **Weiter:** Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

Sie können über die Szenarien für die Bereitstellung zur Verfügung gestellt andere erweiterte VPN-Features zur Verbesserung der Sicherheit und Verfügbarkeit der VPN-Verbindung hinzufügen. Beispielsweise können solche Komponenten sicherstellen, dass der verbindende Client fehlerfrei ist, bevor Sie eine Verbindung zulassen.


## Hohe Verfügbarkeit

Nachfolgend finden Sie zusätzliche Optionen für hohe Verfügbarkeit.


|Option  |Beschreibung  |
|---------|---------|
|Server Stabilität und Lastenausgleich     |In Umgebungen, die hohe Verfügbarkeit oder Unterstützung für große Anzahl von Anfragen erfordern, können Sie steigern die Leistung und Stabilität des Remotezugriffs mit Lastenausgleich zwischen mehreren Servern, die ausgeführt (Network Policy Server, NPS) und Aktivieren des Remotezugriffs Zugriff auf Server-clustering.<p>Zugehörige Dokumente:<ul><li>[NPS-Proxy Server Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Bereitstellen des Remotezugriffs in einem Cluster](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|Geografische Standort Zertifizierungstest     |Für die IP-basierte Geolocation können Sie globale Traffic Manager mit DNS in Windows Server 2016 verwenden. Robuster geografische Lastenausgleich, können Sie globale Load Balancing für Server-Lösungen, z. B. Microsoft Azure Traffic Manager verwenden.<p>Zugehörige Dokumente:<ul><li>[Übersicht über Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

---

## Erweiterte Authentifizierung

Nachfolgend finden Sie zusätzliche Optionen für die Authentifizierung.


|Option  |Beschreibung  |
|---------|---------|
|Windows Hello for Business     |Unter Windows 10 werden Kennwörter von Windows Hello for Business durch eine sichere zweistufige Authentifizierung auf Computern und mobilen Geräten ersetzt. Diese Authentifizierung besteht aus einer neuen Art von Benutzeranmeldeinformationen, die auf ein Gerät gebunden ist und ein biometrisches Merkmal verwendet oder persönliche Identifikationsnummer (PIN).<p>Der Windows 10-VPN-Client ist kompatibel mit Windows Hello for Business. Nachdem der Benutzer sich mit einer Geste anmeldet, verwendet die VPN-Verbindung für die Windows Hello for Business-Zertifikat für die zertifikatbasierte Authentifizierung.<p>Zugehörige Dokumente:<ul><li>[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Technischen Fallstudie: [für das Aktivieren des Remotezugriffs mit Windows Hello for Business in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-Factor Authentication (MFA)     |Azure MFA verfügt über die Cloud und lokalen Versionen, die Sie mit der Windows-VPN-Authentifizierungsmechanismus integrieren können.<p>Weitere Informationen dazu, wie dieser Mechanismus funktioniert finden Sie unter [integrieren RADIUS-Authentifizierung mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

---

## Erweiterte VPN-Features

Nachfolgend finden Sie zusätzliche Optionen für erweiterte Funktionen.


|Option  |Beschreibung  |
|---------|---------|
|Filtern von Datenverkehr     |Wenn Sie erzwingen, welche Anwendungen-VPN-Clients zugreifen können müssen, können Sie die VPN-Datenverkehrsfilter aktivieren.<p>Weitere Informationen finden Sie unter [VPN-Sicherheitsfeatures](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features).         |
|Apps ausgelösten VPN     |Sie können VPN-Profile automatisch eine Verbindung beim Starten von bestimmten Anwendungen oder Anwendungstypen konfigurieren.<p>Weitere Informationen zu dieser und anderen auslösenden Optionen finden Sie unter [VPN-Profiloptionen automatisch ausgelöst verfügbar](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|VPN-bedingten Zugriff   |Bedingter Zugriff und Geräte Compliance kann verwaltete Geräten die-Standards erfüllt, bevor sie die VPN-Verbindung können voraussetzen. Eine der erweiterten Funktionen für bedingten Zugriff VPN ermöglicht Ihnen, die VPN-Verbindungen nur die beschränken, in denen das Client-Authentifizierungszertifikat 'AAD bedingten Zugriff OID des ' 1.3.6.1.4.1.311.87' enthält.<p>Um die VPN-Verbindungen zu beschränken, müssen Sie:<ol><li>Öffnen Sie auf dem Netzwerkrichtlinienserver **Network Policy Server** -Snap-in.</li><li>Erweitern Sie **Richtlinien** > **Netzwerkrichtlinien**.</li><li>Mit der rechten Maustaste die Netzwerkrichtlinie **Virtual Private Network (VPN)-Verbindungen** , und wählen Sie **Eigenschaften**.</li><li>Wählen Sie die Registerkarte " **Einstellungen** ".</li><li>Wählen Sie **Bestimmte Anbieter** , und klicken Sie auf **Hinzufügen**.</li><li>Wählen Sie die Option **Zugelassenen-Zertifikat-OID** , und klicken Sie auf **Hinzufügen**.</li><li>Fügen Sie die OID AAD bedingten Zugriff **1.3.6.1.4.1.311.87** als Attributwert ein, und klicken Sie dann zweimal auf **OK** .</li><li>Klicken Sie auf **Schließen** und dann auf **anwenden**.<p>Wenn VPN-Clients versuchen, eine Verbindung über ein Zertifikat als das Zertifikat mit kurzer Laufzeit Cloud, wird die Verbindung jetzt fehl.</li></ol>Weitere Informationen über den bedingten Zugriff finden Sie unter [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access).   |

---


## Zusätzlichen Schutz

**Trusted Platform Module (TPM)-Schlüsselnachweis**<p>
Ein Benutzerzertifikat mit einem Schlüssel TPM--bescheinigte bietet eine höhere Absicherung, nicht Exportierbarkeit Anti-hammering und Isolation von Schlüsseln durch das TPM bereitgestellten gesichert.

Weitere Informationen zu TPM-schlüsselnachweis in Windows 10 finden Sie unter [TPM-Schlüsselnachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation).

## Nächster Schritt
[Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md): Bevor Sie die RAS-Server-Rolle auf dem Computer Sie zur Verwendung als VPN-Server planen installieren, führen Sie die folgenden Aufgaben. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  

---

## Verwandte Themen
- [NPS Proxy Server Load Balancing](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): Remote Authentication Dial-In User Service (RADIUS)-Clients, die Zugriff Netzwerkserver wie Server virtuelle private Netzwerke (VPN) und Zugriffspunkten möglich sind, verbindungsanforderungen erstellen und senden sie an RADIUS Server, z. B. NPS. In einigen Fällen ein NPS-Servers zu viele verbindungsanforderungen zu einem bestimmten Zeitpunkt erhalten möglicherweise Leistungseinbußen oder eine Überladung resultierenden.

- [Übersicht über die der Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): Dieses Thema enthält eine Übersicht der Azure Traffic Manager, das Ihnen ermöglicht, die Verteilung von Datenverkehr von Benutzern für Dienstendpunkte steuern. Traffic Manager verwendet das Domain Name System (DNS), um Clientanforderungen an den am besten geeigneten Endpunkt basierend auf eine Methode Datenverkehr-routing und die Integrität von den Endpunkten weitergeleitet. 

- [Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): Dieses Thema enthält die erforderlichen Komponenten, z. B. nur Cloud und hybridbereitstellungen.  Dieses Thema enthält auch häufig gestellte Fragen zu Windows Hello for Business.

- [Technischen Fallstudie: Aktivieren der Remote Access mit Windows Hello for Business in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx): In dieser technischen Fallstudie erfahren Sie, wie Microsoft remote Access mit Windows Hello for Business implementiert.  Windows Hello for Business ist einem privaten und einem öffentlichen Schlüssel oder zertifikatbasierte Authentifizierung Ansatz für Organisationen und Verbraucher, der Kennwörter hinausgeht. Diese Art der Authentifizierung basiert auf Schlüsselpaar Anmeldeinformationen, die Kennwörter ersetzen und sind widerstandsfähiger gegen Angriffsarten, Diebstahl und Phishing. 

- [Integrieren von RADIUS-Authentifizierung mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): Dieses Thema führt Sie durch das Hinzufügen und Konfigurieren von einem RADIUS-Client-Authentifizierung mit Azure Multi-Factor Authentication-Server. RADIUS ist ein standard-Protokoll Authentifizierungsanfragen akzeptieren und diese Anforderungen zu verarbeiten. Azure Multi-Factor Authentication-Server kann als RADIUS-Server fungieren. 

- [VPN-Sicherheitsfeatures](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): in diesem Thema erhalten Sie VPN-Sicherheitsrichtlinien für LockDown VPN, Windows Information Protection (WIP)-Integration mit VPN und Datenverkehr filtert. 

- [VPN-Auto - Profiloptionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): in diesem Thema erhalten Sie VPN-Profil automatisch ausgelöst Optionen, z. B. app-Trigger, namenbasierter Auslöser und Always On.

- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Dieses Thema enthält eine Übersicht über cloudbasierten bedingten Zugriffsplattform um eine gerätekompatibilitätsoption für Remoteclients bereitzustellen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

- [TPM-Schlüsselnachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): Dieses Thema enthält eine Übersicht der Trusted Platform Module (TPM) und Schritte zum Bereitstellen von TPM Schlüssel Attestation. Sie können auch zur Problembehandlung Informationen und Schritte zum Beheben von Problemen finden. 

---