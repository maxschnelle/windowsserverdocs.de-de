---
title: Übersicht über den Remote Zugriff Always on VPN-Migration
description: Always on-VPN adressiert die vorherigen Lücken zwischen Windows-VPNs und DirectAccess sowie die Migration von DirectAccess zu Always on VPN.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: bd4d0d4d3b165a4e89a00cd2975ace20687aed7d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314988"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>Übersicht über die DirectAccess auf Always On VPN-migration 

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

&#187;[ **Weiter:** Planen der DirectAccess-Always on für die VPN-Migration](da-always-on-migration-planning.md)

In früheren Versionen der Windows-VPN-Architektur war es schwierig, die für die Ersetzung von DirectAccess erforderlichen wichtigen Funktionen bereitzustellen, wie z. b. automatische Verbindungen, die vor der Anmeldung von Benutzern initiiert wurden. Always On VPN hat die meisten dieser Einschränkungen behoben oder die VPN-Funktion über die Funktionen von DirectAccess erweitert. Always on-VPN werden die vorherigen Lücken zwischen Windows-VPNs und DirectAccess behandelt.

Der DirectAccess-–-Always on-VPN-Migrationsprozess umfasst vier primäre Komponenten und allgemeine Prozesse:


1.  **Planen Sie die Always on VPN-Migration.** Die Planung hilft bei der Identifizierung von Ziel Clients für die Trennung von Benutzer Phasen sowie von Infrastruktur und Funktionalität.

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **Stellen Sie eine Seite-an-Seite-VPN-Infrastruktur bereit.** Nachdem Sie die Migrations Phasen und die Features, die Sie in die Bereitstellung einbeziehen möchten, festgelegt haben, stellen Sie die Always on VPN-Infrastruktur nebeneinander mit der vorhandenen DirectAccess-Infrastruktur bereit.  

3.  **Stellen Sie die Zertifikate und die Konfiguration für die Clients bereit.**  Sobald die VPN-Infrastruktur bereit ist, erstellen Sie die erforderlichen Zertifikate und veröffentlichen Sie auf dem Client. Wenn die Clients die Zertifikate erhalten haben, stellen Sie das Konfigurationsskript VPN_Profile. ps1 bereit. Alternativ können Sie InTune verwenden, um den VPN-Client zu konfigurieren. Verwenden Sie Microsoft Endpoint Configuration Manager oder Microsoft InTune, um erfolgreiche VPN-Konfigurations Bereitstellungen zu überwachen.

4.  **Entfernen und Außerbetriebsetzen.** Deaktivieren Sie die Umgebung ordnungsgemäß, nachdem Sie alle Benutzer von DirectAccess migriert haben.

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>DirectAccess-Bereitstellungs Szenario

In diesem Bereitstellungs Szenario verwenden Sie ein einfaches DirectAccess-Bereitstellungs Szenario als Ausgangspunkt für die Migration dieses Handbuchs. Sie müssen dieses Bereitstellungs Szenario nicht erfüllen, bevor Sie zu Always on VPN migrieren, aber für viele Organisationen ist diese einfache Einrichtung eine genaue Darstellung Ihrer aktuellen DirectAccess-Bereitstellung. In der folgenden Tabelle finden Sie eine Liste der grundlegenden Features für dieses Setup.

Viele DirectAccess-Bereitstellungs Szenarien und-Optionen sind vorhanden, sodass sich Ihre Implementierung wahrscheinlich von der hier beschriebenen unterscheidet. Wenn dies der Fall ist, lesen Sie die [Featurezuordnung zwischen DirectAccess und Always on VPN](../vpn/vpn-map-da.md) , um die Always on VPN-Featuresatz Zuordnung für Ihre aktuellen Ergänzungen zu ermitteln, und fügen Sie diese Funktionen dann der Konfiguration hinzu. Außerdem können Sie auf die Always on- [VPN-Erweiterungen](../vpn/always-on-vpn/always-on-vpn-enhancements.md) verweisen, um ihrer Always on-VPN-Bereitstellung Optionen hinzuzufügen.

>[!NOTE] 
>Bei Geräten, die keiner Domäne beigetreten sind, gibt es weitere Überlegungen, wie z. b. die Zertifikat Registrierung. Weitere Informationen finden Sie unter [Always on-VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md).

### <a name="deployment-scenario-feature-list"></a>Funktionsliste des Bereitstellungs Szenarios

| DirectAccess-Funktion | Typisches Szenario |
|-----|----|
| Bereitstellungsszenario                   | Bereitstellen von vollständigem DirectAccess für den Client Zugriff und die Remote Verwaltung                                               |
| Netzwerkadapter                      | 2                                                                                                              |
| Benutzerauthentifizierung                   | Active Directory-Anmeldeinformationen                                                                                   |
| Verwenden von Computer Zertifikaten             | Ja                                                                                                            |
| Sicherheitsgruppen                       | Ja                                                                                                            |
| Einzelner DirectAccess-Server            | Ja                                                                                                            |
| Netzwerktopologie                      | Netzwerk Adressübersetzung (Network Address Translation, NAT) hinter einer Edge-Firewall mit zwei Netzwerkadaptern                            |
| Zugriffsmodus                           | End-to-Edge                                                                                                    |
| Tunneling                             | Geteilter Tunnel                                                                                                   |
| Authentifizierung                        | Standard Authentifizierung der Public Key-Infrastruktur (PKI) mit einem Computer Zertifikat und Kerberos (nicht kerbproxy) |
| Protokolle                             | IP über HTTPS (IP-HTTPS)                                                                                       |
| Nicht im Feld Netzwerkadressen Server (NLS) | Ja                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always on-VPN-Bereitstellungs Szenario

In diesem Bereitstellungs Szenario konzentrieren Sie sich auf das Migrieren einer einfachen DirectAccess-Umgebung in eine einfache Always on-VPN-Umgebung, die die DirectAccess-Ersetzungs Lösung ist. In der folgenden Tabelle finden Sie die Funktionen, die in dieser einfachen Lösung verwendet werden. Ausführlichere Informationen zu zusätzlichen Erweiterungen für den Always on VPN-Client finden Sie unter [Always on von VPN-Erweiterungen](../vpn/always-on-vpn/always-on-vpn-enhancements.md).

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>Always on in der einfachen Umgebung verwendete VPN-Features

| VPN-Feature | Konfiguration der Bereitstellungs Szenarien |
|-----|-----|
| Verbindungstyp | Native Internetschlüsselaustausch Version 2 (IKEv2) |
| Netzwerkadapter   | 2        |
| Benutzerauthentifizierung  | Active Directory-Anmeldeinformationen            |
| Verwenden von Computer Zertifikaten        | Ja                          |
| Routing | Tunnelung aufteilen |
| Namensauflösung | Domänen Namen-Informationsliste und Domain Name System-Suffix (DNS) |
| Ängste | Erkennung von Always on und vertrauenswürdigem Netzwerk |
| Authentifizierung  | Protected Extensible Authentication Protocol-Transport Layer Security (PAP-TLS) mit Trusted Platform Module – geschützten Benutzer Zertifikaten |

## <a name="next-step"></a>Nächster Schritt

[Planen Sie DirectAccess, um die VPN-Migration Always on](da-always-on-migration-planning.md). Die Hauptaufgabe der Migration ist das Aufrechterhalten der Remote-Konnektivität für das Büro während des gesamten Prozesses.

---