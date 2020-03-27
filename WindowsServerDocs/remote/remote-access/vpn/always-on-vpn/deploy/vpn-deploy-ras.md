---
title: Konfigurieren des RAS-Servers für Always On VPN
description: RRAS ist so konzipiert, dass Sie sowohl einen Router als auch einen Remote Zugriffs Server ausführen können. Daher unterstützt es eine Vielzahl von Features.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: lizross
author: eross-msft
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 9d3afb21c466ef1010a20ec811df45b9dcb2b711
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312255"
---
# <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>Schritt 3: Konfigurieren des RAS-Servers für Always On VPN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 2: Konfigurieren der Server Infrastruktur](vpn-deploy-server-infrastructure.md)
- [**Vorheriges:** Schritt 4: Installieren und Konfigurieren des Netzwerk Richtlinien Servers (NPS)](vpn-deploy-nps.md)

RRAS ist so konzipiert, dass Sie sowohl einen Router als auch einen RAS-Server ausführen, da er eine Vielzahl von Features unterstützt. Für diese Bereitstellung benötigen Sie nur eine kleine Teilmenge dieser Features: Unterstützung für IKEv2-VPN-Verbindungen und LAN-Routing.

IKEv2 ist ein VPN-Tunnelingprotokoll, das in Internet Engineering Task Force Request for Comments 7296 beschrieben wird. Der Hauptvorteil von IKEv2 besteht darin, dass Unterbrechungen in der zugrunde liegenden Netzwerkverbindung toleriert werden. Wenn beispielsweise die Verbindung vorübergehend unterbrochen wird oder ein Benutzer einen Client Computer von einem Netzwerk auf einen anderen verschiebt, stellt IKEv2 die VPN-Verbindung automatisch wieder her, wenn die Netzwerkverbindung wieder hergestellt wird – ohne Benutzereingriff.

Konfigurieren Sie den RRAS-Server für die Unterstützung von IKEv2-Verbindungen, während nicht verwendete Protokolle deaktiviert werden, wodurch die Sicherheitsanforderungen des Servers reduziert werden. Außerdem konfigurieren Sie den Server für die Zuweisung von Adressen zu VPN-Clients aus einem statischen Adresspool. Sie können Adressen entweder aus einem Pool oder einem DHCP-Server zuweisen. die Verwendung eines DHCP-Servers erhöht jedoch die Komplexität des Entwurfs und bietet nur minimale Vorteile.

>[!IMPORTANT]
>Folgendes ist wichtig:
>- Installieren Sie zwei Ethernet-Netzwerkadapter auf dem physischen Server. Wenn Sie den VPN-Server auf einem virtuellen Computer installieren, müssen Sie zwei externe virtuelle Switches erstellen, eine für jeden physischen Netzwerkadapter. Erstellen Sie dann zwei virtuelle Netzwerkadapter für die VM, wobei jeder Netzwerkadapter mit einem virtuellen Switch verbunden ist.
>
>- Installieren Sie den Server in Ihrem Umkreis Netzwerk zwischen Ihren Edge-und internen Firewalls, mit einem Netzwerkadapter, der mit dem externen Umkreis Netzwerk verbunden ist, und einem Netzwerkadapter, der mit dem internen Umkreis Netzwerk verbunden ist.

>[!WARNING]
>Bevor Sie beginnen, stellen Sie sicher, dass Sie IPv6 auf dem VPN-Server aktivieren. Andernfalls kann keine Verbindung hergestellt werden, und es wird eine Fehlermeldung angezeigt.

## <a name="install-remote-access-as-a-ras-gateway-vpn-server"></a>Installieren des Remote Zugriffs als RAS-Gateway-VPN-Server

In diesem Verfahren installieren Sie die Remote Zugriffs Rolle als einzelner Mandanten-RAS-Gateway-VPN-Server. Weitere Informationen finden Sie unter [Remote Access](../../../Remote-Access.md).

### <a name="install-the-remote-access-role-by-using-windows-powershell"></a>Installieren der Remote Zugriffs Rolle mithilfe von Windows PowerShell

1. Öffnen Sie Windows PowerShell als **Administrator**.

2. Geben Sie folgendes Cmdlet ein, und führen Sie es aus:

   ```powershell
   Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools
   ```

   Nachdem die Installation abgeschlossen ist, wird die folgende Meldung in Windows PowerShell angezeigt.

   ```powershell
   | Success | Restart Needed | Exit Code |               Feature Result               |
   |---------|----------------|-----------|--------------------------------------------|
   |  True   |       No       |  Success  | {RAS Connection Manager Administration Kit |
   ```

### <a name="install-the-remote-access-role-by-using-server-manager"></a>Installieren Sie die Remote Zugriffs Rolle mit Server-Manager

Mithilfe des folgenden Verfahrens können Sie die Remote Zugriffs Rolle mithilfe von Server-Manager installieren.

1. Wählen Sie auf dem VPN-Server in Server-Manager die Option **Verwalten** aus, und wählen Sie **Rollen und Features hinzufügen**aus.
   
   Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2. Wählen Sie auf der Seite Vorbereitung die Option **weiter**aus.

3. Wählen Sie auf der Seite Installationstyp auswählen die Option **rollenbasierte oder featurebasierte Installation** aus, und klicken Sie auf **weiter**.

4. Wählen Sie auf der Seite Zielserver auswählen die Option **einen Server aus dem Server Pool auswählen aus** .

5. Wählen Sie unter Server Pool den lokalen Computer aus, und klicken Sie auf **weiter**.

6. Wählen Sie auf der Seite Server Rollen auswählen unter **Rollen**die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter**.

7. Wählen Sie auf der Seite Features auswählen die Option **weiter**aus.

8. Wählen Sie auf der Seite Remote Zugriff die Option **weiter**aus.

9.  Wählen Sie auf der Seite Rollen Dienst auswählen unter **Rollen Dienste**die Option **DirectAccess und VPN (RAS)** aus.

   Das Dialogfeld **Assistent zum Hinzufügen von Rollen und Features** wird geöffnet.

11. Klicken Sie im Dialogfeld Rollen und Features hinzufügen auf **Features hinzufügen** , und klicken Sie dann auf **weiter**.

12. Wählen Sie auf der Seite Webserver Rolle (IIS) die Option **weiter**aus.

13. Wählen Sie auf der Seite Rollen Dienste auswählen die Option **weiter**aus.

14. Überprüfen Sie auf der Seite Installations Auswahl bestätigen Ihre Auswahl, und wählen Sie dann **Installieren**aus.

15. Wenn die Installation abgeschlossen ist, wählen Sie **Schließen**aus.

## <a name="configure-remote-access-as-a-vpn-server"></a>Konfigurieren des Remote Zugriffs als VPN-Server

In diesem Abschnitt können Sie das RAS-VPN so konfigurieren, dass es IKEv2-VPN-Verbindungen zulässt, Verbindungen von anderen VPN-Protokollen ablehnen und einen statischen IP-Adresspool für die Ausstellung von IP-Adressen für die Verbindung mit autorisierten VPN-Clients zuweisen.

1. Wählen Sie auf dem VPN-Server in Server-Manager das **Benachrichtigungs** Kennzeichen aus.

2. Wählen Sie im Menü **Aufgaben** **die Option Assistenten für die** ersten Schritte öffnen aus.

   Der Assistent zum Konfigurieren des Remote Zugriffs wird geöffnet.

   >[!NOTE]
   >Der Assistent zum Konfigurieren des Remote Zugriffs kann hinter Server-Manager geöffnet werden. Wenn Sie der Ansicht sind, dass es zu lange dauert, bis der Assistent geöffnet ist, verschieben oder minimieren Sie Server-Manager, um herauszufinden, ob der Assistent dahinter liegt. Falls nicht, warten Sie, bis der Assistent initialisiert wurde.

3. Wählen Sie **nur VPN**bereitstellen aus.

    Der Routing-und RAS-Microsoft Management Console (MMC) wird geöffnet.

4. Klicken Sie mit der rechten Maustaste auf den VPN-Server, und wählen Sie dann **Konfigurieren und Remote Zugriff aktivieren**aus.

   Der Setup-Assistent für den Routing-und RAS-Server wird geöffnet.

5. Wählen Sie in der Willkommensseite des Setup-Assistenten für den Routing-und RAS-Server die Option **weiter**aus.

6. Wählen Sie unter **Konfiguration**die Option **benutzerdefinierte Konfiguration**aus, und klicken Sie dann auf **weiter**.

7. Wählen Sie unter **benutzerdefinierte Konfiguration**die Option **VPN-Zugriff**, und klicken Sie dann auf **weiter**.

   Der Assistent zum Abschließen des Routing-und RAS-Servers wird geöffnet.

8. Wählen Sie **Fertig** stellen aus, um den Assistenten zu schließen, und klicken Sie dann auf **OK** , um das Dialogfeld Routing und RAS zu schließen

9. Wählen Sie **Dienst starten** , um den Remote Zugriff zu starten.

10. Klicken Sie in der Remote Zugriffs-MMC mit der rechten Maustaste auf den VPN-Server, und wählen Sie **Eigenschaften**aus.

11. Wählen Sie unter "Eigenschaften" die Registerkarte " **Sicherheit** " aus, und

    a. Wählen Sie **Authentifizierungs Anbieter** und dann **RADIUS-Authentifizierung**aus.

    b. Wählen Sie **Konfigurieren**aus.

       Das Dialogfeld RADIUS-Authentifizierung wird geöffnet.

    c. Wählen Sie **Hinzufügen**.

       Das Dialogfeld RADIUS-Server hinzufügen wird geöffnet.

    d. Geben Sie unter **Server Name**den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) des NPS-Servers in Ihrer Organisation/Ihrem Unternehmensnetzwerk ein.
    
       Wenn der NetBIOS-Name des NPS-Servers beispielsweise NPS1 lautet und Ihr Domänen Name Corp.contoso.com lautet, geben Sie **NPS1.Corp.contoso.com**ein.

    e. Wählen Sie unter **gemeinsamer geheimer**Schlüssel die Option **ändern**aus.

       Das Dialogfeld Geheimnis ändern wird geöffnet.

    f. Geben Sie unter **neues Geheimnis**eine Text Zeichenfolge ein.

    g. Geben Sie in **neues Geheimnis bestätigen**die gleiche Text Zeichenfolge ein, und klicken Sie dann auf **OK**.

    >[!IMPORTANT]
    >Speichern Sie diese Text Zeichenfolge. Wenn Sie den NPS-Server in Ihrer Organisation/Ihrem Unternehmensnetzwerk konfigurieren, fügen Sie diesen VPN-Server als RADIUS-Client hinzu. Während dieser Konfiguration verwenden Sie den gleichen gemeinsamen geheimen Schlüssel, damit die NPS-und VPN-Server kommunizieren können.

12. Überprüfen **Sie in RADIUS-Server hinzufügen**die Standardeinstellungen für:

    - **Timeout**

    - **Anfängliche Bewertung**

    - **Port**

13. Ändern Sie ggf. die Werte entsprechend den Anforderungen für Ihre Umgebung, und wählen Sie **OK**aus.

    Ein NAS ist ein Gerät, das ein gewisses Maß an Zugriff auf ein größeres Netzwerk bietet. Ein NAS, das eine RADIUS-Infrastruktur verwendet, ist auch ein RADIUS-Client, der Verbindungsanforderungen und Buchhaltungs Nachrichten an einen RADIUS-Server zur Authentifizierung, Autorisierung und Kontoführung sendet.

14. Überprüfen Sie die Einstellung für den **Kontoführungs Anbieter**:

    |                    Wenn Sie möchten...                     |                                                     Dann ...                                                      |
    |-----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
    | Remote Zugriffs Aktivität auf dem RAS-Server protokolliert |                               Stellen Sie sicher, dass Windows-Konto **Führung** ausgewählt ist.                               |
    |        NPS zum Durchführen von Buchhaltungs Diensten für VPN         | Ändern Sie den Konto **Buchhaltungs Anbieter** in die RADIUS-Konto **Führung** , und konfigurieren Sie dann den NPS als Buchhaltungs Anbieter. |

15. Wählen Sie die Registerkarte **IPv4** aus.

    a. Wählen Sie **statischer Adresspool**aus.

    b. Wählen Sie **Hinzufügen** , um einen IP-Adresspool zu konfigurieren.

       Der statische Adresspool sollte Adressen aus dem internen Umkreis Netzwerk enthalten. Diese Adressen sind über die interne Netzwerkverbindung auf dem VPN-Server, nicht über das Unternehmensnetzwerk.

    c. Geben Sie in **Start-IP-Adresse**die IP-Startadresse in dem Bereich ein, der den VPN-Clients zugewiesen werden soll.

    d. Geben Sie unter **End-IP-Adresse**die IP-Endadresse in dem Bereich ein, der den VPN-Clients zugewiesen werden soll, oder geben Sie **die Nummer der Adresse ein, die**Sie zur Verfügung stellen möchten. Wenn Sie DHCP für dieses Subnetz verwenden, stellen Sie sicher, dass Sie einen entsprechenden Adress Ausschluss auf Ihren DHCP-Servern konfigurieren.

    e. Optionale Wenn Sie DHCP verwenden, wählen Sie **Adapter**aus, und wählen Sie in der Ergebnisliste den Ethernet-Adapter aus, der mit Ihrem internen Umkreis Netzwerk verbunden ist.

16. Optionale *Wenn Sie den bedingten Zugriff für VPN-Konnektivität konfigurieren*, wählen Sie in der Dropdown Liste **Zertifikat** unter **SSL-Zertifikat Bindung**die VPN-Server Authentifizierung aus.

17. Optionale *Wenn Sie den bedingten Zugriff für VPN-Konnektivität konfigurieren*, erweitern Sie in der NPS-MMC **Richtlinien\\Netzwerk Richtlinien** , und gehen Sie wie folgt vor: 

    a. Rechts: die **Verbindungen mit der Netzwerk Richtlinie für den Routing-und RAS-Server von Microsoft** und wählen **Eigenschaften**aus.

    b. Wählen Sie den **Zugriff gewähren aus. Gewähren Sie Zugriff, wenn die Verbindungsanforderung mit dieser Richtlinien Option übereinstimmt** .

    c. Wählen Sie unter Typ des Netzwerk Zugriffs Servers in der Dropdown-Datei den Eintrag RAS- **Server (VPN-Dial-up)** aus.

18. Klicken Sie in der MMC für Routing und RAS mit der rechten Maustaste auf **Ports,** und wählen Sie dann **Eigenschaften**aus. 
    
    Das Dialogfeld Eigenschaften von Ports wird geöffnet.

19. Wählen Sie **WAN Miniport (SSTP)** aus, und wählen Sie **Konfigurieren**aus. Das Dialogfeld Device-WAN-Miniport konfigurieren (SSTP) wird geöffnet.

    a. Deaktivieren Sie die Kontrollkästchen RAS- **Verbindungen (nur eingehend)** und **Routing Verbindungen nach Bedarf (eingehend und ausgehend)** .

    b. Wählen Sie **OK**.

20. Wählen Sie **WAN Miniport (L2TP)** , und wählen Sie **Konfigurieren**aus. Das Dialogfeld Device-WAN-Miniport konfigurieren (L2TP) wird geöffnet.

    a. Geben Sie unter Maximale Anzahl von **Ports**die Anzahl der Ports ein, die der maximalen Anzahl gleichzeitiger VPN-Verbindungen entsprechen soll, die Sie unterstützen möchten.

    b. Wählen Sie **OK**.

21. Wählen Sie **WAN Miniport (PPTP)** aus, und wählen Sie **Konfigurieren**aus. Das Dialogfeld Device-WAN-Miniport konfigurieren (PPTP) wird geöffnet.

    a. Geben Sie unter Maximale Anzahl von **Ports**die Anzahl der Ports ein, die der maximalen Anzahl gleichzeitiger VPN-Verbindungen entsprechen soll, die Sie unterstützen möchten.

    b. Wählen Sie **OK**.

22. Wählen Sie **WAN Miniport (IKEv2)** , und wählen Sie **Konfigurieren**aus. Das Dialogfeld Device-WAN-Miniport konfigurieren (IKEv2) wird geöffnet.

     a. Geben Sie unter Maximale Anzahl von **Ports**die Anzahl der Ports ein, die der maximalen Anzahl gleichzeitiger VPN-Verbindungen entsprechen soll, die Sie unterstützen möchten.

     b. Wählen Sie **OK**.

23. Wenn Sie dazu aufgefordert werden, wählen Sie **Ja** aus, um den Server neu zu starten, und wählen Sie **Schließen** aus, um den Server

## <a name="next-step"></a>Nächster Schritt

[Schritt 4: Installieren und Konfigurieren des Netzwerk Richtlinien Servers (NPS)](vpn-deploy-nps.md): in diesem Schritt installieren Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe von Windows PowerShell oder des Server-Manager Assistenten zum Hinzufügen von Rollen und Features. Außerdem können Sie NPS so konfigurieren, dass alle Authentifizierungs-, Autorisierungs-und Buchhaltungsaufgaben für Verbindungsanforderungen verarbeitet werden, die vom VPN-Server empfangen werden.
