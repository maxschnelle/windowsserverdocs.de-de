---
title: Konfigurieren der Richtlinie für bedingten Zugriff
description: Nachdem ein Stamm Zertifikat erstellt wurde, löst die "VPN-Konnektivität" die Erstellung der cloudanwendung "VPN-Server" im Mandanten des Kunden aus.
ms.topic: article
ms.date: 05/25/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 7535de9f11a8daf38ad1aab2fe95a620f9682025
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946703"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>Schritt 7.3: Konfigurieren der Richtlinie für bedingten Zugriff

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 7,2. Stamm Zertifikate für die VPN-Authentifizierung mit Azure AD erstellen](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**Weiter:** Schritt 7,4. Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff im lokalen AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Konnektivität. Wenn das erste Stamm Zertifikat auf dem Blatt "VPN-Konnektivität" erstellt wird, wird automatisch eine "VPN Server"-cloudanwendung im Mandanten erstellt.

Erstellen Sie eine Richtlinie für bedingten Zugriff, die der Gruppe "VPN-Benutzer" zugewiesen **ist, und legen Sie den**Bereich der **Cloud-App**

- **Benutzer**: VPN-Benutzer
- **Cloud-App**: VPN-Server
- **Grant (Zugriffs Steuerung)**: "Multi-Factor Authentication erforderlich". Andere Steuerelemente können bei Bedarf verwendet werden.

**Prozedur:** In diesem Schritt wird die Erstellung der grundlegendsten Richtlinie für den bedingten Zugriff behandelt.Wenn gewünscht, können zusätzliche Bedingungen und Steuerelemente verwendet werden.


1. Wählen Sie auf der Seite **bedingter Zugriff** auf der Symbolleiste am oberen Rand die Option **Hinzufügen**aus.

    ![Auswählen von „Hinzufügen“ auf der Seite „Bedingter Zugriff“](../../media/Always-On-Vpn/07.png)

2. Geben Sie auf der Seite **neu** im Feld **Name** einen Namen für die Richtlinie ein. Geben Sie z. b. **VPN-Richtlinie**ein.

    ![Hinzufügen des Namens für die Richtlinie auf der Seite „Bedingter Zugriff“](../../media/Always-On-Vpn/08.png)

3. Wählen Sie im Abschnitt **Zuweisung** die Option **Benutzer und Gruppen**aus.

    ![Auswählen von „Benutzer und Gruppen“](../../media/Always-On-Vpn/09.png)

4. Führen Sie auf der Seite **Benutzer und Gruppen** die folgenden Schritte aus:

    ![Auswählen eines Testbenutzers](../../media/Always-On-Vpn/10.png)

    a. Wählen Sie **Benutzer und Gruppen auswählen**aus.

    b. Wählen Sie **Auswählen**.

    c. Wählen Sie auf der Seite **auswählen** die Gruppe **VPN-Benutzer** aus, und wählen Sie dann **auswählen**aus.

    d. Wählen Sie auf der Seite **Benutzer und Gruppen** die Option **abgeschlossen**aus.

5. Führen Sie auf der Seite **Neu** die folgenden Schritte aus:

    ![Auswählen der Cloud-Apps](../../media/Always-On-Vpn/11.png)

    a. Wählen Sie im Abschnitt **Zuweisungen** die Option **Cloud-apps**aus.

    b. Wählen Sie auf der Seite **Cloud-apps** die Option **apps auswählen**aus.

    d. Wählen Sie **VPN-Server** aus.

6.  Wählen Sie auf der Seite **neu** im Abschnitt Steuer **Elemente** die **Option erteilen aus**, um die Seite **erteilen** zu öffnen.

    ![Auswählen von „Gewährung“](../../media/Always-On-Vpn/13.png)

7.  Führen Sie auf der Seite **Gewährung** die folgenden Schritte aus:

    ![Auswählen von „Erfordern von Multi-Factor Authentication“](../../media/Always-On-Vpn/14.png)

    a. Wählen Sie **Mehrstufige Authentifizierung erforderlich** aus.

    b. Wählen Sie **Auswählen**.

8.  Wählen Sie auf der Seite **neu** unter **Richtlinie aktivieren**die Option **ein aus.**

    ![Richtlinie aktivieren](../../media/Always-On-Vpn/15.png)

9.  Wählen Sie auf der Seite **neu** die Option **Erstellen**aus.


## <a name="next-steps"></a>Nächste Schritte
[Schritt 7,4. ](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff im lokalen AD: in diesem Schritt stellen Sie das Stamm Zertifikat für den bedingten Zugriff als vertrauenswürdiges Stamm Zertifikat für die VPN-Authentifizierung in Ihrem lokalen AD bereit.
