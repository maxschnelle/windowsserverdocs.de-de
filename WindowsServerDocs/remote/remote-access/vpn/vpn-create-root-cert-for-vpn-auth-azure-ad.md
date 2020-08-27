---
title: Erstellen von Stammzertifikaten für die VPN-Authentifizierung mit Azure AD
description: In Azure AD wird das VPN-Zertifikat zum Signieren von Zertifikaten verwendet, die für Windows 10-Clients ausgestellt werden, wenn die Authentifizierung bei Azure AD für VPN-Verbindungen erfolgt. Das als primär gekennzeichnete Zertifikat ist der Aussteller, der von Azure AD verwendet wird.
ms.topic: article
ms.date: 06/28/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: dfcdea3b719cee685222fdf5919ce5e674ca1e64
ms.sourcegitcommit: 52a8d5d7e969eaa07fd3a45ed6d3cb5a5173b6d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970637"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>Schritt 7.2: Erstellen von Stamm Zertifikaten für den bedingten Zugriff für die VPN-Authentifizierung mit Azure AD

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 7,1. Konfigurieren von EAP-TLS zum Ignorieren der CRL-Überprüfung (Zertifikat Sperr Liste)](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**Weiter:** Schritt 7,3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die Stamm Zertifikate für den bedingten Zugriff für die VPN-Authentifizierung mit Azure AD, wodurch automatisch eine Cloud-App mit dem Namen VPN-Server im Mandanten erstellt wird. Erforderliche Schritte zum Konfigurieren des bedingten Zugriffs für VPN-Verbindungen:

1. Erstellen eines VPN-Zertifikats über das Azure-Portal
2. Herunterladen des VPN-Zertifikats
3. Stellen Sie das Zertifikat für Ihre VPN-und NPS-Server bereit.

> [!IMPORTANT]
> Sobald ein VPN-Zertifikat in der Azure-Portal erstellt wurde, wird es von Azure AD sofort verwendet, um dem VPN-Client kurzlebige Zertifikate auszustellen. Es ist wichtig, dass das VPN-Zertifikat sofort auf dem VPN-Server bereitgestellt wird, um Probleme mit der Überprüfung der Anmelde Informationen des VPN-Clients zu vermeiden.

Wenn ein Benutzer versucht, eine VPN-Verbindung herzustellen, ruft der VPN-Client den Webkonto-Manager (WAM) auf dem Windows 10-Client auf. WAM Ruft die VPN-Server-Cloud-App auf. Wenn die Bedingungen und Steuerelemente in der Richtlinie für bedingten Zugriff erfüllt sind, stellt Azure AD ein Token in Form eines kurzlebigen Zertifikats (1 Stunde) für das WAM aus. Das Zertifikat wird vom WAM in den Zertifikat Speicher des Benutzers eingefügt, und die Steuerung wird an den VPN-Client weitergeleitet. 

Der VPN-Client sendet dann das von Azure AD ausgestellte Zertifikat zur Überprüfung der Anmelde Informationen an das VPN. 

> [!NOTE]
> Azure AD verwendet das zuletzt erstellte Zertifikat auf dem Blatt VPN-Konnektivität als Aussteller.

**Dringlichkeit**

1. Melden Sie sich als globaler Administrator beim [Azure-Portal](https://portal.azure.com) an.
2. Klicken Sie im linken Menü auf **Azure Active Directory**.
3. Klicken Sie auf der Seite **Azure Active Directory** im Abschnitt **Verwalten** auf **Sicherheit**.
4. Klicken Sie auf der Seite **Sicherheit** im Abschnitt **Schutz** auf **bedingter Zugriff**.
5. Bei **bedingtem Zugriff | ** Auf der Seite Richtlinien im Abschnitt **Verwalten** auf **VPN-Konnektivität**.
5. Klicken Sie auf der Seite **VPN-Konnektivität** auf **Neues Zertifikat**.
6. Führen Sie auf der Seite **neu** die folgenden Schritte aus: a. Wählen Sie für **Select Duration**entweder 1, 2 oder 3 Jahre aus.
    b. Klicken Sie auf **Erstellen**.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7,3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md): in diesem Schritt konfigurieren Sie die Richtlinie für den bedingten Zugriff für VPN-Konnektivität.
