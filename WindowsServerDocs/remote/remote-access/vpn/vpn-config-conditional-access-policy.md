---
title: Konfigurieren der Richtlinie für bedingten Zugriff
description: Nachdem Sie ein Stammzertifikat erstellt wurde, löst die "VPN-Konnektivität" die Erstellung der "VPN-Server"-Cloud-Anwendung im Mandanten des Kunden.
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
ms.openlocfilehash: 466e76d01ca99a1e1ed72fa955ccd287ae63c5df
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749498"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 7.2. Erstellen von Stammzertifikaten für die VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**nächster:** Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Verbindungen. Wenn das erste Stammzertifikat auf dem Blatt "VPN-Konnektivität" erstellt wird, erstellt es automatisch eine Cloudanwendung "VPN-Server" im Mandanten an.

Erstellen Sie eine Richtlinie für bedingten Zugriff, die Gruppe "Benutzer"-VPN-Bereich zugewiesen und ist, die **Cloud-app** zu **VPN-Server**:

- **Benutzer**: VPN-Benutzer
- **Cloud-App**: VPN-Server
- **Grant (Access Control)** : "Erfordern Sie Multi-Factor Authentication". Falls gewünscht, können andere Steuerelemente verwendet werden.

**Vorgehensweise:** Dieser Schritt behandelt die Erstellung von den grundlegendsten Richtlinie für bedingten Zugriff.  Falls gewünscht, können zusätzliche Bedingungen und Steuerelemente verwendet werden.


1. Auf der **für den bedingten Zugriff** Seite, auf der Symbolleiste am oberen Rand **hinzufügen**.

    ![Wählen Sie auf der Seite für bedingten Zugriff hinzufügen](../../media/Always-On-Vpn/07.png)

2. Auf der **neu** auf der Seite die **Namen** Geben Sie einen Namen für Ihre Richtlinie. Geben Sie z. B. **VPN-Richtlinie**.

    ![Hinzufügen von Namen für die Richtlinie für bedingten Zugriff auf](../../media/Always-On-Vpn/08.png)

3. In der **Zuweisung** wählen Sie im Abschnitt **Benutzer und Gruppen**.

    ![Benutzer und Gruppen auswählen](../../media/Always-On-Vpn/09.png)

4. Auf der **Benutzer und Gruppen** führen die folgenden Schritte aus:

    ![Auswählen eines Testbenutzers](../../media/Always-On-Vpn/10.png)

    a. Wählen Sie **Benutzer und Gruppen auswählen**.

    b. Wählen Sie **wählen**.

    c. Auf der **wählen** Seite die **VPN-Benutzer** Gruppe, und wählen Sie dann **wählen**.

    d. Auf der **Benutzer und Gruppen** Seite **Fertig**.

5. Auf der **neu** führen die folgenden Schritte aus:

    ![Cloud-apps auswählen](../../media/Always-On-Vpn/11.png)

    a. In der **Zuweisungen** wählen Sie im Abschnitt **Cloud-apps**.

    b. Auf der **Cloud-apps** Seite **wählen Sie die apps**.

    d. Wählen Sie **VPN-Server**.

6.  Auf der **neu** Seite zu öffnen der **Grant** auf der Seite die **Steuerelemente** wählen Sie im Abschnitt **Grant**.

    ![SELECT-Berechtigung](../../media/Always-On-Vpn/13.png)

7.  Auf der **Grant** führen die folgenden Schritte aus:

    ![Wählen Sie die mehrstufige Authentifizierung anfordern](../../media/Always-On-Vpn/14.png)

    a. Wählen Sie **erfordern Multi-Factor Authentication**.

    b. Wählen Sie **wählen**.

8.  Auf der **neu** Seite **Richtlinie aktivieren**Option **auf**.

    ![Richtlinie aktivieren](../../media/Always-On-Vpn/15.png)

9.  Auf der **neu** Seite **erstellen**.


## <a name="next-steps"></a>Nächste Schritte
[Schritt 7.4: Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md): In diesem Schritt, Sie stellen das Stammzertifikat für den bedingten Zugriff als vertrauenswürdiges Stammzertifikat für die VPN-Authentifizierung auf Ihrem lokalen AD.
