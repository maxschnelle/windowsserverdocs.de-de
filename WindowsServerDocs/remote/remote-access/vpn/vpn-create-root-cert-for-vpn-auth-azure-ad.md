---
title: Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD
description: Azure AD verwendet das VPN-Zertifikat zum Signieren von Zertifikaten, die für Windows 10-Clients ausgestellt werden, bei der Authentifizierung in Azure AD für VPN-Verbindungen. Das Zertifikat als primär markiert ist, den Aussteller, die Azure AD verwendet wird.
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: dc24f0275e8639ffd972ae24550d0ada38eff4f1
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749636"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>Schritt 7.2. Erstellen Sie für den bedingten Zugriff Stammzertifikate für die VPN-Authentifizierung mit Azure AD

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 7.1. Konfigurieren von EAP-TLS für das Ignorieren der Zertifikatssperrlisten-Überprüfung](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**nächster:** Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie die Stammzertifikate für den bedingten Zugriff für VPN-Authentifizierung mit Azure AD, die automatisch eine Cloud-app-VPN-Server bezeichnet, im Mandanten erstellt. Zum Konfigurieren des bedingten Zugriffs für VPN-Verbindungen müssen Sie:

1. Erstellen Sie ein VPN-Zertifikat im Azure-Portal (Sie können mehr als ein Zertifikat erstellen).
2. Herunterladen des VPN-Zertifikats an.
3. Stellen Sie das Zertifikat für Ihre VPN- und NPS-Server bereit.

Wenn ein Benutzer eine VPN-Verbindung versucht wird, ruft der VPN-Client in die Web Account Manager (WAM) auf dem Windows 10-Client. WAM ruft in der Cloud-app-VPN-Server. Wenn die Bedingungen und Steuerelemente in der Richtlinie für bedingten Zugriff erfüllt sind, stellt Azure AD ein Token in Form eines kurzlebigen (1 Stunde)-Zertifikats die WAM. Die WAM platziert das Zertifikat im Zertifikatspeicher des Benutzers und Steuerung dem VPN-Client übergibt.  

Der VPN-Client sendet dann die Zertifikatsprobleme von Azure AD mit dem VPN für die Überprüfung der Anmeldeinformationen.  Azure AD verwendet das Zertifikat mit der Kennzeichnung **primären** in das Blatt "VPN-Konnektivität" als Aussteller. 

Im Azure-Portal erstellen Sie zwei Zertifikate, um den Übergang zu gewährleisten, wenn ein Zertifikat läuft bald ab. Wenn Sie ein Zertifikat erstellen, wählen Sie, ob es sich um das primäre Zertifikat handelt, die während der Authentifizierung zum Signieren des Zertifikats für die Verbindung verwendet wird.

**Vorgehensweise:**

1. Melden Sie sich bei Ihrem [Azure-Portal](https://portal.azure.com) als globaler Administrator.

2. Klicken Sie auf die Sie im linken Menü auf **Azure Active Directory**. 

    ![Azure Active Directory auswählen](../../media/Always-On-Vpn/01.png)

3. Auf der **Azure Active Directory** auf der Seite die **verwalten** auf **für den bedingten Zugriff**.

    ![Wählen Sie für den bedingten Zugriff](../../media/Always-On-Vpn/02.png)

4. Auf der **für den bedingten Zugriff** auf der Seite die **verwalten** auf **VPN-Konnektivität (Vorschau)** .

    ![Wählen Sie die VPN-Konnektivität](../../media/Always-On-Vpn/03.png)

5. Auf der **VPN-Konnektivität** auf **neues Zertifikat**.

    ![Wählen Sie neues Zertifikat](../../media/Always-On-Vpn/04.png)

6. Auf der **neu** führen die folgenden Schritte aus:

    ![Wählen Sie die Dauer und primäre](../../media/Always-On-Vpn/05.png)

    a. Für **Dauer auswählen**, wählen Sie entweder 1 oder 2 Jahre. Sie können bis zu zwei Zertifikate, um die Übergänge zu verwalten, wenn das Zertifikat abzulaufen droht hinzufügen. Sie können auswählen, welches das primäre Replikat (das eine während der Authentifizierung zum Signieren des Zertifikats für Verbindungen verwendete) ist.

    b. Für **primären**Option **Ja**.

    c. Wählen Sie **Erstellen** aus.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.3: Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md): In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Verbindungen. 
