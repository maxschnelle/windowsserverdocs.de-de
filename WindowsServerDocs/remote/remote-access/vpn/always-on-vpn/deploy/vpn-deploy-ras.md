---
title: Konfigurieren des RAS-Servers für Always On VPN
description: RRAS dient zum sowie einen Router und RAS-Server ausführen. aus diesem Grund wird eine Breite Palette von Features unterstützt.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067388"
---
# Schritt 3. Konfigurieren des RAS-Servers für Always On VPN

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 2. Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md)<br>
& #187;  [ **Vorherigen:** Schritt 4. Installieren und Konfigurieren von Netzwerkrichtlinienserver (Network Policy Server, NPS)](vpn-deploy-nps.md)


RRAS dient zur sowie einen Router und RAS-Server ausgeführt werden, da es eine Breite Palette von Features unterstützt. Für die Zwecke dieses Bereitstellung können Sie nur eine kleine Teilmenge dieser Features erfordern: Unterstützung für IKEv2-VPN-Verbindungen und LAN-routing.

IKEv2 ist ein VPN-Tunneling-Protokoll im Internet Engineering Task Force anfordern für Kommentare 7296 beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es Unterbrechung der zugrunde liegenden Netzwerkverbindung verträglich. Z. B. wenn die Verbindung vorübergehend nicht mehr auffindbar ist oder wenn ein Benutzer einen Clientcomputer von einem Netzwerk in ein anderes bewegt, IKEv2 automatisch wiederherstellt, die VPN-Verbindung, wenn die Verbindung wiederhergestellt ist – alles ohne Eingreifen des Benutzers.

Konfigurieren Sie den RRAS-Server zur Unterstützung von IKEv2-Verbindungen, während das Deaktivieren des nicht verwendete Protokolle, der wodurch der Server Security Speicherbedarf verringert wird. Darüber hinaus konfigurieren Sie den Server zum Zuweisen von Adressen VPN-Clients von einem statischen Adresspool. Sie können Adressen Zeitfensters aus einem Pool oder ein DHCP-Server zuweisen. Allerdings wird ein DHCP-Server erhöht die Komplexität des Designs und minimale Vorteile bietet.


>[!Important]
>Es ist wichtig zu:
>- Installieren Sie zwei Ethernet-Netzwerkadapter auf dem physischen Server. Wenn Sie den VPN-Server auf einem virtuellen Computer installieren, müssen Sie zwei externen virtuellen Switches, eine für jeden physischen Netzwerkadapter erstellen. und erstellen Sie zwei virtuellen Netzwerkadapter für den virtuellen Computer mit einzelnen Netzwerkadapter mit einem virtuellen Switch verbunden.
>
>- Installieren Sie Server in Ihrem Umkreisnetzwerk zwischen Ihrem Edge und interne Firewalls mit einem Netzwerkadapter verbunden mit dem externen Umkreisnetzwerk und eine Netzwerkkarte, die mit dem internen Umkreisnetzwerk verbunden.


>[!Warning]
>Bevor Sie beginnen, stellen Sie sicher, dass IPv6 auf dem VPN-Server aktivieren. Andernfalls kann keine Verbindung hergestellt werden, und eine Fehlermeldung angezeigt wird.

## Installieren von RAS als RAS-Gateway VPN-Server

In diesem Verfahren installieren Sie die RAS-Rolle als einzelne Mandanten RAS-Gateway VPN-Server. Weitere Informationen finden Sie unter [Remote Access](../../../Remote-Access.md).


### Installieren Sie die RAS-Rolle mithilfe von Windows PowerShell

1. Öffnen Sie Windows PowerShell als **Administrator**.

2. Geben Sie den folgenden Befehl aus, und drücken Sie die **EINGABETASTE**:

   `Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools`

   Nach Abschluss der Installation wird in Windows PowerShell die folgende Meldung angezeigt.
    
   | Erfolgreich | Neustart erforderlich | Exit-Code | Feature Ergebnis                             |
   |---------|----------------|-----------|--------------------------------------------|
   | Wahr    | Nein             | Erfolgreich   | {RAS-Verbindungs-Manager-Verwaltungskit |
   ---

### Installieren Sie die RAS-Rolle mithilfe des Server-Managers

Im folgende Verfahren können Sie die RAS-Rolle mit Server-Manager installieren.

1.  Klicken Sie auf dem VPN-Server im Server-Manager auf **Verwalten** , und klicken Sie auf **Rollen und Features hinzufügen**. <p>Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  Auf vor Seite zu beginnen, klicken Sie auf**Weiter**.

3.  Auf der Seite "Select Installation Type" **rollenbasierte oder featurebasierte Installation** die Option, und klicken Sie auf **Weiter**.

4.  Wählen Sie auf der Seite Select Destination Server die Option **einen Server aus dem Serverpool auswählen** .

5.  Wählen Sie unter Serverpool den lokalen Computer, und klicken Sie auf **Weiter**.

6.  Klicken Sie auf der Seite Select Server-Rollen in **Rollen** **Remote Access**und anschließend auf **Weiter**.

7.  Klicken Sie auf der Seite Select Features auf **Weiter**.

8.  Klicken Sie auf der Seite Remotezugriff auf **Weiter**.

9.  Klicken Sie auf der Seite Select Role Service in **Rollendienste****DirectAccess und VPN (RAS)**.<p>Das Dialogfeld **Hinzufügen von Rollen und Features-Assistent** wird geöffnet.

10. Hinzufügen von Rollen und Features-Dialogfeld klicken Sie auf **Features hinzufügen** und dann auf **Weiter**.

11. Klicken Sie auf der Seite "Web Server Rolle (IIS)" auf **Weiter**.

12. Klicken Sie auf der Seite Select Rolle Dienste auf **Weiter**.

13. Überprüfen Sie Ihre Auswahl auf der Seite Confirm Installation Auswahl, und klicken Sie auf **Installieren**.

14. Wenn die Installation abgeschlossen ist, klicken Sie auf " **Schließen**".

## Konfigurieren von Remote Access als VPN-Server

In diesem Abschnitt können Sie Remote Access VPN für IKEv2-VPN-Verbindung zulassen, verweigern, die Verbindungen von anderen VPN-Protokolle und weisen Sie einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zu verbinden von autorisierten VPN-Clients konfigurieren.

1.  Klicken Sie auf dem VPN-Server im Server-Manager auf die **Benachrichtigungen** .

2.  Klicken Sie im Menü " **Aufgaben** " auf **den Schnellstart-Assistenten zu öffnen**.<p>Konfigurieren des RAS-Assistenten wird geöffnet. 

    >[!NOTE] 
    >Konfigurieren des RAS-Assistenten möglicherweise hinter dem Server-Manager öffnen. Wenn Sie, dass der Assistent zum Öffnen zu lange dauert vermuten, verschieben oder Server-Manager, um herauszufinden, ob der Assistent dahinter ist zu minimieren. Wenn dies nicht der Fall ist, warten Sie, um den Assistenten zu initialisieren.

3.  Klicken Sie auf **nur VPN bereitstellen**.<p>Das Routing und Remote Access Microsoft Management Console (MMC) wird geöffnet.

4.  Mit der rechten Maustaste in des VPN-Servers, und klicken Sie auf **Konfigurieren und Aktivieren von Routing und RAS**.<p>Der Routing- und RAS-Server Setup-Assistent wird geöffnet.

5.  Klicken Sie in die Willkommensseite den Routing- und RAS-Server Setup-Assistent auf " **Weiter**".

6.  Klicken Sie in der **Konfiguration**auf **Benutzerdefinierte Konfiguration**, und klicken Sie auf **Weiter**.

7.  **Benutzerdefinierte Konfiguration**auf **VPN-Zugriff**, und klicken Sie dann auf **Weiter**.<p>Abschließen der Routing- und RAS-Server Setup-Assistent wird geöffnet.

8.  Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen, und klicken Sie auf **OK** , um das Routing- und RAS-Dialogfeld zu schließen.

9.  Klicken Sie auf **Dienst starten** , um den Remotezugriff starten.

10. In der RAS-MMC mit der rechten Maustaste in des VPN-Servers, und klicken Sie auf **Eigenschaften**.

11. Klicken Sie in den Eigenschaften auf der Registerkarte " **Sicherheit** ", und führen:

    a. Klicken Sie auf **Authentifizierungsanbieter** , und klicken Sie auf **RADIUS-Authentifizierung**.
    
    b. Klicken Sie auf **Konfigurieren**.<p>Das Dialogfeld RADIUS-Authentifizierung wird geöffnet.
    
    c. Klicken Sie auf **Hinzufügen**.<p>Das Dialogfeld RADIUS-Server hinzufügen wird geöffnet.
    
    d. Geben Sie den vollständig qualifizierten Domänennamen (FQDN) des Netzwerkrichtlinienservers in **Servername**auf Ihre Organisation /-Unternehmensnetzwerk.<p>Wenn der NetBIOS-Namen des NPS-Servers NPS1 ist und Ihren Domänennamen corp.contoso.com ist, geben Sie z. B. **NPS1.corp.contoso.com**.
    
    e. Klicken Sie im **freigegebenen geheimen Schlüssel**auf **Ändern**.<p>Das Dialogfeld Schlüssel ändern wird geöffnet.
    
    f. Geben Sie im **neuen geheimen Schlüssel**einer Textzeichenfolge hinzugefügt.
    
    g. Geben Sie im **neuen geheimen Schlüssel bestätigen**die gleichen Textzeichenfolgen, und klicken Sie auf **OK**.

    >[!IMPORTANT] 
    >Speichern Sie diese Textzeichenfolge. Wenn Sie den Netzwerkrichtlinienserver auf Ihre Organisation /-Unternehmensnetzwerk konfigurieren, fügen Sie diesen VPN-Server als RADIUS-Client. Während die Konfiguration verwenden Sie diese denselben gemeinsamen geheimen Schlüssel, damit die NPS und VPN-Server kommunizieren können.

12. Überprüfen Sie in **RADIUS-Server hinzufügen**die Standardeinstellungen für:

    - **Timeout**
    
    - **Anfängliche Bewertung**
    
    - **Port**

13. Ändern Sie ggf. die Werte, um die Anforderungen für Ihre Umgebung übereinstimmen, und klicken Sie auf **OK**.<p>Ein NAS ist ein Gerät, das einige Ebene des Zugriffs auf ein größeres Netzwerk bereitstellt. Ein NAS eine RADIUS-Infrastruktur ist auch ein RADIUS-Client, Senden von verbindungsanforderungen und Kontoführungsnachrichten mit einem RADIUS-Server für die Authentifizierung, Autorisierung und Kontoführung.

14. Überprüfen Sie die Einstellung für **Buchhaltung Anbieter**:

    | Wenn Sie möchten die …  | Dann...             |
    |---------------------|-------------------|
    | Remote Access-Aktivität auf dem RAS-Server protokolliert | Stellen Sie sicher, dass **Windows-Kontoführung** aktiviert ist.      |
    | NPS zum Ausführen von Services Kontoführung für VPN   | Ändern Sie **Kontoführung für den Anbieter** in **RADIUS-Kontoführung** , und konfigurieren Sie die NPS als Buchhaltung Anbieter. |
    ---

15. Klicken Sie auf der Registerkarte " **IPv4** ", und führen Sie:

    a. Klicken Sie auf **statischen Adresse Speicherpool**.
    
    b. Klicken Sie auf **Hinzufügen** , um einen Pool IP-Adresse zu konfigurieren.<p>Der statischen Adressenpool sollte Adressen aus dem internen Umkreisnetzwerk enthalten. Diese Adressen sind für die internen Netzwerkverbindung auf dem VPN-Server nicht im Unternehmensnetzwerk.
    
    c. Geben Sie im **Start-IP-Adresse**die IP-Startadresse des Bereichs, die Sie VPN-Clients zuweisen möchten.
    
    d. **End-IP-Adresse**Geben Sie die Ende-IP-Adresse im Bereich Sie VPN-Clients zuweisen möchten, oder im **Anzahl von Adressen**, geben Sie die Anzahl der Adresse, die Sie zur Verfügung stellen möchten. Wenn Sie DHCP für dieses Subnetz verwenden, stellen Sie sicher, dass Sie einen entsprechende Adressausschluss auf DHCP-Servern konfigurieren.
    
    e. (Optional) Wenn Sie DHCP verwenden, klicken Sie auf **Adapter**, und klicken Sie in der Liste der Ergebnisse, auf den Ethernet-Adapter mit Ihrem internen Umkreisnetzwerk verbunden.

16. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindung konfigurieren*, wählen Sie aus dem **Zertifikat** Dropdown-Liste unter **SSL Zertifikat binden**, die VPN-Server-Authentifizierung.

17. (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindung konfigurieren*, in der NPS-MMC **Policies\\Network Richtlinien** zu erweitern, und führen Sie: 

    a. Rechten – der Netzwerk- **Verbindungen mit Microsoft Routing- und RAS-Server** -Richtlinie, und wählen Sie **Eigenschaften**.
    
    b. Wählen Sie die **Zugriff gewähren. Zugriff gewähren, wenn die verbindungsanforderung diese Richtlinie entspricht** Option.
    
    c. Wählen Sie unter Art der Server für den Netzwerkzugriff **RAS-Server (VPN-DFÜ-)** aus der Dropdown-Liste aus.

3.  In den Routing- und RAS-MMC mit der rechten Maustaste **Ports,** und klicken Sie dann auf **Eigenschaften**. <p>Das Dialogfeld Eigenschaften von Ports wird geöffnet.

4.  Klicken Sie auf **WAN-Miniport (SSTP)** , und klicken Sie auf **Konfigurieren**. Gerät konfigurieren - WAN-Miniport (SSTP)-Dialogfeld wird geöffnet.

    a. Deaktivieren Sie die Kontrollkästchen **RAS-Verbindungen (nur eingehend)** und **bei Bedarf routing Verbindungen (eingehenden und ausgehenden)** .
    
    b. Klicken Sie auf **OK**.

5.  Klicken Sie auf **WAN-Miniport (L2TP)** , und klicken Sie auf **Konfigurieren**. Gerät konfigurieren - WAN-Miniport (L2TP)-Dialogfeld wird geöffnet.

    a. **Maximale Ports**Geben Sie die Anzahl der Ports, um die maximale Anzahl gleichzeitig aktiver VPN-Verbindungen abzugleichen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.

6.  Klicken Sie auf **WAN-Miniport (PPTP)** , und klicken Sie auf **Konfigurieren**. Gerät konfigurieren - WAN-Miniport (PPTP)-Dialogfeld wird geöffnet.

    a. **Maximale Ports**Geben Sie die Anzahl der Ports, um die maximale Anzahl gleichzeitig aktiver VPN-Verbindungen abzugleichen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.
    
7. Klicken Sie auf **WAN-Miniport (IKEv2)** , und klicken Sie auf **Konfigurieren**. Gerät konfigurieren - WAN-Miniport (IKEv2)-Dialogfeld wird geöffnet.

    a. **Maximale Ports**Geben Sie die Anzahl der Ports, um die maximale Anzahl gleichzeitig aktiver VPN-Verbindungen abzugleichen, die Sie unterstützen möchten.
    
    b. Klicken Sie auf **OK**.

7.  Wenn Sie aufgefordert werden, klicken Sie auf **Ja,** um zu bestätigen, einen Neustart des Servers, und klicken Sie auf **Schließen** um den Server neu starten.

## Nächster Schritt
[Schritt 4. Installieren und Konfigurieren von Netzwerkrichtlinienserver (Network Policy Server, NPS)](vpn-deploy-nps.md): In diesem Schritt Sie Netzwerkrichtlinienserver (Network Policy Server, NPS) mithilfe von Windows PowerShell oder die Server-Manager Hinzufügen von Rollen und Features Assistenten installieren. Sie auch Konfigurieren von NPS zum Behandeln von allen Authentifizierung, Autorisierung und Kontoführung Aufgaben für Verbindung Anforderungen, die sie aus der VPN-Server empfängt.





---
