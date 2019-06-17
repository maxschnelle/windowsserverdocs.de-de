---
title: Hinzufügen von Servern zu Server-Manager
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aab895f2-fe4d-4408-b66b-cdeadbd8969e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.localizationpriority: medium
ms.date: 02/01/2018
ms.openlocfilehash: a47ecbc0c7359438ed60ed34c94adf0096b14967
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435449"
---
# <a name="add-servers-to-server-manager"></a>Hinzufügen von Servern zu Server-Manager

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In Windows Server können Sie mehrere Remoteserver mit einer einzigen Server-Manager-Konsole verwalten. Server, die Sie mithilfe von Server-Manager verwalten möchten, können Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen. Beachten Sie, dass eine neuere Version von Windows Server nicht mit einer älteren Version des Server-Manager verwaltet werden kann.

In diesem Thema wird beschrieben, wie Sie dem Server-Manager-Serverpool Server hinzufügen können.

> [!NOTE]
> Bei unseren Tests lassen sich mit dem Server-Manager in Windows Server 2012 und späteren Versionen von Windows Server bis zu 100 Server verwalten, die mit einer typischen Arbeitsauslastung konfiguriert sind. Die Anzahl der Server, die Sie mit einer einzelnen Server-Manager-Konsole verwalten können, kann von der Datenmenge abhängig sein, die Sie von den verwalteten Servern anfordern, sowie von den Hardware- und Netzwerkressourcen, die für den Computer mit dem Server-Manager zur Verfügung stehen. Wenn die anzuzeigende Datenmenge die Ressourcenkapazität des Computers erreicht, kann es zu langsamen Reaktionszeiten des Server-Managers und Verzögerungen bei der Durchführung von Aktualisierungen kommen. Um die Anzahl der Server zu erhöhen, die Sie mit dem Server-Manager verwalten können, sollten Sie die Ereignisdaten, die der Server-Manager von den verwalteten Servern empfängt, über das Dialogfeld **Ereignisdaten konfigurieren** beschränken. Sie können das Dialogfeld über das Menü **Aufgaben** in der Kachel **Ereignisse** öffnen. Wenn Sie in Ihrer Organisation eine organisationsübergreifende Anzahl von Servern verwalten müssen, wird empfohlen, die Produkte in der [Microsoft System Center-Suite](https://go.microsoft.com/fwlink/p/?LinkId=239437) auszuwerten.
> 
> Server-Manager kann von Servern unter Windows Server 2003 nur den Online- oder Offlinestatus empfangen. Obwohl Sie Server-Manager zum Ausführen von Verwaltungsaufgaben auf Servern unter Windows Server 2008 R2 oder Windows Server 2008 verwenden können, können Sie keine Rollen und Features auf Server hinzufügen, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.
> 
> Server-Manager kann nicht verwendet werden, um eine neuere Version des Betriebssystems Windows Server zu verwalten. Server-Manager auf Windows Server 2012 R2, Windows Server 2012, Windows 8.1 oder Windows 8 kann nicht verwendet werden, um Server unter Windows Server 2016 zu verwalten.

Dieses Thema enthält die folgenden Abschnitte:

-   [Fügen Sie zu verwaltende Server hinzu](#BKMK_add)

-   [Geben Sie Anmeldeinformationen mit dem Befehl verwalten als](#BKMK_creds)

## <a name="BKMK_creds"></a>Geben Sie Anmeldeinformationen mit dem Befehl verwalten als
Wenn Sie dem Server-Manger Remoteserver hinzufügen, sind für den Zugriff auf einige dieser Server sowie für deren Verwaltung unterschiedliche Benutzerkonten-Anmeldeinformationen erforderlich. Um Anmeldeinformationen für einen verwalteten Server anzugeben, die sich von denen unterscheiden, die Sie verwenden, um sich bei dem Computer anzumelden, auf dem Sie den Server-Managern ausführen, verwenden Sie den Befehl **Verwalten als**, nachdem Sie dem Server-Manager einen Server hinzugefügt haben. Hierzu klicken Sie mit der rechten Maustaste auf der Kachel **Server** einer Rollen- oder Gruppen-Homepage auf den Eintrag für einen verwalteten Server. Beim Klicken auf **Verwalten als** wird das Dialogfeld **Windows-Sicherheit** geöffnet, in dem Sie einen Benutzernamen, der auf dem verwalteten Server über Zugriffsrechte verfügt, in einem der folgenden Formate eingeben können.

-   *Benutzername*

-   *Benutzername*@example.domain.com

-   *Domäne*\\*Benutzername*

Das Dialogfeld **Windows-Sicherheit**, das mit dem Befehl **Verwalten als** geöffnet wird, kann keine Smartcardanmeldeinformationen akzeptieren; die Bereitstellung von Smartcardanmeldeinformationen über den Server-Manager wird nicht unterstützt. Anmeldeinformationen, die Sie mit dem Befehl **Verwalten als** für einen verwalteten Server eingeben, werden zwischengespeichert und beibehalten, solange Sie den Server mit dem gleichen Computer verwalten, auf dem Sie derzeit den Server-Manager ausführen, oder solange Sie sie nicht mit leeren oder anderen Anmeldeinformationen für den gleichen Server überschreiben. Wenn Sie Ihre Server-Manager-Einstellungen auf andere Computer exportieren, oder Ihr Domänenprofil als servergespeichert konfigurieren, um die Nutzung von Server-Manager-Einstellungen auf anderen Computern zu ermöglichen, werden **Verwalten als**-Anmeldeinformationen für Server in Ihrem Serverpool nicht als servergespeichertes Profil gespeichert. Server-Manager-Benutzer müssen diese auf dem jeweiligen Computer hinzufügen, den sie verwalten wollen.

Nachdem Sie anhand der in diesem Thema beschriebenen Verfahren zu verwaltende Server hinzugefügt haben, jedoch vor der Verwendung des Befehls **Verwalten als** zum Angeben alternativer Anmeldeinformationen, die zum Verwalten eines von Ihnen hinzugefügten Servers erforderlich sein könnten, können die folgenden Verwaltbarkeitsstatusfehler für den Server angezeigt werden:

-   Fehler bei Kerberos-Zielauflösung

-   Fehler bei Kerberos-Authentifizierung

-   Online – Zugriff verweigert

> [!NOTE]
> Zu den Rollen und Features, die den Befehl **Verwalten als** nicht unterstützen, zählen Remotedesktopdienste (Remotedesktopdienste, RDS) und IP-Adressverwaltung-Server (IP Address Management, IPAM). Wenn Sie den RDS oder IPAM-Server nicht mit den gleichen Anmeldeinformationen verwalten können, die Sie auf dem Computer verwenden, auf dem Sie den Server-Manager ausführen, versuchen Sie, das Konto, das Sie in der Regel verwenden, um diese Remoteserver zu verwalten, der Gruppe "Administratoren" auf dem Computer hinzuzufügen, der den Server-Manager ausführt. Melden Sie sich dann bei dem Computer, auf dem der Server-Manager ausgeführt wird, mit dem Konto an, das Sie verwenden, um den Remoteserver zu verwalten, auf dem RDS oder IPAM ausgeführt wird.

## <a name="BKMK_add"></a>Fügen Sie zu verwaltende Server hinzu
Sie können Server-Manager zu verwaltende Server hinzufügen, indem Sie eine der drei Methoden verwenden, die im Dialogfeld **Server hinzufügen** verfügbaren sind.

-   **Active Directory Domain Servicese (AD DS)** Fügen Sie zu verwaltende Server hinzu, die von Active Directory in derselben Domäne gefunden werden, in der sich der lokale Computer befindet.

-   **Domain Name System (DNS)-Eintrag** Suchen Sie anhand des Computernamens oder der IP-Adresse nach zu verwaltenden Servern.

-   **Mehrere Server importieren** Geben Sie mehrere zu importierende Server in einer Datei an, in der die Server anhand des Computernamens oder der IP-Adresse aufgelistet sind.

#### <a name="to-add-servers-to-the-server-pool"></a>So fügen Sie Server zum Serverpool hinzu

1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

    -   Klicken Sie auf der Windows-**Startseite** auf die Kachel Server-Manager.

2.  Klicken Sie im Menü **Verwalten** auf **Server hinzufügen**.

3.  Führen Sie eine der folgenden Aktionen aus.

    -   Wählen Sie auf der Registerkarte **Active Directory** die Server aus, die sich in der aktuellen Domäne befinden. Halten Sie die STRG-Taste **** gedrückt, um mehrere Server auszuwählen. Klicken Sie auf die Schaltfläche mit dem Pfeil nach rechts, um die ausgewählten Server in die Liste **ausgewählt** zu verschieben.

    -   Geben Sie auf der Registerkarte **DNS** die ersten Zeichen eines Computernamens oder einer IP-Adresse ein, und drücken Sie dann die EINGABETASTE **** , oder klicken Sie auf **Suchen**. Wählen Sie die hinzuzufügenden Server aus, und klicken Sie dann auf die Schaltfläche mit dem Pfeil nach rechts.

    -   Suchen Sie auf der Registerkarte **Import** nach einer Textdatei mit den DNS-Namen oder IP-Adressen der Computer, die Sie hinzufügen möchten (die Datei enthält jeweils einen Namen oder eine IP-Adresse pro Zeile).

4.  Klicken Sie nach dem Hinzufügen der Server auf **OK**.

### <a name="add-and-manage-servers-in-workgroups"></a>Hinzufügen und Verwalten von Servern in Arbeitsgruppen
Es kann möglich sein, dem Server-Manager Server hinzuzufügen, die sich in Arbeitsgruppen befinden. Aber nach dem Hinzufügen werden in der Spalte **Verwaltbarkeit** der Kachel **Server** (auf einer Rollen- oder Gruppenseite, die einen Arbeitsgruppenserver enthält) ggf. Fehler vom Typ **Anmeldeinformationen nicht gültig** angezeigt, wenn versucht wird, eine Verbindung mit einem Remote-Arbeitsgruppenserver herzustellen oder Daten von diesem Server zu sammeln.

Diese oder ähnliche Fehler können unter den folgenden Bedingungen auftreten.

-   Der verwaltete Server befindet sich in der gleichen Arbeitsgruppe wie der Computer, auf dem der Server-Manager ausgeführt wird.

-   Der verwaltete Server befindet sich in einer anderen Arbeitsgruppe als der Computer, auf dem der Server-Manager ausgeführt wird.

-   Einer der Computer befindet sich in einer Arbeitsgruppe, der andere in einer Domäne.

-   Der Computer, auf dem der Server-Manager ausgeführt wird, befindet sich in einer Arbeitsgruppe, und verwaltete Remoteserver befinden sich in einem anderen Subnetz.

-   Beide Computer befinden sich in Domänen, aber es besteht keine Vertrauensstellung zwischen den beiden Domänen.

-   Beide Computer befinden sich in Domänen, aber es besteht nur eine einseitige Vertrauensstellung zwischen den beiden Domänen.

-   Der Server, den Sie verwalten möchten, wurde mithilfe seiner IP-Adresse hinzugefügt.

##### <a name="to-add-remote-workgroup-servers-to-server-manager"></a>So fügen Sie Remotearbeitsgruppenserver zum Server-Manager hinzu

1.  Fügen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, den Namen des Arbeitsgruppenservers der Liste **TrustedHosts** hinzu. Dies ist eine Voraussetzung für die NTLM-Authentifizierung. Um einen Computernamen einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen, fügen Sie dem Befehl den Parameter `Concatenate` hinzu. Verwenden Sie beispielsweise den folgenden Befehl, um den Computer `Server01` zu einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Stellen Sie fest, ob die Arbeitsgruppe, die Sie verwalten möchten, sich im gleichen Subnetz wie der Arbeitsgruppencomputer befindet, auf dem Sie Server-Manager ausführen.

    Wenn sich die beiden Computer im gleichen Subnetz befinden oder wenn das Netzwerkprofil des Arbeitsgruppenservers im **Netzwerk- und Freigabecenter** auf **Privat** gesetzt ist, fahren Sie mit dem nächsten Schritt fort.

    Wenn sie sich nicht im gleichen Subnetz befinden oder wenn das Netzwerkprofil des Arbeitsgruppenservers nicht auf **Privat** gesetzt ist, ändern Sie auf dem Arbeitsgruppenserver in der Windows-Firewall die eingehende Einstellung **Windows-Remoteverwaltung (HTTP eingehend)** , um Verbindungen von Remotecomputern explizit zuzulassen. Fügen Sie hierzu die Computernamen auf der Registerkarte **Computer** im Dialogfeld **Eigenschaften** der Einstellung hinzu.

3.  > [!IMPORTANT]
    > Durch das Ausführen des Cmdlets in diesem Schritt werden Mechanismen der Benutzerkontensteuerung außer Kraft gesetzt, die die Ausführung von Prozessen mit erhöhen Rechten auf Arbeitsgruppencomputern verhindern, sofern die Prozesse nicht über das integrierte Administrator- oder Systemkonto ausgeführt werden. Das Cmdlet ermöglicht es, dass Mitglieder der Administratorengruppe den Arbeitsgruppenserver verwalten, ohne dass sie sich über das integrierte Administratorkonto anmelden müssen. Wenn zusätzlichen Benutzern das Verwalten des Arbeitsgruppenservers ermöglicht wird, kann dies die Sicherheit des Servers herabsetzen. Diese Vorgehensweise ist jedoch sicherer, als die Anmeldeinformationen des integrierten Administratorkontos möglicherweise einer ganzen Gruppe von Personen zur Verfügung zu stellen, die für die Verwaltung des Arbeitsgruppenservers zuständig sind.

    Wenn Sie für Prozesse, die mit erhöhen Rechten auf Arbeitsgruppencomputern ausgeführt werden, die Einschränkungen der Benutzerkontensteuerung (UAC) überschreiben möchten, erstellen Sie auf dem Arbeitsgruppenserver einen Registrierungseintrag namens **LocalAccountTokenFilterPolicy** , indem Sie das folgende Cmdlet ausführen.

    ```
    New-ItemProperty -Name LocalAccountTokenFilterPolicy -path HKLM:\SOFTWARE\Microsoft\Windows\Currentversion\Policies\System -propertytype DWord -value 1
    ```

4.  Öffnen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, die Seite **Alle Server**.

5.  Wenn sich der Computer, auf dem Server-Manager ausgeführt wird, und der Ziel-Arbeitsgruppenserver in derselben Arbeitsgruppe befinden, fahren Sie mit dem letzten Schritt fort. Befinden sich die beiden Computer nicht in derselben Arbeitsgruppe, klicken Sie mit der rechten Maustaste in der Kachel **Server** auf den Ziel-Arbeitsgruppenserver, und klicken Sie dann auf **Verwalten als**.

6.  Melden Sie sich am Arbeitsgruppenserver an, und verwenden Sie hierfür das integrierte Administratorkonto für den Arbeitsgruppenserver.

7.  Stellen Sie sicher, dass Server-Manager eine Verbindung mit dem Arbeitsgruppenserver herstellen und Daten von diesem Server sammeln kann, indem Sie die Seite **Alle Server** aktualisieren und dann den Verwaltbarkeitsstatus für den Arbeitsgruppenserver anzeigen.

##### <a name="to-add-remote-servers-when-server-manager-is-running-on-a-workgroup-computer"></a>So fügen Sie Remoteserver hinzu, wenn der Server-Manager auf einem Arbeitsgruppencomputer ausgeführt wird

1.  Fügen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, der Liste **TrustedHosts** des lokalen Computers in einer Windows PowerShell-Sitzung Remoteserver hinzu. Um einen Computernamen einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen, fügen Sie dem Befehl den Parameter `Concatenate` hinzu. Verwenden Sie beispielsweise den folgenden Befehl, um den Computer `Server01` zu einer vorhandenen Liste vertrauenswürdiger Hosts hinzuzufügen.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Stellen Sie fest, ob die Arbeitsgruppe, die Sie verwalten möchten, sich im gleichen Subnetz wie der Arbeitsgruppencomputer befindet, auf dem Sie Server-Manager ausführen.

    Wenn sich die beiden Computer im gleichen Subnetz befinden oder wenn das Netzwerkprofil des Arbeitsgruppencomputers im **Netzwerk- und Freigabecenter** auf **Privat** gesetzt ist, fahren Sie mit dem nächsten Schritt fort.

    Wenn sie sich nicht im gleichen Subnetz befinden oder wenn das Netzwerkprofil des Arbeitsgruppencomputers nicht auf **Privat** gesetzt ist, ändern Sie auf dem Arbeitsgruppencomputer, auf dem Server-Manager ausgeführt wird, in der Windows-Firewall die eingehende Einstellung **Windows-Remoteverwaltung (HTTP eingehend)** , um Verbindungen von Remotecomputern explizit zuzulassen. Fügen Sie hierzu die Computernamen auf der Registerkarte **Computer** im Dialogfeld **Eigenschaften** der Einstellung hinzu.

3.  Öffnen Sie auf dem Computer, auf dem Server-Manager ausgeführt wird, die Seite **Alle Server**.

4.  Stellen Sie sicher, dass Server-Manager eine Verbindung mit dem Remoteserver herstellen und Daten von diesem Server sammeln kann, indem Sie die Seite **Alle Server** aktualisieren und dann den Verwaltbarkeitsstatus für den Remoteserver anzeigen. Wenn auf der Kachel **Server** immer noch ein Verwaltbarkeitsfehler für den Remoteserver angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

5.  Melden Sie sich vom Computer ab, auf dem Server-Manager ausgeführt wird, und melden Sie sich dann wieder mit dem integrierten Administratorkonto an. Wiederholen Sie den vorherigen Schritt, um sicherzustellen, dass Server-Manager über eine Verbindung mit dem Remoteserver hergestellt und Daten vom Remoteserver gesammelt werden können.

Wenn Sie die Verfahren in diesem Abschnitt befolgt haben und weiter Probleme mit dem Verwalten von Arbeitsgruppencomputern oder Verwalten anderer Computer von Arbeitsgruppencomputern aus haben, finden Sie weitere Informationen im Thema [zur Remoteproblembehandlung](https://technet.microsoft.com/library/dd347642.aspx) auf der Microsoft-Website.

### <a name="add-and-manage-servers-in-clusters"></a>Hinzufügen und Verwalten von Servern in Clustern
Sie können den Server-Manager zur Verwaltung von Servern verwenden, die sich in Failoverclustern (auch Servercluster oder MSCS genannt) befinden. Server in Failoverclustern – unabhängig davon, ob die Clusterknoten physisch oder virtuell sind – weisen einige eindeutige Verhaltensweisen und Verwaltungseinschränkungen im Server-Manager auf.

-   Physische und virtuelle Server in Clustern werden dem Server-Manager automatisch hinzugefügt, wenn ein Server im Cluster dem Server-Manager hinzugefügt wird. Wenn Sie einen gruppierten Server aus dem Server-Manager entfernen, werden Sie entsprechend gefragt, ob andere Server im Cluster entfernt werden sollen.

-   Server-Manager zeigt keine Daten für gruppierte virtuelle Server an, da die Daten dynamisch und identisch mit den Daten für den Server sind, auf dem der virtuelle Clusterknoten gehostet wird. Sie können den Server auswählen, der den virtuellen Server zum Anzeigen der Daten hostet.

-   Wenn Sie dem Server-Manager einen Server unter Verwendung des Namens seines virtuellen Clusterobjekts hinzufügen, wird in Server-Manager der Name des virtuellen Objekts anstelle des Namens des physischen Servers angezeigt (erwartet).

-   Sie können auf einem gruppierten virtuellen Server keine Rollen und Features installieren.

## <a name="see-also"></a>Siehe auch
[Server-Manager](server-manager.md)
[Erstellen und Verwalten von Servergruppen](create-and-manage-server-groups.md)
