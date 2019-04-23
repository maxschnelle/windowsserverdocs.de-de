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
ms.openlocfilehash: a338ddfec1ed5cd0e9198f64dc4952eb591cdc1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829671"
---
# <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>Schritt 3 Konfigurieren des RAS-Servers für Always On VPN

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**Vorherige:** Schritt 2 Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md)<br>
&#187;  [**Vorherige:** Schritt 4 Installieren Sie und konfigurieren Sie (Network Policy Server, NPS)](vpn-deploy-nps.md)


RRAS dient auch als Router und RAS-Server ausführen, da es sich um ein breites Spektrum an Funktionen unterstützt. Für die Zwecke dieser Bereitstellung können Sie nur eine kleine Teilmenge dieser Funktionen benötigen: Unterstützung für IKEv2-VPN-Verbindungen und LAN-routing.

IKEv2 befindet es sich um ein VPN-Tunneling-Protokoll in die Internet Engineering Task Force-Anforderung für Kommentare 7296 beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es sich um Unterbrechungen in die zugrunde liegende Netzwerkverbindung toleriert. Z. B. wenn die Verbindung vorübergehend unterbrochen wird, oder wenn ein Benutzer einen Clientcomputer aus einem Netzwerk zu einem anderen bewegt, IKEv2 automatisch wiederherstellt, die VPN-Verbindung, wenn die Verbindung wiederhergestellt ist – alles ohne Eingreifen des Benutzers.

Konfigurieren von RRAS-Servers zur Unterstützung von IKEv2-Verbindungen beim Deaktivieren nicht verwendeter Protokolle, die Sicherheitsbedarf des Servers reduziert. Außerdem konfigurieren Sie den Server, um Adressen zu VPN-Clients von einem statischen Adresspool zugewiesen. Sie können berechtigterweise Adressen aus einem Pool oder einem DHCP-Server zuweisen. Allerdings wird mit einem DHCP-Server erhöht die Komplexität des Entwurfs und bietet minimale Vorteile.


>[!Important]
>Es ist wichtig:
>- Installieren Sie zwei Ethernet-Netzwerkadapter auf dem physischen Server an. Wenn Sie den VPN-Server auf einem virtuellen Computer installieren, müssen Sie zwei externen virtuellen Switches, einen für jeden physischen Netzwerkadapter erstellen; und erstellen Sie zwei virtuelle Netzwerkadapter für den virtuellen Computer mit einzelnen Netzwerkadapter mit einem virtuellen Switch verbunden.
>
>- Installieren Sie den Server im Umkreisnetzwerk zwischen dem Rand und die internen Firewalls mit ein Netzwerkadapter mit dem externen Netzwerk des Umkreisnetzwerks und ein Netzwerkadapter mit dem internen Umkreisnetzwerk.


>[!Warning]
>Bevor Sie beginnen, stellen Sie sicher, dass IPv6 auf dem VPN-Server zu aktivieren. Andernfalls kann eine Verbindung kann nicht hergestellt werden, und eine Fehlermeldung angezeigt wird.

## <a name="install-remote-access-as-a-ras-gateway-vpn-server"></a>Installieren Sie den Remotezugriff als RAS-Gateway-VPN-Server

In diesem Verfahren installieren Sie die Rolle "Remotezugriff" als einzelner Mandant RAS-VPN-Gateway-Server an. Weitere Informationen finden Sie unter [Remote Access](../../../Remote-Access.md).


### <a name="install-the-remote-access-role-by-using-windows-powershell"></a>Installieren Sie die Rolle "Remotezugriff" mithilfe von Windows PowerShell

1. Öffnen Sie Windows PowerShell als **Administrator**.

2. Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**:

   `Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools`

   Nach Abschluss der Installation wird die folgende Meldung angezeigt, in Windows PowerShell.
    
   | Erfolgreich | Neustart erforderlich | Exitcode | Ergebnis der Funktion                             |
   |---------|----------------|-----------|--------------------------------------------|
   | True    | Nein             | Erfolgreich   | {RAS-Verbindungs-Manager-Verwaltungskit |
   ---

### <a name="install-the-remote-access-role-by-using-server-manager"></a>Installieren Sie die Rolle "Remotezugriff" mithilfe von Server-Manager

Sie können das folgende Verfahren verwenden, der Rolle "Remotezugriff" mit Server-Manager zu installieren.

1.  Klicken Sie auf die VPN-Server im Server-Manager auf **verwalten** , und klicken Sie auf **Hinzufügen von Rollen und Features**. <p>Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Auf der Seite zu beginnen, klicken Sie auf **Weiter**.

3.  Wählen Sie auf der Seite Installationstyp auswählen die **rollenbasierte oder featurebasierte Installation** aus, und klicken Sie auf **Weiter**.

4.  Wählen Sie auf der Seite Zielserver auswählen den Server der **wählen Sie einen Server aus dem Serverpool** Option.

5.  Wählen Sie unter Server-Ressourcenpool, den lokalen Computer, und klicken Sie auf **Weiter**.

6.  Wählen Sie im Server-Rollen auf der Seite **Rollen**, klicken Sie auf **RAS**, und klicken Sie dann **Weiter**.

7.  Klicken Sie auf der Seite %%amp;quot;Features auswählen%%amp;quot; auf **Weiter**.

8.  Klicken Sie auf der Seite den Remotezugriff auf **Weiter**.

9.  Auf der Seite Rolle auswählen in **Rollendienste**, klicken Sie auf **DirectAccess und VPN (RAS)**.<p>Die **Hinzufügen von Rollen und Features Assistenten** Dialogfeld wird geöffnet.

10. Klicken Sie im Dialogfeld Hinzufügen von Rollen und Features auf **Features hinzufügen** , und klicken Sie auf **Weiter**.

11. Klicken Sie auf der Seite "Webserverrolle (IIS)" auf **Weiter**.

12. Klicken Sie auf der Seite; Rollendienste auswählen% Dienste auf **Weiter**.

13. Klicken Sie auf der Seite Installationsauswahl bestätigen, überprüfen Sie Ihre Auswahl, und klicken Sie auf **installieren**.

14. Klicken Sie nach dem Abschluss der Installation auf **Schließen**.

## <a name="configure-remote-access-as-a-vpn-server"></a>Konfigurieren des Remotezugriffs einen VPN-Server

In diesem Abschnitt können Sie Remote Access VPN für IKEv2-VPN-Verbindungen zulassen, verweigern Verbindungen von anderen VPN-Protokolle und zuweisen einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zum Herstellen einer Verbindung autorisierte VPN-Clients konfigurieren.

1.  Klicken Sie auf die VPN-Server im Server-Manager auf die **Benachrichtigungen** Flag.

2.  In der **Aufgaben** Menü klicken Sie auf **öffnen Sie den Assistenten für erste Schritte**.<p>Das Konfigurieren des Remotezugriffs-Assistent wird geöffnet. 

    >[!NOTE] 
    >Konfigurieren von RAS-Assistenten möglicherweise hinter den Server-Manager zu öffnen. Wenn Sie, dass der Assistent glauben geöffnet zu lange dauert, verschieben Sie oder minimieren Sie des Server Manager, um herauszufinden, ob der Assistent dahinter ist. Wenn dies nicht der Fall ist, warten Sie, um den Assistenten zu initialisieren.

3.  Klicken Sie auf **Bereitstellen eines VPN nur**.<p>Der Routing- und RAS Zugriff Microsoft Management Console (MMC) wird geöffnet.

4.  Mit der rechten Maustaste in des VPN-Servers, und klicken Sie auf **konfigurieren und Aktivieren von Routing und Remotezugriff**.<p>Der Routing- und RAS-Server-Setup-Assistent wird geöffnet.

5.  Willkommen bei den Routing- und RAS-Server-Setup-Assistent, klicken Sie auf **Weiter**.

6.  In **Konfiguration**, klicken Sie auf **benutzerdefinierte Konfiguration**, und klicken Sie dann auf **Weiter**.

7.  In **benutzerdefinierte Konfiguration**, klicken Sie auf **VPN-Zugriff**, und klicken Sie dann auf **Weiter**.<p>Das Abschließen der Routing- und RAS-Server-Setup-Assistent wird geöffnet.

8.  Klicken Sie auf **Fertig stellen** um den Assistenten schließen, und klicken Sie auf **OK** um das Routing und RAS-Dialogfeld zu schließen.

9.  Klicken Sie auf **Dienst starten** um Remotezugriff zu starten.

10. Klicken Sie in der RAS-MMC, mit der rechten Maustaste in des VPN-Servers, und klicken Sie auf **Eigenschaften**.

11. Klicken Sie in den Eigenschaften, auf die **Sicherheit** Registerkarte, und führen:

    a. Klicken Sie auf **Authentifizierungsanbieter** , und klicken Sie auf **RADIUS-Authentifizierung**.
    
    b. Klicken Sie auf **Konfigurieren**.<p>Das Dialogfeld "RADIUS-Authentifizierung" wird geöffnet.
    
    c. Klicken Sie auf **Hinzufügen**.<p>Das Dialogfeld "RADIUS-Server hinzufügen" wird geöffnet.
    
    d. In **Servernamen**, geben Sie den vollständig qualifizierten Domänennamen (FQDN) des NPS-Servers in Ihrem Netzwerk der Organisation/Corporate (Unternehmen).<p>Geben Sie beispielsweise, wenn der NetBIOS-Namen des NPS-Servers NPS1 ist, und Ihr Domänenname corp.contoso.com ist, **NPS1.corp.contoso.com**.
    
    e. In **gemeinsamer geheimer Schlüssel**, klicken Sie auf **Änderung**.<p>Der Schlüssel ändern-Dialogfeld wird geöffnet.
    
    f. In **neuer geheimer**, geben Sie eine Textzeichenfolge.
    
    g. In **neuen geheimen Schlüssel bestätigen**, geben Sie die gleiche Textzeichenfolge ein, und klicken Sie auf **OK**.

    >[!IMPORTANT] 
    >Speichern Sie die Textzeichenfolge. Wenn Sie den NPS-Server in Ihrem Netzwerk der Organisation/Corporate (Unternehmen) konfigurieren, fügen Sie dieses VPN-Server als RADIUS-Client hinzu. Bei dieser Konfiguration verwenden Sie dieses gleiche gemeinsame Geheimnis, damit die NPS- und VPN-Server kommunizieren können.

12. In **RADIUS-Server hinzufügen**, überprüfen Sie die Standardeinstellungen für:

    - **Time-out**
    
    - **Anfängliche Bewertung**
    
    - **Port**

13. Ändern Sie ggf. die Werte entsprechend die Anforderungen für Ihre Umgebung und auf **OK**.<p>NAS ist ein Gerät, das Zugriff auf ein größeres Netzwerk bereitstellt. Eine RADIUS-Infrastruktur NAS ist auch ein RADIUS-Client, senden verbindungsanforderungen und Kontoführungsnachrichten an einen RADIUS-Server für die Authentifizierung, Autorisierung und ressourcenerfassung.

14. Überprüfen Sie die Einstellung für **Kontoanbieter**:

    | Wenn Sie möchten die...  | Dann...             |
    |---------------------|-------------------|
    | Remote Access-Aktivität, die auf dem RAS-Server protokolliert | Stellen Sie sicher, dass **Windows Accounting** ausgewählt ist.      |
    | NPS auszuführenden Accounting-Dienste für VPN   | Änderung **Kontoanbieter** zu **RADIUS-Kontoführung** und konfigurieren Sie den NPS als Kontoführungsanbieter. |
    ---

15. Klicken Sie auf die **IPv4** Registerkarte und zu tun:

    a. Klicken Sie auf **statischen Adresspool**.
    
    b. Klicken Sie auf **hinzufügen** so konfigurieren Sie einen IP-Adresspool.<p>Statische Adresspool muss es sich um Adressen aus dem internen Netzwerk enthalten. Diese Adressen sind für die interne Netzwerkverbindung auf dem VPN-Server nicht im Unternehmensnetzwerk.
    
    c. In **Start-IP-Adresse**, geben die IP-Startadresse des Bereichs, der Sie den VPN-Clients zuweisen möchten.
    
    d. In **End-IP-Adresse**, geben Sie die IP-Endadresse in den Bereich, der Sie den VPN-Clients oder im zuweisen möchten **Anzahl von Adressen**, geben Sie die Anzahl der Adresse, die Sie zur Verfügung stellen möchten. Wenn Sie DHCP für dieses Subnetz verwenden, stellen Sie sicher, dass Sie einen Adressausschluss für entsprechende von DHCP-Servern konfigurieren.
    
    e. (Optional) Wenn Sie DHCP verwenden, klicken Sie auf **Adapter**, und klicken Sie in der Liste der Ergebnisse, auf dem Ethernet-Adapter, die mit Ihrem internen Umkreisnetzwerk verbunden.

16. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren*, aus der **Zertifikat** Dropdown-Liste unter **SSL-Zertifikatbindung**, wählen Sie den VPN-Server die Authentifizierung.

17. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren*, erweitern Sie in der NPS-MMC **Richtlinien\\Netzwerkrichtlinien** und: 

    a. Rechts die **Verbindungen mit Microsoft-Routing und RAS-Server** Netzwerkrichtlinie ein, und wählen Sie **Eigenschaften**.
    
    b. Wählen Sie die **Zugriff gewähren. Zugriff gewähren, wenn die verbindungsanforderung dieser Richtlinie entspricht** Option.
    
    c. Wählen Sie unter Typ des Netzwerkzugriffsservers **RAS-Server (VPN-DFÜ-)** aus der Dropdownliste aus.

3.  In den Routing- und RAS-MMC, mit der Maustaste **Ports** , und klicken Sie dann auf **Eigenschaften**. <p>Das Dialogfeld "Eigenschaften" wird geöffnet.

4.  Klicken Sie auf **WAN Miniport (SSTP)** , und klicken Sie auf **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (SSTP).

    a. Deaktivieren der **RAS-Verbindungen (nur eingehend)** und **routing für Wählen bei Bedarf-Verbindungen (eingehend und ausgehend)** Kontrollkästchen.
    
    b. Klicken Sie auf **OK**.

5.  Klicken Sie auf **WAN Miniport (L2TP)** , und klicken Sie auf **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (L2TP).

    a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.

6.  Klicken Sie auf **WAN Miniport (PPTP)** , und klicken Sie auf **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (PPTP).

    a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.
    
7. Klicken Sie auf **WAN Miniport (IKEv2)** , und klicken Sie auf **konfigurieren**. Gerät konfigurieren – Dialogfeld wird geöffnet WAN Miniport (IKEv2).

    a. In **maximale Ports**, geben Sie die Anzahl der Ports, die die maximale Anzahl von gleichzeitigen Verbindungen zu entsprechen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.

7.  Wenn Sie dazu aufgefordert werden, klicken Sie auf **Ja** um zu bestätigen, Neustart der Server und auf **schließen** den Server neu starten.

## <a name="next-step"></a>Nächster Schritt
[Schritt 4. Installieren und konfigurieren (Network Policy Server, NPS)](vpn-deploy-nps.md): In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten. Sie auch konfigurieren, NPS, um alle Authentifizierung, Autorisierung und Kontoführung von Aufgaben für die Verbindung verarbeitet Anforderungen, die von der VPN-Server empfangen.





---
