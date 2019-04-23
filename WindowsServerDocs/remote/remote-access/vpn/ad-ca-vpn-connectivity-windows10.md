---
title: Bedingter Zugriff für VPN-Konnektivität mit Azure AD
description: In diesem optionalen Schritt können Sie Ihre Ressourcen mithilfe von Azure Active Directory (Azure AD) bedingten Zugriff von autorisierten VPN-Benutzerzugriff optimieren.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885271"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>Schritt 7 (Optional) Bedingter Zugriff für VPN-Verbindungen mithilfe von Azure AD

&#171;  [**Vorherige:** Schritt 6 Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)<br>
&#187; [ **Next:** Schritt 7.1. Konfigurieren von EAP-TLS, um die Prüfung (Certificate Revocation List, CRL) ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md)

In diesem optionalen Schritt können Sie optimieren, wie Ihre Ressourcen mithilfe von VPN-Benutzer Zugriff auf [Azure Active Directory (Azure AD) bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Mit Azure AD für bedingten Zugriff für Verbindungen über virtuelles privates Netzwerk (VPN) helfen Ihnen, die VPN-Verbindungen schützen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

## <a name="prerequisites"></a>Vorraussetzungen

Sie sind mit den folgenden Themen vertraut sind:
- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

Um Azure Active Directory für bedingten Zugriff für VPN-Verbindungen konfigurieren zu können, müssen Sie die folgenden Komponenten konfiguriert haben:
- [Server-Infrastruktur](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [RAS-Server für Always On-VPN](always-on-vpn/deploy/vpn-deploy-ras.md)
- [Netzwerkrichtlinienserver](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS und Firewall-Einstellungen](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Windows 10-Clientsysteme Always On-VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checkingvpn-config-eap-tls-to-ignore-crl-checkingmd"></a>[Dies ist Schritt 7.1. Konfigurieren von EAP-TLS, um die Prüfung (Certificate Revocation List, CRL) ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md)

Sie können in diesem Schritt hinzufügen **IgnoreNoRevocationCheck** und legen Sie ihn auf die Authentifizierung von Clients zuzulassen, wenn das Zertifikat keine Sperrlisten-Verteilungspunkte enthält. Standardmäßig wird die IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

Ein EAP-TLS-Client keine Verbindung herstellen, es sei denn, der NPS-Server eine sperrungsüberprüfung der Zertifikatkette (einschließlich des Stammzertifikats) abgeschlossen ist. Cloud-Zertifikate, die für den Benutzer von Azure AD ausgestellten müssen keine Zertifikatsperrliste, da sie kurzlebige Zertifikate über eine Gültigkeitsdauer von einer Stunde sind. EAP für NPS muss konfiguriert werden, um das Fehlen einer Zertifikatsperrliste zu ignorieren. Da die Authentifizierungsmethode EAP-TLS ist, dieser Registrierungswert ist nur erforderlich, unter **EAP\13**. Wenn andere EAP-Authentifizierungsmethoden verwendet werden, sollte der Registrierungswert sowie unterhalb dieser hinzugefügt. 




## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-advpn-create-root-cert-for-vpn-auth-azure-admd"></a>[Dies ist Schritt 7.2. Stammzertifikate für die VPN-Authentifizierung mit Azure AD zu erstellen.](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

In diesem Schritt konfigurieren Sie die Stammzertifikate für die VPN-Authentifizierung mit Azure AD, die automatisch eine VPN-Server-Cloud-app im Mandanten erstellt.  

Zum Konfigurieren des bedingten Zugriffs für VPN-Verbindungen müssen Sie:
1. Erstellen Sie ein VPN-Zertifikat im Azure-Portal (Sie können mehr als ein Zertifikat erstellen).
2. Herunterladen des VPN-Zertifikats an.
3. Bereitstellen Sie das Zertifikat auf Ihrem VPN-Server.

## <a name="step-73-configure-the-conditional-access-policyvpn-config-conditional-access-policymd"></a>[Dies ist Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Verbindungen. 

Um die Richtlinie für bedingten Zugriff konfigurieren zu können, müssen Sie:
1. Erstellen Sie eine Richtlinie für bedingten Zugriff, die VPN-Benutzer zugewiesen ist.
2. Legen Sie die Cloud-app auf **VPN-Server**.
3. Legen Sie die Zuweisung (Access Control) auf **erfordern Multi-Factor Authentication**.  Sie können andere Steuerelemente nach Bedarf verwenden.

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-advpn-deploy-cond-access-root-cert-to-on-premise-admd"></a>[Dies ist Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt haben Sie ein vertrauenswürdiges Stammzertifikat für die VPN-Authentifizierung bereitstellen, auf Ihre lokale AD.

Um das vertrauenswürdige Stammzertifikat bereitzustellen, müssen Sie:
1. Fügen Sie das heruntergeladene Zertifikat als eine *vertrauenswürdigen Stamm-CA für die Authentifizierung der VPN-*.
2. Importieren Sie das Stammzertifikat in das VPN-Server und VPN-Client an.
3. Stellen Sie sicher, dass die Zertifikate vorhanden sind, und zeigen als vertrauenswürdig.


## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devicesvpn-create-oma-dm-based-vpnv2-profilesmd"></a>[Dies ist Schritt 7.5. Erstellen Sie OMA-DM-basierte VPNv2-Profile für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

In diesem Schritt erstellen Sie können OMA-DM-basierte VPNv2-Profile, die mithilfe von Intune zum Bereitstellen einer Konfigurationsrichtlinie für VPN-Gerät. Wenn Sie SCCM oder PowerShell-Skript zum Erstellen von VPNv2-Profilen finden Sie unter verwenden möchten [VPNv2 CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) Weitere Details. 


## <a name="next-step"></a>Nächster Schritt
[Dies ist Schritt 7.1. Konfigurieren von EAP-TLS, um die Prüfung (Certificate Revocation List, CRL) ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md): In diesem Schritt müssen Sie hinzufügen **IgnoreNoRevocationCheck** und legen Sie ihn auf die Authentifizierung von Clients zuzulassen, wenn das Zertifikat keine Sperrlisten-Verteilungspunkte enthält. Standardmäßig wird die IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

---

## <a name="related-topics"></a>Verwandte Themen
- [VPNv2-Profile konfigurieren](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Der VPN-Client kann nun in die cloudbasierte Plattform für den bedingten Zugriff integriert werden, um eine Gerätekompatibilitätsoption für Remoteclients bereitzustellen. In diesem Schritt konfigurieren Sie die VPNv2-Profile mit  **\<DeviceCompliance > \<aktiviert > "true"\</aktiviert >**. 
 
- [Erweitern des Remotezugriffs unter Windows 10 mit einer automatischen VPN-Profil](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): Erfahren Sie, wie Microsoft für bedingten Zugriff für VPN-Verbindungen implementiert. VPN-Profile enthalten alle Informationen, die ein Gerät erfordert, für die Verbindung mit dem Unternehmensnetzwerk, einschließlich der Authentifizierungsmethoden, die unterstützt werden und der VPN-Server, dem das Gerät eine Verbindung herstellen soll. Änderungen in Windows 10 Anniversary Update, einschließlich der für den bedingten Zugriff und single Sign-on, es wurde ermöglicht, für uns, unsere Always On-VPN-clientverbindungsprofil zu erstellen. Wir erstellt haben, das Verbindungsprofil für die Domäne eingebundenen und Microsoft Intune verwalteten Geräten mit System Center Configuration Manager-Konsole. 

- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): Sicherheit ist ein wichtiges Anliegen von Organisationen, die mithilfe der Cloud. Ein wichtiger Aspekt von Cloud-Sicherheit ist die Identitäts- und zugriffsverwaltung, bei der Verwaltung Ihrer Cloudressourcen. In einer Welt primär auf Mobil- und Cloudtechnologie ausgelegte können Benutzer Ressourcen Ihrer Organisation, die mit einer Vielzahl von Geräten und apps von überall aus zugreifen. Daher reicht reicht eine Konzentration auf, die eine Ressource zugreifen kann nicht mehr. Um das Gleichgewicht zwischen Sicherheit und Produktivität zu bewahren, müssen IT-Experten auch berücksichtigen, wie eine Ressource in der Wahl der Zugriffssteuerung zugegriffen wird.

- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Der VPN-Client kann nun in die cloudbasierte Plattform für den bedingten Zugriff integriert werden, um eine Gerätekompatibilitätsoption für Remoteclients bereitzustellen. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

---