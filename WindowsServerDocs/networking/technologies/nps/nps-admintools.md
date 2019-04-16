---
title: NPS-Verwaltungs-Verwaltungsprogramme
description: In diesem Thema können Sie die Tools erläutert, die Sie zum Verwalten der Netzwerkrichtlinienserver in Windows Server 2016 verwenden können.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cdb82c5bc1c541f19b1b2f4c8db837af4a812f81
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-management-with-administration-tools"></a>NPS-Verwaltungs-Verwaltungsprogramme

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die Tools erläutert, die Sie verwenden können, um die NPS-Server zu verwalten.

Nach der Installation von NPS können Sie NPS-Server verwalten:

- Lokal mithilfe des \(MMC\) NPS-MMC-Snap-Ins, die statische NPS-Konsole in der Verwaltung, Windows PowerShell-Befehle oder die Network Shell-Befehle \(Netsh\) für den NPS.
- Von einem Remoteserver NPS-Server mithilfe von NPS-MMC-Snap-in, Netsh-Befehle für Netzwerkrichtlinienserver, die Windows PowerShell-Befehle für Netzwerkrichtlinienserver oder Remote Desktop Connection.
- Von einer remote-Arbeitsstation, mithilfe der Remotedesktopverbindung in Kombination mit anderen Tools, z. B. die NPS-MMC oder Windows PowerShell.

>[!NOTE]
>In Windows Server 2016 können Sie den lokalen NPS-Server mithilfe der NPS-Konsole verwalten. Zum Verwalten von lokalen und remote NPS-Server müssen Sie die NPS-MMC-Snap-in verwenden.

Die folgenden Abschnitte enthalten Informationen zur Verwaltung Ihrer lokalen und remote NPS-Server.

## <a name="configure-the-local-nps-server-by-using-the-nps-console"></a>Konfigurieren Sie den lokalen NPS-Server mithilfe der NPS-Konsole

Nach der Installation von NPS können Sie dieses Verfahren, um den lokalen NPS-Server zu verwalten, mithilfe der NPS-MMC.

**Administrative Anmeldeinformationen** 

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-configure-the-local-nps-server-by-using-the-nps-console"></a>So konfigurieren Sie den lokalen NPS-Server mithilfe der NPS-Konsole

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Klicken Sie in der NPS-Konsole auf NPS \(Local\). Klicken Sie im Detailbereich, wählen Sie entweder **Standardkonfiguration** oder **Advanced Configuration**, und führen Sie dann einen der folgenden entsprechend Ihrer Auswahl:
    - Bei Auswahl **Standardkonfiguration**, wählen Sie ein Szenario aus der Liste, und folgen Sie dann die Anweisungen, um den Assistenten zu starten.
    - Bei Auswahl **Advanced Configuration**, klicken Sie auf den Pfeil, um die erweitern **Erweiterte Konfigurationsoptionen**, und überprüfen und konfigurieren Sie die verfügbaren Optionen, die basierend auf den NPS-Funktionen, die Sie möchten –, RADIUS-Server, RADIUS-Proxy oder beides.

## <a name="manage-multiple-nps-servers-by-using-the-nps-mmc-snap-in"></a>Verwalten Sie mehrere NPS-Server mithilfe der NPS-MMC-Snap-in

Dieses Verfahrens können Sie um den lokalen NPS-Server und mehrere NPS-Remoteserver zu verwalten, indem Sie mit der NPS-MMC-Snap-in.

Bevor Sie das folgende Verfahren durchführen, müssen Sie NPS auf dem lokalen Computer und auf Remotecomputern installieren.

Je nach netzwerkbedingungen und die Anzahl der NPS-Server, die Sie verwalten, indem Sie mit der NPS-MMC-Snap-in, möglicherweise langsam Antwort MMC-Snap-in. Darüber hinaus wird NPS-Server-Konfiguration Datenverkehr über das Netzwerk während einer Sitzung remote-Verwaltung gesendet mithilfe der NPS-Snap-in. Stellen Sie sicher, dass Ihr Netzwerk physisch sicheren ist und dass böswillige Benutzer keinen Zugriff auf den Netzwerkdatenverkehr.

**Administrative Anmeldeinformationen** 

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-manage-multiple-nps-servers-by-using-the-nps-snap-in"></a>Mehrere NPS-Server zu verwalten, mit der NPS-Snap-in

1. Führen Sie Windows PowerShell als Administrator, um MMC zu starten. Geben Sie in Windows PowerShell **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console wird geöffnet.
2. In der MMC auf die **Datei** Menü klicken Sie auf **Snap-in hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.
3. In **hinzufügen oder Entfernen von Snap-Ins**im **verfügbaren Snap-Ins**, führen Sie einen Bildlauf nach unten, klicken Sie auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf **hinzufügen**. Die **Computer auswählen** Dialogfeld wird geöffnet.
4. In **Computer auswählen**, überprüfen Sie, ob **lokalen Computer \ (der Computer, auf dem diese Konsole ist Running\)** ausgewählt ist, und klicken Sie dann auf **OK**. Das Snap-in für den lokalen NPS-Server in die Liste aufgenommen **ausgewählten Snap-Ins**.
5. In **hinzufügen oder Entfernen von Snap-Ins**im **verfügbaren Snap-Ins**, stellen Sie sicher, dass **Netzwerkrichtlinienserver** ist markiert, und klicken Sie dann auf **hinzufügen**. Die **Computer auswählen** das Dialogfeld wird erneut angezeigt.
6. In **Computer auswählen**, klicken Sie auf **einem anderen Computer**, und geben Sie dann die IP-Adresse oder den vollqualifizierten Namen \(FQDN\) des NPS-Remoteserver, die Sie verwalten, indem Sie die NPS-Snap-in verwenden möchten. Optional: Klicken Sie auf **Durchsuchen** auf das Verzeichnis für den Computer zu überprüfen, die Sie hinzufügen möchten. Klicken Sie auf **OK**.
7. Wiederholen Sie die Schritte 5 und 6, um weitere NPS-Server die NPS-Snap-in hinzufügen. Wenn Sie die NPS-Server, die Sie verwalten möchten hinzugefügt haben, klicken Sie auf **OK**.
8. Um die NPS-Snap-in für die spätere Verwendung zu speichern, klicken Sie auf **Datei**, und klicken Sie dann auf **speichern**. In der **speichern** Dialogfeld Durchsuchen, um die Festplatte Speicherort zum Speichern Sie die Datei, geben Sie einen Namen für die Microsoft Management Console \(.msc\)-Datei, und klicken Sie dann auf **speichern**. 

## <a name="manage-an-nps-server-by-using-remote-desktop-connection"></a>Verwalten Sie einen NPS-Server mithilfe der Remotedesktopverbindungs

Dieses Verfahrens können Sie um einen NPS-Remoteserver zu verwalten, indem Sie mithilfe der Remotedesktopverbindung.

Mithilfe der Remotedesktopverbindung können Sie Ihre NPS-Server mit Windows Server 2016 remote verwalten. Sie können auch Remote auf einem Computer unter Windows 10 oder früheren Windows-Clientbetriebssysteme NPS-Server verwalten.

Remotedesktopverbindung können Sie um mehrere NPS-Server zu verwalten, indem Sie eine der beiden folgenden Methoden verwenden.

1. Erstellen Sie eine Remotedesktopverbindung mit jedem NPS-Server einzeln.
2. Verwenden Sie den Remotedesktop eine Verbindung mit einem NPS-Server, und verwenden Sie die NPS-MMC auf diesem Server auf um anderen Remoteservern zu verwalten. Weitere Informationen finden Sie im vorherigen Abschnitt **verwalten mehrere NPS-Server mithilfe der NPS-MMC-Snap-in**.

**Administrative Anmeldeinformationen** 

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" auf dem NPS-Server sein.

### <a name="to-manage-an-nps-server-by-using-remote-desktop-connection"></a>Zum Verwalten von NPS-Server mithilfe der Remotedesktopverbindung

1. Wählen Sie auf jeden NPS-Server, die Sie im Server-Manager Remote verwalten möchten **lokalen Server**. Klicken Sie im Server-Manager Detailbereich, Anzeigen der **Remotedesktop** Einstellung, und führen Sie eine der folgenden. 
    1. Wenn der Wert der **Remotedesktop** Einstellung ist **aktiviert**, müssen Sie nicht einige der Schritte in diesem Verfahren ausführen. Überspringen Sie zu Schritt 4 Konfigurieren von Benutzerberechtigungen für Remote Desktop gestartet.
    2. Wenn die **Remotedesktop** Einstellung ist **deaktiviert**, klicken Sie auf das Wort **deaktiviert**. Die **Systemeigenschaften** das Dialogfeld wird angezeigt, auf die **Remote** Registerkarte.
2. In **Remotedesktop**, klicken Sie auf **zulassen von Remoteverbindungen mit diesem Computer**. Die **Remotedesktopverbindung** Dialogfeld wird geöffnet. Führen Sie eine der folgenden.
    1. Zum Anpassen von Netzwerkverbindungen, die zulässig sind, klicken Sie auf **Windows-Firewall mit erweiterter Sicherheit**, und konfigurieren Sie die Einstellungen, die Sie zulassen möchten. 
    2. Damit der Remotedesktopverbindung für alle-Verbindungen auf dem Computer Netzwerk, klicken Sie auf **OK**.
3. In **Systemeigenschaften**im **Remotedesktop**, entscheiden Sie, ob aktivieren **zulassen von Verbindungen nur von Computern, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird**, und treffen Sie Ihre Auswahl.
4. Klicken Sie auf **wählen Benutzer**. Die **Remote Desktop Users** Dialogfeld wird geöffnet.
5. In **Remote Desktop Users**, um die Berechtigung für einen Benutzer eine Remoteverbindung mit dem NPS-Server, klicken Sie auf **hinzufügen**, und geben Sie dann den Benutzernamen für das Konto des Benutzers. Klicken Sie auf **OK**.
6. Wiederholen Sie Schritt 5 für jeden Benutzer, die für die RAS-Berechtigung für den NPS-Server werden soll. Wenn Sie das Hinzufügen von Benutzern fertig sind, klicken Sie auf **OK** zu schließen die **Remote Desktop Users** Dialogfeld und **OK** erneut zu schließen die **Systemeigenschaften** Dialogfeld.
7. Zur Verbindung mit eines NPS-Remoteserver, die Sie mit den vorherigen Schritten konfiguriert haben, klicken Sie auf **starten**, scrollen Sie nach unten der alphabetischen Liste, und klicken Sie dann auf **Windows-Zubehör**, und klicken Sie auf **Remotedesktopverbindung**. Die **Remotedesktopverbindung** Dialogfeld wird geöffnet.
8. In der **Remotedesktopverbindung** Dialogfeld **Computer**, geben Sie den NPS-Servername oder IP-Adresse. Wenn Sie es vorziehen, klicken Sie auf **Optionen**, konfigurieren Sie zusätzliche Optionen, und klicken Sie dann auf **speichern** zum Speichern der Verbindung für die wiederholte Verwendung.
9. Klicken Sie auf **verbinden**, und geben Sie Anmeldeinformationen für ein Benutzerkonto für ein Konto, das über Berechtigungen zum Anmelden und den NPS-Server konfigurieren.

## <a name="use-netsh-nps-commands-to-manage-an-nps-server"></a>Verwenden Sie NPS Netsh-Befehle zum Verwalten von NPS-Server

Sie können Befehle in Netsh NPS-Kontext verwenden, um anzuzeigen, und legen Sie die Konfiguration der Authentifizierung und Autorisierung, Kontoführung und Überwachung von NPS und RAS-Dienst verwendete Datenbank. Verwenden von Befehlen im Netsh NPS-Kontext zu:

- Konfigurieren von einem NPS-Server, die alle Aspekte des Netzwerkrichtlinienservers, die mit der NPS-Konsole in der Windows-Benutzeroberfläche auch für die Konfiguration verfügbar sind, oder konfigurieren.
- Exportieren Sie die Konfiguration eines NPS-Servers (Quellserver), einschließlich Registrierungsschlüssel und NPS-Konfigurationsspeicher als Netsh-Skript.
- Importieren Sie die Konfiguration mithilfe von Netsh-Skript und die exportierte Konfigurationsdatei aus der NPS-Quellserver zu einem anderen NPS-Server.

Sie können diese Befehle über die Windows Server 2016-Eingabeaufforderung oder von Windows PowerShell ausführen. Sie können auch die Netsh-Befehle für Netzwerkrichtlinienserver in Skripts und Batchdateien ausführen.

**Administrative Anmeldeinformationen** 

Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein.

### <a name="to-enter-the-netsh-nps-context-on-an-nps-server"></a>Netsh NPS-Kontext auf einem Netzwerkrichtlinienserver eingeben

1. Öffnen Sie die Befehlszeile oder WindowsPowerShell.
2. Typ **Netsh**, und drücken Sie dann die EINGABETASTE.
3. Typ **Nps**, und drücken Sie dann die EINGABETASTE.
4. Um eine Liste der verfügbaren Befehle anzeigen möchten, geben Sie ein Fragezeichen \(?\), und drücken Sie die EINGABETASTE.


Weitere Informationen zu Netsh NPS-Befehlen finden Sie unter [Netsh-Befehle für Netzwerkrichtlinienserver in Windows Server 2008](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx), oder Laden Sie die gesamte [technische Referenz zu Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) von TechNet Gallery. Dieser Download ist die vollständige Network Shell technische Referenz für Windows Server 2008 und Windows Server 2008 R2. Das Format ist die Windows-Hilfe \(*.chm\) in einer Zip-Datei. Diese Befehle sind in Windows Server 2016 und Windows 10 noch vorhanden, damit Sie in diesen Umgebungen Netsh verwenden können, obwohl mit Windows PowerShell empfohlen wird.

## <a name="use-windows-powershell-to-manage-nps-servers"></a>Verwenden von Windows PowerShell zum Verwalten von NPS-Server

Sie können Windows PowerShell-Befehle zum Verwalten von NPS-Server verwenden. Weitere Informationen finden Sie unter den folgenden Themen der Windows PowerShell-Befehl.

- [Network Policy Server (NPS)-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx). Sie können diese Netsh-Befehle in Windows Server 2012 R2 oder höher verwenden.
- [NPS-Modul](https://technet.microsoft.com/itpro/powershell/windows/nps/index). Sie können diese Netsh-Befehle in Windows Server 2016 verwenden.

Weitere Informationen über die NPS-Verwaltung finden Sie unter [verwalten Network Policy Server (NPS)](nps-manage-top.md).
