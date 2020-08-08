---
title: Add Servers to Server Manager
description: Server-Manager
ms.topic: article
ms.assetid: aab895f2-fe4d-4408-b66b-cdeadbd8969e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.localizationpriority: medium
ms.date: 02/01/2018
ms.openlocfilehash: b1c3e2f1c521615ff365642566745411db8aa612
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991942"
---
# <a name="add-servers-to-server-manager"></a>Add Servers to Server Manager

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server können Sie mehrere Remote Server mit einer einzigen Server-Manager-Konsole verwalten. Server, die Sie mithilfe von Server-Manager verwalten möchten, können Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen. Beachten Sie, dass Sie eine neuere Version von Windows Server nicht mit einer älteren Version von Server-Manager verwalten können.

In diesem Thema wird beschrieben, wie Sie dem Server-Manager Server Pool Server hinzufügen.

> [!NOTE]
> In unseren Tests können Server-Manager in Windows Server 2012 und neueren Versionen von Windows Server zum Verwalten von bis zu 100 Servern verwendet werden, die mit einer typischen Arbeitsauslastung konfiguriert sind. Die Anzahl der Server, die Sie mithilfe einer einzigen Server-Manager Konsole verwalten können, kann je nach der von den verwalteten Servern angeforderten Datenmenge und den Hardware-und Netzwerkressourcen, die für den Computer mit Server-Manager verfügbar sind, variieren. Wenn die anzuzeigende Datenmenge die Ressourcenkapazität des Computers erreicht, kann es zu langsamen Antworten von Server-Manager und Verzögerungen bei der Beendigung von Aktualisierungen kommen. Um die Anzahl der Server zu erhöhen, die Sie mithilfe von Server-Manager verwalten können, empfiehlt es sich, die Ereignisdaten, die von den verwalteten Servern abgerufen Server-Manager, mithilfe von Einstellungen im Dialogfeld **Ereignisdaten konfigurieren** einzuschränken. Sie können das Dialogfeld über das Menü **Aufgaben** in der Kachel **Ereignisse** öffnen. Wenn Sie eine unternehmensweite Anzahl von Servern in Ihrer Organisation verwalten müssen, empfiehlt es sich, die Produkte in der [Microsoft System Center-Suite](https://go.microsoft.com/fwlink/p/?LinkId=239437)zu evaluieren.
>
> Server-Manager kann von Servern unter Windows Server 2003 nur den Online- oder Offlinestatus empfangen. Obwohl Sie Server-Manager zum Ausführen von Verwaltungsaufgaben auf Servern mit Windows Server 2008 R2 oder Windows Server 2008 verwenden können, können Sie Servern, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird, keine Rollen und Features hinzufügen.
>
> Server-Manager können nicht verwendet werden, um eine neuere Version des Windows Server-Betriebssystems zu verwalten. Server-Manager, die unter Windows Server 2012 R2, Windows Server 2012, Windows 8.1 oder Windows 8 ausgeführt werden, können nicht zum Verwalten von Servern verwendet werden, auf denen Windows Server 2016 ausgeführt wird.

Dieses Thema enthält folgende Abschnitte:

-   [Hinzufügen von zu verwaltenden Servern](#BKMK_add)

-   [Angeben von Anmeldeinformationen mit dem Befehl "Verwalten als"](#BKMK_creds)

## <a name="provide-credentials-with-the-manage-as-command"></a><a name=BKMK_creds></a>Angeben von Anmeldeinformationen mit dem Befehl "Verwalten als"
Wenn Sie Server-Manager Remote Server hinzufügen, benötigen einige der Server, die Sie hinzufügen, möglicherweise andere Anmelde Informationen für das Benutzerkonto, um darauf zuzugreifen oder Sie zu verwalten. Um Anmelde Informationen für einen verwalteten Server anzugeben, die sich von denen unterscheiden, die Sie zum Anmelden an dem Computer verwenden, auf dem Server-Manager ausgeführt wird, verwenden Sie den Befehl **verwalten als** , nachdem Sie einen Server zu Server-Manager hinzugefügt haben. Klicken Sie hierzu mit der rechten Maustaste auf den Eintrag für einen verwalteten Server auf der Kachel **Server** einer Rollen-oder Gruppen-Startseite. Beim Klicken auf **Verwalten als** wird das Dialogfeld **Windows-Sicherheit** geöffnet, in dem Sie einen Benutzernamen, der auf dem verwalteten Server über Zugriffsrechte verfügt, in einem der folgenden Formate eingeben können.

-   *Benutzername*

-   *Benutzername*@example.domain.com

-   *Domäne* \\ *Benutzername*

Das Dialogfeld **Windows-Sicherheit** , das mit dem Befehl **verwalten als** geöffnet wird, kann keine Smartcard-Anmelde Informationen akzeptieren. das Angeben von Smartcard-Anmelde Informationen über Server-Manager wird nicht unterstützt. Anmelde Informationen, die Sie mit dem Befehl **verwalten als** für einen verwalteten Server bereitstellen, werden zwischengespeichert und beibehalten, solange Sie den Server mit dem gleichen Computer verwalten, auf dem Sie zurzeit Server-Manager ausführen, oder solange Sie Sie nicht überschreiben, indem Sie für denselben Server leere oder andere Anmelde Informationen angeben. Wenn Sie Ihre Server-Manager Einstellungen auf andere Computer exportieren oder Ihr Domänen Profil als Roaming konfigurieren, damit Server-Manager Einstellungen auf anderen Computern verwendet werden können, werden die **Verwaltung als** Anmelde Informationen für Server in Ihrem Server Pool nicht im Server gespeicherten Profil gespeichert. Server-Manager Benutzer müssen Sie auf allen Computern hinzufügen, von denen Sie verwaltet werden möchten.

Nachdem Sie anhand der in diesem Thema beschriebenen Verfahren zu verwaltende Server hinzugefügt haben, jedoch vor der Verwendung des Befehls **Verwalten als** zum Angeben alternativer Anmeldeinformationen, die zum Verwalten eines von Ihnen hinzugefügten Servers erforderlich sein könnten, können die folgenden Verwaltbarkeitsstatusfehler für den Server angezeigt werden:

-   Fehler bei Kerberos-Zielauflösung

-   Fehler bei Kerberos-Authentifizierung

-   Online – Zugriff verweigert

> [!NOTE]
> Zu den Rollen und Features, die den Befehl **verwalten als** nicht unterstützen, gehören Remotedesktopdienste (RDS) und IP-Adress Verwaltungs Server (IPAM). Wenn Sie den Remote-RDS oder IPAM-Server nicht mit den gleichen Anmelde Informationen verwalten können, die Sie auf dem Computer verwenden, auf dem Sie Server-Manager ausführen, fügen Sie das Konto, das Sie in der Regel zur Verwaltung dieser Remote Server verwenden, der Gruppe "Administratoren" auf dem Computer, auf dem Server-Manager ausgeführt wird, hinzu. Melden Sie sich dann bei dem Computer, auf dem Server-Manager ausgeführt wird, mit dem Konto an, das Sie zum Verwalten des Remote Servers verwenden, auf dem rdS oder IPAM ausgeführt wird.

## <a name="add-servers-to-manage"></a><a name=BKMK_add></a>Hinzufügen zu verwaltender Server
Sie können Server zu Server-Manager hinzufügen, die Sie verwalten möchten, indem Sie eine der drei Methoden im Dialogfeld **Server hinzufügen** verwenden.

-   **Active Directory Domain Services** Hinzufügen von Servern zum Verwalten von Active Directory in derselben Domäne wie der lokale Computer.

-   **Domain Name System (DNS)-Eintrag** Suchen Sie anhand des Computernamens oder der IP-Adresse nach zu verwaltenden Servern.

-   **Importieren mehrerer Server** Geben Sie mehrere zu importierende Server in einer Datei an, die Server enthält, die nach Computername oder IP-Adresse aufgelistet sind.

#### <a name="to-add-servers-to-the-server-pool"></a>So fügen Sie Server zum Serverpool hinzu

1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

    -   Klicken Sie auf dem Windows- **Start** Bildschirm auf die Kachel Server-Manager.

2.  Klicken Sie im Menü **Verwalten** auf **Server hinzufügen**.

3.  Führen Sie einen der folgenden Schritte aus:

    -   Wählen Sie auf der Registerkarte **Active Directory** die Server aus, die sich in der aktuellen Domäne befinden. Halten Sie die STRG-Taste**** gedrückt, um mehrere Server auszuwählen. Klicken Sie auf die Schaltfläche mit dem Pfeil nach rechts, um ausgewählte Server in die Liste **ausgewählt** zu verschieben.

    -   Geben Sie auf der Registerkarte **DNS** die ersten Zeichen eines Computernamens oder einer IP-Adresse ein, und drücken Sie dann die EINGABETASTE****, oder klicken Sie auf **Suchen**. Wählen Sie die hinzu zufügenden Server aus, und klicken Sie dann auf die Schaltfläche mit dem Pfeil nach rechts.

    -   Suchen Sie auf der Registerkarte **importieren** nach einer Textdatei mit den DNS-Namen oder IP-Adressen der Computer, die Sie hinzufügen möchten (ein Name oder eine IP-Adresse pro Zeile).

4.  Klicken Sie nach dem Hinzufügen der Server auf **OK**.

### <a name="add-and-manage-servers-in-workgroups"></a>Hinzufügen und Verwalten von Servern in Arbeitsgruppen
Obwohl das Hinzufügen von Servern, die zu Server-Manager in Arbeitsgruppen vorhanden sind, möglicherweise erfolgreich ist, können nach dem Hinzufügen der Spalte **Verwaltbarkeit** der Kachel **Server** auf einer Rollen-oder Gruppenseite, die einen Arbeitsgruppenserver enthält, **Anmelde Informationen ohne gültige** Fehler angezeigt werden, die auftreten, wenn Sie versuchen, eine Verbindung mit dem Remote Arbeitsgruppenserver herzustellen oder Daten zu sammeln

Diese oder ähnliche Fehler können unter den folgenden Bedingungen auftreten.

-   Der verwaltete Server befindet sich in derselben Arbeitsgruppe wie der Computer, auf dem Server-Manager ausgeführt wird.

-   Der verwaltete Server befindet sich in einer anderen Arbeitsgruppe als der Computer, auf dem Server-Manager ausgeführt wird.

-   Einer der Computer befindet sich in einer Arbeitsgruppe, der andere in einer Domäne.

-   Der Computer, auf dem Server-Manager ausgeführt wird, befindet sich in einer Arbeitsgruppe, und verwaltete Remote Server befinden sich in einem anderen Subnetz.

-   Beide Computer befinden sich in Domänen, aber es besteht keine Vertrauensstellung zwischen den beiden Domänen.

-   Beide Computer befinden sich in Domänen, aber es besteht nur eine einseitige Vertrauensstellung zwischen den beiden Domänen.

-   Der Server, den Sie verwalten möchten, wurde mithilfe seiner IP-Adresse hinzugefügt.

##### <a name="to-add-remote-workgroup-servers-to-server-manager"></a>So fügen Sie Remotearbeitsgruppenserver zum Server-Manager hinzu

1.  Fügen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, den Namen des Arbeitsgruppen Servers zur Liste " **Treuhänder Hosts** " hinzu. Dies ist eine Voraussetzung für die NTLM-Authentifizierung. Um einen Computernamen einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen, fügen Sie dem Befehl den Parameter `Concatenate` hinzu. Verwenden Sie beispielsweise den folgenden Befehl, um den Computer `Server01` zu einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Stellen Sie fest, ob sich der Arbeitsgruppenserver, den Sie verwalten möchten, im gleichen Subnetz wie der Computer befindet, auf dem Server-Manager ausgeführt wird.

    Wenn sich die beiden Computer im gleichen Subnetz befinden oder wenn das Netzwerk Profil des Arbeitsgruppen Servers im **Netzwerk-und Freigabe Center**auf **Privat** festgelegt ist, fahren Sie mit dem nächsten Schritt fort.

    Wenn Sie sich nicht im gleichen Subnetz befinden oder wenn das Netzwerk Profil des Arbeitsgruppen Servers nicht auf **Privat**festgelegt ist, ändern Sie auf dem Arbeitsgruppenserver die Einstellung für Eingeh **Ende Windows-Remote Verwaltung (http eingehend)** in Windows-Firewall, um Verbindungen von Remote Computern explizit zuzulassen. Fügen Sie hierzu die Computernamen auf der Registerkarte **Computer** im Dialogfeld **Eigenschaften** der Einstellung hinzu.

3.  > [!IMPORTANT]
    > Durch das Ausführen des Cmdlets in diesem Schritt werden Mechanismen der Benutzerkontensteuerung außer Kraft gesetzt, die die Ausführung von Prozessen mit erhöhen Rechten auf Arbeitsgruppencomputern verhindern, sofern die Prozesse nicht über das integrierte Administrator- oder Systemkonto ausgeführt werden. Das Cmdlet ermöglicht es, dass Mitglieder der Administratorengruppe den Arbeitsgruppenserver verwalten, ohne dass sie sich über das integrierte Administratorkonto anmelden müssen. Wenn zusätzlichen Benutzern das Verwalten des Arbeitsgruppenservers ermöglicht wird, kann dies die Sicherheit des Servers herabsetzen. Diese Vorgehensweise ist jedoch sicherer, als die Anmeldeinformationen des integrierten Administratorkontos möglicherweise einer ganzen Gruppe von Personen zur Verfügung zu stellen, die für die Verwaltung des Arbeitsgruppenservers zuständig sind.

    Wenn Sie für Prozesse, die mit erhöhen Rechten auf Arbeitsgruppencomputern ausgeführt werden, die Einschränkungen der Benutzerkontensteuerung (UAC) überschreiben möchten, erstellen Sie auf dem Arbeitsgruppenserver einen Registrierungseintrag namens **LocalAccountTokenFilterPolicy**, indem Sie das folgende Cmdlet ausführen.

    ```
    New-ItemProperty -Name LocalAccountTokenFilterPolicy -path HKLM:\SOFTWARE\Microsoft\Windows\Currentversion\Policies\System -propertytype DWord -value 1
    ```

4.  Öffnen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, die Seite **alle Server** .

5.  Wenn sich der Computer, auf dem Server-Manager ausgeführt wird, und der Ziel-Arbeitsgruppen Server in derselben Arbeitsgruppe befinden, fahren Sie mit dem letzten Schritt fort. Befinden sich die beiden Computer nicht in derselben Arbeitsgruppe, klicken Sie mit der rechten Maustaste in der Kachel **Server** auf den Ziel-Arbeitsgruppenserver, und klicken Sie dann auf **Verwalten als**.

6.  Melden Sie sich am Arbeitsgruppenserver an, und verwenden Sie hierfür das integrierte Administratorkonto für den Arbeitsgruppenserver.

7.  Überprüfen Sie, ob Server-Manager eine Verbindung mit dem Arbeitsgruppenserver herstellen und Daten sammeln kann, indem Sie die Seite **alle Server** aktualisieren und dann den verwaltbarkeitsstatus für den Arbeitsgruppenserver anzeigen.

##### <a name="to-add-remote-servers-when-server-manager-is-running-on-a-workgroup-computer"></a>So fügen Sie Remoteserver hinzu, wenn der Server-Manager auf einem Arbeitsgruppencomputer ausgeführt wird

1.  Fügen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, der Liste " **Treuhänder** " des lokalen Computers in einer Windows PowerShell-Sitzung Remote Server hinzu. Um einen Computernamen einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen, fügen Sie dem Befehl den Parameter `Concatenate` hinzu. Verwenden Sie beispielsweise den folgenden Befehl, um den Computer `Server01` zu einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Stellen Sie fest, ob sich der zu verwaltende Server im gleichen Subnetz wie der Arbeitsgruppen Computer befindet, auf dem Server-Manager ausgeführt wird.

    Wenn sich die beiden Computer im gleichen Subnetz befinden oder wenn das Netzwerk Profil des Arbeitsgruppen Computers im **Netzwerk-und Freigabe Center**auf **Privat** festgelegt ist, fahren Sie mit dem nächsten Schritt fort.

    Wenn Sie sich nicht im gleichen Subnetz befinden oder wenn das Netzwerk Profil des Arbeitsgruppen Computers nicht auf **Privat**festgelegt ist, ändern Sie auf dem Arbeitsgruppen Computer, auf dem Server-Manager ausgeführt wird, die Einstellung für Eingeh **Ende Windows-Remote Verwaltung (http eingehend)** in der Windows-Firewall, um Verbindungen von Remote Computern explizit zuzulassen. Fügen Sie hierzu die Computernamen auf der Registerkarte **Computer** **im Dialogfeld**

3.  Öffnen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, die Seite **alle Server** .

4.  Vergewissern Sie sich, dass Server-Manager eine Verbindung mit dem Remote Server herstellen und Daten vom Remote Server sammeln kann, indem Sie die Seite **alle Server** aktualisieren und dann den verwaltbarkeitsstatus für den Remote Server anzeigen. Wenn auf der Kachel **Server** immer noch ein Verwaltbarkeitsfehler für den Remoteserver angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

5.  Melden Sie sich vom Computer ab, auf dem Sie Server-Manager ausführen, und melden Sie sich dann wieder mit dem integrierten Administrator Konto an. Wiederholen Sie den vorherigen Schritt, um zu überprüfen, ob Server-Manager eine Verbindung mit dem Remote Server herstellen und Daten vom Remote Server sammeln kann.

Wenn Sie die Verfahren in diesem Abschnitt befolgt haben und weiterhin Probleme beim Verwalten von Arbeitsgruppen Computern oder bei der Verwaltung anderer Computer von Arbeitsgruppen Computern haben, finden Sie weitere Informationen unter [about_remote_Troubleshooting](/previous-versions/dd347642(v=technet.10)) auf der Microsoft-Website.

### <a name="add-and-manage-servers-in-clusters"></a>Hinzufügen und Verwalten von Servern in Clustern
Sie können Server-Manager zum Verwalten von Servern verwenden, die sich in Failoverclustern (auch Server Cluster oder MSCS genannt) befinden. Server in Failoverclustern (unabhängig davon, ob die Cluster Knoten physisch oder virtuell sind) weisen einige eindeutige Verhaltensweisen und Verwaltungs Einschränkungen in Server-Manager auf.

-   Physische und virtuelle Server in Clustern werden Server-Manager automatisch hinzugefügt, wenn Server-Manager ein Server im Cluster hinzugefügt wird. Wenn Sie einen geclusterten Server aus Server-Manager entfernen, werden Sie aufgefordert, andere Server im Cluster zu entfernen.

-   Server-Manager zeigt keine Daten für gruppierte virtuelle Server an, da die Daten dynamisch sind und identisch mit den Daten für den Server sind, auf dem der virtuelle Cluster Knoten gehostet wird. Sie können den Server auswählen, der den virtuellen Server zum Anzeigen der Daten hostet.

-   Wenn Sie Server-Manager mithilfe des Namens des virtuellen Cluster Objekts des Servers einen Server hinzufügen, wird der Name des virtuellen Objekts in Server-Manager anstelle des Namens des physischen Servers angezeigt (erwartet).

-   Sie können auf einem gruppierten virtuellen Server keine Rollen und Features installieren.

## <a name="see-also"></a>Weitere Informationen
[Server-Manager](server-manager.md) 
 [Erstellen und Verwalten von Server Gruppen](create-and-manage-server-groups.md)