---
title: 'Schritt 2: Konfigurieren von WSUS'
description: 'Thema zu Windows Server Update Service (WSUS): Konfigurieren von WSUS in einem vierstufigen Verfahren zum Bereitstellen von WSUS'
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: d4adc568-1f23-49f3-9a54-12a7bec5f27c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 386ef1d8683b75bdc94fc1aa4ac7cb8acf6cd6fa
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544484"
---
# <a name="step-2-configure-wsus"></a>Schritt 2: Konfigurieren von WSUS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie die WSUS-Serverrolle auf dem Server installiert haben, müssen Sie sie korrekt konfigurieren. In der folgenden Prüfliste werden die Schritte zusammengefasst, die bei der Erstkonfiguration des WSUS-Servers erforderlich sind.

|Aufgabe|Beschreibung|
|----|--------|
|[2,1. Konfigurieren von Netzwerkverbindungen](#21-configure-network-connections)|Konfigurieren Sie das Clusternetzwerk mithilfe des Netzwerkkonfigurations-Assistenten.|
|[2,2. Konfigurieren von WSUS mit dem WSUS-Konfigurations-Assistenten](#22-configure-wsus-by-using-the-wsus-configuration-wizard)|Verwenden Sie den WSUS-Konfigurations-Assistenten, um die WSUS-Basiskonfiguration auszuführen.|
|[2,3. Konfigurieren von WSUS-Computer Gruppen](#23-configure-wsus-computer-groups)|Erstellen Sie Computergruppen in der WSUS-Verwaltungskonsole zum Verwalten von Updates in Ihrer Organisation.|
|[2,4. Konfigurieren von Client Updates](#24-configure-client-updates)|Geben Sie an, wie und wann automatische Updates auf Clientcomputern angewendet werden.|
|[2,5. Schützen von WSUS mit dem Secure Sockets Layer Protokoll](#25-secure-wsus-with-the-secure-sockets-layer-protocol)|Konfigurieren Sie das Secure Sockets Layer (SSL)-Protokoll zum Schutz von Windows Server Update Services (WSUS).|

## <a name="21-configure-network-connections"></a>2.1. Konfigurieren der Netzwerkverbindungen
Bevor Sie mit der Konfiguration beginnen, müssen Sie sich die folgenden Fragen beantworten:

1.  Ist die Firewall des Servers so konfiguriert, dass Clients auf den Server zugreifen können?

2.  Kann dieser Computer eine Verbindung mit dem Upstreamserver herstellen (z. B. dem Server, der zum Herunterladen von Updates von Microsoft Update verwendet wird)?

3.  Kennen Sie den Namen des Proxyservers und die Benutzeranmeldeinformationen für den Proxyserver, falls Sie sie benötigen?

In der Standardkonfiguration ruft WSUS Updates von Microsoft Update ab. Wenn Sie über einen Proxy Server im Netzwerk verfügen, können Sie WSUS für die Verwendung des Proxy Servers konfigurieren. Wenn eine Unternehmens Firewall zwischen WSUS und dem Internet vorhanden ist, müssen Sie möglicherweise die Firewall konfigurieren, um sicherzustellen, dass WSUS Updates abrufen kann.

> [!TIP]
> Obwohl Internetkonnektivität erforderlich ist, um Updates von Microsoft Update herunterzuladen, bietet WSUS die Möglichkeit, Updates in Netzwerke zu importieren, die nicht mit dem Internet verbunden sind.

Wenn Sie die Antworten auf diese Fragen kennen, können Sie mit der Konfiguration der folgenden WSUS-Netzwerkeinstellungen beginnen:

-   **Updates** Geben Sie an, wie dieser Server Updates abruft (von Microsoft Update oder von einem anderen WSUS-Server).

-   **Proxy** wenn WSUS einen Proxy Server für den Internet Zugriff verwenden muss, müssen Sie die Proxy Einstellungen auf dem WSUS-Server konfigurieren.

-   **Firewall** Wenn Sie ermittelt haben, dass sich WSUS hinter einer Unternehmens Firewall befindet, müssen einige zusätzliche Schritte auf dem Edgegerät ausgeführt werden, um den WSUS-Datenverkehr ordnungsgemäß zuzulassen.

### <a name="211-connection-from-the-wsus-server-to-the-internet"></a>2.1.1. Verbindung zwischen WSUS-Server und Internet
Falls eine Unternehmensfirewall zwischen WSUS und dem Internet vorhanden ist, müssen Sie sie ggf. konfigurieren, um sicherzustellen, dass WSUS Updates abrufen kann. Der WSUS-Server verwendet den Port 443 für das HTTPS-Protokoll, um Updates von Microsoft Update herunterzuladen. Obwohl die meisten Unternehmens Firewalls diese Art von Datenverkehr zulassen, gibt es einige Unternehmen, die den Internet Zugriff von den Servern aufgrund der Sicherheitsrichtlinien des Unternehmens einschränken. Wenn Ihr Unternehmen den Zugriff einschränkt, benötigen Sie eine Autorisierung, um den Internet Zugriff von WSUS auf die folgende Liste von URLs zuzulassen:

- http://windowsupdate.microsoft.com

- http://*.windowsupdate.microsoft.com

- https://*.windowsupdate.microsoft.com

- http://*.update.microsoft.com

- https://*.update.microsoft.com

- http://*.windowsupdate.com

- http://download.windowsupdate.com

- https://download.microsoft.com

- http://*.download.windowsupdate.com

- http://wustat.windows.com

- http://ntservicepack.microsoft.com

- http://go.microsoft.com

- http://dl.delivery.mp.microsoft.com

- https://dl.delivery.mp.microsoft.com

> [!IMPORTANT]
> Ein Szenario, in dem WSUS aufgrund von Firewallkonfigurationen keine Updates abrufen kann, finden Sie im [Artikel 885819](https://support.microsoft.com/kb/885819) in der Microsoft Knowledge Base.

Im folgenden Abschnitt wird beschrieben, wie eine Unternehmensfirewall zwischen WSUS und dem Internet konfiguriert wird. Da WSUS den gesamten Netzwerk Datenverkehr initiiert, ist es nicht erforderlich, die Windows-Firewall auf dem WSUS-Server zu konfigurieren. Obwohl die Verbindung zwischen Microsoft Update und WSUS erfordert, dass die Ports 80 und 443 geöffnet sind, können Sie mehrere WSUS-Server zur Synchronisierung mit einem benutzerdefinierten Port konfigurieren.

### <a name="212-connection-between-wsus-servers"></a>2.1.2. Verbindung zwischen WSUS-Servern
Upstream- und Downstream-WSUS-Server werden auf dem Port synchronisiert, der vom WSUS-Administrator konfiguriert wurde. Diese Ports sind standardmäßig folgendermaßen konfiguriert:

-   Bei WSUS 3.2 und früher: Port 80 für HTTP und 443 für HTTPS

-   Unter WSUS 6,2 und höher (mindestens Windows Server 2012) wird Port 8530 für http und 8531 für HTTPS verwendet.

Die Firewall auf dem WSUS-Server muss für das Zulassen von eingehendem Datenverkehr auf diesen Ports konfiguriert werden.

### <a name="213-connection-between-clients-windows-update-agent-and-wsus-servers"></a>2.1.3. Verbindung zwischen Clients (Windows Update-Agent) und WSUS-Servern
Die Überwachungsschnittstellen und Ports werden auf den IIS-Websites für WSUS und in allen Gruppenrichtlinieneinstellungen zur Konfiguration von Clientcomputern konfiguriert. Die Standardports sind identisch mit denen im vorherigen Abschnitt **Verbindung zwischen WSUS-Servern**, und die Firewall auf dem WSUS-Server muss ebenfalls für eingehenden Datenverkehr über diese Ports konfiguriert werden.

## <a name="configure-the-proxy-server"></a>Konfigurieren der Proxyserver
Wenn das Unternehmensnetzwerk Proxyserver verwendet, müssen die Proxyserver die Protokolle HTTP und SSL unterstützen und Standardauthentifizierung oder Windows-Authentifizierung verwenden. Diese Anforderungen können mithilfe einer der folgenden Konfigurationen erfüllt werden:

1.  Ein einzelner Proxyserver, der zwei Protokollkanäle unterstützt. In diesem Fall legen Sie einen Kanal für die Verwendung von HTTP und den anderen Kanal für HTTPS fest.

    > [!NOTE]
    > Sie können einen Proxyserver einrichten, der beide Protokolle für WSUS während der Installation der WSUS-Serversoftware verarbeitet.

2.  Zwei Proxyserver, von denen jeder ein einzelnes Protokoll unterstützt. In diesem Fall ist ein Proxyserver für die Verwendung von HTTP und der andere Proxyserver zur Verwendung von HTTPS konfiguriert.

Verwenden Sie zum Einrichten von zwei Proxyservern, von denen jeder ein Protokoll für WSUS behandelt, das folgende Verfahren:

#### <a name="to-set-up-wsus-to-use-two-proxy-servers"></a>Einrichten von WSUS zur Verwendung der beiden Proxyserver

1.  Melden Sie sich bei dem Computer, der als WSUS-Server verwendet wird, mit einem Konto an, das Mitglied der lokalen Administratorgruppe ist.

2.  Installieren Sie die WSUS-Serverrolle. Geben Sie während der Ausführung des WSUS-Konfigurations-Assistenten (im nächsten Abschnitt erläutert) keinen Proxyserver an.

3.  Öffnen Sie eine Eingabeaufforderung (Cmd.exe) als Administrator. Wählen Sie zum Öffnen einer Eingabeaufforderung als Administrator **Start**aus. Geben Sie in **Suche starten**die **Eingabeaufforderung**ein. Klicken Sie oben im Startmenü mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**. Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, geben Sie die entsprechenden Anmelde Informationen ein (falls angefordert), vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf **weiter**.

4.  Wechseln Sie im Eingabe Aufforderungs Fenster zum Ordner "c:\Programme\Update Services\Tools". Geben Sie den folgenden Befehl ein:

    **WSUSutil Konfigurationselement Proxy [< Proxy ProxyPort >]-enable**, wobei:

    1.  Proxyserver für den Namen des Proxyservers steht, der HTTPS unterstützt.

    2.  Proxyport die Portnummer des Proxyservers ist.

5.  Schließen Sie das Eingabe Aufforderungs Fenster.

Führen Sie das folgende Verfahren aus, um den Proxyserver hinzuzufügen, der das HTTP-Protokoll für die WSUS-Konfiguration verwendet:

#### <a name="to-add-a-proxy-server-that-uses-the-http-protocol"></a>Hinzufügen eines Proxyservers, der das HTTP-Protokoll verwendet

1.  Öffnen Sie die WSUS-Verwaltungskonsole.

2.  Erweitern Sie im linken Bereich den Servernamen, und klicken Sie dann auf **Optionen**.

3.  Klicken Sie im Bereich **Optionen** auf **Updatequelle und Proxyserver** und anschließend auf die Registerkarte **Proxyserver**.

4.  Verwenden Sie die folgenden Optionen, um die vorhandene Proxyserverkonfiguration zu ändern:

    ###### <a name="to-change-or-add-a-proxy-server-to-the-wsus-configuration"></a>Ändern oder Hinzufügen eines Proxyservers zur WSUS-Konfiguration

    1.  Aktivieren Sie das Kontrollkästchen für **Proxyserver für die Synchronisierung verwenden**.

    2.  Geben Sie im Textfeld **Proxyservername** den Namen des Proxyservers ein.

    3.  Geben Sie im Textfeld **Proxyportnummer** die Portnummer des Proxyservers ein. Die Standardportnummer ist 80.

    4.  FF der Proxy Server erfordert, dass Sie ein bestimmtes Benutzerkonto verwenden, aktivieren Sie das Kontrollkästchen **Benutzer Anmelde Informationen zum Herstellen einer Verbindung mit dem Proxy Server verwenden** . Geben Sie den erforderlichen Benutzernamen, die Domäne und das Kennwort in die entsprechenden Textfelder ein.

    5.  Falls der Proxyserver Standardauthentifizierung unterstützt, aktivieren Sie das Kontrollkästchen **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** .

    6.  Klicken Sie auf **OK**.

    ###### <a name="to-remove-a-proxy-server-from-the-wsus-configuration"></a>Entfernen eines Proxyservers aus der WSUS-Konfiguration

    1.  Um einen Proxyserver aus der WSUS-Konfiguration zu entfernen, deaktivieren Sie das Kontrollkästchen **Proxyserver für die Synchronisierung verwenden**.

    2.  Klicken Sie auf **OK**.

## <a name="22-configure-wsus-by-using-the-wsus-configuration-wizard"></a>2.2. Konfigurieren von WSUS mit dem WSUS-Konfigurations-Assistenten
Dieses Verfahren setzt voraus, dass Sie den WSUS-Konfigurations-Assistenten verwenden, der beim erstmaligen Starten der WSUS-Verwaltungskonsole angezeigt wird. Weiter unter in diesem Thema wird beschrieben, wie Sie diese Konfigurationen auf der Seite **Optionen** ausführen.

#### <a name="to-configure-wsus"></a>So konfigurieren Sie WSUS

1.  Klicken Sie im Navigationsbereich des Server-Managers auf **Dashboard**, auf **Tools** und dann auf **Windows Server Update Services**.

    > [!NOTE]
    > Wenn das Dialogfeld **WSUS-Installation vervollständigen** angezeigt wird, klicken Sie auf **Ausführen**. Klicken Sie im Dialogfeld **WSUS-Installation abschließen** auf **Schließen** , wenn die Installation erfolgreich abgeschlossen wurde.

2.  Der WSUS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Informationen auf der Seite **Vorbemerkungen** , und klicken Sie dann auf **Weiter**.

3.  Lesen Sie die Anweisungen auf der Seite **Am Programm zur Verbesserung von Microsoft Update teilnehmen**, und entscheiden Sie, ob Sie am Programm teilnehmen möchten. Wenn Sie am Programm teilnehmen möchten. behalten Sie die Standardauswahl bei, oder deaktivieren Sie das Kontrollkästchen, und klicken Sie dann auf **weiter**.

4.  Auf der Seite **Upstreamserver auswählen** stehen Ihnen zwei Optionen zur Verfügung:

    1.  Updates mit Microsoft Update synchronisieren

    2.  Von einem anderen Windows Server Update Services-Server synchronisieren

        -   Wenn Sie sich für die Synchronisierung von einem anderen WSUS-Server entscheiden, geben Sie den Servernamen und den Port an, auf dem dieser Server mit dem Upstreamserver kommunizieren soll.

        -   Wenn Sie SSL verwenden möchten, aktivieren Sie das Kontrollkästchen **SSL beim Synchronisieren der Updateinformationen verwenden** . Die Server verwenden den Port 443 für die Synchronisierung. (Stellen Sie sicher, dass dieser Server und der Upstreamserver SSL unterstützen).

        -   Wenn es sich um einen Replikat Server handelt, aktivieren Sie das Kontrollkästchen **Dies ist ein Replikat des** Upstreamservers.

5.  Nachdem Sie die entsprechenden Optionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter**, um fortzufahren.

6.  Aktivieren Sie auf der Seite **Proxyserver angeben** das Kontrollkästchen **Proxyserver für die Synchronisierung verwenden** , und geben Sie dann den Namen des Proxyservers und die Portnummer (standardmäßig Port 80) in die entsprechenden Felder ein.

    > [!IMPORTANT]
    > Dieser Schritt muss ausgeführt werden, wenn WSUS einen Proxyserver für den Internetzugriff benötigt.

7.  Wenn Sie mithilfe bestimmter Benutzer Anmelde Informationen eine Verbindung mit dem Proxy Server herstellen möchten, aktivieren Sie das Kontrollkästchen **Benutzer Anmelde Informationen zum Herstellen einer Verbindung mit dem Proxy Server verwenden** , und geben Sie dann den Benutzernamen, die Domäne und das Kennwort des Benutzers in die entsprechenden Felder ein. Wenn Sie für den Benutzer, der eine Verbindung mit dem Proxy Server herstellt, die Standard Authentifizierung aktivieren möchten, aktivieren Sie das Kontrollkästchen Standard **Authentifizierung zulassen (Kennwort wird in Klartext gesendet)** .

8.  Klicken Sie auf **Weiter**. Klicken Sie auf der Seite **mit Upstreamserver verbinden** auf **Verbindung starten**.

9. Wenn die Verbindung hergestellt wurde, klicken Sie auf **Weiter** , um fortzufahren.

10. Auf der Seite **Sprachen auswählen** können Sie die Sprachen auswählen, von denen WSUS Updates empfängt, alle Sprachen oder eine Teilmenge von Sprachen. Wenn Sie eine Teilmenge von Sprachen auswählen, sparen Sie Speicherplatz. es ist jedoch wichtig, alle Sprachen auszuwählen, die für alle Clients dieses WSUS-Servers erforderlich sind. Wenn Sie Updates nur für bestimmte Sprachen herunterladen möchten, wählen Sie **Updates nur in diesen Sprachen herunterladen**aus, und wählen Sie dann die gewünschten Sprachen aus. überlassen Sie andernfalls die Standardauswahl.

    > [!WARNING]
    > Wenn Sie die Option **Updates nur in folgenden Sprachen herunterladen** auswählen und ein WSUS-Downstreamserver mit dem Server verbunden ist, werden für den Downstreamserver ebenfalls nur die ausgewählten Sprachen verwendet.

11. Nachdem Sie die entsprechenden Sprachoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

12. Auf der Seite **Produkte auswählen** können Sie die Produkte angeben, für die Sie Updates herunterladen möchten. Wählen Sie Produktkategorien wie Windows oder bestimmte Produkte wie Windows Server 2008 aus. durch die Auswahl einer Produktkategorie werden alle Produkte in dieser Kategorie ausgewählt.

13. Wählen Sie die entsprechenden Produktoptionen für Ihre Bereitstellung aus, und klicken Sie dann auf **weiter**.

14. Wählen Sie auf der Seite **Klassifizierungen auswählen** die gewünschten Updateklassifizierungen aus. Sie können alle Klassifizierungen oder eine Teilmenge auswählen. Klicken Sie anschließend auf **Weiter**.

15. Auf der Seite **Synchronisierungszeitplan festlegen** können Sie auswählen, ob die Synchronisierung manuell oder automatisch ausgeführt werden soll.

    -   Wenn Sie **manuell synchronisieren**auswählen, müssen Sie den Synchronisierungs Prozess über die WSUS-Verwaltungskonsole starten.

    -   Wenn Sie **automatisch synchronisieren**auswählen, wird der WSUS-Server in festgelegten Intervallen synchronisiert.

    Legen Sie die Zeit für **Erste Synchronisierung**fest, und geben Sie die Anzahl von **Synchronisierungen pro Tag** an, die dieser Server ausführen soll. Wenn Sie z. B. vier Synchronisierungen pro Tag mit der ersten Synchronisierung um 3:00 Uhr festlegen, finden um 3:00 Uhr, 9:00 Uhr, 15:00 Uhr und 21:00 Uhr Synchronisierungen statt

16. Nachdem Sie die entsprechenden Synchronisierungsoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

17. Auf der Seite **Fertig gestellt** haben Sie die Möglichkeit, die Synchronisierung direkt zu starten, indem Sie das Kontrollkästchen **Erstsynchronisierung starten** aktivieren. Wenn Sie diese Option nicht auswählen, müssen Sie die WSUS-Verwaltungskonsole verwenden, um die erst Synchronisierung auszuführen. Klicken Sie auf **Weiter** , wenn Sie mehr über zusätzliche Einstellungen erfahren möchten, oder auf **Fertig stellen** , um den Assistenten zu beenden und die WSUS-Erstkonfiguration abzuschließen.

18. Nach dem Klicken auf **Fertig stellen**wird die WSUS-Verwaltungskonsole angezeigt.

Damit ist die grundlegende WSUS-Konfiguration abgeschlossen. Lesen Sie jetzt die nächsten Abschnitte, um mehr über das Ändern der Einstellungen mithilfe der WSUS-Verwaltungskonsole zu erfahren.

## <a name="23-configure-wsus-computer-groups"></a>2.3. Konfigurieren von WSUS-Computer Gruppen
Computer Gruppen sind ein wichtiger Bestandteil von Windows Server Update Services (WSUS)-bereit Stellungen. Mithilfe von Computergruppen können Sie Updates testen und gezielt für bestimmte Computer anwenden. Es gibt die folgenden zwei Standardcomputergruppen: Alle Computer und nicht zugewiesene Computer. Standardmäßig fügt der WSUS-Server jeden Clientcomputer bei der ersten Verbindungsherstellung mit dem Server einer dieser beiden Gruppen hinzu.

Sie können beliebig viele benutzerdefinierte Computergruppen erstellen, um Updates in Ihrer Organisation zu verwalten. Es wird empfohlen, mindestens eine Computergruppe zu erstellen, mit der Updates getestet werden können, bevor sie auf anderen Computern in der Organisation bereitgestellt werden.

Gehen Sie wie im Folgenden beschrieben vor, um eine neue Gruppe zu erstellen und ihr einen Computer zuzuweisen:

#### <a name="to-create-a-computer-group"></a>So erstellen Sie eine Computergruppe

1.  Erweitern Sie in der WSUS-Verwaltungskonsole unter **Update Services**den WSUS-Server, erweitern Sie **Computer**, klicken Sie mit der rechten Maustaste auf **alle Computer**, und klicken Sie dann auf **Computergruppe hinzufügen**.

2.  Geben Sie im Dialogfeld **Computergruppe hinzufügen** unter **Name**den Namen der neuen Gruppe an, und klicken Sie dann auf **Hinzufügen**.

3.  Klicken Sie auf **Computer**, und wählen Sie dann die Computer aus, die Sie dieser neuen Gruppe zuweisen möchten.

4.  Klicken Sie mit der rechten Maustaste auf die Computernamen, die Sie im vorherigen Schritt ausgewählt haben, und klicken Sie dann auf **Mitgliedschaft ändern**.

5.  Wählen Sie im Dialogfeld **Computer Gruppenmitgliedschaft festlegen** die erstellte Testgruppe aus, und klicken Sie dann auf **OK**.

## <a name="24-configure-client-updates"></a>2.4. Konfigurieren von Clientupdates
Beim WSUS-Setup wird IIS automatisch so konfiguriert, dass die aktuelle Version von %%amp;quot;Automatische Updates%%amp;quot; an jeden Clientcomputer verteilt wird, der eine Verbindung mit dem WSUS-Server herstellt. Die für %%amp;quot;Automatische Updates%%amp;quot; am besten geeignete Konfiguration hängt von der Netzwerkumgebung ab.

-   In einer Umgebung, die den Active Directory-Verzeichnisdienst verwendet, können Sie ein vorhandenes domänenbasiertes Gruppenrichtlinie Objekt (GPO) verwenden oder ein neues GPO erstellen.

-   Verwenden Sie in einer Umgebung ohne Active Directory den Editor für lokale Gruppenrichtlinie, um automatische Updates zu konfigurieren und die Client Computer dann auf den WSUS-Server zu verweisen.

> [!IMPORTANT]
> Bei den folgenden Verfahren wird davon ausgegangen, dass Ihr Netzwerk Active Directory ausführt. Zudem wird vorausgesetzt, dass Sie mit dem Feature %%amp;quot;Gruppenrichtlinie%%amp;quot; vertraut sind und es zum Verwalten des Netzwerks verwenden.

Verwenden Sie die folgenden Verfahren, um %%amp;quot;Automatische Updates%%amp;quot; für Clientcomputer zu konfigurieren:

-   [Schritt 4: Konfigurieren von Gruppenrichtlinien für automatische Updates](4-configure-group-policy-settings-for-automatic-updates.md)

-   [2,3. Konfigurieren von Computer](#23-configure-wsus-computer-groups) Gruppen in diesem Thema

### <a name="configure-automatic-updates-in-group-policy"></a>Konfigurieren von %%amp;quot;Automatische Updates%%amp;quot; in %%amp;quot;Gruppenrichtlinie%%amp;quot;

Wenn Sie Active Directory in Ihrem Netzwerk eingerichtet haben, können Sie einen oder mehrere Computer gleichzeitig konfigurieren, indem Sie Sie in ein Gruppenrichtlinie Objekt (GPO) einschließen und dieses GPO anschließend mit WSUS-Einstellungen konfigurieren. Es wird empfohlen, ein neues GPO zu erstellen, das nur WSUS-Einstellungen enthält.

Verknüpfen Sie dieses WSUS-GPO mit einem Active Directory-Container, der für Ihre Umgebung geeignet ist. In einer einfachen Umgebung reicht es u. U. aus, ein WSUS-GPO mit der Domäne zu verknüpfen. In einer komplexeren Umgebung müssen Sie möglicherweise mehrere WSUS-GPOs mit mehreren Organisationseinheiten (Organizational Unit, OU) verknüpfen, sodass Sie unterschiedliche WSUS-Richtlinieneinstellungen für verschiedene Computertypen anwenden können.

##### <a name="to-enable-wsus-through-a-domain-gpo"></a>So aktivieren Sie WSUS über ein Domänen-GPO

1.  Navigieren Sie in der Gruppenrichtlinien-Verwaltungskonsole (GPMC) zu dem GPO, in dem Sie WSUS konfigurieren möchten, und klicken Sie dann auf **Bearbeiten**.

2.  Erweitern Sie in der GPMC nacheinander **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**und **Windows-Komponenten**, und klicken Sie dann auf **Windows Update**.

3.  Doppelklicken Sie im Detailbereich auf **Automatische Updates konfigurieren**. Die Richtlinie **Automatische Updates konfigurieren** wird geöffnet.

4.  Klicken Sie auf **Aktiviert**, und wählen Sie anschließend eine der folgenden Optionen unter der Einstellung **Automatische Updates konfigurieren** aus:

    -   **Vor Herunterladen und Installation benachrichtigen**. Bei Auswahl dieser Option wird ein angemeldeter Administrator vor dem Herunterladen und Installieren der Updates benachrichtigt.

    -   **Autom. Herunterladen, aber vor Installation benachrichtigen**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend wird ein angemeldeter Administrator benachrichtigt, bevor die Updates installiert werden. Diese Option ist standardmäßig ausgewählt.

    -   **Autom. Herunterladen und laut Zeitplan installieren**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend werden die Updates zu dem von Ihnen angegebenen Zeitpunkt installiert.

    -   **Lokalen Administrator ermöglichen, Einstellung auszuwählen**. Bei Auswahl dieser Option können lokale Administratoren den Bereich %%amp;quot;Automatische Updates%%amp;quot; in der Systemsteuerung verwenden, um eine Konfigurationsoption auszuwählen. Sie können z. B. einen geplanten Installationszeitpunkt auswählen. Lokale Administratoren können %%amp;quot;Automatische Updates%%amp;quot; nicht deaktivieren.

5.  Wählen Sie **Client seitige Zielgruppen Steuerung aktivieren**und dann **aktiviert**aus, und geben Sie dann den Namen der WSUS-Computergruppe, der Sie diesen Computer hinzufügen möchten, in das Feld **Zielgruppen Name für diesen Computer** ein.

    > [!NOTE]
    > Durch die Option **Clientseitige Zielzuordnung aktivieren** können Clientcomputer sich selbst Zielcomputergruppen auf dem WSUS-Server hinzufügen, wenn automatische Updates auf einen WSUS-Server umgeleitet werden. Wenn der Status auf Aktiviert festgelegt ist, wird dieser Computer sich selbst als Mitglied einer bestimmten Computergruppe identifizieren, wenn er Informationen an den WSUS-Server sendet, der ihn verwendet, um zu bestimmen, welche Updates auf diesem Computer bereitgestellt werden. Diese Einstellung zeigt dem WSUS-Server an, welche Gruppe der Clientcomputer verwendet. Sie müssen die Gruppe auf dem WSUS-Server erstellen und ihr Domänenmitgliedscomputer hinzufügen.

6.  Klicken Sie auf **OK**, um die Richtlinie **Clientseitige Zielzuordnung aktivieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

7.  Klicken Sie auf **OK**, um die Richtlinie **Automatische Updates konfigurieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

8.  Doppelklicken Sie im Detailbereich **Windows Update** auf **Internen Pfad für den Microsoft Updatedienst angeben**.

9. Klicken Sie auf **Aktiviert**, und geben Sie dann die URL des gleichen WSUS-Servers in die Felder **Interner Updatedienst zum Ermitteln von Updates** und **Intranetserver für die Statistik** ein. Geben *http://servername* Sie beispielsweise in beide Felder ein (wobei *Server* Name der Name des WSUS-Servers ist).

    > [!WARNING]
    > Beim Eingeben der Intranetadresse des WSUS-Servers muss der zu verwendende Port angegeben werden. Standardmäßig verwendet WSUS den Port 8530 für HTTP und den Port 8531 für HTTPS. Wenn Sie z. b. http verwenden, müssen Sie eingeben **http://servername:8530** .

10. Klicken Sie auf **OK**.

Nach dem Einrichten eines Client Computers dauert es einige Minuten, bis der Computer auf der Seite **Computer** in der WSUS-Verwaltungskonsole angezeigt wird. Bei Clientcomputern, die mit einem domänenbasierten GPO konfiguriert werden, kann es bis zu 20 Minuten dauern, bis die neuen Richtlinieneinstellungen von der Gruppenrichtlinie auf den Clientcomputer angewendet werden. Standardmäßig Gruppenrichtlinie Updates im Hintergrund alle 90 Minuten mit einem zufälligen Offset von 0-30 Minuten. Wenn Sie Gruppenrichtlinie früher aktualisieren möchten, können Sie auf dem Client Computer ein Eingabe Aufforderungs Fenster öffnen und gpupdate/force. eingeben.

bei Client Computern, die mit dem Editor für lokale Gruppenrichtlinie konfiguriert werden, wird das GPO sofort angewendet, und das Update dauert ungefähr 20 Minuten. Wenn Sie die Ermittlung manuell starten, müssen Sie nicht 20 Minuten warten, bis der Client Computer eine Verbindung mit WSUS hergestellt hat.

Da das Warten auf den Start der Ermittlung zeitaufwändig sein kann, können Sie ggf. das folgende Verfahren verwenden, um die Ermittlung sofort zu initiieren.

##### <a name="to-initiate-wsus-detection"></a>So starten Sie die WSUS-Ermittlung

1.  Öffnen Sie auf dem Client Computer ein Eingabe Aufforderungs Fenster mit erhöhten Rechten.

2.  Geben Sie wuauclt. exe/detectnow ein, und drücken Sie dann die EINGABETASTE.

## <a name="25-secure-wsus-with-the-secure-sockets-layer-protocol"></a>2.5. Schützen von WSUS mit dem Secure Sockets Layer-Protokoll

Sie können das Secure Sockets Layer (SSL)-Protokoll zum Sichern der WSUS-Bereitstellung verwenden. SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Server verwendet. SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Updates verwendet.

> [!IMPORTANT]
> Clients und Downstreamserver, die für die Verwendung von Transport Layer Security (TLS) oder HTTPS konfiguriert werden, müssen auch zur Verwendung eines vollqualifizierten Domänennamens (FQDN) für WSUS-Upstreamserver konfiguriert werden.

SSL wird von WSUS nur für Metadaten und nicht für Updatedateien verwendet. Auf diese Weise verteilt auch Microsoft Update die Updates. Microsoft reduziert das Risiko beim Senden von Updatedateien über einen unverschlüsselten Kanal, indem jedes Update signiert wird. Darüber hinaus wird ein Hashwert berechnet und zusammen mit den Metadaten für jedes Update gesendet. Wenn ein Update heruntergeladen wird, überprüft WSUS die digitale Signatur und den Hashwert. Wenn das Update geändert wurde, wird es nicht installiert.

### <a name="limitations-of-wsus-ssl-deployments"></a>Einschränkungen von WSUS-SSL-Bereitstellungen
Berücksichtigen Sie bei Verwendung von SSL zum Sichern der WSUS-Bereitstellung die folgenden Einschränkungen:

1.  Die Verwendung von SSL erhöht die Auslastung des Servers. Sie sollten aufgrund des Aufwands zur Verschlüsselung aller Metadaten, die über das Netzwerk gesendet wird, von einem Leistungsverlust von 10 % ausgehen.

2.  Wenn Sie WSUS mit einer SQL Server-Remotedatenbank verwenden, wird die Verbindung zwischen dem WSUS-Server und dem Datenbankserver nicht durch SSL gesichert. Wenn die Verbindung mit der Datenbank gesichert werden muss, sollten Sie folgende Empfehlungen berücksichtigen:

-   Verschieben Sie die WSUS-Datenbank auf den WSUS-Server.

-   Verschieben Sie den Remote-Datenbankserver und den WSUS-Server in ein privates Netzwerk.

-   Stellen Sie die Internet Protokoll Sicherheit (IPSec) bereit, um den Netzwerk Datenverkehr zu sichern. Weitere Informationen zu IPsec finden Sie unter [Creating and Using IPsec Policies](https://go.microsoft.com/fwlink/?LinkID=203841).

### <a name="configure-ssl-on-the-wsus-server"></a>Konfigurieren von SSL auf dem WSUS-Server
WSUS erfordert zwei Ports für SSL: einen Port, der HTTPS für das Senden verschlüsselter Metadaten verwendet, und einen Port, der HTTP für das Senden der Updates verwendet. Beachten Sie beim Konfigurieren von WSUS für SSL Folgendes:

-   Sie können nicht die gesamte WSUS-Website so konfigurieren, dass SSL erforderlich ist, da der gesamte Datenverkehr an die WSUS-Website verschlüsselt werden müsste. WSUS verschlüsselt nur Updatemetadaten. Wenn ein Computer versucht, Update Dateien auf dem HTTPS-Port abzurufen, schlägt die Übertragung fehl.

    Sie sollten SSL nur für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **SimpleAuthWebService**

    -   **DssAuthWebService**

    -   **ServerSyncWebService**

    -   **APIremoting30**

    -   **Clientweb Service**

    Sie sollten SSL nicht für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **Inhalt**

    -   **Lager**

    -   **Berichterstattungsweb Diensts**

    -   **Selbst Aktualisierungs**

-   Das Zertifikat der Zertifizierungsstelle (CA) muss in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computerspeichers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service auf WSUS-Downstreamservern importiert werden. Wenn das Zertifikat nur in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Benutzers importiert wird, wird der Downstream-WSUS-Server nicht auf dem Upstreamserver authentifiziert.

    Weitere Informationen zur Verwendung von SSL-Zertifikaten in IIS finden Sie unter [erforderliche Secure Sockets Layer (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=203846).

-   Sie müssen das Zertifikat auf allen Computern importieren, die mit dem WSUS-Server kommunizieren. Dies umfasst alle Clientcomputer, Downstreamserver und Computer, auf denen die WSUS-Verwaltungskonsole ausgeführt wird. Das Zertifikat sollte in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service importiert werden.

-   Sie können einen beliebigen Port für SSL verwenden. Der Port, den Sie für SSL eingerichtet haben, bestimmt jedoch auch den Port, über den WSUS unverschlüsselt den HTTP-Datenverkehr sendet. Beachten Sie folgende Beispiele:

    -   Wenn Sie den Branchen Standardport 443 für HTTPS-Datenverkehr verwenden, verwendet WSUS den Industriestandard-Port 80 für den HTTP-Datenverkehr.

    -   Wenn Sie einen anderen Port als 443 für HTTPS-Datenverkehr verwenden, sendet WSUS unverschlüsselten HTTP-Datenverkehr über den Port, der numerisch vor dem Port für HTTPS steht. Wenn Sie beispielsweise Port 8531 für HTTPS verwenden, wird WSUS Port 8530 für HTTP verwendet.

-   Sie müssen *ClientServicingProxy* erneut initialisieren, wenn der Servername, die SSL-Konfiguration oder die Portnummer geändert wird.

##### <a name="to-configure-ssl-on-the-wsus-root-server"></a>So konfigurieren Sie SSL auf dem WSUS-Server

1.  Melden Sie sich bei dem WSUS-Server mit einem Konto an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Wechseln Sie zu **Start**, geben Sie **cmd**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**

3.  Navigieren Sie zu der *%ProgramFiles%***\Update Services\Tools\\* * Ordner.

4.  Geben Sie im Eingabe Aufforderungs Fenster den folgenden Befehl ein:

    **Wsusutil configuressl** *certificateName*

    Dabei gilt:

    *certificateName* ist der DNS-Name des WSUS-Servers.

### <a name="configure-ssl-on-client-computers"></a>Konfigurieren von SSL auf Clientcomputern
Wenn Sie SSL auf Clientcomputern konfigurieren, sollten Sie Folgendes berücksichtigen:

-   Sie müssen eine URL für einen sicheren Port auf dem WSUS-Server einschließen. Da SSL auf dem Server nicht erzwungen werden kann, können Sie nur sicherstellen, dass der Clientcomputer einen sicheren Kanal verwenden kann, indem eine URL genutzt wird, die HTTPS angibt. Wenn Sie einen anderen Port als 443 für SSL verwenden, müssen Sie auch diesen Port in die URL einschließen.

-   Das Zertifikat auf einem Client Computer muss in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers oder in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers importiert werden. Wenn das Zertifikat nur in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Benutzers importiert wird, schlägt die Server Authentifizierung automatische Updates fehl.

-   Die Clientcomputer müssen dem Zertifikat vertrauen, das Sie an den WSUS-Server binden. Je nach verwendetem Zertifikattyp müssen Sie möglicherweise einen Dienst einrichten, sodass die Clientcomputer dem an den WSUS-Server gebundenen Zertifikat vertrauen.

### <a name="configure-ssl-for-downstream-wsus-servers"></a>Konfigurieren von SSL für WSUS-Downstreamserver
Die folgenden Anweisungen dienen der Konfiguration der Synchronisierung eines Downstreamservers mit einem Upstreamserver, der SSL verwendet.

##### <a name="to-synchronize-a-downstream-server-to-an-upstream-server-that-uses-ssl"></a>So synchronisieren Sie einen Downstreamserver mit einem Upstreamserver, der SSL verwendet

1.  Melden Sie sich mit einem Konto beim Computer an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Klicken Sie im **Startmenü**auf **Alle Programme**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server Update Service**.

3.  Erweitern Sie im rechten Bereich den Namen des Servers.

4.  Klicken Sie auf **Optionen**und dann auf **Updatequelle und Proxyserver**.

5.  Wählen Sie auf der Seite **Updatequelle** die Option **Von einem Windows Server Update Services-Server synchronisieren**aus.

6.  Geben Sie den Namen des Upstreamservers in das Textfeld **Servername** ein. Geben Sie die Portnummer ein, die vom Server für SSL-Verbindungen in das Textfeld **Portnummer** verwendet wird.

7.  Aktivieren Sie das Kontrollkästchen **SSL beim Synchronisieren der Update Informationen verwenden** , und klicken Sie dann auf **OK**.

### <a name="additional-ssl-resources"></a>Zusätzliche SSL-Ressourcen
Die Schritte zum Einrichten einer Zertifizierungsstelle, zum Binden des Zertifikats an die WSUS-Website und zum Einrichten einer Vertrauensstellung zwischen Clientcomputern und Zertifikat gehen über den Rahmen dieses Handbuchs hinaus. Weitere Informationen und eine Anleitung zum Installieren von Zertifikaten sowie zum Einrichten der Umgebung finden Sie in den folgenden Themen:

-   [Schritt-für-Schritt-Anleitung für Suite B PKI](https://go.microsoft.com/fwlink/?LinkID=203858)

-   [Implementieren und Verwalten von Zertifikat Vorlagen](https://go.microsoft.com/fwlink/?LinkID=203859)

-   [Handbuch für die Aktualisierung und Migration von Active Directory-Zertifikat Diensten](https://go.microsoft.com/fwlink/?LinkID=203860)

-   [Konfigurieren der automatischen Registrierung von Zertifikaten](https://go.microsoft.com/fwlink/?LinkID=203861)

### <a name="26-complete-iis-configuration"></a>2.6. Abschluss der IIS-Konfiguration
Standardmäßig ist der anonyme Lesezugriff für die Standardwebsite und alle neuen IIS-Websites aktiviert. Einige Programme, vor allem Windows SharePoint Services, können den anonymen Zugriff entfernen. Wenn dies der Fall ist, müssen Sie den anonymen Lesezugriff erneut aktivieren, bevor Sie WSUS erfolgreich installieren und ausführen können.

Führen Sie die Schritte für die entsprechende Version von IIS aus, um anonymen Lesezugriff zu aktivieren:

1.  [Enable Anonymous Authentication (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=205316)– IIS 7-Handbuch.

2.  [Enabling Anonymous Authentication (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=211391)– IIS 6.0-Handbuch.

### <a name="27-configure-a-signing-certificate"></a>2.7. Konfigurieren eines Signaturzertifikats
WSUS bietet die Möglichkeit, benutzerdefinierte Updatepakete für Produkte von Microsoft und andere Produkte zu veröffentlichen. WSUS kann diese benutzerdefinierten Updatepakete für Sie automatisch mit einem Authenticode-Zertifikat signieren. Um die Signatur von benutzerdefinierten Updates zu aktivieren, müssen Sie ein Paketsignaturzertifikat auf dem WSUS-Server installieren. Bei der Signatur benutzerdefinierter Updates sind verschiedene Aspekte zu beachten.

1.  **Zertifikatverteilung**. Der private Schlüssel muss auf dem WSUS-Server installiert sein, und der öffentliche Schlüssel muss explizit im Speicher für vertrauenswürdige Zertifikate auf allen Client-PCs und Servern installiert werden, die benutzerdefinierte signierte Updates erhalten sollen.

2.  **Ablaufdatum**. Wenn das selbstsignierte Zertifikat abläuft oder sich das Ablaufdatum nähert, protokolliert WSUS entsprechende Ereignisse im Ereignisprotokoll.

3.  **Zertifikatupdates/Zertifikatsperre**. Wenn Sie ein Zertifikat aktualisieren oder widerrufen möchten (d. h. Nachdem Sie festgestellt haben, dass es abgelaufen ist), hat WSUS keine Funktionalität angeboten, um dies zu ermöglichen. Dafür mussten manuelle Aufgaben ausgeführt werden, die entweder sehr schwierig manuell auszuführen waren oder sich schlecht automatisieren ließen.


