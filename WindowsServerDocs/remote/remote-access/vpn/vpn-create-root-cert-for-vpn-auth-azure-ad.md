---
title: Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD
description: Azure AD verwendet das VPN-Zertifikat zum Signieren von Zertifikaten, die für Windows 10-Clients bei der Authentifizierung bei Azure AD für VPN-Konnektivität ausgestellt wurden. Das als primär gekennzeichnete Zertifikat ist der Aussteller, der von Azure AD verwendet wird.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 06/28/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: f4501c244726ee9b23a6d517c4b835f0c9418302
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818803"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>Schritt 7.2. Erstellen von Stamm Zertifikaten für den bedingten Zugriff für die VPN-Authentifizierung mit Azure AD

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 7,1. Konfigurieren von EAP-TLS zum Ignorieren der CRL-Überprüfung (Zertifikat Sperr Liste)](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**Weiter:** Schritt 7,3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die Stamm Zertifikate für den bedingten Zugriff für die VPN-Authentifizierung mit Azure AD, wodurch automatisch eine Cloud-App mit dem Namen VPN-Server im Mandanten erstellt wird. Zum Konfigurieren des bedingten Zugriffs für VPN-Konnektivität müssen Sie folgende Schritte ausführen:

1. Erstellen Sie ein VPN-Zertifikat in der Azure-Portal.
2. Laden Sie das VPN-Zertifikat herunter.
3. Stellen Sie das Zertifikat für Ihre VPN-und NPS-Server bereit.

> [!IMPORTANT]
> Sobald ein VPN-Zertifikat in der Azure-Portal erstellt wurde, wird es von Azure AD sofort verwendet, um dem VPN-Client kurzlebige Zertifikate auszustellen. Es ist wichtig, dass das VPN-Zertifikat sofort auf dem VPN-Server bereitgestellt wird, um Probleme mit der Überprüfung der Anmelde Informationen des VPN-Clients zu vermeiden.

Wenn ein Benutzer versucht, eine VPN-Verbindung herzustellen, ruft der VPN-Client den Webkonto-Manager (WAM) auf dem Windows 10-Client auf. WAM Ruft die VPN-Server-Cloud-App auf. Wenn die Bedingungen und Steuerelemente in der Richtlinie für bedingten Zugriff erfüllt sind, stellt Azure AD ein Token in Form eines kurzlebigen Zertifikats (1 Stunde) für das WAM aus. Das Zertifikat wird vom WAM in den Zertifikat Speicher des Benutzers eingefügt, und die Steuerung wird an den VPN-Client weitergeleitet.  

Der VPN-Client sendet die Zertifikat Probleme dann an das VPN, um die Überprüfung der Anmelde Informationen durch Azure AD.  

> [!NOTE]
> Azure AD verwendet das zuletzt erstellte Zertifikat auf dem Blatt VPN-Konnektivität als Aussteller.

**Dringlichkeit**

1. Melden Sie sich bei Ihrem [Azure-Portal](https://portal.azure.com) als globaler Administrator an.
2. Klicken Sie im Menü auf der linken Seite auf **Azure Active Directory**.
3. Klicken Sie auf der Seite **Azure Active Directory** im Abschnitt **Verwalten** auf **bedingter Zugriff**.
4. Klicken Sie auf der Seite **bedingter Zugriff** im Abschnitt **Verwalten** auf **VPN-Konnektivität (Vorschau)** .
5. Klicken Sie auf der Seite **VPN-Konnektivität** auf **Neues Zertifikat**.
6. Führen Sie auf der Seite **neu** die folgenden Schritte aus: a. Wählen Sie für **Select Duration**entweder 1, 2 oder 3 Jahre aus.
   b. Wählen Sie **Erstellen** aus.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7,3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md): in diesem Schritt konfigurieren Sie die Richtlinie für den bedingten Zugriff für VPN-Konnektivität.
