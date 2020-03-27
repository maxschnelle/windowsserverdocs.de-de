---
title: Netzwerkrichtlinienserver-Verwaltung mit Verwaltungstools
description: In diesem Thema erfahren Sie mehr über die Tools, die Sie zum Verwalten des Netzwerk Richtlinien Servers in Windows Server 2016 verwenden können.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1bb6447197bfed1108a62be077b0a076bef995da
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316350"
---
# <a name="network-policy-server-management-with-administration-tools"></a>Netzwerkrichtlinienserver-Verwaltung mit Verwaltungstools

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Tools, die Sie zum Verwalten Ihrer NPSS verwenden können.

Nachdem Sie NPS installiert haben, können Sie NPSS verwalten:

- Lokal, mithilfe der NPS Microsoft Management Console \(MMC\) Snap-in, der statischen NPS-Konsole in "Verwaltung", Windows PowerShell-Befehlen oder der Netzwerkshell \(Netsh\)-Befehle für NPS.
- Von einem Remote-NPS mithilfe des NPS-MMC-Snap-Ins, der Netsh-Befehle für NPS, der Windows PowerShell-Befehle für NPS oder Remotedesktopverbindung.
- Von einer Remote Arbeitsstation aus mithilfe von Remotedesktopverbindung in Verbindung mit anderen Tools, z. b. der NPS-MMC oder Windows PowerShell.

>[!NOTE]
>In Windows Server 2016 können Sie den lokalen NPS mithilfe der NPS-Konsole verwalten. Zum Verwalten von Remote-und lokalem NPSS müssen Sie das NPS-MMC-Snap\-in verwenden.

Die folgenden Abschnitte enthalten Anweisungen zum Verwalten Ihrer lokalen und Remote-NPSS.

## <a name="configure-the-local-nps-by-using-the-nps-console"></a>Konfigurieren des lokalen NPS mithilfe der NPS-Konsole

Nachdem Sie NPS installiert haben, können Sie dieses Verfahren verwenden, um den lokalen NPS mithilfe der NPS-MMC zu verwalten.

**Administrator Anmelde Informationen** 

Sie müssen Mitglied der Gruppe Administratoren sein, um diesen Vorgang auszuführen.

### <a name="to-configure-the-local-nps-by-using-the-nps-console"></a>So konfigurieren Sie den lokalen NPS mithilfe der NPS-Konsole

1. Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.

2. Klicken Sie in der NPS-Konsole auf NPS \(lokalen\). Wählen Sie im Detailbereich entweder **Standard Konfiguration** oder **Erweiterte Konfiguration**aus, und führen Sie dann basierend auf Ihrer Auswahl eine der folgenden Aktionen aus:
    - Wenn Sie die Option **Standard Konfiguration**auswählen, wählen Sie ein Szenario aus der Liste aus, und befolgen Sie dann die Anweisungen zum Starten eines Konfigurations-Assistenten.
    - Wenn Sie **Erweiterte Konfiguration**auswählen, klicken Sie auf den Pfeil, um **Erweiterte Konfigurationsoptionen**zu erweitern, und überprüfen und konfigurieren Sie dann die verfügbaren Optionen basierend auf der NPS-Funktionalität, die Sie wünschen: RADIUS-Server, RADIUS-Proxy oder beides.

## <a name="manage-multiple-npss-by-using-the-nps-mmc-snap-in"></a>Verwalten mehrerer NPSS mithilfe des NPS-MMC-Snap\-in

Mit diesem Verfahren können Sie die lokalen NPS und mehrere Remote-NPSS mithilfe des NPS-MMC-Snap-\-in verwalten.

Bevor Sie das nachfolgende Verfahren ausführen, müssen Sie NPS auf dem lokalen Computer und auf Remote Computern installieren.

Abhängig von den Netzwerkbedingungen und der Anzahl von NPSS, die Sie mithilfe des NPS-MMC-Snap\-in verwalten, kann die Antwort des MMC-Snap\-in langsam sein. Außerdem wird der NPS-Konfigurations Datenverkehr während einer Remote Verwaltungssitzung über das Netzwerk gesendet, indem das NPS-Snap-in\-in verwendet wird. Stellen Sie sicher, dass Ihr Netzwerk physisch sicher ist und dass böswillige Benutzer keinen Zugriff auf den Netzwerk Datenverkehr haben.

**Administrator Anmelde Informationen** 

Sie müssen Mitglied der Gruppe Administratoren sein, um diesen Vorgang auszuführen.

### <a name="to-manage-multiple-npss-by-using-the-nps-snap-in"></a>So verwalten Sie mehrere NPSS mithilfe des NPS-Snap-\-in

1. Führen Sie Windows PowerShell als Administrator aus, um die MMC zu öffnen. Geben Sie in Windows PowerShell **MMC**ein, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. Klicken Sie in der MMC im Menü **Datei** auf **Snap\-in hinzufügen/entfernen**. Das Dialogfeld **Snap\-ins hinzufügen bzw. entfernen** wird geöffnet.
3. Scrollen Sie in **Snap\-ins hinzufügen oder entfernen**in **Verfügbare Snap\-ins**in der Liste nach unten, klicken Sie auf **Netzwerk Richtlinien Server**, und klicken Sie dann auf **Hinzufügen**. Das Dialogfeld **Computer auswählen** wird geöffnet.
4. Vergewissern Sie sich unter **Computer auswählen**, dass **der lokale Computer \(Computer, auf dem diese Konsole ausgeführt wird\)** ausgewählt ist, und klicken Sie dann auf **OK**. Das Snap-in für die lokale NPS-\-wird der Liste in **Ausgewählte Snap\-ins**hinzugefügt.
5. Stellen Sie sicher, dass unter **Verfügbare\-Snap**-ins **Hinzufügen oder\-entfernen**der Option **Netzwerk Richtlinien Server** weiterhin ausgewählt ist, und klicken Sie dann auf **Hinzufügen**. Das Dialogfeld **Computer auswählen** wird erneut geöffnet.
6. Klicken Sie unter **Computer auswählen**auf **einen anderen Computer**, und geben Sie dann die IP-Adresse oder den voll qualifizierten Domänen Namen \(FQDN\) der Remote-NPS ein, die Sie mithilfe des NPS-Snap\-in verwalten möchten. Optional können Sie auf **Durchsuchen** klicken, um das Verzeichnis für den Computer zu verwenden, den Sie hinzufügen möchten. Klicken Sie auf **OK**.
7. Wiederholen Sie die Schritte 5 und 6, um weitere NPSS zum NPS-Snap\-in hinzuzufügen. Wenn Sie alle NPSS hinzugefügt haben, die Sie verwalten möchten, klicken Sie auf **OK**.
8. Um das NPS-Snap-in für die spätere Verwendung zu speichern, klicken Sie auf **Datei**und dann auf **Speichern**. Navigieren Sie im Dialogfeld **Speichern** unter zu dem Speicherort der Festplatte, an dem Sie die Datei speichern möchten, geben Sie einen Namen für Ihre Microsoft Management Console \(. msc\) Datei ein, und klicken Sie dann auf **Speichern**. 

## <a name="manage-an-nps-by-using-remote-desktop-connection"></a>Verwalten eines NPS mit Remotedesktopverbindung

Mithilfe des folgenden Verfahrens können Sie eine Remote-NPS mithilfe Remotedesktopverbindung verwalten.

Mithilfe Remotedesktopverbindung können Sie Ihre NPSS, die Windows Server 2016 ausführen, remote verwalten. Sie können NPSS auch von einem Computer, auf dem Windows 10 oder frühere Windows-Client Betriebssysteme ausgeführt werden, remote verwalten.

Sie können Remotedesktop Verbindung verwenden, um mehrere NPSS mit einer von zwei Methoden zu verwalten.

1. Erstellen Sie eine Remotedesktop Verbindung zu jedem ihrer NPSS einzeln.
2. Verwenden Sie Remotedesktop, um eine Verbindung mit einem NPS herzustellen, und verwenden Sie dann die NPS-MMC auf diesem Server, um andere Remote Server zu verwalten. Weitere Informationen finden **Sie im vorherigen Abschnitt Manage Multiple NPSS using the NPS MMC Snap\-in**.

**Administrator Anmelde Informationen** 

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" auf dem NPS sein.

### <a name="to-manage-an-nps-by-using-remote-desktop-connection"></a>So verwalten Sie einen NPS mithilfe Remotedesktopverbindung

1. Wählen Sie auf jedem NPS, den Sie remote verwalten möchten, in Server-Manager die Option **lokaler Server**aus. Zeigen Sie im Bereich Server-Manager Details die Einstellung **Remotedesktop** an, und führen Sie einen der folgenden Schritte aus. 
    1. Wenn der Wert der **Remotedesktop** Einstellung **aktiviert**ist, müssen Sie einige der Schritte in dieser Prozedur nicht ausführen. Fahren Sie mit Schritt 4 fort, um die Konfiguration Remotedesktop Benutzerberechtigungen zu starten.
    2. Wenn die **Remotedesktop** Einstellung **deaktiviert**ist, klicken Sie auf das Wort **deaktiviert**. Das Dialogfeld **System Eigenschaften** wird auf der Registerkarte **Remote** geöffnet.
2. Klicken Sie in **Remotedesktop**auf **Remote Verbindungen mit diesem Computer zulassen**. Das Dialogfeld **Remotedesktopverbindung** wird geöffnet. Führen Sie einen der folgenden Schritte aus:
    1. Klicken Sie zum Anpassen der zulässigen Netzwerkverbindungen auf **Windows-Firewall mit**erweiterter Sicherheit, und konfigurieren Sie dann die Einstellungen, die Sie zulassen möchten. 
    2. Klicken Sie auf **OK**, um Remotedesktopverbindung für alle Netzwerkverbindungen auf dem Computer zu aktivieren.
3. Wählen Sie unter **System Eigenschaften**in **Remotedesktop**aus, ob Sie **Verbindungen nur von Computern zulassen möchten, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt**wird, und treffen Sie Ihre Auswahl.
4. Klicken Sie auf **Benutzer auswählen**. Das Dialogfeld **Remotedesktop Benutzer** wird geöffnet.
5. Klicken Sie in **Remotedesktop Benutzer**auf **Hinzufügen**, um einem Benutzer die Berechtigung zum Herstellen einer Remote Verbindung mit dem NPS zu erteilen, und geben Sie dann den Benutzernamen für das Benutzerkonto ein. Klicken Sie auf **OK**.
6. Wiederholen Sie Schritt 5 für jeden Benutzer, dem Sie die Remote Zugriffsberechtigung für den NPS gewähren möchten. Wenn Sie die Benutzer hinzugefügt haben, klicken Sie auf **OK** , um das Dialogfeld **Remotedesktop Benutzer** zu schließen, und klicken Sie dann erneut auf **OK** , um das Dialogfeld **System Eigenschaften**
7. Zum Herstellen einer Verbindung mit einem NPS, den Sie mit den vorherigen Schritten konfiguriert haben, klicken Sie auf **Start**, Scrollen Sie in der alphabetischen Liste nach unten, und klicken Sie dann auf **Windows-Zubehör**und dann auf **Remotedesktopverbindung**. Das Dialogfeld **Remotedesktopverbindung** wird geöffnet.
8. Geben Sie im Dialogfeld **Remotedesktopverbindung** unter **Computer**den NPS-Namen oder die IP-Adresse ein. Wenn Sie möchten, klicken Sie auf **Optionen**, konfigurieren Sie zusätzliche Verbindungsoptionen, und klicken Sie dann auf **Speichern** , um die Verbindung für die wiederholte Verwendung zu speichern.
9. Klicken Sie auf **verbinden**, und geben Sie bei entsprechender Aufforderung Benutzerkonto-Anmelde Informationen für ein Konto an, das über Berechtigungen zum Anmelden bei und zum Konfigurieren des NPS verfügt.

## <a name="use-netsh-nps-commands-to-manage-an-nps"></a>Verwenden von Netsh NPS-Befehlen zum Verwalten von NPS

Mit Befehlen im Netsh NPS-Kontext können Sie die Konfiguration der Authentifizierungs-, Autorisierungs-, Buchhaltungs-und Überwachungs Datenbank anzeigen und festlegen, die sowohl von NPS als auch vom RAS-Dienst verwendet wird. Verwenden Sie Befehle im Netsh NPS-Kontext für Folgendes:

- Konfigurieren oder Neukonfigurieren eines NPS, einschließlich aller Aspekte von NPS, die auch über die NPS-Konsole in der Windows-Benutzeroberfläche für die Konfiguration verfügbar sind.
- Exportieren Sie die Konfiguration eines NPS (dem Quell Server), einschließlich der Registrierungsschlüssel und des NPS-Konfigurations Speicher, als Netsh-Skript.
- Importieren Sie die Konfiguration in ein anderes NPS, indem Sie ein Netsh-Skript und die exportierte Konfigurationsdatei aus dem NPS der Quelle verwenden.

Sie können diese Befehle an der Windows Server 2016-Eingabeaufforderung oder in Windows PowerShell ausführen. Sie können auch Netsh NPS-Befehle in Skripts und Batch Dateien ausführen.

**Administrator Anmelde Informationen** 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe Administratoren auf dem lokalen Computer sein.

### <a name="to-enter-the-netsh-nps-context-on-an-nps"></a>So geben Sie den Netsh NPS-Kontext in einem NPS ein

1. Öffnen Sie die Eingabeaufforderung oder Windows PowerShell.
2. Geben Sie **netsh**ein, und drücken Sie dann die EINGABETASTE.
3. Geben Sie **NPS**ein, und drücken Sie dann die EINGABETASTE.
4. Geben Sie ein Fragezeichen \(ein, um eine Liste der verfügbaren Befehle anzuzeigen.\) und drücken Sie die EINGABETASTE.


Weitere Informationen zu Netsh NPS-Befehlen finden Sie unter [Netsh-Befehle für den Netzwerk Richtlinien Server unter Windows Server 2008](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx), oder laden Sie die gesamte [Technische Referenz zu Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) aus der TechNet Gallery herunter. Bei diesem Download handelt es sich um die vollständige technische Referenz für die Netzwerk Shell für Windows Server 2008 und Windows Server 2008 R2. Das Format ist Windows-Hilfe \(*. chm\) in einer ZIP-Datei. Diese Befehle sind weiterhin in Windows Server 2016 und Windows 10 vorhanden, sodass Sie netsh in diesen Umgebungen verwenden können, obwohl die Verwendung von Windows PowerShell empfohlen wird.

## <a name="use-windows-powershell-to-manage-npss"></a>Verwenden von Windows PowerShell zum Verwalten von NPSS

Sie können Windows PowerShell-Befehle zum Verwalten von NPSS verwenden. Weitere Informationen finden Sie in den folgenden Windows PowerShell-Befehlsreferenz Themen.

- [Cmdlets für Netzwerk Richtlinien Server (Network Policy Server, NPS) in Windows PowerShell](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx). Sie können diese Netsh-Befehle in Windows Server 2012 R2 oder höheren Betriebssystemen verwenden.
- [NPS-Modul](https://technet.microsoft.com/itpro/powershell/windows/nps/index). Sie können diese Netsh-Befehle in Windows Server 2016 verwenden.

Weitere Informationen zur NPS-Verwaltung finden Sie unter [Verwalten des Netzwerk Richtlinien Servers (Network Policy Server, NPS)](nps-manage-top.md).
