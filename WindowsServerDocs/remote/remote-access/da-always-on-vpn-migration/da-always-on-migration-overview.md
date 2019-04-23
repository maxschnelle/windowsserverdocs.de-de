---
title: Übersicht über die Remote Access Always On-VPN-migration
description: Always On-VPN-werden die vorherigen Lücken zwischen den Windows-VPN und DirectAccess, und Migration von DirectAccess zu Always On-VPN-behandelt.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 402d8ff72fe869572c9e6129cdf1aa7e755c354a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845981"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>Übersicht über die DirectAccess auf Always On VPN-migration 

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

&#187; [**Next:** Planen von DirectAccess auf Always On-VPN-migration](da-always-on-migration-planning.md)

In früheren Versionen der Windows-VPN-Architektur war plattformeinschränkungen es schwierig zu wichtigen Funktionen erforderlich sind, um DirectAccess, z. B. automatische Verbindungen initiiert werden, bevor Benutzer sich anmelden zu ersetzen. Always On VPN hat die meisten dieser Einschränkungen behoben oder die VPN-Funktion über die Funktionen von DirectAccess erweitert. Always On-VPN-Adressen der vorherigen Lücken zwischen den Windows-VPN und DirectAccess.

Der DirectAccess –, – Always On-VPN-Migrationsprozess besteht aus vier Hauptkomponenten und Prozesse auf hoher Ebene:


1.  **Planen Sie die Always On-VPN-Migration.** Planen der erleichtert das Identifizieren von Zielclients für Phase Trennung von Benutzern als auch die Infrastruktur und Funktionen.

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **Stellen Sie eine Seite-an-Seite-VPN-Infrastruktur bereit.** Nachdem Sie ermittelt haben, Ihre Migrationsphasen und die Features, die in Ihrer Bereitstellung enthalten sein sollen, stellen Sie die Always On-VPN-Infrastruktur parallel mit der vorhandenen DirectAccess-Infrastruktur.  

3.  **Bereitstellen Sie Zertifikate und die Konfiguration für die Clients.**  Nachdem die VPN-Infrastruktur fertig ist, erstellen und veröffentlichen die erforderlichen Zertifikate an den Client. Wenn die Clients die Zertifikate erhalten haben, stellen Sie das Konfigurationsskript VPN_Profile.ps1 bereit. Alternativ können Sie Intune zum Konfigurieren des VPN-Clients verwenden. Verwenden Sie Microsoft System Center Configuration Manager oder Microsoft Intune, um die erfolgreiche VPN-Konfiguration-Bereitstellungen zu überwachen.

4.  **Entfernen Sie aus, und außer Betrieb nehmen.** Ordnungsgemäß außer Betrieb der umgebungs, nachdem Sie alle Benutzer deaktiviert DirectAccess migriert haben.

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>Szenario der DirectAccess-Bereitstellung

In diesem Szenario verwenden Sie ein einfaches Szenario der DirectAccess-Bereitstellung als Ausgangspunkt für die Migration, die diesem Handbuch werden. Sie müssen nicht bei diesem Bereitstellungsszenario vor der Migration zu Always On-VPN-übereinstimmen, aber für viele Organisationen dieses einfache Setup eine genaue Darstellung ihrer aktuellen DirectAccess-Bereitstellung ist. Die folgende Tabelle enthält eine Liste der grundlegenden Funktionen für diese Konfiguration.

Viele DirectAccess-Bereitstellungsszenarien und Optionen vorhanden sind, ist Ihre Implementierung wahrscheinlich von den hier beschriebenen unterscheiden. Wenn dies der Fall ist, finden Sie unter [Feature-Zuordnung zwischen DirectAccess und Always On-VPN-](../vpn/vpn-map-da.md) zu bestimmen, das Feature Always On-VPN-Zuordnung für die aktuelle Erweiterungen, und fügen Sie dann die Funktionen Ihrer Konfiguration hinzu. Darüber hinaus sehen Sie sich die [Verbesserungen für Always On-VPN-](../vpn/always-on-vpn/always-on-vpn-enhancements.md) Optionen zur Always On-VPN-Bereitstellung hinzufügen.

>[!NOTE] 
>Für nicht-Domänenkonto eingebundene Geräte sind zusätzliche Überlegungen, wie z. B. Registrierung von Zertifikaten. Weitere Informationen finden Sie unter [Always On-VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md).

### <a name="deployment-scenario-feature-list"></a>Bereitstellung Szenario-Funktionsliste

| DirectAccess-Funktion | Typisches Szenario |
|-----|----|
| Bereitstellungsszenario                   | Bereitstellen Sie gesamtes DirectAccess für Clientzugriff und Remoteverwaltung                                               |
| Netzwerkadapter                      | 2                                                                                                              |
| Benutzerauthentifizierung                   | Active Directory-Anmeldeinformationen                                                                                   |
| Computerzertifikate verwenden             | Ja                                                                                                            |
| Sicherheitsgruppen                       | Ja                                                                                                            |
| DirectAccess-Servers            | Ja                                                                                                            |
| Netzwerktopologie                      | Netzwerkadressübersetzung (NAT) hinter einer Edge-Firewall mit zwei Netzwerkadaptern                            |
| Zugriffsmodus                           | End-to edge                                                                                                    |
| Tunneling                             | Split-Tunneling                                                                                                   |
| Authentifizierung                        | Standard: public Key-Infrastruktur (PKI)-Authentifizierung mit Computerzertifikat sowie Kerberos (nicht KerbProxy) |
| Protokolle                             | IP über HTTPS (IP-HTTPS)                                                                                       |
| Network Location Server (NLS) Feld | Ja                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always On-VPN-Bereitstellungsszenario

In diesem Szenario liegt der Schwerpunkt auf die Migration von einer einfachen DirectAccess-Umgebung zu einer einfachen Always On-VPN-Umgebung handelt es sich der DirectAccess-Lösung ersetzt. Die folgende Tabelle enthält die Funktionen, die in dieser einfachen Lösung verwendet. Ausführlichere Informationen zu weiteren Verbesserungen an der Always On-VPN-Client finden Sie unter [Verbesserungen für Always On-VPN-](../vpn/always-on-vpn/always-on-vpn-enhancements.md).

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>Always On-VPN-Features, die in der einfachen Umgebung verwendet

| VPN-Funktion | Szenario-Bereitstellungskonfiguration |
|-----|-----|
| Verbindungstyp | Systemeigene Internet Key Exchange Version 2 (IKEv2) |
| Netzwerkadapter   | 2        |
| Benutzerauthentifizierung  | Active Directory-Anmeldeinformationen            |
| Computerzertifikate verwenden        | Ja                          |
| Routing | Split-Tunneling |
| Namensauflösung | Liste der Domänennameninformationen und Domain Name System (DNS-Suffix) |
| Auslösen | Erkennung von Always on und vertrauenswürdiges Netzwerk |
| Authentifizierung  | Protected Extensible Authentication Protocol-Transport Layer Security (PEAP-TLS) mit Trusted Platform Module – geschützt Benutzerzertifikate |

## <a name="next-step"></a>Nächster Schritt

[Planen von DirectAccess auf die Migration zu Always On-VPN-](da-always-on-migration-planning.md). Die Hauptaufgabe der Migration ist das Aufrechterhalten der Remote-Konnektivität für das Büro während des gesamten Prozesses.

---