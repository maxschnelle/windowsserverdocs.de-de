---
title: Konfigurieren der Richtlinie für bedingten Zugriff
description: Nachdem ein Stammzertifikat erstellt wurde, löst "VPN-Konnektivität die Erstellung der Cloudanwendung"VPN-Server"im Mandanten des Kunden.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067295"
---
# Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 7.2. Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)<br>
& #187; [ **Weiter:** Schritt 7.4. Bereitstellen von Stammzertifikate bedingten Zugriff auf lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

In diesem Schritt konfigurieren Sie die bedingten Zugriffsrichtlinien für VPN-Konnektivität. Wenn das erste Stammzertifikat im Blatt "VPN-Konnektivität" erstellt wird, wird automatisch eine Cloudanwendung "VPN-Server" im Mandanten erstellt. 

Erstellen Sie eine Conditional Access-Richtlinie, die VPN-Benutzergruppe und Umfang der **Cloud-app** mit **VPN-Server**zugewiesen ist: 

- **Benutzer**: VPN-Benutzer
- **Cloud-App**: VPN-Server
- **GRANT (Access Control)**: "Multi-Factor Authentication erforderlich". Andere Steuerelemente können verwendet werden, wenn gewünscht.

**Verfahren:** Dieser Schritt erläutert Erstellung der einfachste bedingten Zugriff Richtlinie.Falls gewünscht, können zusätzliche Bedingungen und Steuerelemente verwendet werden.


1. Klicken Sie auf der Seite **Bedingten Zugriff** in der Symbolleiste auf die oben auf **Hinzufügen**.

    ![Wählen Sie hinzufügen auf der Seite bedingten Zugriff](../../media/Always-On-Vpn/07.png)

2. Geben Sie auf der Seite " **neu** " in das Feld **Name** einen Namen für Ihre Richtlinie aus. Geben Sie z. B. ein **VPN-Richtlinie**.

    ![Namen für die Richtlinie auf bedingten Zugriff Seite hinzufügen](../../media/Always-On-Vpn/08.png)

3. Klicken Sie im Abschnitt **Zuordnung** auf **Benutzer und Gruppen**.

    ![Benutzer und Gruppen auswählen](../../media/Always-On-Vpn/09.png)

4. Führen Sie auf der Seite der **Benutzer und Gruppen** die folgenden Schritte aus:

    ![Wählen Sie Test-Benutzer](../../media/Always-On-Vpn/10.png)

    a. Klicken Sie auf **Benutzer und Gruppen auswählen**.

    b. Klicken Sie auf **auswählen**.

    c. Wählen Sie auf der Seite " **Wählen Sie** " die **VPN-Benutzer** aus, und klicken Sie auf **auswählen**.

    d. Klicken Sie auf der Seite der **Benutzer und Gruppen** auf **Fertig**.

5. Führen Sie auf der Seite " **neu** " die folgenden Schritte aus:

    ![Auswahl der Cloud-apps](../../media/Always-On-Vpn/11.png)

    a. Klicken Sie im Abschnitt **Aufgaben** auf **Cloud-apps**.

    b. Klicken Sie auf der Seite **Cloud-apps** auf **apps auswählen**.

    d. Wählen Sie die **VPN-Server**.

13. Klicken Sie auf der Seite " **neu** " zum Öffnen der Seite " **Grant** " im Abschnitt **Steuerelemente** **gewähren**.

    ![Wählen Sie gewähren](../../media/Always-On-Vpn/13.png)

14. Führen Sie auf der Seite " **Grant** " die folgenden Schritte aus:

    ![Wählen Sie eine mehrstufige Authentifizierung erforderlich](../../media/Always-On-Vpn/14.png)

    a. Wählen Sie **eine mehrstufige Authentifizierung erforderlich**.

    b. Klicken Sie auf **auswählen**.

15. Klicken Sie auf der Seite " **neu** " unter **Richtlinie aktivieren**, **auf**.

    ![Aktivieren Sie Richtlinie](../../media/Always-On-Vpn/15.png)

16. Klicken Sie auf der Seite **neu** **Erstellen**.


## Nächster Schritt
[Schritt 7.4. Bereitstellen von Stammzertifikate bedingten Zugriff auf lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md): Sie stellen In diesem Schritt das Stammzertifikat für bedingten Zugriff als vertrauenswürdiges Stammzertifikat für VPN-Authentifizierung zu Ihrer lokalen AD.

---