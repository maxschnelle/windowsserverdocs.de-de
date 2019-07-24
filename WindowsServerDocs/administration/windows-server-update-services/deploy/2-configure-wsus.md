---
title: 'Schritt 2: Konfigurieren von WSUS'
description: Windows Server Update Service (WSUS)-Thema – Konfigurieren von WSUS ist Schritt 2 in vier Schritten für die Bereitstellung von WSUS
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: d4adc568-1f23-49f3-9a54-12a7bec5f27c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae151c2a6f0f5ef72b263fbe7f1f0d26933452af
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811000"
---
# <a name="step-2-configure-wsus"></a>Schritt 2: Konfigurieren von WSUS

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Nachdem Sie die WSUS-Serverrolle auf dem Server installiert haben, müssen Sie sie korrekt konfigurieren. Die folgende Checkliste werden die Schritte zum Ausführen der anfänglichen Konfigurations für den WSUS-Server zusammengefasst.

|Aufgabe|Beschreibung|
|----|--------|
|[2.1. Konfigurieren der Netzwerkverbindungen](#21-configure-network-connections)|Konfigurieren Sie das Clusternetzwerk mithilfe des Netzwerkkonfigurations-Assistenten.|
|[2.2. Konfigurieren von WSUS mithilfe der WSUS-Konfigurations-Assistent](#22-configure-wsus-by-using-the-wsus-configuration-wizard)|Verwenden Sie den WSUS-Konfigurations-Assistenten, um die WSUS-Basiskonfiguration auszuführen.|
|[2.3. Konfigurieren von WSUS-Computergruppen](#23-configure-wsus-computer-groups)|Erstellen Sie Computergruppen in der WSUS-Verwaltungskonsole zum Verwalten von Updates in Ihrer Organisation.|
|[2.4. Konfigurieren von Clientupdates](#24-configure-client-updates)|Geben Sie an, wie und wann automatische Updates auf Clientcomputern angewendet werden.|
|[2.5. Schützen von WSUS mit dem Secure Sockets Layer-Protokoll](#25-secure-wsus-with-the-secure-sockets-layer-protocol)|Konfigurieren Sie das Secure Sockets Layer (SSL)-Protokoll zum Schutz von Windows Server Update Services (WSUS).|

## <a name="21-configure-network-connections"></a>2.1. Konfigurieren der Netzwerkverbindungen
Bevor Sie mit der Konfiguration beginnen, müssen Sie sich die folgenden Fragen beantworten:

1.  Ist die Firewall des Servers so konfiguriert, dass Clients auf den Server zugreifen können?

2.  Kann dieser Computer eine Verbindung mit dem Upstreamserver herstellen (z. B. dem Server, der zum Herunterladen von Updates von Microsoft Update verwendet wird)?

3.  Kennen Sie den Namen des Proxyservers und die Benutzeranmeldeinformationen für den Proxyserver, falls Sie sie benötigen?

In der Standardkonfiguration ruft WSUS Updates von Microsoft Update ab. Wenn Sie einen Proxyserver im Netzwerk verfügen, können Sie WSUS zur Verwendung des Proxyservers konfigurieren. liegt eine Unternehmensfirewall zwischen WSUS und dem Internet, müssen Sie möglicherweise die Firewall so konfigurieren, stellen Sie sicher, dass WSUS Updates abrufen kann.

> [!TIP]
> Obwohl Internetkonnektivität erforderlich ist, um Updates von Microsoft Update herunterzuladen, bietet WSUS die Möglichkeit, Updates in Netzwerke zu importieren, die nicht mit dem Internet verbunden sind.

Wenn Sie die Antworten auf diese Fragen kennen, können Sie mit der Konfiguration der folgenden WSUS-Netzwerkeinstellungen beginnen:

-   **Updates** Geben Sie an, wie dieser Server Updates abruft (von Microsoft Update oder von einem anderen WSUS-Server).

-   **Proxy** , wenn Sie ermittelt, dass WSUS einen Proxyserver verwenden, auf das Internet zugreifen muss, müssen Sie Proxyeinstellungen im WSUS-Server zu konfigurieren.

-   **Firewall** , wenn Sie ermittelt, dass WSUS hinter einer Unternehmensfirewall befindet, stehen Ihnen einige zusätzliche Schritte, die auf dem Edge-Gerät, um den WSUS-Datenverkehr korrekt zuzulassen ausgeführt werden.

### <a name="211-connection-from-the-wsus-server-to-the-internet"></a>2.1.1. Verbindung zwischen WSUS-Server und Internet
Falls eine Unternehmensfirewall zwischen WSUS und dem Internet vorhanden ist, müssen Sie sie ggf. konfigurieren, um sicherzustellen, dass WSUS Updates abrufen kann. Der WSUS-Server verwendet den Port 443 für das HTTPS-Protokoll, um Updates von Microsoft Update herunterzuladen. Obwohl die meisten Unternehmensfirewalls zu diese Art von Datenverkehr ermöglichen, sind einige Unternehmen, die Zugriff auf das Internet der Server aber aufgrund der Sicherheitsrichtlinien des Unternehmens zu beschränken. Wenn Ihr Unternehmen den Zugriff einschränkt, müssen Sie Autorisierung, um Zugriff auf das Internet von WSUS zu ermöglichen, mit der folgenden Liste von URLs zu erhalten:

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
> Ein Szenario, in dem WSUS Fehler beim Abrufen des Updates aufgrund von Firewallkonfigurationen, finden Sie [Artikel 885819](https://support.microsoft.com/kb/885819) in der Microsoft Knowledge Base.

Im folgenden Abschnitt wird beschrieben, wie eine Unternehmensfirewall zwischen WSUS und dem Internet konfiguriert wird. Da WSUS den gesamten Netzwerkdatenverkehr initiiert, ist es nicht erforderlich, Windows-Firewall auf dem WSUS-Server zu konfigurieren. Obwohl die Verbindung zwischen Microsoft Update und WSUS erfordert, dass die Ports 80 und 443 geöffnet sind, können Sie mehrere WSUS-Server zur Synchronisierung mit einem benutzerdefinierten Port konfigurieren.

### <a name="212-connection-between-wsus-servers"></a>2.1.2. Verbindung zwischen WSUS-Servern
Upstream- und Downstream-WSUS-Server werden auf dem Port synchronisiert, der vom WSUS-Administrator konfiguriert wurde. Diese Ports sind standardmäßig folgendermaßen konfiguriert:

-   Bei WSUS 3.2 und früher: Port 80 für HTTP und 443 für HTTPS

-   Bei WSUS 6.2 und höher (mindestens Windows Server 2012),-port 8530 für HTTP und 8531 für HTTPS verwendet werden

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

3.  Öffnen Sie eine Eingabeaufforderung (Cmd.exe) als Administrator. Wählen Sie zum Öffnen einer Eingabeaufforderung als Administrator **Start**aus. In **Suche starten**, Typ **Eingabeaufforderung**. am oberen Rand des Startmenüs, Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**. Wenn die **User Account Control** Dialogfeld angezeigt wird, geben Sie die entsprechenden Anmeldeinformationen (falls angefordert), und bestätigen Sie, dass die Aktion angezeigt wird, was Sie möchten, und klicken Sie dann auf **Weiter**.

4.  Das Eingabeaufforderungsfenster wechseln Sie zum Ordner c:\Programme\Microsoft Programme\Update Services\Tools. Geben Sie den folgenden Befehl ein:

    **WSUSUTIL ConfigureSSlproxy [< Proxyserver Proxyport >]-aktivieren**, wobei:

    1.  Proxyserver für den Namen des Proxyservers steht, der HTTPS unterstützt.

    2.  Proxyport die Portnummer des Proxyservers ist.

5.  Schließen Sie das Eingabeaufforderungsfenster.

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

    4.  FF der Proxyserver erfordert, dass Sie ein bestimmtes Benutzerkonto verwenden, wählen Sie die **Benutzeranmeldeinformationen für die Verbindung mit dem Proxyserver verwenden** Kontrollkästchen. Geben Sie die erforderlichen Benutzer, Domäne, und ein Kennwort in die entsprechenden Textfelder ein.

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
    > Wenn die **WSUS-Installation abschließen** klicken Sie im angezeigten Dialogfeld **ausführen**. In der **WSUS-Installation abschließen** Dialogfeld klicken Sie auf **schließen** Wenn die Installation erfolgreich abgeschlossen wurde.

2.  Der WSUS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Informationen auf der Seite **Vorbemerkungen** , und klicken Sie dann auf **Weiter**.

3.  Lesen Sie die Anweisungen auf der Seite **Am Programm zur Verbesserung von Microsoft Update teilnehmen**, und entscheiden Sie, ob Sie am Programm teilnehmen möchten. Wenn Sie am Programm teilnehmen möchten. die Standardauswahl beibehalten oder deaktivieren Sie dieses Kontrollkästchen, und klicken Sie dann auf **Weiter**.

4.  Auf der Seite **Upstreamserver auswählen** stehen Ihnen zwei Optionen zur Verfügung:

    1.  Updates mit Microsoft Update synchronisieren

    2.  Von einem anderen Windows Server Update Services-Server synchronisieren

        -   Wenn Sie von einem anderen WSUS-Server synchronisieren möchten, geben Sie den Servernamen und den Port auf dem dieser Server kommuniziert mit dem Upstreamserver.

        -   Wenn Sie SSL verwenden möchten, aktivieren Sie das Kontrollkästchen **SSL beim Synchronisieren der Updateinformationen verwenden** . Die Server verwenden den Port 443 für die Synchronisierung. (Stellen Sie sicher, dass dieser Server und der Upstreamserver SSL unterstützen).

        -   Wenn es sich um einen Replikatserver handelt, wählen Sie die **Dies ist ein Replikat des Upstreamservers** Kontrollkästchen.

5.  Nachdem Sie die entsprechenden Optionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter**, um fortzufahren.

6.  Aktivieren Sie auf der Seite **Proxyserver angeben** das Kontrollkästchen **Proxyserver für die Synchronisierung verwenden** , und geben Sie dann den Namen des Proxyservers und die Portnummer (standardmäßig Port 80) in die entsprechenden Felder ein.

    > [!IMPORTANT]
    > Dieser Schritt muss ausgeführt werden, wenn WSUS einen Proxyserver für den Internetzugriff benötigt.

7.  Sollten Sie mit dem Proxyserver herstellen von Verbindungen mithilfe von spezifischen Anmeldeinformationen, wählen Sie die **Benutzeranmeldeinformationen für die Verbindung mit dem Proxyserver verwenden** , und geben Sie dann in der entsprechenden der Benutzername, Domäne und das Kennwort des Benutzers zu deaktivieren. Wenn Sie die Standardauthentifizierung für den Benutzer aktivieren, die eine Verbindung mit dem Proxyserver herstellt möchten die **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** das Kontrollkästchen.

8.  Klicken Sie auf **Weiter**. Auf der **mit Upstreamserver verbinden** auf **Herstellen einer Verbindung starten**.

9. Wenn die Verbindung hergestellt wurde, klicken Sie auf **Weiter** , um fortzufahren.

10. Auf der **Sprachen auswählen** Seite haben Sie die Möglichkeit, die die Sprachen auswählen, aus dem WSUS-Updates – alle Sprachen oder eine Teilmenge von Sprachen empfängt. Auswahl einer Teilmenge von Sprachen sparen Sie Speicherplatz, aber es ist wichtig, alle Sprachen auszuwählen, die von allen Clients des WSUS-Servers erforderlich sind. Wenn Sie nur für bestimmte Sprachen Updates abrufen möchten, wählen Sie **Updates nur in folgenden Sprachen herunterladen**, und wählen Sie dann die Sprachen für den Sie die Updates werden soll, andernfalls lassen Sie die Standardauswahl.

    > [!WARNING]
    > Wenn Sie die Option **Updates nur in folgenden Sprachen herunterladen** auswählen und ein WSUS-Downstreamserver mit dem Server verbunden ist, werden für den Downstreamserver ebenfalls nur die ausgewählten Sprachen verwendet.

11. Nachdem Sie die entsprechenden Sprachoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

12. Auf der Seite **Produkte auswählen** können Sie die Produkte angeben, für die Sie Updates herunterladen möchten. Wählen Sie Produktkategorien wie Windows oder bestimmte Produkte wie Windows Server 2008. eine Produktkategorie auswählen, werden alle Produkte in dieser Kategorie auswählt.

13. Wählen Sie die entsprechenden Produktoptionen für Ihre Bereitstellung, und klicken Sie dann auf **Weiter**.

14. Wählen Sie auf der Seite **Klassifizierungen auswählen** die gewünschten Updateklassifizierungen aus. Sie können alle Klassifizierungen oder eine Teilmenge auswählen. Klicken Sie anschließend auf **Weiter**.

15. Auf der Seite **Synchronisierungszeitplan festlegen** können Sie auswählen, ob die Synchronisierung manuell oder automatisch ausgeführt werden soll.

    -   auf Wunsch **manuell synchronisieren**, müssen Sie die Synchronisierung über die WSUS-Verwaltungskonsole starten.

    -   auf Wunsch **automatisch synchronisieren**, der WSUS-Server die Synchronisierung in festgelegten Intervallen.

    Legen Sie die Zeit für **Erste Synchronisierung**fest, und geben Sie die Anzahl von **Synchronisierungen pro Tag** an, die dieser Server ausführen soll. Wenn Sie z. B. vier Synchronisierungen pro Tag mit der ersten Synchronisierung um 3:00 Uhr festlegen, finden um 3:00 Uhr, 9:00 Uhr, 15:00 Uhr und 21:00 Uhr Synchronisierungen statt

16. Nachdem Sie die entsprechenden Synchronisierungsoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

17. Auf der Seite **Fertig gestellt** haben Sie die Möglichkeit, die Synchronisierung direkt zu starten, indem Sie das Kontrollkästchen **Erstsynchronisierung starten** aktivieren. Wenn Sie diese Option nicht auswählen, müssen Sie WSUS-Verwaltungskonsole zu verwenden, um die erste Synchronisierung durchführen. Klicken Sie auf **Weiter** , wenn Sie mehr über zusätzliche Einstellungen erfahren möchten, oder auf **Fertig stellen** , um den Assistenten zu beenden und die WSUS-Erstkonfiguration abzuschließen.

18. Nach dem Klicken auf **Fertig stellen**wird die WSUS-Verwaltungskonsole angezeigt.

Damit ist die grundlegende WSUS-Konfiguration abgeschlossen. Lesen Sie jetzt die nächsten Abschnitte, um mehr über das Ändern der Einstellungen mithilfe der WSUS-Verwaltungskonsole zu erfahren.

## <a name="23-configure-wsus-computer-groups"></a>2.3. Konfigurieren von WSUS-Computergruppen
Computergruppen sind ein wichtiger Bestandteil der Windows Server Update Services (WSUS)-Bereitstellungen. Mithilfe von Computergruppen können Sie Updates testen und gezielt für bestimmte Computer anwenden. Es gibt die folgenden zwei Standardcomputergruppen: Alle Computer und nicht zugewiesene Computer. Standardmäßig fügt der WSUS-Server jeden Clientcomputer bei der ersten Verbindungsherstellung mit dem Server einer dieser beiden Gruppen hinzu.

Sie können beliebig viele benutzerdefinierte Computergruppen erstellen, um Updates in Ihrer Organisation zu verwalten. Es wird empfohlen, mindestens eine Computergruppe zu erstellen, mit der Updates getestet werden können, bevor sie auf anderen Computern in der Organisation bereitgestellt werden.

Gehen Sie wie im Folgenden beschrieben vor, um eine neue Gruppe zu erstellen und ihr einen Computer zuzuweisen:

#### <a name="to-create-a-computer-group"></a>So erstellen Sie eine Computergruppe

1.  In der WSUS-Verwaltungskonsole unter **Updatedienste**, erweitern Sie den WSUS-Server, erweitern Sie **Computer**, mit der rechten Maustaste **alle Computer**, und klicken Sie dann auf **Computer Gruppe hinzufügen**.

2.  In der **Computer Gruppe hinzufügen** Dialogfeld **Namen**, geben Sie den Namen der neuen Gruppe ein, und klicken Sie dann **hinzufügen**.

3.  Klicken Sie auf **Computer**, und wählen Sie dann auf die Computern, die Sie zu dieser neuen Gruppe zuweisen möchten.

4.  Mit der rechten Maustaste in den Namen der Computer, die Sie im vorherigen Schritt ausgewählt haben, und klicken Sie dann auf **ändern Mitgliedschaft**.

5.  In der **legen Sie die Computer der Gruppenmitgliedschaft** (Dialogfeld), wählen Sie der Test zu gruppieren, die Sie erstellt, und klicken Sie dann auf **OK**.

## <a name="24-configure-client-updates"></a>2.4. Konfigurieren von Clientupdates
Beim WSUS-Setup wird IIS automatisch so konfiguriert, dass die aktuelle Version von %%amp;quot;Automatische Updates%%amp;quot; an jeden Clientcomputer verteilt wird, der eine Verbindung mit dem WSUS-Server herstellt. Die für %%amp;quot;Automatische Updates%%amp;quot; am besten geeignete Konfiguration hängt von der Netzwerkumgebung ab.

-   In einer Umgebung, die active Directory-Dienst verwendet wird, können Sie einen vorhandenen domänenbasierten Gruppenrichtlinienobjekt (GPO) verwenden oder ein neues GPO erstellen.

-   Klicken Sie in einer Umgebung ohne active Directory verwenden Sie den lokalen Gruppenrichtlinien-Editor, um automatische Updates konfigurieren, und zeigen Sie dann die Client-Computer, auf dem WSUS-Server.

> [!IMPORTANT]
> Die folgenden Verfahren wird davon ausgegangen, dass Ihr Netzwerk mit active Directory ausgeführt wird. Zudem wird vorausgesetzt, dass Sie mit dem Feature %%amp;quot;Gruppenrichtlinie%%amp;quot; vertraut sind und es zum Verwalten des Netzwerks verwenden.

Verwenden Sie die folgenden Verfahren, um %%amp;quot;Automatische Updates%%amp;quot; für Clientcomputer zu konfigurieren:

-   [Schritt 4: Konfigurieren von Gruppenrichtlinien für automatische Updates](4-configure-group-policy-settings-for-automatic-updates.md)

-   [2.3. Konfigurieren von Computergruppen](#23-configure-wsus-computer-groups) in diesem Thema

### <a name="configure-automatic-updates-in-group-policy"></a>Konfigurieren von %%amp;quot;Automatische Updates%%amp;quot; in %%amp;quot;Gruppenrichtlinie%%amp;quot;

Wenn Sie active Directory in Ihrem Netzwerk eingerichtet haben, können Sie einen oder mehrere Computer gleichzeitig konfigurieren, durch die Einbettung in einen (Group Policy Object, GPO), und klicken Sie dann das GPO mit WSUS-Einstellungen konfigurieren. Es wird empfohlen, ein neues GPO zu erstellen, das nur WSUS-Einstellungen enthält.

Verknüpfen Sie dieses WSUS-GPO, mit active Directory-Container, der für Ihre Umgebung geeignet ist. In einer einfachen Umgebung reicht es u. U. aus, ein WSUS-GPO mit der Domäne zu verknüpfen. In einer komplexeren Umgebung müssen Sie möglicherweise mehrere WSUS-GPOs mit mehreren Organisationseinheiten (Organizational Unit, OU) verknüpfen, sodass Sie unterschiedliche WSUS-Richtlinieneinstellungen für verschiedene Computertypen anwenden können.

##### <a name="to-enable-wsus-through-a-domain-gpo"></a>So aktivieren Sie WSUS über ein Domänen-GPO

1.  In der Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC) in das Gruppenrichtlinienobjekt auf dem Sie WSUS konfigurieren möchten, und klicken Sie dann auf **bearbeiten**.

2.  Erweitern Sie in der Gruppenrichtlinien-Verwaltungskonsole **Computer Konfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **Windows-Komponenten**, und klicken Sie dann auf **Windows Update**.

3.  Doppelklicken Sie im Detailbereich auf **Automatische Updates konfigurieren**. Die Richtlinie **Automatische Updates konfigurieren** wird geöffnet.

4.  Klicken Sie auf **Aktiviert**, und wählen Sie anschließend eine der folgenden Optionen unter der Einstellung **Automatische Updates konfigurieren** aus:

    -   **Vor Herunterladen und Installation benachrichtigen**. Bei Auswahl dieser Option wird ein angemeldeter Administrator vor dem Herunterladen und Installieren der Updates benachrichtigt.

    -   **Autom. Herunterladen, aber vor Installation benachrichtigen**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend wird ein angemeldeter Administrator benachrichtigt, bevor die Updates installiert werden. Diese Option ist standardmäßig ausgewählt.

    -   **Autom. Herunterladen und laut Zeitplan installieren**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend werden die Updates zu dem von Ihnen angegebenen Zeitpunkt installiert.

    -   **Lokalen Administrator ermöglichen, Einstellung auszuwählen**. Bei Auswahl dieser Option können lokale Administratoren den Bereich %%amp;quot;Automatische Updates%%amp;quot; in der Systemsteuerung verwenden, um eine Konfigurationsoption auszuwählen. Sie können z. B. einen geplanten Installationszeitpunkt auswählen. Lokale Administratoren können %%amp;quot;Automatische Updates%%amp;quot; nicht deaktivieren.

5.  Wählen Sie **clientseitige zielzuordnung aktivieren**Option **aktiviert**, und geben Sie dann den Namen der WSUS-Computergruppe, die Sie diesen Computer hinzufügen möchten, die **Zielgruppenname für diesen Computer**  Feld.

    > [!NOTE]
    > Durch die Option **Clientseitige Zielzuordnung aktivieren** können Clientcomputer sich selbst Zielcomputergruppen auf dem WSUS-Server hinzufügen, wenn automatische Updates auf einen WSUS-Server umgeleitet werden. Wenn der Status auf aktiviert festgelegt ist, wird dieser Computer identifizieren sich selbst als Mitglied einer bestimmten Computergruppe beim Senden von Informationen an den WSUS-Server, die verwendet wird, um zu bestimmen, welche Updates auf diesem Computer bereitgestellt werden. Diese Einstellung zeigt dem WSUS-Server an, welche Gruppe der Clientcomputer verwendet. Sie müssen die Gruppe auf dem WSUS-Server erstellen und ihr Domänenmitgliedscomputer hinzufügen.

6.  Klicken Sie auf **OK**, um die Richtlinie **Clientseitige Zielzuordnung aktivieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

7.  Klicken Sie auf **OK**, um die Richtlinie **Automatische Updates konfigurieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

8.  Doppelklicken Sie im Detailbereich **Windows Update** auf **Internen Pfad für den Microsoft Updatedienst angeben**.

9. Klicken Sie auf **Aktiviert**, und geben Sie dann die URL des gleichen WSUS-Servers in die Felder **Interner Updatedienst zum Ermitteln von Updates** und **Intranetserver für die Statistik** ein. Geben Sie z. B. *http://servername* in beide Felder ein (wobei *Servername* ist der Name des WSUS-Servers).

    > [!WARNING]
    > Beim Eingeben der Intranetadresse des WSUS-Servers muss der zu verwendende Port angegeben werden. Standardmäßig verwendet WSUS den Port 8530 für HTTP und den Port 8531 für HTTPS. Wenn Sie HTTP verwenden, Sie sollten Geben Sie beispielsweise **http://servername:8530** .

10. Klicken Sie auf **OK**.

Nach dem Sie eine Client-Computer eingerichtet haben, dauert es einige Minuten, bis der Computer wird angezeigt, auf die **Computer** Seite in der WSUS-Verwaltungskonsole. Bei Clientcomputern, die mit einem domänenbasierten GPO konfiguriert werden, kann es bis zu 20 Minuten dauern, bis die neuen Richtlinieneinstellungen von der Gruppenrichtlinie auf den Clientcomputer angewendet werden. In der Standardeinstellung remoteaktualisierungen der Gruppenrichtlinie im Hintergrund alle 90 Minuten mit einer zufälligen Verschiebung von 0 bis 30 Minuten. Wenn Sie die Gruppenrichtlinie gruppenrichtlinienaktualisierung früher ausführen möchten, können Sie ein Eingabeaufforderungsfenster auf dem Client Computer und geben Sie Gpupdate/force öffnen.

Bei Clientcomputern, die mithilfe des Editors für lokale Gruppenrichtlinien konfiguriert sind, das GPO direkt angewendet, und die Aktualisierung dauert ca. 20 Minuten. Wenn Sie die Ermittlung manuell starten, müssen Sie nicht warten Sie 20 Minuten dauern, bis die Verbindung mit WSUS auf dem Client-Computer.

Da das Warten auf den Start der Ermittlung zeitaufwändig sein kann, können Sie ggf. das folgende Verfahren verwenden, um die Ermittlung sofort zu initiieren.

##### <a name="to-initiate-wsus-detection"></a>So starten Sie die WSUS-Ermittlung

1.  Öffnen Sie auf dem Clientcomputer ein Eingabeaufforderungsfenster mit erhöhten Rechten aus.

2.  Geben Sie wuauclt.exe/detectnow ein, und drücken Sie dann die EINGABETASTE.

## <a name="25-secure-wsus-with-the-secure-sockets-layer-protocol"></a>2.5. Schützen von WSUS mit dem Secure Sockets Layer-Protokoll

Sie können das Secure Sockets Layer (SSL)-Protokoll zum Sichern der WSUS-Bereitstellung verwenden. SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Server verwendet. SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Updates verwendet.

> [!IMPORTANT]
> Clients und Downstreamserver, die für die Verwendung von Transport Layer Security (TLS) oder HTTPS konfiguriert werden, müssen auch zur Verwendung eines vollqualifizierten Domänennamens (FQDN) für WSUS-Upstreamserver konfiguriert werden.

SSL wird von WSUS nur für Metadaten und nicht für Updatedateien verwendet. Auf diese Weise verteilt auch Microsoft Update die Updates. Microsoft reduziert das Risiko beim Senden von Updatedateien über einen unverschlüsselten Kanal, indem jedes Update signiert wird. Darüber hinaus wird ein Hashwert berechnet und zusammen mit den Metadaten für jedes Update gesendet. Wenn ein Update heruntergeladen wird, überprüft WSUS die digitale Signatur und den Hashwert. Wenn das Update geändert wurde, ist es nicht installiert.

### <a name="limitations-of-wsus-ssl-deployments"></a>Einschränkungen von WSUS-SSL-Bereitstellungen
Berücksichtigen Sie bei Verwendung von SSL zum Sichern der WSUS-Bereitstellung die folgenden Einschränkungen:

1.  Die Verwendung von SSL erhöht die Auslastung des Servers. Sie sollten aufgrund des Aufwands zur Verschlüsselung aller Metadaten, die über das Netzwerk gesendet wird, von einem Leistungsverlust von 10 % ausgehen.

2.  Wenn Sie WSUS mit einer SQL Server-Remotedatenbank verwenden, wird die Verbindung zwischen dem WSUS-Server und dem Datenbankserver nicht durch SSL gesichert. Wenn die Verbindung mit der Datenbank gesichert werden muss, sollten Sie die folgenden Empfehlungen:

-   Verschieben Sie die WSUS-Datenbank, mit dem WSUS-Server.

-   Verschieben Sie die remote-Datenbankserver und den WSUS-Server mit einem privaten Netzwerk an.

-   Stellen Sie Internet Protocol Security (IPsec) bereit, um den Netzwerkverkehr zu sichern. Weitere Informationen zu IPsec finden Sie unter [Creating and Using IPsec Policies](https://go.microsoft.com/fwlink/?LinkID=203841).

### <a name="configure-ssl-on-the-wsus-server"></a>Konfigurieren von SSL auf dem WSUS-Server
WSUS erfordert zwei Ports für SSL: einen Port, der HTTPS für das Senden verschlüsselter Metadaten verwendet, und einen Port, der HTTP für das Senden der Updates verwendet. Beachten Sie beim Konfigurieren von WSUS für SSL Folgendes:

-   Sie können nicht die gesamte WSUS-Website so konfigurieren, dass SSL erforderlich ist, da der gesamte Datenverkehr an die WSUS-Website verschlüsselt werden müsste. WSUS verschlüsselt nur Updatemetadaten. Wenn ein Computer versucht, Updatedateien auf den HTTPS-Port zu abzurufen, wird die Übertragung fehl.

    Sie sollten SSL nur für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **SimpleAuthWebService**

    -   **DSSAuthWebService**

    -   **ServerSyncWebService**

    -   **APIremoting30**

    -   **ClientWebService**

    Sie sollten SSL nicht für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **Inhalt**

    -   **Hardwareinventur**

    -   **ReportingWebService**

    -   **SelfUpdate**

-   Das Zertifikat der Zertifizierungsstelle (CA) muss in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computerspeichers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service auf WSUS-Downstreamservern importiert werden. Wenn nur das Zertifikat importiert wurde auf den lokalen Benutzer vertrauenswürdigen Stamm-CA zu speichern, die downstream-WSUS-Server nicht auf dem Upstreamserver authentifiziert.

    Weitere Informationen zur Verwendung von SSL-Zertifikate in IIS finden Sie unter [Require Secure Sockets Layer (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=203846).

-   Sie müssen das Zertifikat auf allen Computern importieren, die mit dem WSUS-Server kommunizieren. Dies umfasst alle Clientcomputer, Downstreamserver und Computer, auf denen die WSUS-Verwaltungskonsole ausgeführt wird. Das Zertifikat sollte in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service importiert werden.

-   Sie können einen beliebigen Port für SSL verwenden. Der Port, den Sie für SSL eingerichtet haben, bestimmt jedoch auch den Port, über den WSUS unverschlüsselt den HTTP-Datenverkehr sendet. Beachten Sie folgende Beispiele:

    -   Bei Verwendung des branchenstandardports 443 für HTTPS-Datenverkehr verwendet WSUS den branchenstandardport 80 für unverschlüsselten HTTP-Datenverkehr.

    -   Wenn Sie einen anderen Port als 443 für HTTPS-Datenverkehr verwenden, sendet WSUS unverschlüsselten HTTP-Datenverkehr über den Port, die numerisch vor dem Port für HTTPS liegt. Wenn Sie beispielsweise Port 8531 für HTTPS verwenden, wird WSUS Port 8530 für HTTP verwendet.

-   Sie müssen *ClientServicingProxy* erneut initialisieren, wenn der Servername, die SSL-Konfiguration oder die Portnummer geändert wird.

##### <a name="to-configure-ssl-on-the-wsus-root-server"></a>So konfigurieren Sie SSL auf dem WSUS-Server

1.  Melden Sie sich bei dem WSUS-Server mit einem Konto an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Wechseln Sie zu **starten**, Typ **CMD**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

3.  Navigieren Sie zu der *%ProgramFiles%* **\Update Services\Tools\\* * Ordner.

4.  Geben Sie im Eingabeaufforderungsfenster Befehl den folgenden Befehl ein:

    **Wsusutil configuressl** *certificateName*

    Dabei gilt Folgendes:

    *certificateName* ist der DNS-Name des WSUS-Servers.

### <a name="configure-ssl-on-client-computers"></a>Konfigurieren von SSL auf Clientcomputern
Wenn Sie SSL auf Clientcomputern konfigurieren, sollten Sie Folgendes berücksichtigen:

-   Sie müssen eine URL für einen sicheren Port auf dem WSUS-Server einschließen. Da SSL auf dem Server nicht erzwungen werden kann, können Sie nur sicherstellen, dass der Clientcomputer einen sicheren Kanal verwenden kann, indem eine URL genutzt wird, die HTTPS angibt. Wenn Sie einen anderen Port als 443 für SSL verwenden, müssen Sie auch diesen Port in der URL einschließen.

-   Das Zertifikat auf einem Clientcomputer muss in den Speicher des lokalen Computers vertrauenswürdigen Stamm-CA oder die automatische Update-Dienst vertrauenswürdigen Stamm-CA-Store importiert werden. Wenn das Zertifikat in den vertrauenswürdigen Stamm-CA-Speicher nur des lokalen Benutzers importiert wird, schlägt automatische Updates auf Server-Authentifizierung fehl.

-   Die Clientcomputer müssen dem Zertifikat vertrauen, das Sie an den WSUS-Server binden. Je nach verwendetem Zertifikattyp müssen Sie möglicherweise einen Dienst einrichten, sodass die Clientcomputer dem an den WSUS-Server gebundenen Zertifikat vertrauen.

### <a name="configure-ssl-for-downstream-wsus-servers"></a>Konfigurieren von SSL für WSUS-Downstreamserver
Die folgenden Anweisungen dienen der Konfiguration der Synchronisierung eines Downstreamservers mit einem Upstreamserver, der SSL verwendet.

##### <a name="to-synchronize-a-downstream-server-to-an-upstream-server-that-uses-ssl"></a>So synchronisieren Sie einen Downstreamserver mit einem Upstreamserver, der SSL verwendet

1.  Melden Sie sich mit einem Konto beim Computer an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Klicken Sie auf **starten**, klicken Sie auf **Programme**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server Update Service**.

3.  Erweitern Sie im rechten Bereich den Namen des Servers.

4.  Klicken Sie auf **Optionen**und dann auf **Updatequelle und Proxyserver**.

5.  Wählen Sie auf der Seite **Updatequelle** die Option **Von einem Windows Server Update Services-Server synchronisieren**aus.

6.  Geben Sie den Namen des Upstreamservers in das **Servernamen** Textfeld. Geben Sie die Portnummer, die der Server für SSL-Verbindungen in verwendet die **Portnummer** Textfeld.

7.  Wählen Sie die **SSL beim Synchronisieren der Updateinformationen** , und klicken Sie dann auf **OK**.

### <a name="additional-ssl-resources"></a>zusätzliche SSL-Ressourcen
Die Schritte zum Einrichten einer Zertifizierungsstelle, zum Binden des Zertifikats an die WSUS-Website und zum Einrichten einer Vertrauensstellung zwischen Clientcomputern und Zertifikat gehen über den Rahmen dieses Handbuchs hinaus. Weitere Informationen und eine Anleitung zum Installieren von Zertifikaten sowie zum Einrichten der Umgebung finden Sie in den folgenden Themen:

-   [Schrittweise Anleitung für die Suite B PKI](https://go.microsoft.com/fwlink/?LinkID=203858)

-   [Implementieren und Verwalten von Zertifikatvorlagen](https://go.microsoft.com/fwlink/?LinkID=203859)

-   [Active Directory Certificate Services Upgrade and Migration Guide](https://go.microsoft.com/fwlink/?LinkID=203860)

-   [Konfigurieren der automatischen Registrierung von Zertifikaten](https://go.microsoft.com/fwlink/?LinkID=203861)

### <a name="26-complete-iis-configuration"></a>2.6. Abschluss der IIS-Konfiguration
Standardmäßig ist der anonyme Lesezugriff für die Standardwebsite und alle neuen IIS-Websites aktiviert. Einige Programme, vor allem Windows SharePoint Services, können den anonymen Zugriff entfernen. Wenn dies der Fall, müssen Sie den anonymen Lesezugriff erneut aktivieren, bevor Sie erfolgreich installieren und betreiben von WSUS können.

Führen Sie die Schritte für die entsprechende Version von IIS aus, um anonymen Lesezugriff zu aktivieren:

1.  [Enable Anonymous Authentication (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=205316)– IIS 7-Handbuch.

2.  [Enabling Anonymous Authentication (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=211391)– IIS 6.0-Handbuch.

### <a name="27-configure-a-signing-certificate"></a>2.7. Konfigurieren eines Signaturzertifikats
WSUS bietet die Möglichkeit, benutzerdefinierte Updatepakete für Produkte von Microsoft und andere Produkte zu veröffentlichen. WSUS kann diese benutzerdefinierten Updatepakete für Sie automatisch mit einem Authenticode-Zertifikat signieren. Um die Signatur von benutzerdefinierten Updates zu aktivieren, müssen Sie ein Paketsignaturzertifikat auf dem WSUS-Server installieren. Bei der Signatur benutzerdefinierter Updates sind verschiedene Aspekte zu beachten.

1.  **Zertifikatverteilung**. Der private Schlüssel muss auf dem WSUS-Server installiert sein, und der öffentliche Schlüssel muss explizit im Speicher für vertrauenswürdige Zertifikate auf allen Client-PCs und Servern installiert werden, die benutzerdefinierte signierte Updates erhalten sollen.

2.  **Ablaufdatum**. Wenn das selbstsignierte Zertifikat abläuft oder sich das Ablaufdatum nähert, protokolliert WSUS entsprechende Ereignisse im Ereignisprotokoll.

3.  **Zertifikatupdates/Zertifikatsperre**. Wenn Sie möchten, aktualisieren oder zu Sperren eines Zertifikats (d. h. nach Erkennung des Ablaufdatums), angeboten WSUS keine Funktionalität, um dies zu ermöglichen. Dafür mussten manuelle Aufgaben ausgeführt werden, die entweder sehr schwierig manuell auszuführen waren oder sich schlecht automatisieren ließen.


