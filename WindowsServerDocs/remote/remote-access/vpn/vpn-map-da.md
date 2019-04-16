---
title: Always On VPN-features
description: In diesem Thema erhalten Sie Informationen über die Features und Funktionen von Always On VPN.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.assetid: 8fe1c810-4599-4493-b4b8-73fa9aa18535
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 68d8561eb55b844a80c8b6a38d1255ad44457af6
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066854"
---
# Always On VPN-Features und Funktionen

>Betrifft: Windows Server \(Semi-Annual Channel\), Windows Server 2016, Windows 10

&#171;  [**Früher:** Always On VPN-Bereitstellung für Windows Server und Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md)<br>
&#187; [ **Weiter:** Erfahren Sie mehr über Always On VPN-Verbesserungen](../vpn/always-on-vpn/always-on-vpn-enhancements.md)

In diesem Thema erhalten Sie Informationen über die Features und Funktionen von Always On VPN.  In der folgenden Tabelle ist kein vollständige Liste, er umfasst jedoch einige der am häufigsten verwendeten Features und Funktionen in RAS-Lösungen verwendet. 

>[!TIP]
>Wenn Sie derzeit DirectAccess verwenden, empfehlen wir, dass Sie die Always On VPN-Funktionalität sorgfältig, um festzustellen, ob behandelt, dass all Ihre Bedürfnisse RAS vor dem Migrieren von DirectAccess auf Always On VPN bilden untersuchen.  

| Im Bereich | Always On VPN  |
| ---- | ---- |
| Nahtlose, transparente Konnektivität mit dem Unternehmensnetzwerk. | Sie können Always On VPN zur Unterstützung der automatische Auslösung basierend auf dem Anwendungsstart oder der Namespace lösungsanforderungen konfigurieren.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/AlwaysOn**<br>**VPNv2/ProfileName/AppTriggerList**<br>**VPNv2/ProfileName/DomainNameInformationList/AutoTrigger** |
| Verwendung eines dedizierten Infrastrukturtunnels Konnektivität für Benutzer nicht angemeldet, in dem Unternehmensnetzwerk bereitstellen. | Sie können diese Funktion durch Nutzen des Gerätetunnelfeatures im VPN-Profil verwenden.<p><p>_**Hinweis:**_<br>Gerätetunnelfunktion kann nur auf Geräte in einer Domäne mithilfe von IKEv2 mit Computer Zertifikatauthentifizierung konfiguriert werden.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/DeviceTunnel** |
| Verwendung von verwalten mehr, remote Connectivity Clients von Management-Systeme im Unternehmensnetzwerk befinden können. | Sie können diese Funktion durch Nutzen des Gerätetunnelfeatures im VPN-Profil verwenden in Kombination mit der Konfiguration der VPN-Verbindung, so dass die IP-Adressen der VPN-Schnittstelle mit internen DNS-Diensten dynamisch registriert wird.<p><p>_**Hinweis:**_<br>Wenn Sie Datenverkehrsfilter im Profil Gerätetunnelfunktion aktivieren, wird den Gerätetunnel eingehenden Datenverkehr (vom Unternehmensnetzwerk an den Client) verweigert.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/RegisterDNS** |
| Greifen Sie zurück, wenn Clients sich hinter Firewalls oder Proxy-Servern befinden. | Sie können auf SSTP (von IKEv2) zurückgreifen, indem Sie den automatischen Tunnel-/Protokolltyp innerhalb des VPN-Profils konfigurieren.<p><p>_**Hinweis:**_<br>Benutzer Tunnel unterstützt SSTP und IKEv2 und Gerätetunnelfunktion IKEv2 nur mit keine Unterstützung für SSTP Fallback unterstützt.<p>Definieren Sie mithilfe von:<br>**VPNv2/ProfilName/NativeProfile/NativeProtocolType** |
| Unterstützung für die End-to-Edge-Zugriffsmodus. | Always On VPN bietet Konnektivität zu Unternehmensressourcen durch Tunnelrichtlinien, die die Authentifizierung und Verschlüsselung erfordern, bis sie das VPN-Gateway erreichen. Standardmäßig enden Tunnel-Sitzungen auf dem VPN-Gateway, das auch als Gateway IKEv2, End-to-Edge-Sicherheit funktioniert. |
| Unterstützung für die Computerzertifikatauthentifizierung. | Der IKEv2 Protokolltyp als Teil der Always On VPN-Plattform insbesondere die Verwendung der Computer oder Computerzertifikate für die VPN-Authentifizierung unterstützt verfügbar ist.<p><p>_**Hinweis:**_<br>IKEv2 ist das einzige unterstützte Protokoll für Gerätetunnelfunktion, und es gibt keine Supportoption für SSTP Fallback. <p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/NativeProfile/Authentication/MachineMethod** |
| Verwenden Sie Sicherheitsgruppen, um RAS-Funktionen für bestimmte Clients zu begrenzen. | Sie können Always On VPN konfigurieren, um die genaue Autorisierung bei Verwendung von RADIUS zu unterstützen, einschließlich der Verwendung von Sicherheitsgruppen zur Kontrolle des VPN-Zugriffs. |
| Unterstützung für Server hinter Edge-Firewall oder NAT-Gerät. | Always On VPN ermöglicht die Verwendung von Protokollen wie IKEv2 und SSTP, die die Verwendung eines VPN-Gateways hinter Edge-Firewall oder NAT-Geräten vollständig unterstützen.<p><p>_**Hinweis:**_<br>Benutzer Tunnel unterstützt SSTP und IKEv2 und Gerätetunnelfunktion IKEv2 nur mit keine Unterstützung für SSTP Fallback unterstützt. |
| Möglichkeit zum Ermitteln der Intranet-Verbindung, wenn mit dem Unternehmensnetzwerk verbunden. | Vertrauenswürdige netzwerkerkennung bietet eine Funktion zum Erkennen von unternehmensnetzwerkverbindungen, und es basiert auf einem verbindungsspezifischen DNS-Suffix der zugewiesenen Netzwerkschnittstellen und Netzwerkprofile.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/TrustedNetworkDetection** |
| Kompatibilität mit Network Access Protection (NAP). | Always On VPN-Client kann mit Azure integriert werden, um bedingten Zugriff der mehrstufigen Authentifizierung, Gerätekompatibilität oder einer Kombination aus beidem zu erzwingen. Beim Einhalten bedingter Zugriffsrichtlinien, stellt Azure AD ein kurzlebiges (standardmäßig 60 Minuten) IPsec-Authentifizierungszertifikat aus, das der Client dann als Gateway VPN-Authentifizierung verwenden kann. Gerätecompliance nutzt System Center Konfigurations-Manager/Intune-Kompatibilitätsrichtlinien, die den Integritätsnachweis für Geräte enthalten kann. Zu diesem Zeitpunkt bietet der bedingte Zugriff von Azure VPN den besten Ersatz zu vorhandenen NAP-Projektmappen, obwohl keine Art Wiederherstellungsdienst oder Quarantäne-Netzwerkfunktionen vorhanden ist. Weitere Informationen finden Sie unter [VPN und bedingter Zugriff](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-conditional-access).<p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/DeviceCompliance** |
| Die Möglichkeit, zu definieren, welche Verwaltungsserver vor der Anmeldung für den Benutzer zugänglich sind. | Sie können diese Funktion in Always On VPN mithilfe des (verfügbar in Version 1709 – für nur IKEv2) gerätetunnelfeatures im VPN-Profil in Kombination mit datenverkehrsfiltern, um zu steuern, welche Managementsysteme auf das Unternehmensnetzwerk über zugänglich sind, erreichen der Gerätetunnelfunktion.<p><p>_**Hinweis:**_<br>Wenn Sie Datenverkehrsfilter im Profil Gerätetunnelfunktion aktivieren, wird den Gerätetunnel eingehenden Datenverkehr (vom Unternehmensnetzwerk an den Client) verweigert.<p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/TrafficFilterList** |
---

## Zusätzliche Funktionen

Jedes Element in diesem Abschnitt ist ein Verwendungsszenario oder eine häufig verwendete RAS-Funktionen für die Always On VPN-Funktionen verbessert – entweder durch eine Erweiterung der Funktion oder den Verzicht auf eine vorherige Einschränkung.


| Im Bereich | Always On VPN  |
| ---- | ---- |
| Mit der Domäne verbundene Geräte mit Enterprise-SKUs Anforderung. | Always On VPN unterstützt mit der Domäne verbundene Geräte, solche, die keiner Domäne beigetreten sind (Arbeitsgruppe) oder in Azure AD eingebundene Geräte sowohl für Unternehmens- und BYOD-Szenarien. Always On VPN ist in allen Windows-Versionen verfügbar, und die Plattformfeatures sind für Dritte über UWP VPN-Plug-In-Unterstützung verfügbar.<p><p>_**Hinweis:**_<br>Gerätetunnelfunktion kann nur auf die Domäne eingebundene Geräte unter Windows 10 Enterprise oder Education Version 1709 oder höher konfiguriert werden. Es gibt keine Unterstützung für Drittanbieter-Kontrolle über den Gerätetunnel. |
| Unterstützung für IPv4 und IPv6. | Mit Always On VPN können Benutzer sowohl auf IPv4 als auch IPv6-Ressourcen im Unternehmensnetzwerk zugreifen. Der Always On VPN-Client verwendet einen Dual-Stack-Ansatz, der nicht speziell von IPv6 oder der Notwendigkeit für das VPN-Gateway abhängt, um NAT64 oder DNS64-Übersetzungsdienste bereitzustellen. |
| Unterstützung für zweistufige oder OTP-Authentifizierung. |Die Always On VPN-Plattform unterstützt EAP, die die Verwendung von verschiedenen Microsoft und Drittanbietern EAP-Typen als Teil der Workflow-Authentifizierung ermöglicht. Always On VPN unterstützt speziell Smartcard (physisch und virtuell) und Windows Hello for Business Zertifikate für zweistufige Authentifizierungsanforderungen. Darüber hinaus unterstützt Always On VPN OTP über MFA (nicht nativ unterstützt, nur auf Drittanbieter-Plug-Ins unterstützt) über EAP RADIUS-Integration.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfilName/NativeProfile/Authentifizierung** |
| Unterstützung für mehrere Domäne und Gesamtstrukturen. | Die Always On VPN-Plattform hat keine Abhängigkeit von der Active Directory Domain Services (AD DS)-Gesamtstruktur oder Domänen-Topologie (oder zugeordneten Funktions-/Schemata-Ebenen), da der VPN-Client nicht der Domäne beitreten muss, um die Funktion zu nutzen. Gruppenrichtlinien sind keine Abhängigkeit, um VPN-Profileinstellungen zu definieren, da Sie nicht während der Clientkonfiguration verwendet werden. Wo die Integration der Active Directory-Autorisierung erforderlich ist, können Sie dies über RADIUS als Teil des EAP-Authentifizierung und Autorisierung erzielen. |
| Unterstützung für geteiltes oder erzwungenes Tunneling für Internet-/Intranet-Datenverkehrstrennung. | Sie können Always On VPN konfigurieren, um geteiltes oder erzwungenes Tunneling systemintern (Standardmodus) zu unterstützen. Always On VPN bietet zusätzliche Granularität für anwendungsspezifische Routingrichtlinien.<p><p>_**Hinweis:**_<br>Nur Benutzer Tunnel unterstützt.<p><p>Definieren Sie mithilfe von:<p> **VPNv2/ProfilName/NativeProfile/RoutingPolicyType**<br>**VPNv2/ProfilName/TrafficFilterList/App/RoutingPolicyType** |
| Unterstützung für mehrere Protokolle. | Always On VPN kann konfiguriert werden, dass SSTP systemintern unterstützt, wenn Secure Sockets Layer-fallback von IKEv2 erforderlich ist.<p><p>_**Hinweis:**_<br>Benutzer Tunnel unterstützt SSTP und IKEv2 und Gerätetunnelfunktion IKEv2 nur mit keine Unterstützung für SSTP Fallback unterstützt.  |
| Konnektivität-Assistenten für Unternehmens-Verbindungsstatus. | Always On VPN ist vollständig in den systemeigenen Netzwerkkonnektivitäts-Assistent integriert und bietet Konnektivitätsstatus über die Benutzeroberfläche für alle Netzwerke. Mit der Einführung von Windows 10 Creators Update (Version 1703), VPN-Verbindungsstatus und VPN-Verbindungssteuerung für Benutzer Tunnel sind jetzt verfügbar über das Netzwerk-flyoutmenü (für die Windows integrierten VPN-Client), ebenfalls. |
| Auflösung von Unternehmensressourcen verwenden Kurznamen, vollqualifizierte Domänennamen (FQDN) und DNS-Suffix. | Always On VPN kann eine oder mehrere DNS-Suffixe systemintern als Teil der VPN-Verbindung und IP-Adressenzuweisung definieren, einschließlich Unternehmensressourcen-Namensauflösung für Kurznamen, FQDNs oder gesamte DNS-Namespaces. Always On VPN unterstützt auch die Verwendung von Name Resolution Policy Tabellen Bereitstellung der Granularität für Namespace-spezifische Auflösung für.<p><p>_**Hinweis:**_<br>Vermeiden Sie die Verwendung von globalen Suffixe, wie sie bei Verwendung von Name Resolution Policy Tabellen Shortname Auflösung beeinträchtigen.<p><p>Definieren Sie mithilfe von:<br>**VPNv2/ProfileName/DnsSuffix**<br>**VPNv2/ProfileName/DomainNameInformationList** |
---



## Nächste Schritte

- [Erfahren Sie mehr über die Always On VPN-Erweiterungen](always-on-vpn/always-on-vpn-enhancements.md)

- [Erfahren Sie mehr über die erweiterten Funktionen von Always On VPN](always-on-vpn/deploy/always-on-vpn-adv-options.md)

- [Erfahren Sie mehr über die Technologie von Always On VPN](always-on-vpn/always-on-vpn-technology-overview.md)

- [Planen der Always On VPN-Bereitstellung](always-on-vpn/deploy/always-on-vpn-deploy-deployment.md)

---
