---
title: Problembehandlung beim Verbinden von Computern mit dem Server in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9b0d11be08840ecedabab6fd4e96f5d453ea4857
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Problembehandlung beim Verbinden von Computern mit dem Server in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials 
  
 Dieses Thema enthält Anleitungen zur Fehlerbehebung für Probleme, die auftreten können, wenn Sie einen Computer mit dem Server mit Windows Server Essentials oder Windows Server Essentials verbinden.  
  
> [!NOTE]
>  Aktuelle Informationen zur Problembehandlung aus dem Windows Server Essentials und Windows Server Essentials-Community, empfehlen wir, Sie besuchen die [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserveressentials). Die Windows Server Essentials-Forum ist ein idealer Ausgangspunkt, um nach Hilfe suchen oder eine Frage stellen.  
  
 Dieses Thema enthält Lösungen für die folgenden Probleme:  
  

-   Problem 1: [ausstellen 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   Problem 2: [ausstellen 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   Problem 3: [ausstellen 3](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   Problem 4: [ausstellen 4](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   Problem 5: [ausstellen 5](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   Problem 6: [ausstellen 6](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   Problem 7: [7 ausstellen](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   Problem 8: [8 ausstellen](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   Problem 9: [ausstellen 9](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   Problem 10: [10 ausstellen](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   Problem 11: [ausstellen 11](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

-   Problem 1: [ausstellen 1](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   Problem 2: [ausstellen 2](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   Problem 3: [ausstellen 3](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   Problem 4: [ausstellen 4](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   Problem 5: [ausstellen 5](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   Problem 6: [ausstellen 6](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   Problem 7: [7 ausstellen](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   Problem 8: [8 ausstellen](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   Problem 9: [ausstellen 9](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   Problem 10: [10 ausstellen](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   Problem 11: [ausstellen 11](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

  
##  <a name="BMRK_Package"></a>Problem 1  
 **Problem**  
  
 Es wird ein Paket, die Installation nicht erfolgreich war. Versuchen Sie, die Windows Server Essentials-Connector erneut zu installieren. Wenn das Problem weiterhin auftritt, wenden Sie sich an den Netzwerk-Administrator-Fehler bei einen Computer mit dem Server verbinden  
  
 **Beschreibung**  
  
 Dieses Problem kann auftreten, wenn Sie einen Computer mit einem Server, die Windows Server Essentials ausgeführt wird verbinden, während andere Windows-Updates oder Anwendungsinstallationen ausstehen und die Connector-Installation wird abgebrochen.  
  
 **Lösung**  
  
 Führen Sie alle anderen Updates und Anwendungsinstallationen. Die Computer neu gestartet, wenn Sie aufgefordert werden.  
  
##  <a name="BKMK_ConnectorIssue2"></a>Problem 2  
 **Problem**  
  
 Das Hinzufügen eines Computers mit Windows Server Essentials ist nicht möglich  
  
 **Beschreibung**  
  
 Computer mit Nicht-ASCII-Zeichen im Computernamen können nicht zu Windows Server Essentials hinzugefügt werden. Wenn der Computername Nicht-ASCII-Zeichen enthält, erhalten Sie die Fehlermeldung "ein unerwarteter Fehler aufgetreten ist."  
  
 **Lösung**  
  
 Benennen Sie die Clientcomputer mit einem Namen, der nur ASCII-Zeichen enthält, und versuchen Sie, den Computer erneut zu Windows Server Essentials hinzufügen.  
  
##  <a name="BKMK_ConnectorIssue2a"></a>Problem 3  
 **Problem**  
  
 Fehlermeldung einen der Connector für die Softwareinstallation wird abgebrochen, wenn einen Computer mit dem Server verbinden  
  
 **Beschreibung**  
  
 Um einen Computer mit dem Server verbinden können, muss das Systemkonto Vollzugriff für Serverordner auf Windows Server Essentials-Dashboard angezeigt haben. Wenn Sie nicht die erforderlichen Berechtigungen gewährt wurden, die Fehlermeldung "die Installation der Connectorsoftware wird abgebrochen" angezeigt.  
  
 **Lösung**  
  
 Erteilen Sie dem Konto SYSTEM **Vollzugriff** Berechtigungen für jeden Serverordner.  
  
#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>Das Systemkonto Vollzugriff Erteilen von Berechtigungen für einen Serverordner  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
3.  Maustaste auf den Serverordner, und klicken Sie dann auf **öffnen Sie den Ordner**. (Wenn Sie nicht angezeigt werden die **öffnen Sie den Ordner** Option, Sie müssen nicht zum Festlegen von Berechtigungen für den Ordner.)  
  
4.  Klicken Sie im Netzwerkpfad oben in der Windows-Explorer auf die Serverfreigabe, um freigegebene Ordner auf dem Server anzuzeigen. Wenn der Pfad ist z.B. **Netzwerk > Server01 > Sicherungen von Dateiversionsverläufen**, klicken Sie auf **Server01**.  
  
5.  Maustaste auf einen Serverordner, und klicken Sie dann auf **Eigenschaften**.  
  
6.  Klicken Sie auf die **Security** Registerkarte.  
  
7.  Wenn **Vollzugriff** ist für das Konto SYSTEM nicht zulässig, klicken Sie auf **bearbeiten**, und klicken Sie dann auf **SYSTEM**. Klicken Sie unter **Berechtigungen für System**, wählen die **zulassen** Sie das Kontrollkästchen neben **Vollzugriff**.  
  
8.  Klicken Sie auf **OK** zweimal, um die Berechtigungen zu aktualisieren, und schließen Sie **Eigenschaften**.  
  
##  <a name="BKMK_ConnectorIssueNetFramework"></a>Problem 4  
 **Problem**  
  
 Ich eine führen diese Anwendung zu erhalten, müssen Sie eine der folgenden Versionen von .NET Framework installieren: V4.5.50709 "Fehler beim Verbinden eines Computers mit dem Server  
  
 **Beschreibung**  
  
 Wenn Sie einen Computer mit einem Server mit Windows Server Essentials oder Windows Server Essentials verbinden, versucht der Assistent zum Installieren von .NET Framework Version 4.5.50709 auf dem Computer. Wenn eine frühere Version von .NET Framework Version 4.5 vorhanden ist, die aktualisierte Version nicht installiert werden, und der Verbindungsversuch misslingt mit dieser Fehlermeldung: zum Ausführen dieser Anwendung müssen Sie eine der folgenden Versionen von .NET Framework installieren: V4.5.50709. Wenden Sie sich an den zuständigen zwecks Anleitung zum Abrufen der entsprechenden Version von .NET Framework.  
  
 **Lösung**  
  
 Deinstallieren Sie .NET Framework 4.5 vom Computer, und klicken Sie dann verbinden Sie den Computer mit dem Server.  
  
#### <a name="to-uninstall-net-framework-45"></a>So deinstallieren Sie .NET Framework 4.5  
  
1.  Auf der **starten** auf dem Clientcomputer öffnen **Systemsteuerung**.  
  
2.  In der Systemsteuerung unter **Programme**, klicken Sie auf **Deinstallieren eines Programms**.  
  
3.  Mit der rechten Maustaste **Microsoft .NET Framework 4.5**, und klicken Sie dann auf **Deinstallieren**.  
  
4.  Nach der erfolgreichen Deinstallation von .NET Framework 4.5 verbinden Sie den Computer mit dem Server. Die richtige Version von .NET Framework 4.5 wird zusammen mit der Connector-Software installiert.  
  
##  <a name="BKMK_Time"></a>Problem 5  
 **Problem**  
  
 Ich erhalte einen der Server ist nicht verfügbar. Um dieses Problem zu beheben, wenden Sie sich an die für das Netzwerk zuständige Person. Fehler bei einen Computer mit dem Server verbinden  
  
 **Beschreibung**  
  
 Dies kann passieren, wenn Datum und Uhrzeit auf dem verbundenen Computer nicht mit Datum und Uhrzeit auf dem Server synchronisiert werden.  Windows Server Essentials und Windows Server Essentials verwenden den Zeitsynchronisierungsdienst, um Datum und Uhrzeit von Computern in einer Windows Server Essentials oder Windows Server Essentials-Netzwerk zu synchronisieren. Eine synchronisierte Uhrzeit ist wichtig, da das standardmäßig verwendete Authentifizierungsprotokoll Serverzeit im Rahmen der Authentifizierung verwendet. Wenn beispielsweise die Uhr auf einem Clientcomputer nicht, auf das richtige Datum und die Uhrzeit, Windows Server Essentials synchronisiert werden oder Windows Server Essentials-Authentifizierung möglicherweise fälschlicherweise interpretieren Sie eine Anforderung für die Anmeldung als Eindringversuch, und verweigern Sie des Zugriffs für den Benutzer.  
  
 Dies kann passieren, wenn der Server s freier Speicher weniger als 5% beträgt.  
  
 Dies kann passieren, wenn Sie bereits über eine VPN-Verbindung mit dem Windows Essentials-Server verfügen und Sie versuchen, die Connector-Software externer mithilfe einer Domänenadresse zu konfigurieren.  
  
 **Lösung**  
  
1.  Synchronisieren Sie Datum und Uhrzeit auf dem Clientcomputer mit dem Server. Verbinden Sie den Computer dann an den Server.  
  
2.  Schließen Sie einige Programme auf dem Server, und klicken Sie dann verbinden Sie den Computer mit dem Server.  
  
3.  Schließen Sie die VPN-Verbindung, und klicken Sie dann verbinden Sie den Computer mit dem Server.  
  
#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>So ändern Sie Datum und Uhrzeit auf dem Clientcomputer  
  
1.  Öffnen Sie auf der Startseite des Clientcomputers **Systemsteuerung**.  
  
2.  Klicken Sie in der Systemsteuerung auf **Zeit, Sprache und Region**, und klicken Sie dann auf **Datum und Uhrzeit**.  
  
3.  Klicken Sie auf **Datum und Uhrzeit ändern**, Datum und Uhrzeit auf dem richtigen Datum und Uhrzeit festgelegt, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie auf **OK**, und schließen Sie dann auf Systemsteuerung.  
  
5.  Versuchen Sie erneut, auf den Clientcomputer mit dem Server verbinden. Eine Anleitung finden Sie unter Verbinden von Computern mit dem Server.  
  
 Wenn Sie weiterhin die Clientcomputer mit dem Server verbinden können, stellen Sie sicher, dass Datum und Uhrzeit auf dem Server richtig sind. Wenn Datum und Uhrzeit nicht richtig sind, diese zu ändern.  
  
#### <a name="to-change-the-date-and-time-on-the-server"></a>So ändern Sie Datum und Uhrzeit auf dem Server  
  
1.  Melden Sie sich an den Server mit dem Kennwort an, das Sie während der Windows Server Essentials oder Windows Server Essentials-Installation und Konfiguration eingerichtet.  
  
    > [!NOTE]
    >  Wenn Sie den Server remote verwalten, müssen Sie sich an den Server mithilfe der Remotedesktopverbindung anmelden.  
  
2.  Auf der **starten** geöffnete Seite **Systemsteuerung**.  
  
3.  Klicken Sie in der Systemsteuerung auf **Zeit, Sprache und Region**, und klicken Sie dann auf **Datum und Uhrzeit**.  
  
4.  Klicken Sie auf **Datum und Uhrzeit ändern**, Datum und Uhrzeit auf dem richtigen Datum und Uhrzeit festgelegt, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **OK**, und schließen Sie dann auf Systemsteuerung.  
  
6.  Versuchen Sie es erneut auf den Clientcomputer mit dem Server verbinden, auf dem Clientcomputer. Eine Anleitung finden Sie unter Verbinden von Computern mit dem Server.  
  
##  <a name="BKMK_ServiceStopped"></a>Problem 6  
 **Problem**  
  
 Ich erhalte eine einer unerwarteter Fehler ist aufgetreten. Um dieses Problem zu beheben, wenden Sie sich an die für das Netzwerk zuständige Person. Fehler bei einen Computer mit dem Server verbinden  
  
 **Beschreibung**  
  
 Wenn Sie diese Fehlermeldung erhalten, kann der Webdienst für WSS-Zertifikats nicht ausgeführt.  
  
 **Lösung**  
  
 Starten Sie den Webdienst für WSS-Zertifikat.  
  
#### <a name="to-start-the-wss-certificate-web-service"></a>Starten Sie den Webdienst für WSS-Zertifikat  
  
1.  Auf des Servers **starten** geöffnete Seite **Verwaltung**.  
  
     In **Verwaltung**, mit der rechten Maustaste **(Internet Information Services, IIS) Manager**, und klicken Sie dann auf **öffnen**.  
  
2.  Klicken Sie im Navigationsbereich auf **Webdienst für WSS-Zertifikate**.  
  
3.  In der **Aktionen** Bereich, klicken Sie auf **starten**.  
  
##  <a name="BKMK_ConnectorIssueReconnect"></a>Problem 7  
 **Problem**  
  
 Beim Versuch, einen Computer nach einem misslungenen Verbindungsversuch erneut mit dem Server verbinden, wird die Warnung, die ein Computer mit diesem Namen bereits mit dem Server verbunden ist  
  
 **Beschreibung**  
  
 Wenn ein früherer Versuch, einen Computer mit dem Server verbinden abgebrochen oder unterbrochen wurde, können Sie folgende Warnung erhalten, wenn Sie versuchen, erneut eine Verbindung herzustellen: ein Computer mit diesem Namen ist bereits mit dem Server verbunden. Dies geschieht, weil ein Zertifikat ausgestellt wurde, wenn Sie versucht haben, beim ersten Verbinden mit dem Server.  
  
 **Lösung** Sie sicher, dass kein anderer Computer mit dem gleichen Namen bereits mit dem Server verbunden ist, klicken Sie auf **Weiter**, und folgen Sie dann die Anweisungen zum Abschließen der **mein Computer mit dem Server verbinden** Assistenten.  
  
##  <a name="BKMK_JoinWin7"></a>Problem 8  
 **Problem**  
  
 Beim Versuch, einen Clientcomputer herstellen, der Windows7 Home mit dem Server ausgeführt wird, wird die Webseite für die Ausführung der Connectorsoftware geöffnet, aber der Clientcomputer kann nicht mit dem Server verbinden  
  
 **Beschreibung**  
  
 Wenn die Router im Netzwerk Multicast aktiviert ist, führen Sie die Kommunikation zwischen dem Server und einem Clientcomputer mit Windows7 Home Basic oder Windows7 Home Premium nicht ordnungsgemäß.  
  
 **Lösung**  
  
 Deaktivieren Sie Multicast auf dem Router. Bei einigen Routern schließt können, die Deaktivieren des Routingprotokolls RIP - 2M enthalten. Weitere Informationen finden Sie in der Dokumentation des Routerherstellers.  
  
##  <a name="BKMK_ConnectorIssueAutologon"></a>Problem 9  
 **Problem**  
  
 Automatische Anmeldung wurde beendet, nachdem ich den Computer mit dem Server verbunden  
  
 **Beschreibung**  
  
 Wenn die automatische Anmeldung für das Benutzerkonto festgelegt ist, wenn Sie den Computer mit Windows Server Essentials verbinden, wird die Einstellung überschrieben, wenn die Connector-Software auf dem Computer installiert ist.  
  
 **Lösung** um dieses Problem zu beheben, wenn Sie den Computer mit dem Server verbinden, beachten Sie das Kennwort, das für das Benutzerkonto, das verwendet wird. Nachdem die Connector-Software installiert ist, konfigurieren Sie automatische Anmeldung aus, um dieses Konto verwenden.  
  
> [!NOTE]
>  Das Windows Server Essentials-Domänenkonto erfordert ein Kennwort, das den Standardkennwortrichtlinien entspricht.  
  
##  <a name="BKMK_ConnectorIssueOldLogs"></a>Problem 10  
 **Problem**  
  
 Beim Deinstallieren einer Vorabversion der Connectorsoftware werden vorhandene Protokolle nicht entfernt  
  
 **Beschreibung**  
  
 Nach der Aktualisierung von einer Vorabversion (Beta oder RC)-Version von Windows Server Essentials zur veröffentlichten Version müssen Sie die Connector-Software auf jedem Computer, die mit dem Server verbunden wurde entfernen und verbinden Sie dann den Computer erneut aus, um die veröffentlichte Version der Connector-Software installieren.  
  
 Wenn Sie die Connector-Software von einem Computer im Netzwerk entfernen, werden die vorhandenen Protokolldateien im Ordner "%ProgramData%\Microsoft\Windows Server\Logs\" auf diesem Computer jedoch nicht gelöscht. Wenn Sie den Ordner "Logs" nicht löschen, können die Protokolldateien beschädigt werden, wenn Sie den Computer mit der endgültigen Produktversion von Windows Server Essentials verbinden.  
  
 **Lösung** zur Vermeidung einer Beschädigung der Protokolldateien manuell löschen Ordner "Logs" vor dem erneuten verknüpfen, dass der Clientcomputer mit dem aktualisierten Server.  
  
#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>Einen Computer Wiederherstellen nach ein Server aktualisieren, ohne das Protokoll der Beschädigung von Dateien  
  
1.  Deinstallieren Sie die Connector-Software auf dem Clientcomputer.  
  
2.  Löschen Sie den Ordner "Logs" aus dem Ordner "%ProgramData%\Microsoft\Windows Server\".  
  
3.  Verbinden Sie den Computer erneut mit dem Server. Zum Installieren von der endgültigen Produktversion von der Connector-Software, erstellen einen neuen Protokollordner und Protokolldateien.  
  
##  <a name="BKMK_UpgradeClientOS"></a>Problem 11  
 **Problem**  
  
 Upgrade des Betriebssystems auf einem Clientcomputer ausgeführt werden soll.  
  
 **Beschreibung**  
  
 Während der Installation der Connectorsoftware erfolgen zahlreiche Prüfungen gegenüber dem Client-Betriebssystem, um sicherzustellen, dass der Client alle Voraussetzungen für den Connector erfüllt. Wenn Sie die Client-Betriebssystem nach der Installation der Connector-Software aktualisieren, einige der Voraussetzungen möglicherweise nicht vorhanden sein, und der Clientconnector schlägt möglicherweise fehl.  
  
 **Lösung**  
  
 Bevor Sie das Clientbetriebssystem auf eine andere Version aktualisieren (z.B. Sie mittels Upgrade von Windows XP auf Windows Vista oder Windows Vista auf Windows7), müssen Sie die Connector-Software deinstallieren. Verwendung **Software** in der Systemsteuerung. Nach Abschluss der Aktualisierung des Client-Betriebssystems können Sie den Clientconnector neu installieren, http://&lt öffnen; *Server*> / Connect in einem Webbrowser, wobei <*Server*> ist der Name des Windows Server Essentials-Servers.  
  
 Wenn Sie den Client bereits mit der Connectorsoftware aktualisiert haben, verwenden Sie **Software** oder **Programme und Funktionen** die Connector-Software deinstallieren. Installieren Sie dann die Connector-Software erneut.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)  
  
-   [Windows2012 Server Essentials ConnectComputer Troubleshooting (TechNet Wiki)](https://social.technet.microsoft.com/wiki/contents/articles/14370.windows-2012-server-essentials-connectcomputer-troubleshooting.aspx)
