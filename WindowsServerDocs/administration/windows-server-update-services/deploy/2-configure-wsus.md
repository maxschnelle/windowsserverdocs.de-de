---
title: 'Schritt 2: Konfigurieren von WSUS'
description: 'WSUS-Thema (Windows Server Update Services): Konfigurieren von WSUS – Zweiter Schritt eines Prozesses mit vier Schritten für die Bereitstellung von WSUS'
ms.topic: article
ms.assetid: d4adc568-1f23-49f3-9a54-12a7bec5f27c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 9/18/2020
ms.openlocfilehash: d791151493e98c833a3981d305b81fe0b536b19c
ms.sourcegitcommit: b5c7eaa78e16f3b395611cdbdd4c88dfc653832b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2020
ms.locfileid: "91406283"
---
# <a name="step-2-configure-wsus"></a>Schritt 2: Konfigurieren von WSUS

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie die WSUS-Serverrolle auf dem Server installiert haben, müssen Sie sie korrekt konfigurieren. In der folgenden Prüfliste sind die Schritte für die Erstkonfiguration des WSUS-Servers zusammengefasst.

|Aufgabe|Beschreibung|
|----|--------|
|[2.1. Konfigurieren der Netzwerkverbindungen](#21-configure-network-connections)|Konfigurieren Sie das Clusternetzwerk mithilfe des Netzwerkkonfigurations-Assistenten.|
|[2.2. Konfigurieren von WSUS mit dem WSUS-Konfigurations-Assistenten](#22-configure-wsus-by-using-the-wsus-configuration-wizard)|Verwenden Sie den WSUS-Konfigurations-Assistenten, um die WSUS-Basiskonfiguration auszuführen.|
|[2.3. Konfigurieren von WSUS-Computergruppen](#23-configure-wsus-computer-groups)|Erstellen Sie Computergruppen in der WSUS-Verwaltungskonsole zum Verwalten von Updates in Ihrer Organisation.|
|[2.4. Konfigurieren von Clientupdates](#24-configure-client-updates)|Geben Sie an, wie und wann automatische Updates auf Clientcomputern angewendet werden.|
|[2.5. Schützen von WSUS mit dem Secure Sockets Layer-Protokoll](#25-secure-wsus-with-the-secure-sockets-layer-protocol)|Konfigurieren Sie das Secure Sockets Layer (SSL)-Protokoll zum Schutz von Windows Server Update Services (WSUS).|

## <a name="21-configure-network-connections"></a>2.1. Konfigurieren der Netzwerkverbindungen
Bevor Sie mit der Konfiguration beginnen, müssen Sie sich die folgenden Fragen beantworten:

1.  Ist die Firewall des Servers so konfiguriert, dass Clients auf den Server zugreifen können?

2.  Kann dieser Computer eine Verbindung mit dem Upstreamserver herstellen (z. B. dem Server, der zum Herunterladen von Updates von Microsoft Update verwendet wird)?

3.  Kennen Sie den Namen des Proxyservers und die Benutzeranmeldeinformationen für den Proxyserver, falls Sie sie benötigen?

In der Standardkonfiguration ruft WSUS Updates von Microsoft Update ab. Wenn du über einen Proxyserver im Netzwerk verfügst, kannst du WSUS für die Verwendung des Proxyservers konfigurieren. Falls eine Unternehmensfirewall zwischen WSUS und dem Internet vorhanden ist, musst du sie ggf. konfigurieren, um sicherzustellen, dass WSUS Updates abrufen kann.

> [!TIP]
> Obwohl Internetkonnektivität erforderlich ist, um Updates von Microsoft Update herunterzuladen, bietet WSUS die Möglichkeit, Updates in Netzwerke zu importieren, die nicht mit dem Internet verbunden sind.

Wenn Sie die Antworten auf diese Fragen kennen, können Sie mit der Konfiguration der folgenden WSUS-Netzwerkeinstellungen beginnen:

-   **Updates** Geben Sie an, wie dieser Server Updates abruft (von Microsoft Update oder von einem anderen WSUS-Server).

-   **Proxy** Wenn WSUS einen Proxyserver für den Internetzugriff verwenden muss, musst du Proxyeinstellungen im WSUS-Server konfigurieren.

-   **Firewall** Wenn sich WSUS hinter einer Unternehmensfirewall befindet, müssen einige zusätzliche Schritte auf dem Edgegerät ausgeführt werden, um den WSUS-Datenverkehr auf richtige Weise zuzulassen.

### <a name="211-connection-from-the-wsus-server-to-the-internet"></a>2.1.1. Verbindung zwischen WSUS-Server und Internet
Falls eine Unternehmensfirewall zwischen WSUS und dem Internet vorhanden ist, müssen Sie sie ggf. konfigurieren, um sicherzustellen, dass WSUS Updates abrufen kann. Der WSUS-Server verwendet den Port 443 für das HTTPS-Protokoll, um Updates von Microsoft Update herunterzuladen. Die meisten Unternehmensfirewalls lassen diese Art von Datenverkehr zu. In einigen Unternehmen ist der Zugriff der Server aber aufgrund der unternehmensspezifischen Sicherheitsrichtlinien eingeschränkt. Falls dein Unternehmen den Zugriff einschränkt, benötigst du die Autorisierung zum Zulassen des Internetzugriffs von WSUS auf die folgenden URLs:

- http\://windowsupdate.microsoft.com

- http\://\*.windowsupdate.microsoft.com

- https\://\*.windowsupdate.microsoft.com

- http\://\*.update.microsoft.com

- https\://\*.update.microsoft.com

- http\://\*.windowsupdate.com

- http\://download.windowsupdate.com

- https\://download.microsoft.com

- http\://\*.download.windowsupdate.com

- http\://wustat.windows.com

- http\://ntservicepack.microsoft.com

- http\://go.microsoft.com

- http\://dl.delivery.mp.microsoft.com

- https\://dl.delivery.mp.microsoft.com

> [!IMPORTANT]
> Informationen zu einem Szenario, bei dem über WSUS aufgrund von Firewallkonfigurationen keine Updates abgerufen werden können, findest du in der Microsoft Knowledge Base unter [Artikel 885819](https://support.microsoft.com/kb/885819).

Im folgenden Abschnitt wird beschrieben, wie eine Unternehmensfirewall zwischen WSUS und dem Internet konfiguriert wird. Da WSUS den gesamten Netzwerkdatenverkehr initiiert, ist es nicht erforderlich, die Windows-Firewall auf dem WSUS-Server zu konfigurieren. Obwohl die Verbindung zwischen Microsoft Update und WSUS erfordert, dass die Ports 80 und 443 geöffnet sind, können Sie mehrere WSUS-Server zur Synchronisierung mit einem benutzerdefinierten Port konfigurieren.

### <a name="212-connection-between-wsus-servers"></a>2.1.2. Verbindung zwischen WSUS-Servern
Upstream- und Downstream-WSUS-Server werden auf dem Port synchronisiert, der vom WSUS-Administrator konfiguriert wurde. Diese Ports sind standardmäßig folgendermaßen konfiguriert:

-   Bei WSUS 3.2 und früher: Port 80 für HTTP und 443 für HTTPS

-   Unter WSUS 6.2 und höher (mindestens Windows Server 2012) werden Port 8530 für HTTP und 8531 für HTTPS verwendet.

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

3.  Öffnen Sie eine Eingabeaufforderung (Cmd.exe) als Administrator. Wählen Sie zum Öffnen einer Eingabeaufforderung als Administrator **Start**aus. Gib in **Suche starten** den Suchbegriff **Eingabeaufforderung** ein. Klicke am oberen Rand des Menüs „Start“ mit der rechten Maustaste auf **Eingabeaufforderung**, und klicke dann auf **Als Administrator ausführen**. Gehe wie folgt vor, wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird: Gib die entsprechenden Anmeldeinformationen ein (falls angefordert), vergewissere dich, dass die gewünschte Aktion angezeigt wird, und klicke dann auf **Weiter**.

4.  Wechsele im Eingabeaufforderungsfenster zum Ordner „C:\Programme\Update Services\Tools“. Gib den folgenden Befehl ein:

    **wsusutil ConfigureSSlproxy [<Proxyserver Proxyport>] -enable**, wobei:

    1.  Proxyserver für den Namen des Proxyservers steht, der HTTPS unterstützt.

    2.  Proxyport die Portnummer des Proxyservers ist.

5.  Schließe das Eingabeaufforderungsfenster.

Führen Sie das folgende Verfahren aus, um den Proxyserver hinzuzufügen, der das HTTP-Protokoll für die WSUS-Konfiguration verwendet:

#### <a name="to-add-a-proxy-server-that-uses-the-http-protocol"></a>Hinzufügen eines Proxyservers, der das HTTP-Protokoll verwendet

1.  Öffnen Sie die WSUS-Verwaltungskonsole.

2.  Erweitern Sie im linken Bereich den Servernamen, und klicken Sie dann auf **Optionen**.

3.  Klicken Sie im Bereich **Optionen** auf **Updatequelle und Proxyserver**und anschließend auf die Registerkarte **Proxyserver** .

4.  Verwenden Sie die folgenden Optionen, um die vorhandene Proxyserverkonfiguration zu ändern:

    ###### <a name="to-change-or-add-a-proxy-server-to-the-wsus-configuration"></a>Ändern oder Hinzufügen eines Proxyservers zur WSUS-Konfiguration

    1.  Aktivieren Sie das Kontrollkästchen für **Proxyserver für die Synchronisierung verwenden**.

    2.  Geben Sie im Textfeld **Proxyservername** den Namen des Proxyservers ein.

    3.  Geben Sie im Textfeld **Proxyportnummer** die Portnummer des Proxyservers ein. Die Standardportnummer ist 80.

    4.  Wenn der Proxyserver erfordert, dass du ein bestimmtes Benutzerkonto verwendest, aktivierst du das Kontrollkästchen **Benutzeranmeldeinformationen für die Verbindungsherstellung mit dem Proxyserver verwenden**. Gib den erforderlichen Benutzernamen, die Domäne und das Kennwort in die entsprechenden Textfelder ein.

    5.  Falls der Proxyserver Standardauthentifizierung unterstützt, aktivieren Sie das Kontrollkästchen **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** .

    6.  Klicken Sie auf **OK**.

    ###### <a name="to-remove-a-proxy-server-from-the-wsus-configuration"></a>Entfernen eines Proxyservers aus der WSUS-Konfiguration

    1.  Um einen Proxyserver aus der WSUS-Konfiguration zu entfernen, deaktivieren Sie das Kontrollkästchen **Proxyserver für die Synchronisierung verwenden**.

    2.  Klicken Sie auf **OK**.

## <a name="22-configure-wsus-by-using-the-wsus-configuration-wizard"></a>2.2. Konfigurieren von WSUS mit dem WSUS-Konfigurations-Assistenten
Dieses Verfahren setzt voraus, dass Sie den WSUS-Konfigurations-Assistenten verwenden, der beim erstmaligen Starten der WSUS-Verwaltungskonsole angezeigt wird. Weiter unter in diesem Thema wird beschrieben, wie Sie diese Konfigurationen auf der Seite **Optionen** ausführen.

#### <a name="to-configure-wsus"></a>So konfigurieren Sie WSUS

1.  Klicken Sie im Navigationsbereich des Server-Managers auf **Dashboard**, auf **Tools**und dann auf **Windows Server Update Services**.

    > [!NOTE]
    > Klicke auf **Ausführen**, wenn das Dialogfeld **WSUS-Installation abschließen** angezeigt wird. Klicke im Dialogfeld **WSUS-Installation abschließen** auf **Schließen**, wenn die Installation erfolgreich abgeschlossen wurde.

2.  Der WSUS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Informationen auf der Seite **Vorbemerkungen** , und klicken Sie dann auf **Weiter**.

3.  Lesen Sie die Anweisungen auf der Seite **Am Programm zur Verbesserung von Microsoft Update teilnehmen** , und entscheiden Sie, ob Sie am Programm teilnehmen möchten. Wenn Sie am Programm teilnehmen möchten. Behalte die Standardauswahl bei, oder deaktiviere das Kontrollkästchen, und klicke dann auf **Weiter**.

4.  Auf der Seite **Upstreamserver auswählen** stehen Ihnen zwei Optionen zur Verfügung:

    1.  Updates mit Microsoft Update synchronisieren

    2.  Von einem anderen Windows Server Update Services-Server synchronisieren

        -   Wenn du dich für die Synchronisierung mit einem anderen WSUS-Server entscheidest, gibst du den Servernamen und den Port an, über den der Server mit dem Upstreamserver kommuniziert.

        -   Wenn Sie SSL verwenden möchten, aktivieren Sie das Kontrollkästchen **SSL beim Synchronisieren der Updateinformationen verwenden** . Die Server verwenden den Port 443 für die Synchronisierung. (Stellen Sie sicher, dass dieser Server und der Upstreamserver SSL unterstützen).

        -   Falls es sich um einen Replikatserver handelt, aktivierst du das Kontrollkästchen **Dies ist ein Replikat des Upstreamservers**.

5.  Nachdem Sie die entsprechenden Optionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

6.  Aktivieren Sie auf der Seite **Proxyserver angeben** das Kontrollkästchen **Proxyserver für die Synchronisierung verwenden** , und geben Sie dann den Namen des Proxyservers und die Portnummer (standardmäßig Port 80) in die entsprechenden Felder ein.

    > [!IMPORTANT]
    > Dieser Schritt muss ausgeführt werden, wenn WSUS einen Proxyserver für den Internetzugriff benötigt.

7.  Wenn für die Verbindung mit dem Proxyserver bestimmte Benutzeranmeldeinformationen verwendet werden sollen, aktivierst du das Kontrollkästchen **Benutzeranmeldeinformationen verwenden, um Verbindung mit dem Proxyserver herzustellen**. Gib anschließend den Benutzernamen, die Domäne und das Kennwort des Benutzers in die entsprechenden Felder ein. Falls du für den Benutzer, der die Verbindung mit dem Proxyserver herstellt, die Standardauthentifizierung aktivieren möchtest, aktivierst du das Kontrollkästchen **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** .

8.  Klicken Sie auf **Weiter**. Klicke auf der Seite **Mit Upstreamserver verbinden** auf **Verbindung starten**.

9. Wenn die Verbindung hergestellt wurde, klicken Sie auf **Weiter** , um fortzufahren.

10. Auf der Seite **Sprachen auswählen** kannst du die Sprachen auswählen, für die WSUS Updates empfängt (alle Sprachen oder eine Teilmenge von Sprachen). Wenn du eine Teilmenge von Sprachen auswählst, sparst du Speicherplatz. Es ist aber WICHTIG, alle Sprachen auszuwählen, die für sämtliche Clients des WSUS-Servers erforderlich sind. Falls du nur für bestimmte Sprachen Updates abrufen möchtest, aktivierst du **Updates nur in folgenden Sprachen herunterladen**. Wähle anschließend die gewünschten Sprachen aus. Andernfalls kannst du die Standardeinstellung übernehmen.

    > [!WARNING]
    > Wenn Sie die Option **Updates nur in folgenden Sprachen herunterladen**auswählen und ein WSUS-Downstreamserver mit dem Server verbunden ist, werden für den Downstreamserver ebenfalls nur die ausgewählten Sprachen verwendet.

11. Nachdem Sie die entsprechenden Sprachoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

12. Auf der Seite **Produkte auswählen** können Sie die Produkte angeben, für die Sie Updates herunterladen möchten. Wähle Produktkategorien wie Windows oder bestimmte Produkte wie Windows Server 2008 aus. Durch die Auswahl einer Produktkategorie werden alle Produkte in der Kategorie ausgewählt.

13. Wähle die entsprechenden Produktoptionen für deine Bereitstellung aus, und klicke dann auf **Weiter**.

14. Wählen Sie auf der Seite **Klassifizierungen auswählen** die gewünschten Updateklassifizierungen aus. Sie können alle Klassifizierungen oder eine Teilmenge auswählen. Klicken Sie anschließend auf **Weiter**.

15. Auf der Seite **Synchronisierungszeitplan festlegen** können Sie auswählen, ob die Synchronisierung manuell oder automatisch ausgeführt werden soll.

    -   Bei Auswahl von **Manuell synchronisieren** musst du die Synchronisierung über die WSUS-Verwaltungskonsole starten.

    -   Bei Auswahl von **Automatisch synchronisieren** führt der WSUS-Server die Synchronisierung in festgelegten Intervallen aus.

    Legen Sie die Zeit für **Erste Synchronisierung**fest, und geben Sie die Anzahl von **Synchronisierungen pro Tag** an, die dieser Server ausführen soll. Wenn Sie z. B. vier Synchronisierungen pro Tag mit der ersten Synchronisierung um 3:00 Uhr festlegen, finden um 3:00 Uhr, 9:00 Uhr, 15:00 Uhr und 21:00 Uhr Synchronisierungen statt

16. Nachdem Sie die entsprechenden Synchronisierungsoptionen für Ihre Bereitstellung ausgewählt haben, klicken Sie auf **Weiter** , um fortzufahren.

17. Auf der Seite **Fertig gestellt** haben Sie die Möglichkeit, die Synchronisierung direkt zu starten, indem Sie das Kontrollkästchen **Erstsynchronisierung starten** aktivieren. Wenn du diese Option nicht auswählst, musst du die Erstsynchronisierung über die WSUS-Verwaltungskonsole ausführen. Klicken Sie auf **Weiter** , wenn Sie mehr über zusätzliche Einstellungen erfahren möchten, oder auf **Fertig stellen** , um den Assistenten zu beenden und die WSUS-Erstkonfiguration abzuschließen.

18. Nach dem Klicken auf **Fertig stellen**wird die WSUS-Verwaltungskonsole angezeigt.

Damit ist die grundlegende WSUS-Konfiguration abgeschlossen. Lesen Sie jetzt die nächsten Abschnitte, um mehr über das Ändern der Einstellungen mithilfe der WSUS-Verwaltungskonsole zu erfahren.

## <a name="23-configure-wsus-computer-groups"></a>2.3. Konfigurieren von WSUS-Computergruppen
Computergruppen sind ein WICHTIGER Bestandteil von WSUS-Bereitstellungen (Windows Server Update Services). Mithilfe von Computergruppen können Sie Updates testen und gezielt für bestimmte Computer anwenden. Es gibt die folgenden zwei Standardcomputergruppen: „Alle Computer“ und „Nicht zugewiesene Computer“. Standardmäßig fügt der WSUS-Server jeden Clientcomputer bei der ersten Verbindungsherstellung mit dem Server einer dieser beiden Gruppen hinzu.

Sie können beliebig viele benutzerdefinierte Computergruppen erstellen, um Updates in Ihrer Organisation zu verwalten. Es wird empfohlen, mindestens eine Computergruppe zu erstellen, mit der Updates getestet werden können, bevor sie auf anderen Computern in der Organisation bereitgestellt werden.

Gehen Sie wie im Folgenden beschrieben vor, um eine neue Gruppe zu erstellen und ihr einen Computer zuzuweisen:

#### <a name="to-create-a-computer-group"></a>So erstellen Sie eine Computergruppe

1.  Erweitere in der WSUS-Verwaltungskonsole unter **Update Services**den Eintrag **Computer**, klicke mit der rechten Maustaste auf **Alle Computer**, und klicke dann auf **Computergruppe hinzufügen**.

2.  Gib im Dialogfeld **Computergruppe hinzufügen** den Namen der neuen Gruppe in das Feld **Name** ein, und klicke dann auf **Hinzufügen**.

3.  Klicke auf **Computer**, und wähle anschließend die Computer aus, die du der neuen Gruppe zuweisen möchtest.

4.  Klicke mit der rechten Maustaste auf die im vorherigen Schritt ausgewählten Computernamen, und klicke dann auf **Mitgliedschaft ändern**.

5.  Wähle im Dialogfeld **Gruppenmitgliedschaft für Computer festlegen** die erstellte Testgruppe aus, und klicke dann auf **OK**.

## <a name="24-configure-client-updates"></a>2.4. Konfigurieren von Clientupdates
Beim WSUS-Setup wird IIS automatisch so konfiguriert, dass die aktuelle Version von %%amp;quot;Automatische Updates%%amp;quot; an jeden Clientcomputer verteilt wird, der eine Verbindung mit dem WSUS-Server herstellt. Die für %%amp;quot;Automatische Updates%%amp;quot; am besten geeignete Konfiguration hängt von der Netzwerkumgebung ab.

-   In einer Umgebung, in der der Active Directory-Verzeichnisdienst verwendet wird, kannst du ein vorhandenes domänenbasiertes Gruppenrichtlinienobjekt (Group Policy Object, GPO) verwenden oder ein neues GPO erstellen.

-   In einer Umgebung ohne Active Directory konfigurierst du „Automatische Updates“ mit dem Editor für lokale Gruppenrichtlinien und verweist anschließend auf den Clientcomputern auf den WSUS-Server.

> [!IMPORTANT]
> Die folgenden Verfahren gelten für Netzwerke, in denen Active Directory ausgeführt wird. Zudem wird vorausgesetzt, dass Sie mit dem Feature %%amp;quot;Gruppenrichtlinie%%amp;quot; vertraut sind und es zum Verwalten des Netzwerks verwenden.

Verwenden Sie die folgenden Verfahren, um %%amp;quot;Automatische Updates%%amp;quot; für Clientcomputer zu konfigurieren:

-   [Schritt 4: Konfigurieren von Gruppenrichtlinien für automatische Updates](4-configure-group-policy-settings-for-automatic-updates.md)

-   [2.3. Konfigurieren von Computergruppen](#23-configure-wsus-computer-groups) in diesem Thema

### <a name="configure-automatic-updates-in-group-policy"></a>Konfigurieren von %%amp;quot;Automatische Updates%%amp;quot; in %%amp;quot;Gruppenrichtlinie%%amp;quot;

Wenn du Active Directory in deinem Netzwerk eingerichtet hast, kannst du mehrere Computer gleichzeitig konfigurieren, indem du sie in ein GPO einfügst und dieses GPO anschließend mit WSUS-Einstellungen konfigurierst. Es wird empfohlen, ein neues GPO zu erstellen, das nur WSUS-Einstellungen enthält.

Verknüpfe dieses WSUS-GPO mit einem für die Umgebung geeigneten Active Directory-Container. In einer einfachen Umgebung reicht es u. U. aus, ein WSUS-GPO mit der Domäne zu verknüpfen. In einer komplexeren Umgebung müssen Sie möglicherweise mehrere WSUS-GPOs mit mehreren Organisationseinheiten (Organizational Unit, OU) verknüpfen, sodass Sie unterschiedliche WSUS-Richtlinieneinstellungen für verschiedene Computertypen anwenden können.

##### <a name="to-enable-wsus-through-a-domain-gpo"></a>So aktivieren Sie WSUS über ein Domänen-GPO

1.  Navigiere in der Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC) zu dem GPO, in dem du WSUS konfigurieren möchtest, und klicke dann auf **Bearbeiten**.

2.  Erweitere in der GPMC nacheinander **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen** und **Windows-Komponenten**, und klicke dann auf **Windows Update**.

3.  Doppelklicken Sie im Detailbereich auf **Automatische Updates konfigurieren**. Die Richtlinie **Automatische Updates konfigurieren** wird geöffnet.

4.  Klicken Sie auf **Aktiviert**, und wählen Sie anschließend eine der folgenden Optionen unter der Einstellung **Automatische Updates konfigurieren** aus:

    -   **Vor Herunterladen und Installation benachrichtigen**. Bei Auswahl dieser Option wird ein angemeldeter Administrator vor dem Herunterladen und Installieren der Updates benachrichtigt.

    -   **Autom. Herunterladen, aber vor Installation benachrichtigen**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend wird ein angemeldeter Administrator benachrichtigt, bevor die Updates installiert werden. Diese Option ist standardmäßig ausgewählt.

    -   **Autom. Herunterladen und laut Zeitplan installieren**. Bei Auswahl dieser Option wird der Download von Updates automatisch gestartet, und anschließend werden die Updates zu dem von Ihnen angegebenen Zeitpunkt installiert.

    -   **Lokalen Administrator ermöglichen, Einstellung auszuwählen**. Bei Auswahl dieser Option können lokale Administratoren den Bereich %%amp;quot;Automatische Updates%%amp;quot; in der Systemsteuerung verwenden, um eine Konfigurationsoption auszuwählen. Sie können z. B. einen geplanten Installationszeitpunkt auswählen. Lokale Administratoren können %%amp;quot;Automatische Updates%%amp;quot; nicht deaktivieren.

5.  Wähle **Clientseitige Zielzuordnung aktivieren** und dann **Aktiviert** aus. Gib anschließend den Namen der WSUS-Computergruppe, der du diesen Computer hinzufügen möchtest, im Feld **Zielgruppenname für diesen Computer** ein.

    > [!NOTE]
    > Durch die Option**Clientseitige Zielzuordnung aktivieren** können Clientcomputer sich selbst Zielcomputergruppen auf dem WSUS-Server hinzufügen, wenn automatische Updates auf einen WSUS-Server umgeleitet werden. Falls der Status „Aktiviert“ lautet, identifiziert sich dieser Computer selbst als Mitglied einer bestimmten Computergruppe, wenn er Informationen an den WSUS-Server sendet, mit denen ermittelt wird, welche Updates auf diesem Computer bereitgestellt werden. Diese Einstellung zeigt dem WSUS-Server an, welche Gruppe der Clientcomputer verwendet. Sie müssen die Gruppe auf dem WSUS-Server erstellen und ihr Domänenmitgliedscomputer hinzufügen.

6.  Klicken Sie auf **OK** , um die Richtlinie **Clientseitige Zielzuordnung aktivieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

7.  Klicken Sie auf **OK** , um die Richtlinie **Automatische Updates konfigurieren** zu schließen und zum Detailfenster „Windows Update“ zurückzukehren.

8.  Doppelklicken Sie im Detailbereich **Windows Update** auf **Internen Pfad für den Microsoft Updatedienst angeben**.

9. Klicken Sie auf **Aktiviert**, und geben Sie dann die URL des gleichen WSUS-Servers in die Felder **Interner Updatedienst zum Ermitteln von Updates** und **Intranetserver für die Statistik** ein. Gib beispielsweise *http://servername* in beide Felder ein (wobei *servername* der Name des WSUS-Servers ist).

    > [!WARNING]
    > Beim Eingeben der Intranetadresse des WSUS-Servers muss der zu verwendende Port angegeben werden. Standardmäßig verwendet WSUS den Port 8530 für HTTP und den Port 8531 für HTTPS. Wenn du HTTP verwendest, musst du beispielsweise **http://servername:8530** eingeben.

10. Klicken Sie auf **OK**.

Nach dem Einrichten eines Clientcomputers dauert es einige Minuten, bis der Computer auf der Seite **Computer** in der WSUS-Verwaltungskonsole angezeigt wird. Bei Clientcomputern, die mit einem domänenbasierten GPO konfiguriert werden, kann es bis zu 20 Minuten dauern, bis die neuen Richtlinieneinstellungen von der Gruppenrichtlinie auf den Clientcomputer angewendet werden. Standardmäßig wird die Gruppenrichtlinienaktualisierung alle 90 Minuten mit einer Verschiebung von 0 bis 30 Minuten im Hintergrund ausgeführt. Wenn du die Gruppenrichtlinienaktualisierung früher ausführen möchtest, kannst du auf dem Clientcomputer ein Eingabeaufforderungsfenster öffnen und „gpupdate /force“ eingeben.

Bei Clientcomputern, die mit dem Editor für lokale Gruppenrichtlinien konfiguriert werden, wird das GPO direkt angewendet, und die Aktualisierung dauert ca. 20 Minuten. Wenn du die Ermittlung manuell startest, musst du nicht 20 Minuten warten, bis der Clientcomputer eine Verbindung mit WSUS herstellt.

Da das Warten auf den Start der Ermittlung zeitaufwändig sein kann, können Sie ggf. das folgende Verfahren verwenden, um die Ermittlung sofort zu initiieren.

##### <a name="to-initiate-wsus-detection"></a>So starten Sie die WSUS-Ermittlung

1.  Öffne auf dem Clientcomputer ein Eingabeaufforderungsfenster mit erhöhten Rechten.

2.  Gib „wuauclt.exe /detectnow“ ein, und drücke dann die EINGABETASTE.

## <a name="25-secure-wsus-with-the-secure-sockets-layer-protocol"></a>2.5. Schützen von WSUS mit dem Secure Sockets Layer-Protokoll

Sie können das Secure Sockets Layer (SSL)-Protokoll zum Sichern der WSUS-Bereitstellung verwenden. SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Server verwendet. SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Updates verwendet.

> [!IMPORTANT]
> Clients und Downstreamserver, die für die Verwendung von Transport Layer Security (TLS) oder HTTPS konfiguriert werden, müssen auch zur Verwendung eines vollqualifizierten Domänennamens (FQDN) für WSUS-Upstreamserver konfiguriert werden.

SSL wird von WSUS nur für Metadaten und nicht für Updatedateien verwendet. Auf diese Weise verteilt auch Microsoft Update die Updates. Microsoft reduziert das Risiko beim Senden von Updatedateien über einen unverschlüsselten Kanal, indem jedes Update signiert wird. Darüber hinaus wird ein Hashwert berechnet und zusammen mit den Metadaten für jedes Update gesendet. Wenn ein Update heruntergeladen wird, überprüft WSUS die digitale Signatur und den Hashwert. Wenn das Update geändert wurde, wird es nicht installiert.

### <a name="limitations-of-wsus-ssl-deployments"></a>Einschränkungen von WSUS-SSL-Bereitstellungen
Berücksichtigen Sie bei Verwendung von SSL zum Sichern der WSUS-Bereitstellung die folgenden Einschränkungen:

1.  Die Verwendung von SSL erhöht die Auslastung des Servers. Sie sollten aufgrund des Aufwands zur Verschlüsselung aller Metadaten, die über das Netzwerk gesendet wird, von einem Leistungsverlust von 10 % ausgehen.

2.  Wenn Sie WSUS mit einer SQL Server-Remotedatenbank verwenden, wird die Verbindung zwischen dem WSUS-Server und dem Datenbankserver nicht durch SSL gesichert. Wenn die Verbindung mit der Datenbank gesichert werden muss, sollten Sie folgende Empfehlungen berücksichtigen:

-   Verschiebe die WSUS-Datenbank auf den WSUS-Server.

-   Verschiebe den Remotedatenbankserver und den WSUS-Server in ein privates Netzwerk.

-   Stelle Internet Protocol Security (IPsec) bereit, um den Netzwerkverkehr zu schützen. Weitere Informationen zu IPsec finden Sie unter [Creating and Using IPsec Policies](https://go.microsoft.com/fwlink/?LinkID=203841).

### <a name="configure-ssl-on-the-wsus-server"></a>Konfigurieren von SSL auf dem WSUS-Server
WSUS erfordert zwei Ports für SSL: einen Port, der HTTPS für das Senden verschlüsselter Metadaten verwendet, und einen Port, der HTTP für das Senden der Updates verwendet. Beachten Sie beim Konfigurieren von WSUS für SSL Folgendes:

-   Sie können nicht die gesamte WSUS-Website so konfigurieren, dass SSL erforderlich ist, da der gesamte Datenverkehr an die WSUS-Website verschlüsselt werden müsste. WSUS verschlüsselt nur Updatemetadaten. Wenn ein Computer versucht, Updatedateien auf dem HTTPS-Port abzurufen, schlägt die Übertragung fehl.

    Sie sollten SSL nur für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **SimpleAuthWebService**

    -   **DSSAuthWebService**

    -   **ServerSyncWebService**

    -   **APIremoting30**

    -   **ClientWebService**

    Sie sollten SSL nicht für die folgenden virtuellen Stammverzeichnisse erfordern:

    -   **Inhalt**

    -   **Inventory**

    -   **ReportingWebService**

    -   **SelfUpdate**

-   Das Zertifikat der Zertifizierungsstelle (CA) muss in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computerspeichers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service auf WSUS-Downstreamservern importiert werden. Wenn das Zertifikat nur in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Benutzers importiert wird, wird der Downstream-WSUS-Server nicht auf dem Upstreamserver authentifiziert.

    Weitere Informationen zur Verwendung von SSL-Zertifikaten in IIS findest du unter [Require Secure Sockets Layer (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=203846).

-   Sie müssen das Zertifikat auf allen Computern importieren, die mit dem WSUS-Server kommunizieren. Dies umfasst alle Clientcomputer, Downstreamserver und Computer, auf denen die WSUS-Verwaltungskonsole ausgeführt wird. Das Zertifikat sollte in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers oder in den vertrauenswürdigen Stamm-CA-Speicher von Windows Server Update Service importiert werden.

-   Sie können einen beliebigen Port für SSL verwenden. Der Port, den Sie für SSL eingerichtet haben, bestimmt jedoch auch den Port, über den WSUS unverschlüsselt den HTTP-Datenverkehr sendet. Betrachten Sie die folgenden Beispiele:

    -   Bei Verwendung des Branchenstandardports 443 für HTTPS-Datenverkehr verwendet WSUS den Branchenstandardport 80 für unverschlüsselten HTTP-Datenverkehr.

    -   Wenn du einen anderen Port als 443 für HTTPS-Datenverkehr verwendest, sendet WSUS unverschlüsselten HTTP-Datenverkehr über den Port, der von der Zahl gesehen vor dem Port für HTTPS liegt. Wenn Sie beispielsweise Port 8531 für HTTPS verwenden, wird WSUS Port 8530 für HTTP verwendet.

-   Sie müssen *ClientServicingProxy* erneut initialisieren, wenn der Servername, die SSL-Konfiguration oder die Portnummer geändert wird.

##### <a name="to-configure-ssl-on-the-wsus-root-server"></a>So konfigurieren Sie SSL auf dem WSUS-Server

1.  Melden Sie sich bei dem WSUS-Server mit einem Konto an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Wechsele zu **Start**, gib **CMD** ein, klicke mit der rechten Maustaste auf **Eingabeaufforderung**, und klicke dann auf **Als Administrator ausführen**.

3.  Navigiere zum Ordner _%ProgramFiles%_ **\\Update Services\\Tools\\** .

4.  Gib in der Eingabeaufforderung den folgenden Befehl ein:

    **Wsusutil configuressl**_certificateName_

    Dabei gilt Folgendes:

    *certificateName* ist der DNS-Name des WSUS-Servers.

### <a name="configure-ssl-on-client-computers"></a>Konfigurieren von SSL auf Clientcomputern
Wenn Sie SSL auf Clientcomputern konfigurieren, sollten Sie Folgendes berücksichtigen:

-   Sie müssen eine URL für einen sicheren Port auf dem WSUS-Server einschließen. Da SSL auf dem Server nicht erzwungen werden kann, können Sie nur sicherstellen, dass der Clientcomputer einen sicheren Kanal verwenden kann, indem eine URL genutzt wird, die HTTPS angibt. Wenn du einen anderen Port als 443 für SSL verwendest, musst du auch diesen Port in die URL einfügen.

-   Das Zertifikat muss in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Computers oder in den vertrauenswürdigen Stamm-CA-Speicher des Diensts für automatische Updates importiert werden. Wenn das Zertifikat nur in den vertrauenswürdigen Stamm-CA-Speicher des lokalen Benutzers importiert wird, schlägt die Serverauthentifizierung für automatische Updates fehl.

-   Die Clientcomputer müssen dem Zertifikat vertrauen, das Sie an den WSUS-Server binden. Je nach verwendetem Zertifikattyp müssen Sie möglicherweise einen Dienst einrichten, sodass die Clientcomputer dem an den WSUS-Server gebundenen Zertifikat vertrauen.

### <a name="configure-ssl-for-downstream-wsus-servers"></a>Konfigurieren von SSL für WSUS-Downstreamserver
Die folgenden Anweisungen dienen der Konfiguration der Synchronisierung eines Downstreamservers mit einem Upstreamserver, der SSL verwendet.

##### <a name="to-synchronize-a-downstream-server-to-an-upstream-server-that-uses-ssl"></a>So synchronisieren Sie einen Downstreamserver mit einem Upstreamserver, der SSL verwendet

1.  Melden Sie sich mit einem Konto beim Computer an, das Mitglied der WSUS-Administratorgruppe oder der lokalen Administratorgruppe ist.

2.  Klicke auf **Start**, **Alle Programme**, **Verwaltung** und dann auf **Windows Server Update Service**.

3.  Erweitern Sie im rechten Bereich den Namen des Servers.

4.  Klicken Sie auf **Optionen**und dann auf **Updatequelle und Proxyserver**.

5.  Wählen Sie auf der Seite **Updatequelle** die Option **Von einem Windows Server Update Services-Server synchronisieren**aus.

6.  Gib den Namen des Upstreamservers in das Textfeld **Servername** ein. Gib die Portnummer, die der Server für SSL-Verbindungen verwendet, in das Textfeld **Portnummer** ein.

7.  Aktiviere das Kontrollkästchen **SSL beim Synchronisieren der Updateinformationen verwenden**, und klicke auf **OK**.

### <a name="additional-ssl-resources"></a>Zusätzliche SSL-Ressourcen
Die Schritte zum Einrichten einer Zertifizierungsstelle, zum Binden des Zertifikats an die WSUS-Website und zum Einrichten einer Vertrauensstellung zwischen Clientcomputern und Zertifikat gehen über den Rahmen dieses Handbuchs hinaus. Weitere Informationen und eine Anleitung zum Installieren von Zertifikaten sowie zum Einrichten der Umgebung finden Sie in den folgenden Themen:

-   [Suite B-PKI: Schritt-für-Schritt-Anleitung](https://go.microsoft.com/fwlink/?LinkID=203858)

-   [Implementieren und Verwalten von Zertifikatvorlagen](https://go.microsoft.com/fwlink/?LinkID=203859)

-   [Active Directory Certificate Services Upgrade and Migration Guide](https://go.microsoft.com/fwlink/?LinkID=203860)

-   [Konfigurieren der automatischen Registrierung von Zertifikaten](https://go.microsoft.com/fwlink/?LinkID=203861)

### <a name="26-complete-iis-configuration"></a>2.6. Abschluss der IIS-Konfiguration
Standardmäßig ist der anonyme Lesezugriff für die Standardwebsite und alle neuen IIS-Websites aktiviert. Einige Programme, vor allem Windows SharePoint Services, können den anonymen Zugriff entfernen. Ist dies der Fall, musst du den anonymen Lesezugriff erneut aktivieren, bevor du WSUS erfolgreich installieren und ausführen kannst.

Führen Sie die Schritte für die entsprechende Version von IIS aus, um anonymen Lesezugriff zu aktivieren:

1.  [Enable Anonymous Authentication (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=205316)– IIS 7-Handbuch.

2.  [Enabling Anonymous Authentication (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=211391)– IIS 6.0-Handbuch.

### <a name="27-configure-a-signing-certificate"></a>2.7. Konfigurieren eines Signaturzertifikats
WSUS bietet die Möglichkeit, benutzerdefinierte Updatepakete für Produkte von Microsoft und andere Produkte zu veröffentlichen. WSUS kann diese benutzerdefinierten Updatepakete für Sie automatisch mit einem Authenticode-Zertifikat signieren. Um die Signatur von benutzerdefinierten Updates zu aktivieren, müssen Sie ein Paketsignaturzertifikat auf dem WSUS-Server installieren. Bei der Signatur benutzerdefinierter Updates sind verschiedene Aspekte zu beachten.

1.  **Zertifikatverteilung**. Der private Schlüssel muss auf dem WSUS-Server installiert sein, und der öffentliche Schlüssel muss explizit im Speicher für vertrauenswürdige Zertifikate auf allen Client-PCs und Servern installiert werden, die benutzerdefinierte signierte Updates erhalten sollen.

2.  **Ablaufdatum**. Wenn das selbstsignierte Zertifikat abläuft oder sich das Ablaufdatum nähert, protokolliert WSUS entsprechende Ereignisse im Ereignisprotokoll.

3.  **Zertifikatupdates/Zertifikatsperre**. Wenn du versucht hast, ein Zertifikat zu aktualisieren oder zu sperren (d. h. nach Erkennung des Ablaufdatums), hat WSUS keine Funktionalität zur Ermöglichung dieses Vorgangs angeboten. Dafür mussten manuelle Aufgaben ausgeführt werden, die entweder sehr schwierig manuell auszuführen waren oder sich schlecht automatisieren ließen.


