---
title: Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD
description: Azure AD verwendet das VPN-Zertifikat zum Signieren von Zertifikaten, die für Windows 10-Clients ausgestellt werden, bei der Authentifizierung in Azure AD für VPN-Verbindungen. Das Zertifikat als primär markiert ist, den Aussteller, die Azure AD verwendet wird.
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 40403f6be65c84cc1e2506a222a009400fcdaacc
ms.sourcegitcommit: 34232723f15c7b4d6a32ca38b7348a417ba30ae0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67464960"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>Schritt 7.2. Erstellen Sie für den bedingten Zugriff Stammzertifikate für die VPN-Authentifizierung mit Azure AD

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 7.1. Konfigurieren von EAP-TLS für das Ignorieren der Zertifikatssperrlisten-Überprüfung](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**nächster:** Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die Stammzertifikate für den bedingten Zugriff für VPN-Authentifizierung mit Azure AD, die automatisch eine Cloud-app-VPN-Server bezeichnet, im Mandanten erstellt. Zum Konfigurieren des bedingten Zugriffs für VPN-Verbindungen müssen Sie:

1. Erstellen Sie ein VPN-Zertifikat im Azure-Portal an.
2. Herunterladen des VPN-Zertifikats an.
3. Stellen Sie das Zertifikat für Ihre VPN- und NPS-Server bereit.

> [!IMPORTANT]
> Nachdem ein VPN-Zertifikat im Azure-Portal erstellt wurde, beginnt Azure AD, damit sie sofort verwenden, um kurze kurzlebige Zertifikate für den VPN-Client auszustellen. Es ist wichtig, dass das VPN-Zertifikat an den VPN-Server zur Vermeidung von Problemen mit Validierung der Anmeldeinformationen des VPN-Clients sofort bereitgestellt werden.

Wenn ein Benutzer eine VPN-Verbindung versucht wird, ruft der VPN-Client in die Web Account Manager (WAM) auf dem Windows 10-Client. WAM ruft in der Cloud-app-VPN-Server. Wenn die Bedingungen und Steuerelemente in der Richtlinie für bedingten Zugriff erfüllt sind, stellt Azure AD ein Token in Form eines kurzlebigen (1 Stunde)-Zertifikats die WAM. Die WAM platziert das Zertifikat im Zertifikatspeicher des Benutzers und Steuerung dem VPN-Client übergibt.  

Der VPN-Client sendet dann die Zertifikatsprobleme von Azure AD mit dem VPN für die Überprüfung der Anmeldeinformationen.  

> [!NOTE]
> Azure AD verwendet das zuletzt erstellte Zertifikat auf dem Blatt des VPN-Verbindung als Aussteller.

**Vorgehensweise:**

1. Melden Sie sich bei Ihrem [Azure-Portal](https://portal.azure.com) als globaler Administrator.
2. Klicken Sie auf die Sie im linken Menü auf **Azure Active Directory**.
3. Auf der **Azure Active Directory** auf der Seite die **verwalten** auf **für den bedingten Zugriff**.
4. Auf der **für den bedingten Zugriff** auf der Seite die **verwalten** auf **VPN-Konnektivität (Vorschau)** .
5. Auf der **VPN-Konnektivität** auf **neues Zertifikat**.
6. Auf der **neu** führen die folgenden Schritte aus: ein. Für **Dauer auswählen**, wählen Sie entweder 1, 2 oder 3 Jahre.
   b. Wählen Sie **Erstellen** aus.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.3: Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md): In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Verbindungen.
