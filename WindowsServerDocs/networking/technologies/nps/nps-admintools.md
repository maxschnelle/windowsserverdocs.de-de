---
title: Netzwerkrichtlinienserver-Verwaltung mit Verwaltungstools
description: Sie können in diesem Thema verwenden, um die Tools kennen, die Sie zum Verwalten der Netzwerkrichtlinienserver unter Windows Server 2016 verwenden können.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa1767e49b16f4a55f36e052d4354aaead540f26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856881"
---
# <a name="network-policy-server-management-with-administration-tools"></a>Netzwerkrichtlinienserver-Verwaltung mit Verwaltungstools

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um die Tools kennen, die Sie verwenden können, um Ihre NPSs zu verwalten.

Nach der Installation von NPS können Sie NPSs verwalten:

- Lokal mithilfe der NPS-MMC \(MMC\) -Snap-in, der statische NPS-Konsole im Administrative Tools, Windows PowerShell-Befehle oder den Netzwerkshell \(Netsh\) -Befehle für Netzwerkrichtlinienserver.
- Von einem Remoteserver NPS mithilfe der NPS-MMC-Snap-in, das Netsh-Befehle für Netzwerkrichtlinienserver, die Windows PowerShell-Befehle für NPS oder Remotedesktop-Verbindung.
- Von einer Remotearbeitsstation mithilfe der Remotedesktopverbindung in Kombination mit anderen Tools wie der NPS-MMC oder über Windows PowerShell.

>[!NOTE]
>In Windows Server 2016 können Sie den lokalen NPS mithilfe der NPS-Konsole verwalten. Zum Verwalten von lokalen und remote NPSs müssen Sie die NPS-MMC-Snap verwenden\-in.

Die folgenden Abschnitte enthalten Anweisungen zum Verwalten Ihrer lokalen und Remotecomputern NPSs.

## <a name="configure-the-local-nps-by-using-the-nps-console"></a>Konfigurieren Sie den lokalen NPS mithilfe der NPS-Konsole

Nach der Installation von NPS können Sie dieses Verfahren, um den lokalen NPS mithilfe der NPS-MMC zu verwalten.

**Administratoranmeldeinformationen** 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-configure-the-local-nps-by-using-the-nps-console"></a>So konfigurieren Sie den lokalen NPS mithilfe der NPS-Konsole

1. Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Klicken Sie in der NPS-Konsole auf NPS \(lokalen\). Wählen Sie im Detailbereich, entweder **Standardkonfiguration** oder **Advanced Configuration**, und führen Sie eine der folgenden basierend auf Ihrer Auswahl:
    - Auf Wunsch **Standardkonfiguration**, wählen Sie ein Szenario aus der Liste, und befolgen Sie dann die Anweisungen, um einen Konfigurationsassistenten zu starten.
    - Auf Wunsch **Advanced Configuration**, klicken Sie auf den Pfeil, um **Erweiterte Konfigurationsoptionen**, und klicken Sie dann überprüfen und konfigurieren Sie die verfügbaren Optionen, die basierend auf den NPS-Funktionen, die Sie möchten: RADIUS-Server, RADIUS-Proxy oder beides.

## <a name="manage-multiple-npss-by-using-the-nps-mmc-snap-in"></a>Verwalten von mehreren NPSs mit der NPS-MMC-Snap\-in

Sie können dieses Verfahren verwenden, um den lokalen NPS und mehrere Remoteserver NPSs verwalten, indem Sie mit der NPS-MMC-Snap\-in.

Bevor Sie das folgende Verfahren durchführen, müssen Sie den NPS auf dem lokalen Computer und auf Remotecomputern installieren.

Je nach netzwerkbedingungen und die Anzahl der NPSs verwalten Sie mit der NPS-MMC-Snap\-Antwort auf das MMC-Snap-in\-in möglicherweise langsam. Darüber hinaus NPS-Konfiguration-Datenverkehr wird über das Netzwerk gesendet während einer Sitzung für die Remoteverwaltung mit der NPS-Snap\-in. Stellen Sie sicher, dass Ihr Netzwerk physisch sicher ist und böswillige Benutzer keinen Zugriff auf diesen Netzwerkdatenverkehr haben.

**Administratoranmeldeinformationen** 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-manage-multiple-npss-by-using-the-nps-snap-in"></a>Um mehrere NPSs zu verwalten, mit der NPS-Snap\-in

1. Um die MMC zu öffnen, führen Sie Windows PowerShell als Administrator aus. Geben Sie in Windows PowerShell **Mmc**, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. In der MMC auf die **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen\-in**. Die **hinzufügen oder entfernen Sie ausrichten\-ins** Dialogfeld wird geöffnet.
3. In **hinzufügen oder entfernen Sie ausrichten\-ins**im **verfügbare Snap\-ins**, scrollen Sie nach unten, klicken Sie auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf  **Hinzufügen**. Die **Computer auswählen** Dialogfeld wird geöffnet.
4. In **Computer auswählen**, überprüfen Sie, ob **lokalen Computer \(dem Computer, auf dem diese Konsole ausgeführt wird\)**  ausgewählt ist, und klicken Sie dann auf **OK**. Der Snap\-im für den lokalen NPS wurde der Liste auf **ausgewählt Snap\-ins**.
5. In **hinzufügen oder entfernen Sie ausrichten\-ins**im **verfügbare Snap\-ins**, sicher, dass **Netzwerkrichtlinienserver** immer noch ausgewählt ist, und klicken Sie dann auf  **Hinzufügen**. Die **Computer auswählen** wieder das Dialogfeld zu öffnen.
6. In **Computer auswählen**, klicken Sie auf **einem anderen Computer**, und geben Sie dann die IP-Adresse oder den vollständig qualifizierten Domänennamen \(FQDN\) von remote NPS, die Sie verwalten, indem Sie den NPS verwenden möchten. Ausrichten\-in. Sie können optional klicken **Durchsuchen** , führen das Verzeichnis für den Computer, die Sie hinzufügen möchten. Klicken Sie auf **OK**.
7. Wiederholen Sie die Schritte 5 und 6, um die NPS-Snap Weitere NPSs hinzufügen\-in. Wenn Sie alle der NPSs, die Sie verwalten möchten hinzugefügt haben, klicken Sie auf **OK**.
8. Um die NPS-Snap-in für die spätere Verwendung zu speichern, klicken Sie auf **Datei**, und klicken Sie dann auf **speichern**. In der **speichern** wechseln, um den Speicherort der Festplatte, in der Sie die Datei speichern möchten, Sie im Dialogfeld Geben Sie einen Namen für Ihre Microsoft Management Console \(.msc\) Datei, und klicken Sie dann auf **speichern**. 

## <a name="manage-an-nps-by-using-remote-desktop-connection"></a>Verwalten Sie ein NPS mithilfe von Remotedesktop

Sie können dieses Verfahren verwenden, ein NPS remote zu verwalten, indem Sie mithilfe einer Remotedesktopverbindung.

Mithilfe von Remotedesktop-Verbindung können Sie Ihre NPSs unter Windows Server 2016 remote verwalten. Sie können auch Remote auf einem Computer unter Windows 10 oder früheren Windows-Clientbetriebssysteme NPSs verwalten.

Sie können die Remotedesktopverbindung verwenden, zum Verwalten von mehreren NPSs mithilfe einer der beiden Methoden.

1. Erstellen Sie eine Remotedesktopverbindung aller Ihrer NPSs einzeln.
2. Verwenden Sie Remotedesktop zur Verbindung mit einem NPS, und klicken Sie dann verwenden Sie die NPS-MMC auf diesem Server auf um anderen Remoteservern zu verwalten. Weitere Informationen finden Sie im vorherigen Abschnitt **mehrere NPSs verwalten, mit der NPS-MMC-Snap\-in**.

**Administratoranmeldeinformationen** 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Administratoren" für den NPS sein.

### <a name="to-manage-an-nps-by-using-remote-desktop-connection"></a>Ein NPS zu verwalten, indem Sie mithilfe einer Remotedesktopverbindung

1. Wählen Sie für jeden NPS, die Sie im Server-Manager Remote verwalten möchten **lokalen Server**. Zeigen Sie im Detailbereich Server-Manager die **Remotedesktop** Einstellung, und führen Sie einen der folgenden. 
    1. Wenn der Wert des der **Remotedesktop** Einstellung **aktiviert**, Sie müssen sich nicht um einige der Schritte in diesem Verfahren ausführen. Schritt 4 beginnen, konfigurieren Remotedesktopbenutzer Berechtigungen fortfahren.
    2. Wenn die **Remotedesktop** Einstellung **deaktiviert**, klicken Sie auf das Wort **deaktiviert**. Die **Systemeigenschaften** Dialogfeld wird geöffnet, auf die **Remote** Registerkarte.
2. In **Remotedesktop**, klicken Sie auf **Remoteverbindungen mit diesem Computer zulassen**. Die **Remotedesktopverbindung** Dialogfeld wird geöffnet. Führen Sie eine der folgenden Aktionen aus.
    1. Um den Netzwerkverbindungen enthaltenen arbeitsplatzverbindungen anzupassen, die zulässig sind, klicken Sie auf **Windows-Firewall mit erweiterter Sicherheit**, und konfigurieren Sie dann die Einstellungen, die Sie zulassen möchten. 
    2. Um Remotedesktop-Verbindung für alle Verbindungen auf dem Computer-Netzwerk zu aktivieren, klicken Sie auf **OK**.
3. In **Systemeigenschaften**im **Remotedesktop**, entscheiden Sie, ob aktivieren **ermöglichen Verbindungen nur von Computern, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebeneausgeführtwird.**, und nehmen Sie die Auswahl.
4. Klicken Sie auf **Benutzer auswählen**. Die **Remote Desktop Users** Dialogfeld wird geöffnet.
5. In **Remote Desktop Users**, zum Gewähren von Berechtigungen für einen Benutzer aus, klicken Sie zum Herstellen einer Remoteverbindung mit der NPS **hinzufügen**, und geben Sie dann den Benutzernamen für das Konto des Benutzers. Klicken Sie auf **OK**.
6. Wiederholen Sie Schritt 5 für jeden Benutzer, die für den RAS-Berechtigung für den NPS werden sollen. Wenn Sie das Hinzufügen von Benutzern fertig sind, klicken Sie auf **OK** zu schließen die **Remote Desktop Users** Dialogfeld und **OK** zu schließen die **Systemeigenschaften**Dialogfeld.
7. Zum Herstellen einer remote-NPS, die Sie mit den vorherigen Schritten konfiguriert haben, klicken Sie auf **starten**, scrollen Sie nach unten der alphabetischen Liste, und klicken Sie dann auf **Windows-Zubehör**, und klicken Sie auf **Remote Herstellen einer Remotedesktopverbindung**. Die **Remotedesktopverbindung** Dialogfeld wird geöffnet.
8. In der **Remotedesktopverbindung** Dialogfeld **Computer**, geben Sie den NPS-Name oder IP-Adresse. Falls gewünscht, klicken Sie auf **Optionen**, konfigurieren Sie zusätzliche Verbindungsoptionen aus, und klicken Sie dann auf **speichern** zum Speichern der Verbindung für die wiederholte Verwendung.
9. Klicken Sie auf **Connect**, wenn Sie aufgefordert werden, und geben Sie Anmeldeinformationen für ein Konto mit Berechtigungen zum Melden Sie sich an, und konfigurieren den NPS.

## <a name="use-netsh-nps-commands-to-manage-an-nps"></a>Verwenden von Netsh NPS-Befehle zum Verwalten von einem NPS

Sie können Befehle im Netsh NPS-Kontext verwenden, um anzuzeigen, und legen die Konfiguration der Authentifizierung, Autorisierung, Kontoführung und Überwachung der Datenbank, die vom NPS und RAS-Dienst verwendet. Verwenden Sie Befehle im Netsh NPS-Kontext zu:

- Konfigurieren Sie einen NPS einschließlich alle Aspekte des Netzwerkrichtlinienservers, die mithilfe der NPS-Konsole in der Windows-Benutzeroberfläche auch für die Konfiguration verfügbar sind, oder konfigurieren.
- Exportieren Sie die Konfiguration eines einzelnen NPS (dem Quellserver befinden), einschließlich der Registrierungsschlüssel und die NPS-Konfiguration, als Netsh-Skript speichern.
- Importieren Sie die Konfiguration an einer anderen NPS mithilfe von Netsh-Skript und die exportierte Konfigurationsdatei aus der Quelle NPS.

Sie können diese Befehle über die Windows Server 2016-Eingabeaufforderung oder über Windows PowerShell ausführen. Sie können auch die Netsh-Befehle für Netzwerkrichtlinienserver in Skripts und Batchdateien ausführen.

**Administratoranmeldeinformationen** 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe Administratoren auf dem lokalen Computer sein.

### <a name="to-enter-the-netsh-nps-context-on-an-nps"></a>Netsh NPS-Kontext auf ein NPS eingeben

1. Öffnen Sie die Befehlszeile oder Windows PowerShell.
2. Typ **Netsh**, und drücken Sie dann die EINGABETASTE.
3. Typ **Nps**, und drücken Sie dann die EINGABETASTE.
4. Um eine Liste der verfügbaren Befehle anzuzeigen, geben Sie ein Fragezeichen \(?\) und drücken Sie EINGABETASTE.


Weitere Informationen zu Netsh NPS-Befehlen finden Sie unter [Netsh-Befehle für Netzwerkrichtlinienserver unter Windows Server 2008](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx), oder Laden Sie die gesamte [technische Referenz zu Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) aus TechNet Gallery. Dieser Download ist die vollständige Network Shell technische Referenz für Windows Server 2008 und Windows Server 2008 R2. Das Format ist Windows-Hilfe \(.chm\) in eine Zip-Datei. Diese Befehle sind in Windows Server 2016 und Windows 10 ist weiterhin vorhanden, sodass Sie Netsh in diesen Umgebungen verwenden können, jedoch, mithilfe von Windows PowerShell empfohlen.

## <a name="use-windows-powershell-to-manage-npss"></a>Verwenden von Windows PowerShell zum Verwalten von NPSs

Sie können Windows PowerShell-Befehle verwenden, um NPSs zu verwalten. Weitere Informationen finden Sie unter den folgenden Referenzthemen für Windows PowerShell-Befehl.

- [Network Policy Server (NPS)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx). Sie können diese Netsh-Befehle in Windows Server 2012 R2 oder höher verwenden.
- [NPS-Modul](https://technet.microsoft.com/itpro/powershell/windows/nps/index). Sie können diese Netsh-Befehle in Windows Server 2016 verwenden.

Weitere Informationen über die NPS-Verwaltung finden Sie unter [verwalten Network Policy Server (NPS)](nps-manage-top.md).
