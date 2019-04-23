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
ms.openlocfilehash: 8c00855c50de79efa1b48c7b8762e1b679db4a87
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870281"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**Vorherige:** Schritt 7.2. Stammzertifikate für die VPN-Authentifizierung mit Azure AD zu erstellen.](vpn-create-root-cert-for-vpn-auth-azure-ad.md)<br>
&#187; [ **Next:** Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Verbindungen. Wenn das erste Stammzertifikat auf dem Blatt "VPN-Konnektivität" erstellt wird, erstellt es automatisch eine Cloudanwendung "VPN-Server" im Mandanten an. 

Erstellen Sie eine Richtlinie für bedingten Zugriff, die Gruppe "Benutzer"-VPN-Bereich zugewiesen und ist, die **Cloud-app** zu **VPN-Server**: 

- **Benutzer**: VPN-Benutzer
- **Cloud-App**: VPN-Server
- **Grant (Access Control)**: "Erfordern Sie Multi-Factor Authentication". Falls gewünscht, können andere Steuerelemente verwendet werden.

**Vorgehensweise:** Dieser Schritt behandelt die Erstellung von den grundlegendsten Richtlinie für bedingten Zugriff.  Falls gewünscht, können zusätzliche Bedingungen und Steuerelemente verwendet werden.


1. Auf der **für den bedingten Zugriff** Seite, auf der Symbolleiste am oberen Rand, klicken Sie auf **hinzufügen**.

    ![Wählen Sie auf der Seite für bedingten Zugriff hinzufügen](../../media/Always-On-Vpn/07.png)

2. Auf der **neu** auf der Seite die **Namen** geben einen Namen für Ihre Richtlinie. Geben Sie z. B. **VPN-Richtlinie**.

    ![Hinzufügen von Namen für die Richtlinie für bedingten Zugriff auf](../../media/Always-On-Vpn/08.png)

3. In der **Zuweisung** auf **Benutzer und Gruppen**.

    ![Benutzer und Gruppen auswählen](../../media/Always-On-Vpn/09.png)

4. Auf der **Benutzer und Gruppen** führen die folgenden Schritte aus:

    ![Auswählen eines Testbenutzers](../../media/Always-On-Vpn/10.png)

    a. Klicken Sie auf **Benutzer und Gruppen auswählen**.

    b. Klicken Sie auf **Auswählen**.

    c. Auf der **wählen** Seite die **VPN-Benutzer** gruppieren, und klicken Sie dann auf **wählen**.

    d. Auf der **Benutzer und Gruppen** auf **Fertig**.

5. Auf der **neu** führen die folgenden Schritte aus:

    ![Cloud-apps auswählen](../../media/Always-On-Vpn/11.png)

    a. In der **Zuweisungen** auf **Cloud-apps**.

    b. Auf der **Cloud-apps** auf **wählen Sie die apps**.

    d. Wählen Sie **VPN-Server**.

13. Auf der **neu** Seite zu öffnen der **Grant** auf der Seite die **Steuerelemente** auf **Grant**.

    ![SELECT-Berechtigung](../../media/Always-On-Vpn/13.png)

14. Auf der **Grant** führen die folgenden Schritte aus:

    ![Wählen Sie die mehrstufige Authentifizierung anfordern](../../media/Always-On-Vpn/14.png)

    a. Wählen Sie **erfordern Multi-Factor Authentication**.

    b. Klicken Sie auf **Auswählen**.

15. Auf der **neu** Seite **Richtlinie aktivieren**, klicken Sie auf **auf**.

    ![Richtlinie aktivieren](../../media/Always-On-Vpn/15.png)

16. Auf der **neu** auf **erstellen**.


## <a name="next-step"></a>Nächster Schritt
[Dies ist Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md): In diesem Schritt, Sie stellen das Stammzertifikat für den bedingten Zugriff als vertrauenswürdiges Stammzertifikat für die VPN-Authentifizierung auf Ihrem lokalen AD.

---