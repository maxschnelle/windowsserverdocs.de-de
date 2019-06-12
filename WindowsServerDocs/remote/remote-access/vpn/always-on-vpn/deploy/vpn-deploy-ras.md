---
title: Konfigurieren des RAS-Servers für Always On VPN
description: RRAS dient auch als Router und RAS-Server ausführen. aus diesem Grund unterstützt ein breites Spektrum an Funktionen.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 3920f7f075f4742a62577ade809cc0494b05bf1f
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749437"
---
# <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>Schritt 3 Konfigurieren des RAS-Servers für Always On VPN

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 2 Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md)
- [**Vorherige:** Schritt 4 Installieren Sie und konfigurieren Sie (Network Policy Server, NPS)](vpn-deploy-nps.md)

RRAS dient auch als Router und RAS-Server ausführen, da es sich um ein breites Spektrum an Funktionen unterstützt. Für die Zwecke dieser Bereitstellung können Sie nur eine kleine Teilmenge dieser Funktionen benötigen: Unterstützung für IKEv2-VPN-Verbindungen und LAN-routing.

IKEv2 befindet es sich um ein VPN-Tunneling-Protokoll in die Internet Engineering Task Force-Anforderung für Kommentare 7296 beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es sich um Unterbrechungen in die zugrunde liegende Netzwerkverbindung toleriert. Z. B. wenn die Verbindung vorübergehend unterbrochen wird, oder wenn ein Benutzer einen Clientcomputer aus einem Netzwerk zu einem anderen bewegt, IKEv2 automatisch wiederherstellt, die VPN-Verbindung, wenn die Verbindung wiederhergestellt ist – alles ohne Eingreifen des Benutzers.

Konfigurieren von RRAS-Servers zur Unterstützung von IKEv2-Verbindungen beim Deaktivieren nicht verwendeter Protokolle, die Sicherheitsbedarf des Servers reduziert. Außerdem konfigurieren Sie den Server, um Adressen zu VPN-Clients von einem statischen Adresspool zugewiesen. Sie können berechtigterweise Adressen aus einem Pool oder einem DHCP-Server zuweisen. Allerdings wird mit einem DHCP-Server erhöht die Komplexität des Entwurfs und bietet minimale Vorteile.

>[!IMPORTANT]
>Es ist wichtig:
>- Installieren Sie zwei Ethernet-Netzwerkadapter auf dem physischen Server an. Wenn Sie den VPN-Server auf einem virtuellen Computer installieren, müssen Sie zwei externen virtuellen Switches, einen für jeden physischen Netzwerkadapter erstellen; und erstellen Sie zwei virtuelle Netzwerkadapter für den virtuellen Computer mit einzelnen Netzwerkadapter mit einem virtuellen Switch verbunden.
>
>- Installieren Sie den Server im Umkreisnetzwerk zwischen dem Rand und die internen Firewalls mit ein Netzwerkadapter mit dem externen Netzwerk des Umkreisnetzwerks und ein Netzwerkadapter mit dem internen Umkreisnetzwerk.

>[!WARNING]
>Bevor Sie beginnen, stellen Sie sicher, dass IPv6 auf dem VPN-Server zu aktivieren. Andernfalls kann eine Verbindung kann nicht hergestellt werden, und eine Fehlermeldung angezeigt wird.

## <a name="install-remote-access-as-a-ras-gateway-vpn-server"></a>Installieren Sie den Remotezugriff als RAS-Gateway-VPN-Server

In diesem Verfahren installieren Sie die Rolle "Remotezugriff" als einzelner Mandant RAS-VPN-Gateway-Server an. Weitere Informationen finden Sie unter [Remote Access](../../../Remote-Access.md).

### <a name="install-the-remote-access-role-by-using-windows-powershell"></a>Installieren Sie die Rolle "Remotezugriff" mithilfe von Windows PowerShell

1. Öffnen Sie Windows PowerShell als **Administrator**.

2. Geben Sie an, und führen Sie das folgende Cmdlet aus:

   ```powershell
   Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools
   ```

   Nach Abschluss der Installation wird die folgende Meldung angezeigt, in Windows PowerShell.

   ```powershell
   | Success | Restart Needed | Exit Code |               Feature Result               |
   |---------|----------------|-----------|--------------------------------------------|
   |  True   |       No       |  Success  | {RAS Connection Manager Administration Kit |
   ```

### <a name="install-the-remote-access-role-by-using-server-manager"></a>Installieren Sie die Rolle "Remotezugriff" mithilfe von Server-Manager

Sie können das folgende Verfahren verwenden, der Rolle "Remotezugriff" mit Server-Manager zu installieren.

1. Wählen Sie auf die VPN-Server im Server-Manager **verwalten** , und wählen Sie **Hinzufügen von Rollen und Features**.
   
   Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2. Auf der Seite zu beginnen, wählen Sie **Weiter**.

3. Wählen Sie auf der Seite Installationstyp auswählen die **rollenbasierte oder featurebasierte Installation** aus, und wählen Sie **Weiter**.

4. Wählen Sie auf der Seite Zielserver auswählen den Server der **wählen Sie einen Server aus dem Serverpool** Option.

5. Wählen Sie unter Server-Ressourcenpool, den lokalen Computer, und wählen Sie **Weiter**.

6. Wählen Sie im Server-Rollen auf der Seite **Rollen**Option **RAS**, klicken Sie dann **Weiter**.

7. Wählen Sie auf der Seite Funktionen auswählen **Weiter**.

8. Wählen Sie auf der Seite RAS **Weiter**.

9.  Auf der Seite Rolle auswählen in **Rollendienste**Option **DirectAccess und VPN (RAS)** .

   Die **Hinzufügen von Rollen und Features Assistenten** Dialogfeld wird geöffnet.

11. Wählen Sie im Dialogfeld Rollen und Features hinzufügen **Features hinzufügen** wählen Sie dann **Weiter**.

12. Wählen Sie auf der Seite "Webserverrolle (IIS)" **Weiter**.

13. Wählen Sie auf der Seite Dienste; Rollendienste auswählen% **Weiter**.

14. Klicken Sie auf der Seite Installationsauswahl bestätigen, überprüfen Sie Ihre Auswahl, und wählen Sie dann **installieren**.

15. Wenn die Installation abgeschlossen ist, wählen Sie **schließen**.

## <a name="configure-remote-access-as-a-vpn-server"></a>Konfigurieren des Remotezugriffs einen VPN-Server

In diesem Abschnitt können Sie Remote Access VPN für IKEv2-VPN-Verbindungen zulassen, verweigern Verbindungen von anderen VPN-Protokolle und zuweisen einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zum Herstellen einer Verbindung autorisierte VPN-Clients konfigurieren.

1. Wählen Sie auf die VPN-Server im Server-Manager die **Benachrichtigungen** Flag.

2. In der **Aufgaben** , wählen Sie im Menü **öffnen Sie den Assistenten für erste Schritte**

   Das Konfigurieren des Remotezugriffs-Assistent wird geöffnet.

   >[!NOTE]
   >Konfigurieren von RAS-Assistenten möglicherweise hinter den Server-Manager zu öffnen. Wenn Sie, dass der Assistent glauben geöffnet zu lange dauert, verschieben Sie oder minimieren Sie des Server Manager, um herauszufinden, ob der Assistent dahinter ist. Wenn dies nicht der Fall ist, warten Sie, um den Assistenten zu initialisieren.

3. Wählen Sie **Bereitstellen eines VPN nur**.

    Der Routing- und RAS Zugriff Microsoft Management Console (MMC) wird geöffnet.

4. Mit der rechten Maustaste in des VPN-Servers aus, und wählen Sie dann **konfigurieren und Aktivieren von Routing und Remotezugriff**.

   Der Routing- und RAS-Server-Setup-Assistent wird geöffnet.

5. Wählen Sie die Willkommensseite der Routing- und RAS-Server-Setup-Assistent, **Weiter**.

6. In **Konfiguration**Option **benutzerdefinierte Konfiguration**, und wählen Sie dann **Weiter**.

7. In **benutzerdefinierte Konfiguration**Option **VPN-Zugriff**, und wählen Sie dann **Weiter**.

   Das Abschließen der Routing- und RAS-Server-Setup-Assistent wird geöffnet.

8. Wählen Sie **Fertig stellen** um den Assistenten zu schließen, und wählen Sie dann **OK** um das Routing und RAS-Dialogfeld zu schließen.

9. Wählen Sie **Dienst starten** um Remotezugriff zu starten.

10. In der RAS-MMC, mit der Maustaste des VPN-Servers aus, und wählen Sie dann **Eigenschaften**.

11. Wählen Sie in Eigenschaften der **Sicherheit** Registerkarte, und führen:

    a. Wählen Sie **Authentifizierungsanbieter** , und wählen Sie **RADIUS-Authentifizierung**.

    b. Wählen Sie **konfigurieren**.

       Das Dialogfeld "RADIUS-Authentifizierung" wird geöffnet.

    c. Wählen Sie **hinzufügen**.

       Das Dialogfeld "RADIUS-Server hinzufügen" wird geöffnet.

    d. In **Servernamen**, geben Sie den vollständig qualifizierten Domänennamen (FQDN) des NPS-Servers in Ihrem Netzwerk der Organisation/Corporate (Unternehmen).
    
       Wenn der NetBIOS-Namen des NPS-Servers NPS1 ist, und Ihr Domänenname corp.contoso.com ist, geben Sie beispielsweise **NPS1.corp.contoso.com**.

    e. In **gemeinsamer geheimer Schlüssel**Option **Änderung**.

       Der Schlüssel ändern-Dialogfeld wird geöffnet.

    f. In **neuer geheimer**, eine Textzeichenfolge einzugeben.

    g. In **neuen geheimen Schlüssel bestätigen**, geben Sie die gleiche Textzeichenfolge ein, und wählen **OK**.

    >[!IMPORTANT]
    >Speichern Sie die Textzeichenfolge. Wenn Sie den NPS-Server in Ihrem Netzwerk der Organisation/Corporate (Unternehmen) konfigurieren, fügen Sie dieses VPN-Server als RADIUS-Client hinzu. Bei dieser Konfiguration verwenden Sie dieses gleiche gemeinsame Geheimnis, damit die NPS- und VPN-Server kommunizieren können.

12. In **RADIUS-Server hinzufügen**, überprüfen Sie die Standardeinstellungen für:

    - **Time-out**

    - **Anfängliche Bewertung**

    - **Port**

13. Ändern Sie die Werte entsprechend die Anforderungen für Ihre Umgebung und wählen Sie bei Bedarf **OK**.

    NAS ist ein Gerät, das Zugriff auf ein größeres Netzwerk bereitstellt. Eine RADIUS-Infrastruktur NAS ist auch ein RADIUS-Client, senden verbindungsanforderungen und Kontoführungsnachrichten an einen RADIUS-Server für die Authentifizierung, Autorisierung und ressourcenerfassung.

14. Überprüfen Sie die Einstellung für **Kontoanbieter**:

    |                    Wenn Sie möchten die...                     |                                                     Dann...                                                      |
    |-----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
    | Remote Access-Aktivität, die auf dem RAS-Server protokolliert |                               Stellen Sie sicher, dass **Windows Accounting** ausgewählt ist.                               |
    |        NPS auszuführenden Accounting-Dienste für VPN         | Änderung **Kontoanbieter** zu **RADIUS-Kontoführung** und konfigurieren Sie den NPS als Kontoführungsanbieter. |

15. Wählen Sie die **IPv4** Registerkarte und zu tun:

    a. Wählen Sie **statischen Adresspool**.

    b. Wählen Sie **hinzufügen** so konfigurieren Sie einen IP-Adresspool.

       Statische Adresspool muss es sich um Adressen aus dem internen Netzwerk enthalten. Diese Adressen sind für die interne Netzwerkverbindung auf dem VPN-Server nicht im Unternehmensnetzwerk.

    c. In **Start-IP-Adresse**, geben Sie die IP-Startadresse des Bereichs, der Sie den VPN-Clients zuweisen möchten.

    d. In **End-IP-Adresse**, geben Sie die IP-Endadresse in den Bereich, der Sie den VPN-Clients oder im zuweisen möchten **Anzahl von Adressen**, geben Sie an die Adresse, die Sie zur Verfügung stellen möchten. Wenn Sie DHCP für dieses Subnetz verwenden, stellen Sie sicher, dass Sie einen Adressausschluss für entsprechende von DHCP-Servern konfigurieren.

    e. (Optional) Wenn Sie DHCP verwenden, wählen Sie **Adapter**, und wählen Sie in der Liste der Ergebnisse, die Ethernet-Adapter, die mit Ihrem internen Umkreisnetzwerk verbunden.

16. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren*, aus der **Zertifikat** Dropdown-Liste unter **SSL-Zertifikatbindung**, wählen Sie den VPN-Server die Authentifizierung.

17. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren*, erweitern Sie in der NPS-MMC **Richtlinien\\Netzwerkrichtlinien** und: 

    a. Rechts die **Verbindungen mit Microsoft-Routing und RAS-Server** Netzwerkrichtlinie ein, und wählen Sie **Eigenschaften**.

    b. Wählen Sie die **Zugriff gewähren. Zugriff gewähren, wenn die verbindungsanforderung dieser Richtlinie entspricht** Option.

    c. Wählen Sie unter Typ des Netzwerkzugriffsservers **RAS-Server (VPN-DFÜ-)** aus der Dropdownliste aus.

18. In den Routing- und RAS-MMC, mit der Maustaste **Ports** und wählen Sie dann **Eigenschaften**. 
    
    Das Dialogfeld "Eigenschaften" wird geöffnet.

19. Wählen Sie **WAN Miniport (SSTP)** , und wählen Sie **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (SSTP).

    a. Deaktivieren der **RAS-Verbindungen (nur eingehend)** und **routing für Wählen bei Bedarf-Verbindungen (eingehend und ausgehend)** Kontrollkästchen.

    b. Wählen Sie **OK**.

20. Wählen Sie **WAN Miniport (L2TP)** , und wählen Sie **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (L2TP).

    a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.

    b. Wählen Sie **OK**.

21. Wählen Sie **WAN Miniport (PPTP)** , und wählen Sie **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (PPTP).

    a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.

    b. Wählen Sie **OK**.

22. Wählen Sie **WAN Miniport (IKEv2)** , und wählen Sie **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (IKEv2).

     a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.

     b. Wählen Sie **OK**.

23. Wenn Sie dazu aufgefordert werden, wählen Sie **Ja** um zu bestätigen, neu zu starten, den Server, und wählen **schließen** den Server neu starten.

## <a name="next-step"></a>Nächster Schritt

[Schritt 4: Installieren und konfigurieren (Network Policy Server, NPS)](vpn-deploy-nps.md): In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten. Sie auch konfigurieren, NPS, um alle Authentifizierung, Autorisierung und Kontoführung von Aufgaben für die Verbindung verarbeitet Anforderungen, die von der VPN-Server empfangen.
