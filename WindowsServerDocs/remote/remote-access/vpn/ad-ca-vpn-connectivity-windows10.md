---
title: Bedingter Zugriff für VPN-Konnektivität mit Azure AD
description: In diesem optionalen Schritt können Sie Ihre Ressourcen mithilfe von bedingtem Zugriff von Azure Active Directory (Azure AD) wie autorisierten VPN-Benutzerzugriff optimieren.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 07/13/2018
ms.reviewer: deverette
ms.openlocfilehash: c9104a5d9ae3069e753b8b771270502c4264db96
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067300"
---
# Schritt 7. (Optional) Bedingter Zugriff für VPN-Konnektivität mit Azure AD

& #171;  [ **Vorherigen:** Schritt 6 fort. Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)<br>
& #187; [ **Weiter:** Schritt 7.1. Konfigurieren von EAP-TLS (Certificate Revocation List, CRL) überprüft ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md)

In diesem optionalen Schritt können Sie optimieren, wie der VPN-Benutzer Ihre Ressourcen mithilfe von [bedingtem Zugriff von Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)zugreifen. Mit Azure AD bedingten Zugriff für virtuelles privates Netzwerk (VPN)-Konnektivität helfen Ihnen die VPN-Verbindungen zu schützen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

## Voraussetzungen

Sie sind mit den folgenden Themen vertraut:
- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

Um Azure Active Directory bedingten Zugriff für VPN-Konnektivität zu konfigurieren, müssen Sie Folgendes konfigurieren:
- [Server-Infrastruktur](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [RAS-Server für Always On VPN](always-on-vpn/deploy/vpn-deploy-ras.md)
- [Netzwerkrichtlinienserver](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS und Firewall-Einstellungen](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Windows 10-Client Always On VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## [Schritt 7.1. Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen](vpn-config-eap-tls-to-ignore-crl-checking.md)

In diesem Schritt können Sie **IgnoreNoRevocationCheck** hinzufügen und legen sie für die Authentifizierung von Clients zuzulassen, wenn das Zertifikat nicht Verteilungspunkte enthalten ist. Standardmäßig wird IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

Ein EAP-TLS-Client kann keine Verbindung herstellen, es sei denn, der Netzwerkrichtlinienserver eine Überprüfung der Zertifikatkette (einschließlich des Stammzertifikats) abgeschlossen ist. Cloud Zertifikaten für Benutzer von Azure AD müssen eine CRL keinen, da sie kurzlebige Zertifikate mit einer Lebensdauer von einer Stunde sind. EAP für NPS muss konfiguriert werden, um das Fehlen der Zertifikatsperrliste ignorieren. Da die Authentifizierungsmethode EAP-TLS ist, ist dieses Registrierungswerts nur unter **EAP\13**erforderlich. Wenn andere EAP-Authentifizierungsmethoden verwendet werden, sollte der Registrierungswert auch unter denen hinzugefügt. 




## [Schritt 7.2. Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

In diesem Schritt konfigurieren Sie Stammzertifikate für VPN-Authentifizierung mit Azure AD, das automatisch eine VPN-Server Cloud-app im Mandanten erstellt.  

Um bedingten Zugriff für VPN-Konnektivität zu konfigurieren, müssen Sie:
1. Erstellen Sie eine VPN-Zertifikat im Azure-Portal (Sie können mehr als ein Zertifikat erstellen).
2. Das VPN-Zertifikat herunterladen.
3. Bereitstellen Sie das Zertifikat für den VPN-Server.

## [Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die bedingten Zugriffsrichtlinien für VPN-Konnektivität. 

Um die Richtlinie bedingten Zugriff zu konfigurieren, müssen Sie:
1. Erstellen einer Richtlinie bedingten Zugriff, die VPN-Benutzern zugewiesen ist.
2. Legen Sie die Cloud-app auf **VPN-Server**.
3. Legen Sie die Grant (Access Control) auf **eine mehrstufige Authentifizierung erfordern**.  Sie können nach Bedarf andere Steuerelemente verwenden.

## [Schritt 7.4. Bereitstellen von Stammzertifikate bedingten Zugriff auf lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt Sie ein vertrauenswürdiges Stammzertifikat für VPN-Authentifizierung bereitstellen, um Ihre lokale AD.

Um die vertrauenswürdiges Stammzertifikat bereitzustellen, müssen Sie:
1. Fügen Sie das heruntergeladene Zertifikat als *Vertrauenswürdige Stammzertifizierungsstelle für VPN-Authentifizierung*.
2. Importieren Sie das Stammzertifikat in der VPN-Server und der VPN-Client.
3. Stellen Sie sicher, dass die Zertifikate vorhanden sind und anzeigen als vertrauenswürdig.


## [Schritt 7.5. Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

In diesem Schritt erstellen Sie OMA-DM-basierte VPNv2-Profilen mithilfe von Intune zum Bereitstellen einer VPN-Gerätekonfiguration Richtlinie. Wenn Sie SCCM oder PowerShell-Skript verwenden, um VPNv2-Profile erstellen möchten, finden Sie weitere Informationen unter [VPNv2-CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) . 


## Nächster Schritt
[Schritt 7.1. Konfigurieren von EAP-TLS (Certificate Revocation List, CRL) überprüft ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md): In diesem Schritt müssen Sie **IgnoreNoRevocationCheck** hinzufügen und legen Sie sie um Authentifizierung von Clients zu ermöglichen, wenn das Zertifikat nicht Verteilungspunkte enthalten ist. Standardmäßig wird IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

---

## Verwandte Themen
- [VPNv2-Profilen konfigurieren](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): der VPN-Client kann nun in die Integration in die Cloud-basierte bedingten Zugriffsplattform um eine gerätekompatibilitätsoption für Remoteclients bereitzustellen. In diesem Schritt konfigurieren Sie die VPNv2-Profile mit **\ < DeviceCompliance > \ < aktiviert > True\ < / aktiviert >**. 
 
- [Verbessern der Remotezugriffs in Windows 10 mit einem automatischen VPN-Profil](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): erfahren Sie, wie Microsoft bedingten Zugriff für VPN-Konnektivität implementiert. VPN-Profile enthalten alle Informationen, die von die einem Gerät benötigt, um eine Verbindung mit dem Unternehmensnetzwerk, einschließlich der Authentifizierungsmethoden zu verwenden, die unterstützt werden und der VPN-Server, dem das Gerät eine Verbindung herstellen soll. Änderungen in Windows 10 Anniversary Update, einschließlich bedingten Zugriff und einmaliges Anmelden, Computerherstellern uns, unseren ununterbrochenes VPN-Verbindungsprofil erstellen. Wir haben das Verbindungsprofil für Domänenbenutzer und Microsoft Intune – verwalteten Geräte mithilfe von System Center Configuration Manager-Konsole. 

- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): Sicherheit ist ein Hauptanliegen für Organisationen mit der Cloud. Ein wesentlicher Aspekt der Cloud-Sicherheit ist Identitäts- und, wenn es darum geht, die Cloudressourcen verwalten. In einer Welt Mobilgeräte und Clouddienste zunehmend können Benutzer Ihrer Organisation von Ressourcen mithilfe von einer Vielzahl von Geräten und apps von überall aus zugreifen. Deshalb ist es reicht nur konzentrieren, die eine Ressource zugreifen kann nicht mehr. Um das Verhältnis zwischen Sicherheit und Produktivität Master-, müssen IT-Experten Gliedern Sie wie eine Ressource in eine Entscheidung Zugriff Steuerelement zugegriffen wird.

- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): der VPN-Client kann nun in die Integration in die Cloud-basierte bedingten Zugriffsplattform um eine gerätekompatibilitätsoption für Remoteclients bereitzustellen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

---