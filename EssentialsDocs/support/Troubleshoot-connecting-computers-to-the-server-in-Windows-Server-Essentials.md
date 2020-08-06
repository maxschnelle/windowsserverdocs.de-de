---
title: Problembehandlung beim Verbinden von Computern mit dem Server in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e832957a5d44851131cb622e4c3bf9d99d4e4a7f
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838269"
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Problembehandlung beim Verbinden von Computern mit dem Server in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Dieses Thema enthält Anleitungen zur Problembehandlung bei Problemen, die auftreten können, wenn Sie einen Computer mit dem Server verbinden, auf dem Windows Server Essentials oder Windows Server Essentials ausgeführt wird.

> [!NOTE]
>  Die aktuellsten Informationen zur Problembehandlung aus der Windows Server Essentials-und der Windows Server Essentials-Community finden Sie im [Windows Server Essentials-Forum](/answers/topics/windows-server-essentials.html). Das Windows Server Essentials-Forum eignet sich optimal, um nach Hilfe zu suchen oder um Fragen zu stellen.

 Dieses Thema bietet Lösungen für die folgenden Probleme:


-   Problem 1: [Problem 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)

-   Problem 2: [Problem 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)

-   Problem 3: [Problem 3](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)

-   Problem 4: [Problem 4](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)

-   Problem 5: [Problem 5](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)

-   Problem 6: [Problem 6](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)

-   Problem 7: [Problem 7](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)

-   Problem 8: [Problem 8](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)

-   Problem 9: [Problem 9](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)

-   Problem 10: [Problem 10](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)

-   Problem 11: [Problem 11](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)


##  <a name="issue-1"></a><a name="BMRK_Package"></a>Problem 1
 **Problem**

 Ich erhalte, dass eine Paketinstallation nicht erfolgreich war. Versuchen Sie, den Windows Server Essentials-Connector erneut zu installieren. Wenn das Problem weiterhin besteht, wenden Sie sich an den Netzwerkadministrator, wenn Sie einen Computer mit dem Server verbinden.

 **Beschreibung**

 Dieses Problem kann auftreten, wenn Sie einen Computer mit einem Server verbinden, auf dem Windows Server Essentials ausgeführt wird, während andere Windows-Updates oder Anwendungs Installationen ausstehen und die Connector-Installation abgebrochen wird.

 **Lösung**

 Schließen Sie alle anderen Updates und Anwendungsinstallationen ab. Starten Sie den Computer bei entsprechender Aufforderung neu.

##  <a name="issue-2"></a><a name="BKMK_ConnectorIssue2"></a>Problem 2
 **Problem**

 Ein Computer kann nicht mit Windows Server Essentials verknüpft werden.

 **Beschreibung**

 Computer mit nicht-ASCII-Zeichen im Computernamen können nicht mit Windows Server Essentials verknüpft werden. Wenn der Computername Nicht-ASCII-Zeichen enthält, erhalten Sie die Fehlermeldung "Ein unerwarteter Fehler ist aufgetreten".

 **Lösung**

 Benennen Sie den Client Computer mit einem Namen um, der nur ASCII-Zeichen enthält, und versuchen Sie, den Computer erneut zu Windows Server Essentials hinzuzufügen.

##  <a name="issue-3"></a><a name="BKMK_ConnectorIssue2a"></a>Problem 3
 **Problem**

 Ich erhalte den Fehler "die Installation der Connector-Software wird abgebrochen" beim Verbinden eines Computers mit dem Server.

 **Beschreibung**

 Um einen Computer mit dem Server verbinden zu können, muss das System Konto über Vollzugriff auf Server Ordner verfügen, die auf dem Windows Server Essentials-Dashboard angezeigt werden. Wenn die erforderlichen Berechtigungen nicht erteilt wurden, wird die Fehlermeldung "Die Installation der Connectorsoftware wird abgebrochen" angezeigt.

 **Lösung**

 Erteilen Sie dem Konto SYSTEM die Berechtigung **Vollzugriff** für jeden Serverordner.

#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>So erteilen Sie dem Konto SYSTEM die Berechtigung "Vollzugriff" für jeden Serverordner

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf **Speicher** und anschließend auf **Serverordner**.

3.  Klicken Sie mit der rechten Maustaste auf den Serverordner, und klicken Sie dann auf **Ordner öffnen**. (Wenn die Option **Ordner öffnen** nicht angezeigt wird, müssen Sie keine Berechtigungen für den Ordner festlegen.)

4.  Klicken Sie im Netzwerkpfad oben im Windows-Explorer auf die Serverfreigabe, um freigegebene Ordner auf dem Server anzuzeigen. Wenn der Pfad z. B. **Netzwerk > Server01 > Sicherungen von Dateiversionsverläufen** lautet, klicken Sie auf **Server01**.

5.  Klicken Sie mit der rechten Maustaste auf einen Serverordner, und klicken Sie anschließend auf **Eigenschaften**.

6.  Klicken Sie auf die Registerkarte **Sicherheit** .

7.  Wenn **Vollzugriff** für das Konto SYSTEM nicht zulässig ist, klicken Sie auf **Bearbeiten** und dann auf **SYSTEM**. Aktivieren Sie unter **Berechtigungen für System** neben **Vollzugriff** das Kontrollkästchen **Zulassen**.

8.  Klicken Sie zweimal auf **OK**, um die Berechtigungen zu aktualisieren, und schließen Sie **Eigenschaften**.

##  <a name="issue-4"></a><a name="BKMK_ConnectorIssueNetFramework"></a>Problem 4
 **Problem**

 Zum Ausführen dieser Anwendung erhalte ich eine der folgenden Versionen des .NET Framework: v 4.5.50709 "Fehler beim Verbinden eines Computers mit dem Server.

 **Beschreibung**

 Wenn Sie einen Computer mit einem Server verbinden, auf dem Windows Server Essentials oder Windows Server Essentials ausgeführt wird, versucht der Assistent, .NET Framework Version 4.5.50709 auf dem Computer zu installieren. Wenn jedoch eine frühere Version von .NET Framework Version 4,5 vorhanden ist, kann die aktualisierte Version nicht installiert werden, und der Verbindungsversuch schlägt mit folgender Fehlermeldung fehl: zum Ausführen dieser Anwendung müssen Sie eine der folgenden Versionen der .NET Framework installieren: v 4.5.50709. Wenden Sie sich an Ihren Allocation Publisher, um eine Anleitung zum Abrufen der entsprechenden Version des .NET Framework zu erhalten.

 **Lösung**

 Deinstallieren Sie .NET Framework 4.5 vom Computer, und verbinden Sie den Computer anschließend mit dem Server.

#### <a name="to-uninstall-net-framework-45"></a>So deinstallieren Sie .NET Framework 4.5

1.  Öffnen Sie auf dem Clientcomputer auf der Seite **Start** die **Systemsteuerung**.

2.  Klicken Sie in der Systemsteuerung unter **Programme** auf **Programm deinstallieren**.

3.  Klicken Sie mit der rechten Maustaste auf **Microsoft .NET Framework 4.5**, und klicken Sie dann auf **Deinstallieren**.

4.  Nach der erfolgreichen Deinstallation von .NET Framework 4.5 verbinden Sie den Computer mit dem Server. Die richtige Version von .NET Framework 4.5 wird zusammen mit der Connectorsoftware installiert.

##  <a name="issue-5"></a><a name="BKMK_Time"></a>Problem 5
 **Problem**

 Ich erhalte, dass der Server nicht verfügbar ist. Wenden Sie sich an die für Ihr Netzwerk verantwortliche Person, um dieses Problem zu beheben. wenn sich ein Computer mit dem Server verbindet.

 **Beschreibung**

 Dies kann geschehen, wenn Datum und Uhrzeit auf dem verbundenen Computer nicht synchron mit Datum und Uhrzeit auf dem Server sind.  Windows Server Essentials und Windows Server Essentials verwenden den Zeit Synchronisierungs Dienst, um das Datum und die Uhrzeit von Computern zu synchronisieren, die in einem Windows Server Essentials-oder Windows Server Essentials-Netzwerk ausgeführt werden. Eine synchronisierte Uhrzeit ist wichtig, da das standardmäßig verwendete Authentifizierungsprotokoll die Uhrzeit des Servers für die Authentifizierung verwendet. Wenn beispielsweise die Uhr auf einem Client Computer nicht mit dem richtigen Datum und der richtigen Uhrzeit synchronisiert ist, interpretiert die Windows Server Essentials-oder Windows Server Essentials-Authentifizierung möglicherweise fälschlicherweise eine Anmelde Anforderung als Eindring Versuch und verweigert dem Benutzer den Zugriff.

 Dies kann vorkommen, wenn der freie Speicher des Servers weniger als 5% beträgt.

 Dies kann geschehen, wenn Sie bereits über eine VPN-Verbindung mit dem Windows Essentials-Server verfügen und versuchen, die Connectorsoftware extern mithilfe einer Domänenadresse zu konfigurieren.

 **Lösung**

1.  Synchronisieren Sie Datum und Uhrzeit auf dem Clientcomputer mit dem Server. Verbinden Sie dann den Computer erneut mit dem Server.

2.  Schließen Sie einige Programme auf dem Server, und verbinden Sie dann den Computer mit dem Server.

3.  Schließen Sie die VPN-Verbindung, und verbinden Sie dann den Computer mit dem Server.

#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>So ändern Sie Datum und Uhrzeit auf dem Clientcomputer

1. Öffnen Sie auf dem Clientcomputer auf der Seite **Start** die Systemsteuerung.

2. Klicken Sie in der Systemsteuerung auf **Zeit, Sprache und Region**, und klicken Sie dann auf **Datum und Uhrzeit**.

3. Klicken Sie auf **Datum und Uhrzeit ändern**, legen Sie Datum und Uhrzeit auf die gewünschten Angaben fest, und klicken Sie dann auf **OK**.

4. Klicken Sie auf **OK**, um die Systemsteuerung zu schließen.

5. Versuchen Sie erneut, den Clientcomputer mit dem Server zu verbinden. Anleitungen finden Sie unter "Verbinden von Computern mit dem Server".

   Wenn sich der Clientcomputer immer noch nicht mit dem Server verbinden kann, stellen Sie sicher, dass Datum und Uhrzeit auf dem Server richtig sind. Wenn Datum und Uhrzeit nicht richtig sind, ändern Sie die Angaben.

#### <a name="to-change-the-date-and-time-on-the-server"></a>So ändern Sie Datum und Uhrzeit auf dem Server

1.  Melden Sie sich mit dem Kennwort, das Sie während der Installation und Konfiguration von Windows Server Essentials oder Windows Server Essentials eingerichtet haben, beim Server an.

    > [!NOTE]
    >  Wenn Sie den Server remote verwalten, müssen Sie sich über eine Remotedesktopverbindung am Server anmelden.

2.  Öffnen Sie auf der Seite **Start** auf **Systemsteuerung**.

3.  Klicken Sie in der Systemsteuerung auf **Zeit, Sprache und Region**, und klicken Sie dann auf **Datum und Uhrzeit**.

4.  Klicken Sie auf **Datum und Uhrzeit ändern**, legen Sie Datum und Uhrzeit auf die gewünschten Angaben fest, und klicken Sie dann auf **OK**.

5.  Klicken Sie auf **OK**, um die Systemsteuerung zu schließen.

6.  Versuchen Sie auf dem Clientcomputer erneut, diesen mit dem Server zu verbinden. Anleitungen finden Sie unter "Verbinden von Computern mit dem Server".

##  <a name="issue-6"></a><a name="BKMK_ServiceStopped"></a>Problem 6
 **Problem**

 Es ist ein unerwarteter Fehler aufgetreten. Wenden Sie sich an die für Ihr Netzwerk verantwortliche Person, um dieses Problem zu beheben. wenn sich ein Computer mit dem Server verbindet.

 **Beschreibung**

 Wenn Sie diese Fehlermeldung erhalten, wird der Webdienst für WSS-Zertifikate ggf. nicht ausgeführt.

 **Lösung**

 Starten Sie den Webdienst für WSS-Zertifikate.

#### <a name="to-start-the-wss-certificate-web-service"></a>So starten Sie den Webdienst für WSS-Zertifikate.

1.  Öffnen Sie auf der Seite **Start** des Servers die Seite **Verwaltung**.

     Klicken Sie auf **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Internetinformationsdienste-Manager**, und klicken Sie dann auf **Öffnen**.

2.  Klicken Sie im Navigationsbereich auf **Webdienst für WSS-Zertifikate**.

3.  Klicken Sie im Bereich **Aktionen** auf **Starten**.

##  <a name="issue-7"></a><a name="BKMK_ConnectorIssueReconnect"></a>Problem 7
 **Problem**

 Wenn ich versuche, einen Computer nach einem erfolglosen Verbindungsversuch erneut mit dem Server zu verbinden, erhalte ich die Warnung, dass ein Computer mit diesem Namen bereits mit dem Server verbunden ist.

 **Beschreibung**

 Wenn ein früherer Versuch, einen Computer mit dem Server zu verbinden, abgebrochen oder unterbrochen wurde, erhalten Sie möglicherweise die folgende Warnung, wenn Sie versuchen, erneut eine Verbindung herzustellen: ein Computer mit diesem Namen ist bereits mit dem Server verbunden. Dies liegt daran, dass ein Zertifikat ausgestellt wurde, als Sie erstmals versucht haben, sich mit dem Server zu verbinden.

 **Lösung** Wenn Sie sicher sind, dass keine anderer Computer mit demselben Namen bereits mit dem Server verbunden ist, klicken Sie auf **Weiter** und befolgen dann die Anweisungen im Assistenten **Computer mit dem Server verbinden**.

##  <a name="issue-8"></a><a name="BKMK_JoinWin7"></a>Problem 8
 **Problem**

 Beim Versuch, einen Clientcomputer mit Windows 7 Home mit dem Server zu verbinden, wird die Webseite für die Ausführung der Connectorsoftware geöffnet, aber der Clientcomputer kann keine Verbindung mit dem Server herstellen.

 **Beschreibung**

 Wenn für den Router im Netzwerk Multicast aktiviert ist, funktioniert die Kommunikation zwischen dem Server und einem Clientcomputer mit Windows 7 Home Basic oder Windows 7 Home Premium nicht ordnungsgemäß.

 **Lösung**

 Deaktivieren Sie Multicast auf dem Router. Bei einigen Routern schließt dies ggf. das Deaktivieren des Routingprotokolls RIP-2M ein. Weitere Informationen finden Sie in der Dokumentation des Routerherstellers.

##  <a name="issue-9"></a><a name="BKMK_ConnectorIssueAutologon"></a>Problem 9
 **Problem**

 Die automatische Anmeldung wurde beendet, nachdem ich den Computer mit dem Server verbunden habe.

 **Beschreibung**

 Wenn die automatische Anmeldung für das Benutzerkonto festgelegt wird, wenn Sie den Computer mit Windows Server Essentials verbinden, wird die Einstellung überschrieben, wenn die Connector-Software auf dem Computer installiert ist.

 **Lösung** Notieren Sie sich zum Beheben dieses Problems das Kennwort des Benutzerkontos, wenn Sie den Computer mit dem Server verbinden. Nachdem die Connectorsoftware installiert ist, konfigurieren Sie die automatische Anmeldung für die Verwendung dieses Kontos.

> [!NOTE]
>  Das Windows Server Essentials-Domänen Konto erfordert ein Kennwort, das den Standardanforderungen für die Kenn Wort Richtlinien entspricht.

##  <a name="issue-10"></a><a name="BKMK_ConnectorIssueOldLogs"></a>Problem 10
 **Problem**

 Beim Deinstallieren einer Vorabversion der Connectorsoftware werden vorhandene Protokolle nicht entfernt.

 **Beschreibung**

 Nachdem Sie von einer Vorabversion (Beta oder RC) von Windows Server Essentials auf die freigegebene Version aktualisiert haben, müssen Sie die Connectorsoftware von jedem Computer entfernen, der mit dem Server verbunden war, und den Computer dann erneut verbinden, um die veröffentlichte Version der Connectorsoftware zu installieren.

 Wenn Sie die Connectorsoftware von einem Computer im Netzwerk entfernen, werden die vorhandenen Protokolldateien im Ordner "%ProgramData%\Microsoft\Windows Server\Logs\" auf diesem Computer jedoch nicht gelöscht. Wenn Sie den Ordner "Logs" nicht löschen, können die Protokolldateien beschädigt werden, wenn Sie den Computer mit der veröffentlichten Version von Windows Server Essentials verbinden.

 **Lösung** Zur Vermeidung einer Beschädigung der Protokolldateien löschen Sie den Ordner "Logs" manuell, bevor Sie den Clientcomputer erneut mit dem aktualisierten Server verbinden.

#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>So stellen Sie nach einem Serverupdate die Verbindung mit einem Computer wieder her, ohne die Protokolldateien zu beschädigen

1.  Deinstallieren Sie die Connectorsoftware mithilfe der Systemsteuerung vom Computer.

2.  Löschen Sie den Ordner "Logs" aus dem Ordner "%ProgramData%\Microsoft\Windows Server\".

3.  Verbinden Sie den Computer erneut mit dem Server. Hierdurch wird die Connectorsoftware in der endgültigen Produktversion installiert, wobei ein neuer Ordner "Logs" und Protokolldateien erstellt werden.

##  <a name="issue-11"></a><a name="BKMK_UpgradeClientOS"></a>Problem 11
 **Problem**

 Ich möchte ein Upgrade des Betriebssystems auf einem Clientcomputer ausführen.

 **Beschreibung**

 Während der Installation der Connectorsoftware erfolgen zahlreiche Prüfungen des Clientbetriebssystems, um sicherzustellen, dass der Client alle Voraussetzungen für den Connector erfüllt. Wenn Sie das Clientbetriebssystem einem Upgrade unterziehen, nachdem Sie die Connectorsoftware installiert haben, sind einige der Voraussetzungen möglicherweise nicht erfüllt, sodass der Clientconnector fehlerhaft sein kann.

 **Lösung**

 Bevor Sie das Clientbetriebssystem auf eine andere Version aktualisieren (z. B. mittels Upgrade von Windows XP auf Windows Vista oder Windows Vista auf Windows 7), müssen Sie die Connectorsoftware deinstallieren. Öffnen Sie in der Systemsteuerung die Option **Software**. Nach Abschluss des Upgrades des Client Betriebssystems können Sie den Clientconnector neu installieren, indem Sie http://<*Server*>/Connect in einem Webbrowser öffnen, wobei <*Server*> der Name des Windows Server Essentials-Servers ist.

 Wenn den Client bereits mit der Connectorsoftware aktualisiert haben, verwenden Sie **Software** oder **Programme und Funktionen**, um die Connectorsoftware zu deinstallieren. Installieren Sie anschließend die Connectorsoftware erneut.

## <a name="additional-references"></a>Weitere Verweise

- [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

- [Windows 2012 Server Essentials ConnectComputer Problembehandlung]()