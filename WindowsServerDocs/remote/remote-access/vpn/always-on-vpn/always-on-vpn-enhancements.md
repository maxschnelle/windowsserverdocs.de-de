---
title: Always On VPN-Verbesserungen
description: Always On VPN hat gegenüber der Windows-VPN-Lösungen in den letzten viele Vorteile. Wichtige Verbesserungen bei der Integration, Sicherheit, Konnektivität, Netzwerk-Steuerelement und Kompatibilität Microsoft Cloud ausgelegt, Mobile ausgelegt Vision Always On VPN ausgerichtet.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7844d93ac898316580123c82e08bb6f02d51a2b
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067340"
---
# Always On VPN-Verbesserungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

& #171; [ **Vorherige:** erfahren Sie mehr über die Always On VPN-Features](../vpn-map-da.md)<br>
& #187; [ **Weiter:** erfahren Sie mehr über die Always On VPN-Technologie](always-on-vpn-technology-overview.md)

Always On VPN hat gegenüber der Windows-VPN-Lösungen in den letzten viele Vorteile. Folgenden wichtigen Verbesserungen ausrichten Always On VPN mit Microsoft Cloud ausgelegt, Mobile ausgelegt Vision:

- **Plattformintegration:** Always On VPN hat verbesserte Integration mit dem Windows-Betriebssystem und Drittanbieter-Lösungen, eine stabile Plattform für zahllose erweiterte Verbindungsszenarien bereitzustellen.

- **Sicherheit:** Always On VPN hat neue, erweiterte Sicherheitsfunktionen für den Typ des Datenverkehrs, einschränken, welche Anwendungen die VPN-Verbindung verwenden können, und welche Authentifizierungsmethoden zu verwenden, die Sie zum Initiieren der Verbindung verwenden können. Wenn die Verbindung in den meisten Fällen aktiv ist, ist es besonders wichtig, um die Verbindung zu sichern. Weitere Informationen finden Sie unter [VPN-Authentifizierungsoptionen](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-authentication).

- **VPN-Konnektivität:** Always On VPN bietet mit oder ohne Gerätetunnelfunktion automatische Auslösung-Funktion. Bevor Sie Always On VPN war die Möglichkeit, eine automatische Verbindung über den Benutzer oder Geräteauthentifizierung auszulösen nicht möglich.  

- **Netzwerke Steuerelement:** Always On VPN ermöglicht Administratoren angeben, Routingrichtlinien auf eine genauere Ebene – sogar an die einzelnen Anwendung – die eignet sich optimal für Line-of-Business (LOB)-apps, die spezielle Remotezugriff benötigen.  Always On VPN ist vollständig kompatibel mit sowohl Internet Protocol Version 4 (IPv4) und IPv6 (Version 6). Im Gegensatz zu DirectAccess besteht es keine bestimmte Abhängigkeit in IPv6.

  >[!Note]
  >Bevor Sie beginnen, stellen Sie sicher, dass IPv6 auf dem VPN-Server aktivieren. Andernfalls kann keine Verbindung hergestellt werden, und eine Fehlermeldung angezeigt wird.
  
- **Konfiguration und Kompatibilität:** Always On VPN kann bereitgestellt und verwaltet, verschiedene Möglichkeiten, die Always On VPN mehrere Vorteile gegenüber der VPN-Clientsoftware ermöglicht werden.

## Plattform-integration

Microsoft hat eingeführt oder die folgenden Integrationsfunktionen in Always On VPN verbessert:

| Wichtige Verbesserung | Beschreibung |
| ---- | ---- |
| **[Windows Information Protection (WIP)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)** | Integration mit WIP können-netzwerkrichtlinienerzwingung bestimmt, ob Datenverkehr über VPN geleitet zulässig ist. Wenn das Benutzerprofil aktiv ist und WIP-Richtlinien angewendet werden, wird automatisch Always On VPN ausgelöst, um eine Verbindung herzustellen. Auch bei der Verwendung von WIP besteht keine Notwendigkeit Apptriggerlist-und die trafficfilterlist-Regel nicht separat im VPN-Profil angeben (es sei denn, Sie komplexere Konfiguration möchten), da die WIP-Richtlinien und die Anwendung Listen automatisch wirksam werden. |
| **[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-overview)** | Always On VPN unterstützt systemintern Windows Hello for Business (im Modus zertifikatbasierte Authentifizierung) um eine nahtlose Anmeldung einmaliges für beide melden Sie sich mit dem Computer und mit dem VPN-Verbindung bereitzustellen. Aus diesem Grund ist keine sekundäre Authentifizierung (Benutzeranmeldeinformationen) für die VPN-Verbindung, wodurch es möglich, eine Verbindung Always On mit Windows Hello for Business-Authentifizierung verwenden erforderlich. |
| **[Bedingter Zugriff in Microsoft Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)** | Der Always On VPN-Client kann mit der Plattform Bedingter Zugriff in Azure Multi-Factor Authentication (MFA), Gerätekompatibilität oder einer Kombination aus beidem zu erzwingen integriert. Beim einhalten bedingter Zugriffsrichtlinien, stellt Azure Active Directory (Azure AD) ein kurzlebiges (standardmäßig 60 Minuten) IP-Sicherheit (IPsec) Authentifizierungszertifikat aus, das der VPN-Gateway-Authentifizierung verwendet werden kann. Gerätekompatibilität verwendet System Center Configuration Manager/Intune-Kompatibilitätsrichtlinien, die den Zustand des geräteintegritätsnachweises Gerät als Teil der Verbindung Compliance-Prüfung aufnehmen können. |
| **Azure MFA** | In Kombination mit Remote Authentication Dial-In User Service (RADIUS) Dienste und die Erweiterung (Network Policy Server, NPS) für Azure MFA können VPN-Authentifizierung starken MFA verwenden. |
| **Drittanbieter-VPN-Plug-in** | Mit der universellen Windows-Plattform (UWP), können VPN-Drittanbieter eine einzelne Anwendung für die sämtliche Windows 10-Geräte erstellen. Die UWP bietet eine garantierte Kern-API-Ebene auf allen Geräten, Wegfall der Komplexität der und häufig Probleme mit dem Schreiben von Treiber auf Kernel-Ebene. Derzeit sind Windows 10-UWP-VPN-Plug-ins für [Pulse Secure](https://www.microsoft.com/p/pulse-secure/9nblggh3b0bp), [F5 Access](https://www.microsoft.com/p/f5-access/9wzdncrdsfn0), [Check Point Capsule-VPN](https://www.microsoft.com/p/check-point-capsule-vpn/9wzdncrdjxtj), [FortiClient](https://www.microsoft.com/p/forticlient/9wzdncrdh6mc), [SonicWall Mobile Connect](https://www.microsoft.com/p/sonicwall-mobile-connect/9wzdncrdsfkz)und [GlobalProtect](https://www.microsoft.com/p/globalprotect/9nblggh6bzl3)vorhanden; Folglich werden andere in Zukunft angezeigt. |
---

## Sicherheit

Die primären Verbesserungen bei der Sicherheit sind in den folgenden Bereichen:

| Wichtige Verbesserung | Beschreibung |
| ---- | ---- |
| **Datenverkehrsfilter** | Über Datenverkehrsfilter können Sie clientseitige Richtlinien festlegen, die bestimmen, welcher Datenverkehr im Unternehmensnetzwerk zugelassen wird. Auf diese Weise können Administratoren app oder Datenverkehr Einschränkungen auf die VPN-Schnittstelle anwenden, seine Verwendung auf bestimmten Quellen, Zielports und IP-Adressen zu begrenzen. Zwei Arten von Regeln für Filterplattform sind verfügbar:<ul><li>**App-basierte Regeln.** App-basierte Firewall-Regeln basieren auf eine Liste der angegebenen Applications, damit nur Datenverkehr vom diese apps sind berechtigt, über die VPN-Schnittstelle geleitet.</li><li>**Datenverkehrsbasierte Regeln.** Datenverkehrsbasierte Firewall-Regeln basieren auf netzwerkanforderungen wie Ports, Adressen und Protokolle. Verwenden Sie diese Regeln nur für den Datenverkehr, der diese bestimmten Bedingungen entspricht zulässig sind, über die VPN-Schnittstelle geleitet.<p><p>_**Hinweis:**_<br>Diese Regeln gelten nur für ausgehenden Datenverkehr vom Gerät. Verwendung von Datenverkehr filtert die eingehenden Datenverkehr vom Unternehmensnetzwerk Blöcke an den Client. </li></ul> |
| **VPN pro App** | VPN pro App ist vergleichbar mit einer app-basierter Datenverkehrsfilter, aber es geht weiter Anwendung Trigger mit einer app-basierter Datenverkehrsfilter kombinieren, damit die VPN-Konnektivität zu einer bestimmten Anwendung im Gegensatz zu alle Anwendungen auf dem VPN-Client zur Verfügung steht. Das Feature initiiert automatisch, wenn die app gestartet wird. |
| **Unterstützung für benutzerdefinierte IPSec-kryptografischen Algorithmen** | Always On VPN unterstützt die Verwendung des RSA- und ECDSA Curve Cryptography-basierter benutzerdefinierte kryptografischen Algorithmen strengen Behörden oder Sicherheitsrichtlinien des Unternehmens erfüllen. |
| **Systemeigene Unterstützung von Extensible Authentication-Protokoll (EAP)** | Always On VPN unterstützt EAP, das Ihnen ermöglicht, einen unterschiedlichen Satz von Microsoft und Drittanbietern EAP-Typen als Teil der Workflow-Authentifizierung verwenden. EAP ermöglicht eine sichere Authentifizierung basierend auf mögliche Authentifizierungstypen:<ul><li>Benutzername und Kennwort</li><li>Smartcard (physische und virtuelle)</li><li>Benutzerzertifikate</li><li>Windows Hello for Business</li><li>MFA-Unterstützung über EAP RADIUS-integration</li></ul>Hersteller der Anwendung steuert Drittanbieter-UWP-VPN-Plug-Ins Authentifizierungsmethoden zu verwenden, die zwar ein Array von verfügbaren Optionen, einschließlich Arten von benutzerdefinierten Anmeldeinformationen und OTP-Unterstützung. |
---

## VPN-Konnektivität

Im folgenden sind die primären Verbesserungen in Always On VPN-Konnektivität:

| Wichtige Verbesserung | Beschreibung |
| ---- | ---- |
| **Always On** | Always On ist ein Windows 10-Feature, das aktive VPN-Profil automatisch eine Verbindung her und verbunden basierend auf Trigger bleiben können – nämlich Anmeldung des Benutzers an, Netzwerk Zustandsänderung oder des Gerätebildschirms im aktiven. Always On ist auch in die verbundener standby Erfahrung Akkulebensdauer integriert. |
| **Auslösen der Anwendung** | Sie können VPN-Profile in Windows 10 beim Start eines angegebenen Satzes von Anwendungen automatisch eine Verbindung konfigurieren. Sie können sowohl Desktop-als auch UWP-Anwendungen zu lösen Sie eine VPN-Verbindung konfigurieren. |
| **Namenbasierte auslösen** | Mit Always On VPN können Sie Regeln definieren, damit bestimmte Domänennamensabfragen die VPN-Verbindung auszulösen. Windows 10 unterstützt jetzt die namenbasierte für die Domäne eingebundene und keiner Domäne beigetreten eingebundene Computer auslösen (bisher nur keiner Domäne beigetreten eingebundenen Computern unterstützt wurden). |
| **Erkennen vertrauenswürdiger Netzwerke** | Always On VPN enthält dieses Feature, um sicherzustellen, dass VPN-Konnektivität dann nicht ausgelöst, wenn ein Benutzer mit einem vertrauenswürdigen Netzwerk innerhalb der Grenzen des Unternehmens verbunden ist. Sie können dieses Feature mit die auslösenden Methoden, um eine nahtlose "nur bei Bedarf verbinden" Reaktionsverhalten erwähnten kombinieren. |
| **[Gerätetunnelfunktion](../vpn-device-tunnel-config.md)** | Always On VPN bietet Ihnen die Möglichkeit, eine dedizierte VPN-Profil für Computer oder Gerät zu erstellen. Im Gegensatz zu _Benutzer Tunnel_, der nur nach der Anmeldung eines Benutzers an das Gerät oder Computer verbunden ist, können _Gerätetunnelfunktion_ VPN-Verbindung herstellen der Verbindung vor der Anmeldung des Benutzers an. Gerätetunnelfunktion und Benutzer Tunnel funktionieren unabhängig mit ihrer VPN-Profile, zur gleichen Zeit verbunden werden kann, und können je nach Bedarf andere Authentifizierungsmethoden zu verwenden und andere Einstellungen für die VPN-Konfiguration verwenden. |
---

## Networking

Im folgenden werden einige der Netzwerken Verbesserungen in Always On VPN:

| Wichtige Verbesserung | Beschreibung |
| ---- | ---- |
| **Dual-Stack-Unterstützung für IPv4 und IPv6** | Always On VPN unterstützt die Verwendung von IPv4 und IPv6 nativ in einem Dual-Stack-Ansatz. Es hat keine bestimmte Abhängigkeit ein Protokoll gegenüber anderen, die maximale IPv4/IPv6-Anwendungskompatibilität in Kombination mit Unterstützung für zukünftige IPv6 Anforderungen networking ermöglicht.<p>**_Hinweis:_** Bevor Sie beginnen, stellen Sie sicher, dass IPv6 auf dem VPN-Server aktivieren. Andernfalls kann keine Verbindung hergestellt werden, und eine Fehlermeldung angezeigt wird.|
| **Anwendungsspezifische Routingrichtlinien** | Zusätzlich zur Definition von globaler VPN-Verbindung Routingrichtlinien für Internet- und Intranet-datenverkehrstrennung, ist es möglich, routing Richtlinien zum Steuern der Verwendung von geteiltes Tunneling oder force Tunnel-Konfigurationen auf einzelne Anwendung hinzufügen. Diese Option bietet Ihnen eine detailliertere Kontrolle darüber, welche apps zulässig sind, welche Ressourcen über die VPN-Tunnel interagieren. |
| **Ausschlussrouten** | Always On VPN unterstützt die Möglichkeit, die Angabe von ausschlussrouten, die speziell routing Verhalten steuern, um der Datenverkehr sollte nur das VPN durchlaufen und wechseln Sie nicht über die physische Netzwerkschnittstelle zu definieren.<p><p>_**Anmerkungen zu dieser.**_<br>-Ausschlussrouten funktionieren derzeit für Datenverkehr im selben Subnetz wie der Client, z. B. LinkLocal.<br>-Ausschlussrouten, funktionieren nur in einem geteiltes Tunneling-Setup. |
---

## Konfiguration und Kompatibilität 

Im folgenden werden einige der Konfiguration und Kompatibilität Verbesserungen in Always On VPN:

| Wichtige Verbesserung | Beschreibung |
| ---- | ---- |
| **Drittanbieter-VPN-Gateway-Kompatibilität** | Der Always On VPN-Client ist die Verwendung von einem Microsoft-basierte VPN-Gateway für den Betrieb nicht erforderlich. Durch die Unterstützung des Protokolls IKEv2 ermöglicht der Client Interoperabilität mit Drittanbieter-VPN-Gateways, die diese branchenüblichen Tunneling-Typ unterstützen. Sie können auch Interoperabilität mit Drittanbieter-VPN-Gateways erreichen, mit einem UWP-VPN-Plug-in in Kombination mit einem benutzerdefinierten Tunneling-Typ ohne Kompromisse bei der Always On VPN-Plattformfeatures und Vorteile.<p><p>_**Hinweis:**_<br>Wenden Sie sich an Ihren Gateway oder Drittanbieter-Back-End-Einheit Anbieter, Konfigurationen und Kompatibilität mit Always On VPN und Gerätetunnelfunktion mithilfe von IKEv2. |
| **Unterstützung von branchenüblichen IKEv2-VPN-Protokolle** | Der Always On VPN-Client unterstützt IKEv2, eine der heutigen am häufigsten verwendet branchenübliche Tunnelingprotokolle aus. Diese Kompatibilität maximiert Interoperabilität mit Drittanbieter-VPN-Gateways. |
| **Plattform-Unterstützung** | AAlways auf VPN unterstützt mit der Domäne, keiner Domäne beigetreten sind (Arbeitsgruppe) oder Azure AD eingebundene Geräte für beide Unternehmen ermöglichen und BYOD your own Device (BYOD)-Szenarien. Always On VPN ist außerdem in allen Windows-Editionen verfügbar. |
| **Diverse Mechanismen für Verwaltung und Bereitstellung** | Sie können viele Verwaltungs- und Mechanismen zur Verwaltung von VPN-Einstellungen (ein _VPN-Profil_genannt), einschließlich Windows PowerShell, System Center Configuration Manager, Intune (oder Mobilgerät Drittanbieter-Verwaltungstool [MDM]) verwenden und Windows Konfigurations-Designer. Diese Optionen vereinfachen die Konfiguration von Always On VPN unabhängig von der Client-Management-Tools, die Sie verwenden. |
| **Standardisierte VPN-Profildefinition** | Always On VPN unterstützt die Konfiguration mithilfe einer XML-Standardprofil (ProfileXML), Bereitstellung von einer Standardkonfiguration Vorlage-Format, das meisten Verwaltung und Bereitstellungstoolsets verwenden. |
---


## Nächste Schritte

- [Erfahren Sie mehr über die erweiterten Funktionen von Always On VPN](deploy/always-on-vpn-adv-options.md)

- [Erfahren Sie mehr über die Technologie von Always On VPN](always-on-vpn-technology-overview.md)

- [Planen der Always On VPN-Bereitstellung](deploy/always-on-vpn-deploy-deployment.md)



---
