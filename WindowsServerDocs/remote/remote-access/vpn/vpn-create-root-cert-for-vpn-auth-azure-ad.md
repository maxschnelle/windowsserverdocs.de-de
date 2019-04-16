---
title: Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD
description: Azure AD verwendet das VPN-Zertifikat zum Signieren von Zertifikaten für Windows 10-Clients bei der Authentifizierung mit Azure AD für VPN-Konnektivität. Das Zertifikat als primären markiert ist den Aussteller an, die Azure AD verwendet.
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
ms.openlocfilehash: 14ef17ab403cc4e7c9891f4ede48e41c25e8522d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067292"
---
# Schritt 7.2. Erstellen Sie bedingten Zugriff Stammzertifikate für VPN-Authentifizierung mit Azure AD

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 7.1. Konfigurieren von EAP-TLS (Certificate Revocation List, CRL) überprüft ignorieren](vpn-config-eap-tls-to-ignore-crl-checking.md)<br>
& #187; [ **Weiter:** Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)

In diesem Schritt konfigurieren Sie Stammzertifikate bedingten Zugriff für VPN-Authentifizierung mit Azure AD, das automatisch eine Cloud-app namens "VPN-Server" in den Mandanten erstellt. Um bedingten Zugriff für VPN-Konnektivität zu konfigurieren, müssen Sie:

1. Erstellen Sie eine VPN-Zertifikat im Azure-Portal (Sie können mehr als ein Zertifikat erstellen).
2. Das VPN-Zertifikat herunterladen.
2. Stellen Sie das Zertifikat für Ihren VPN und NPS-Servern bereit.

Wenn ein Benutzer eine VPN-Verbindung versucht, führt der VPN-Client einen Aufruf in der Web Account Manager (WAM) auf dem Windows 10-Client. WAM führt einen Aufruf an die VPN-Server Cloud-app. Wenn die Bedingungen und Steuerelemente in der bedingten Zugriff Richtlinie erfüllt sind, stellt Azure AD ein Token in Form von ein kurzlebiges (1 Stunde) aus, die WAM. Die WAM speichert das Zertifikat im Zertifikatspeicher des Benutzers und übergibt deaktivieren Sie die Steuerung an dem VPN-Client.  

Der VPN-Client sendet das Zertifikatsprobleme dann von Azure AD mit dem VPN für die Überprüfung der Anmeldeinformationen.Azure AD verwendet das Zertifikat, das markiert ist als**primäre**im VPN-Konnektivität Blatt als den Aussteller an. 

In Azure-Portal erstellen Sie zwei Zertifikate, um den Übergang zu verwalten, wann ein Zertifikat ist in Kürze ablaufen. Wenn Sie ein Zertifikat zu erstellen, wählen Sie, ob es sich um das primäre Zertifikat, die während der Authentifizierung verwendet wird handelt, um das Zertifikat für die Verbindung zu signieren.

**Verfahren:**

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) als globaler Administrator an.

2. Klicken Sie im linken Menü auf **Azure Active Directory**. 

    ![Wählen Sie Azure Active Directory](../../media/Always-On-Vpn/01.png)

3. Klicken Sie auf der Seite **Azure Active Directory** im Abschnitt **Verwalten** auf **bedingten Zugriff**.

    ![Wählen Sie bedingten Zugriff](../../media/Always-On-Vpn/02.png)

4. Klicken Sie auf der Seite **Bedingter Zugriff** im Abschnitt **Verwalten** auf **VPN-Konnektivität (Vorschau)**.

    ![Wählen Sie die VPN-Konnektivität](../../media/Always-On-Vpn/03.png)

5. Klicken Sie auf der Seite " **VPN-Konnektivität** " **Neues Zertifikat**aus.

    ![Wählen Sie neues Zertifikat](../../media/Always-On-Vpn/04.png)

6. Führen Sie auf der Seite " **neu** " die folgenden Schritte aus:

    ![Wählen Sie Dauer und primären](../../media/Always-On-Vpn/05.png)

    a. **Wählen Sie eine Dauer**wählen Sie entweder 1 oder 2 Jahren. Sie können bis zu zwei Zertifikate, um Übergänge zu verwalten, wenn das Zertifikat ist in Kürze ablaufen hinzufügen. Sie können auswählen, welche die primäre (nur während der Authentifizierung verwendet werden, um das Zertifikat für die Konnektivität zu signieren) ist.

    b. Wählen Sie für die **primäre** **Ja**.

    c. Klicken Sie auf **Erstellen**.

## Nächster Schritt
Schritt [7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md): In diesem Schritt konfigurieren Sie die bedingten Zugriffsrichtlinien für VPN-Konnektivität. 

---