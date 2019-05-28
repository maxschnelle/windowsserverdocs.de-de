---
title: Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04f16d84-45c2-4771-84c1-1cc973d0ee02
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18ba3517f6533a85fe7cb24f24a7f4ffdfad6991
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222984"
---
# <a name="install-or-uninstall-roles-role-services-or-features"></a>Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In Windows Server ermöglichen die Server-Manager-Konsole und die Windows PowerShell-Cmdlets für Server-Manager die Installation von Rollen und Features auf lokalen Servern oder Remoteservern oder offline virtuelle Festplatten (VHDs). Sie können mehrere Rollen und Features installieren, auf einen einzelnen Remoteserver oder offline-VHD in einem einzelnen Hinzufügen von Rollen und Features-Assistenten oder Windows PowerShell-Sitzung.  
  
> [!IMPORTANT]  
> Server-Manager kann nicht verwendet werden, um eine neuere Version des Betriebssystems Windows Server zu verwalten. Server-Manager unter Windows Server 2012 R2 oder Windows 8.1 kann nicht verwendet werden, Rollen, Rollendienste und Features auf Servern installieren, auf denen Windows Server 2016 ausgeführt werden.  
  
Sie müssen angemeldet sein auf einen Server als Administrator installieren oder Deinstallieren von Rollen, Rollendienste und Features. Wenn Sie am lokalen Computer mit einem Konto angemeldet sind, das nicht über Administratorrechte auf dem Zielserver verfügt, klicken Sie auf der Kachel **Server** mit der rechten Maustaste auf den Zielserver, und klicken Sie dann auf **Verwalten als** , um ein Konto mit Administratorrechten anzugeben. Der Server, auf dem eine Offline-VHD eingebunden werden soll, muss Server-Manager hinzugefügt werden. Zudem müssen Sie über Administratorrechte für diesen Server verfügen.  
  
Weitere Informationen dazu, welche Rollen, Rollendienste und Features sind, finden Sie unter [Rollen, Rollendienste und Features](https://go.microsoft.com/fwlink/p/?LinkId=239558).  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Installieren von Rollen, Rollendienste und Features mithilfe des Hinzufügen von Rollen und Features-Assistenten](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)  
  
-   [Installieren von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets](#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)  
  
-   [Entfernen von Rollen, Rollendienste und Features mithilfe von Entfernen von Rollen und Features-Assistenten](#remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard)  
  
-   [Entfernen von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets](#remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets)  
  
-   [Installieren von Rollen und Features auf mehreren Servern per Ausführung eines Windows PowerShell-Skripts](#install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script)  
  
-   [Installieren von .NET Framework 3.5 und anderen Features bei Bedarf](#install-net-framework-35-and-other-features-on-demand)  
  
## <a name="install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard"></a>Installieren von Rollen, Rollendienste und Features mithilfe des Hinzufügen von Rollen und Features-Assistenten  
In einer einzelnen Sitzung im Hinzufügen von Rollen und Features-Assistenten können Sie Rollen, Rollendienste und Features auf dem lokalen Server, einem Remoteserver installieren, die Server-Manager oder einer offline-VHD hinzugefügt wurde. Weitere Informationen zum Hinzufügen eines Servers zu Server-Manager zum Verwalten, finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md).  
  
> [!NOTE]  
> Wenn Sie Server-Manager unter Windows Server 2016 oder Windows 10 ausführen, können Sie das Hinzufügen von Rollen und Features-Assistenten zum Installieren von Rollen und Features nur auf Servern und offline-VHDs, die Windows Server 2016 ausgeführt werden.  
  
#### <a name="to-install-roles-and-features-by-using-the-add-roles-and-features-wizard"></a>So installieren Sie Rollen und Features mithilfe des Hinzufügen von Rollen und Features-Assistenten  
  
1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.  
  
    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm, klicken Sie auf die **Server-Manager** Kachel.  
  
2.  Auf der **verwalten** Menü klicken Sie auf **Rollen und Features hinzufügen**.  
  
3.  Überprüfen Sie auf der Seite **Vorbemerkungen**, ob der Zielserver und die Netzwerkumgebung für die Installation der Rolle und des Features vorbereitet sind. Klicken Sie auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, um alle Teile von Rollen oder Features auf einem Server zu installieren. Wählen Sie alternativ **Installation von Remotedesktopdiensten** aus, um entweder eine Desktopinfrastruktur mit virtuellen Computern oder eine sitzungsbasierte Desktopinfrastruktur für die Remotedesktopdienste zu installieren. Bei Verwendung der Option **Szenariobasierte Installation von Remotedesktopdiensten** werden logische Teile der Remotedesktopdienste-Rolle von Administratoren je nach Bedarf auf verschiedene Server verteilt. Klicken Sie auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, oder wählen Sie eine Offline-VHD aus. Um eine Offline-VHD als Zielserver auszuwählen, müssen Sie zuerst den Server auswählen, auf dem die VHD eingebunden werden soll. Wählen Sie anschließend die VHD-Datei aus. Weitere Informationen zum Hinzufügen von Servern zum Serverpool finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md). Klicken Sie nach dem Auswählen des Zielservers auf **Weiter**.  
  
    > [!NOTE]  
    > Zum Installieren von Rollen und Features auf Offline-VHDs müssen Ziel-VHDs die folgenden Anforderungen erfüllen.  
    >   
    > -   VHDs müssen die Version von Windows Server ausgeführt werden, die Version von Server-Manager entspricht, die Sie ausführen. Siehe Hinweis am Anfang des [Installieren von Rollen, Rollendienste und Features mithilfe des Hinzufügen von Rollen und Features Assistenten](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard).  
    > -   VHDs dürfen nicht mehr als ein Systemvolume oder eine Partition aufweisen.  
    > -   Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.  
    >   
    >     -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**  
    >     -   **Vollzugriff** Zugriff auf die **Sicherheit** Registerkarte Datei- oder Ordnerdialogfeld **Eigenschaften** Dialogfeld.  
  
6.  Wählen Sie Rollen und ggf. Rollendienste für die Rolle aus, und klicken Sie dann auf **Weiter** , um Features auszuwählen.  
  
    Wenn Sie fortfahren, benachrichtigt das Hinzufügen von Rollen und Features-Assistenten automatisch, falls Konflikte auf dem Zielserver gefunden wurden, die ausgewählten Rollen bzw. Features Installation oder normale Funktion verhindern können. Sie werden außerdem aufgefordert, Rollen, Rollendienste oder Features hinzuzufügen, die für die ausgewählten Rollen oder Features erforderlich sind.  
  
    Wenn die Rolle von einem anderen Server oder einem Windows Client-basierten Computer mit Remoteserver-Verwaltungstools aus verwaltet werden soll, brauchen Sie die Verwaltungstools und Snap-Ins für Rollen auf dem Zielserver nicht zu installieren. Hinzufügen von Rollen und Features Assistenten standardmäßig werden die Verwaltungstools für die Installation ausgewählt.  
  
7.  Überprüfen Sie auf der Seite **Installationsauswahl bestätigen** Ihre Rollen-, Feature- und Serverauswahl. Wenn Sie bereit sind, die Installation zu starten, klicken Sie auf **Installieren**.  
  
    Sie können Ihre Auswahl auch in eine XML-basierte Konfigurationsdatei exportieren, die Sie für unbeaufsichtigte Installationen mit Windows PowerShell verwenden können. So exportieren Sie die Konfiguration, die Sie angegeben, in diesem Hinzufügen von Rollen und Features-Assistenten-Sitzung, klicken Sie auf **Konfigurationseinstellungen exportieren**, und speichern Sie die XML-Datei an einem geeigneten Speicherort.  
  
    Mit dem Befehl **Alternativen Quellpfad angeben** auf der Seite **Installationsauswahl bestätigen** können Sie einen alternativen Quellpfad für die Dateien angeben, die zum Installieren von Rollen und Features auf dem ausgewählten Server erforderlich sind. In Windows Server 2012 und späteren Versionen von Windows Server [Features bei Bedarf](https://go.microsoft.com/fwlink/p/?LinkID=241573) Sie die Menge des reduzieren belegten Festplattenspeichers vom Betriebssystem, durch das Entfernen der Rollen-und featuredateien von Servern, die ausschließlich verwaltet werden Remote. Wenn Sie Rollen- und Featuredateien mit dem Cmdlet `Uninstall-WindowsFeature -remove` von einem Server entfernt haben, können Sie später Rollen und Features auf dem Server installieren, indem Sie einen alternativen Quellpfad oder eine Freigabe angeben, an dem bzw. auf der die erforderlichen Rollen- und Featuredateien gespeichert sind. Muss die Quelle oder die Dateifreigabe gewähren **lesen** Berechtigungen entweder auf die **jeder** (nicht empfohlen aus Sicherheitsgründen), Gruppe oder dem Computerkonto (*Domäne* \\ *SERverNAME*$) des Zielservers; gewähren des benutzerkontozugriffs ist nicht ausreichend. Weitere Informationen zu Features bei Bedarf finden Sie unter [Windows Server-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkId=241573).  
  
    Sie können eine WIM-Datei als Quelle einer alternativen Funktion angeben, wenn Sie Rollen, Rollendienste und Features auf einem aktiven physischen Server installieren. Der Quellpfad für eine WIM-Datei muss in folgendem Format ein, wobei **WIM** als Präfix und der Index in der die featuredateien befinden als Suffix: **WIM:e:\Sources\Install.wim:4**. Jedoch kann keine WIM-Datei auch direkt als Quelle verwenden, für die Installation von Rollen, Rollendienste und Features auf einer offline-VHD. Sie müssen entweder die offline-VHD einbinden und zeigen Sie auf ihren Bereitstellungspfad für Quelldateien, oder Sie müssen auf einen Ordner mit einer Kopie des Inhalts der WIM-Datei verweisen.  
  
8.  Nachdem Sie auf **installieren**, **Installationsstatus** Installationsstatus, Ergebnisse und Meldungen wie Warnungen, Fehlern oder nach der Installation auszuführenden Konfigurationsschritten, die wird angezeigt erforderlich für die Rollen oder Features, die Sie installiert. In Windows Server 2012 und späteren Versionen von Windows Server, Sie können schließen das Hinzufügen von Rollen und Features-Assistenten während der Installation noch läuft, und Installationsergebnisse anzeigen oder andere Meldungen im wird die **Benachrichtigungen** oben der Server-Manager-Konsole. Klicken Sie auf die **Benachrichtigungen** Flaggensymbol klicken, um weitere Details zu Installationen oder anderen Aufgaben, die Sie im Server-Manager ausführen anzuzeigen.  
  
## <a name="install-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Installieren von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets  
Der Server-Manager-bereitstellungs-Cmdlets für Windows PowerShell funktionieren ähnlich wie der GUI-basierte Rollen und Features-Assistenten hinzufügen und Entfernen von Rollen und Features-Assistenten, jedoch einen wichtigen Unterschied. In Windows PowerShell sind im Gegensatz zum Hinzufügen von Rollen und Features-Assistenten, Verwaltungstools und Snap-Ins für eine Rolle nicht standardmäßig enthalten. Um Verwaltungstools in eine Rolleninstallation einzuschließen, fügen Sie dem Cmdlet den `IncludeManagementTools`-Parameter hinzu. Wenn Sie Rollen und Features auf einem Server installieren, auf denen die Server Core-Installationsoption von Windows Server 2012 oder höheren Versionen ausgeführt wird, Sie können einer Installation Verwaltungstools für eine Rolle hinzufügen, GUI-basierte Verwaltungstools und Snap-Ins können jedoch nicht installiert auf Servern, die die Server Core-Installationsoption von Windows Server ausgeführt werden. Nur Befehlszeilentools und Verwaltungstools für Windows PowerShell können auf Server Core-Installation installiert werden.  
  
#### <a name="to-install-roles-and-features-by-using-the-install-windowsfeature-cmdlet"></a>So installieren Sie Rollen und Features mit dem Cmdlet %%amp;quot;Install-WindowsFeature%%amp;quot;  
  
1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.  
  
    > [!NOTE]  
    > Wenn Sie Rollen und Features auf einem Remoteserver installieren, müssen Sie keine Windows PowerShell mit erhöhten Benutzerrechten ausführen.  
  
    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel für Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.  
  
2.  Geben Sie **Get-WindowsFeature** ein, und drücken Sie anschließend die **EINGABETASTE** , um eine Liste der auf dem lokalen Server verfügbaren und installierten Rollen und Features anzuzeigen. Wenn der lokale Computer kein Server ist oder wenn Sie Informationen zu einem Remoteserver soll, führen **Get-WindowsFeature-Computername <***Computer_name***>** , in dem  *Computer_name* stellt den Namen eines Remotecomputers, auf denen Windows Server 2016 ausgeführt wird. Die Ergebnisse des Cmdlets enthalten die Befehlsnamen von Rollen und Features, die Sie dem Cmdlet in Schritt 4 hinzufügen.  
  
    > [!NOTE]  
    > In Windows PowerShell 3.0 und späteren Versionen von Windows PowerShell ist es nicht erforderlich, importieren das Server-Manager-Cmdlet-Modul in der Windows PowerShell-Sitzung, bevor die Ausführung von Cmdlets, die Teil des Moduls sind. Module werden automatisch importiert, wenn Sie ein zum Modul gehörendes Cmdlet zum ersten Mal ausführen. Darüber hinaus sind weder Windows PowerShell-Cmdlets noch den mit den Cmdlets verwendeten Featurenamen Groß-/Kleinschreibung beachtet.  
  
3.  Typ **Get-Help Install-WindowsFeature**, und drücken Sie dann die **EINGABETASTE** an die Syntax und zugelassene Parameter für die `Install-WindowsFeature` Cmdlet.  
  
4.  Geben Sie Folgendes ein, und drücken Sie dann die **EINGABETASTE**, wobei *Feature_name* stellt den Befehlsnamen einer Rolle oder Feature, das Sie installieren möchten, (abgerufen in Schritt 2), und *Computer_name* einen Remotecomputer, auf dem Sie Rollen und Features installieren möchten. Trennen Sie mehrere Werte für *feature_name* durch Kommas. Der `Restart`-Parameter startet den Zielserver automatisch neu, wenn die Installation der Rolle bzw. des Features dies erfordert.  
  
    ```  
    Install-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart  
    ```  
  
    Fügen Sie zum Installieren von Rollen oder Features auf einer Offline-VHD die Parameter `computerName` und `VHD` hinzu. Wird der `computerName`-Parameter nicht hinzugefügt, geht das Cmdlet davon aus, dass der lokale Computer zum Zugreifen auf die VHD eingebunden wird. Der Parameter `computerName` enthält den Namen des Servers, auf dem die VHD eingebunden werden soll, und der Parameter `VHD` enthält den Pfad zur VHD-Datei auf dem angegebenen Server.  
  
    > [!NOTE]  
    > Sie müssen hinzufügen, die `computerName` -Parameters, wenn Sie dem Cmdlet auf einem Computer, die ausgeführt werden, ein Windows-Clientbetriebssystem ausgeführt wird.  
    >   
    > Zum Installieren von Rollen und Features auf Offline-VHDs müssen Ziel-VHDs die folgenden Anforderungen erfüllen.  
    >   
    > -   VHDs müssen die Version von Windows Server ausgeführt werden, die Version von Server-Manager entspricht, die Sie ausführen. Siehe Hinweis am Anfang des [Installieren von Rollen, Rollendienste und Features mithilfe des Hinzufügen von Rollen und Features Assistenten](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard).  
    > -   VHDs dürfen nicht mehr als ein Systemvolume oder eine Partition aufweisen.  
    > -   Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.  
    >   
    >     -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**  
    >     -   **Vollzugriff** Zugriff auf die **Sicherheit** Registerkarte Datei- oder Ordnerdialogfeld **Eigenschaften** Dialogfeld.  
  
    ```  
    Install-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart  
    ```  
  
    **Beispiel:** Das folgende Cmdlet installiert die active Directory-Domänendienste-Rolle und das Feature "Gruppenrichtlinienverwaltung" auf einem Remoteserver ContosoDC1. Die Verwaltungstools und Snap-Ins werden mit dem Parameter `IncludeManagementTools` hinzugefügt, und der Zielserver wird automatisch neu gestartet, falls dies für die Installation erforderlich ist.  
  
    ```  
    Install-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart  
    ```  
  
5.  Wenn die Installation abgeschlossen ist, Überprüfen der Installation durch Öffnen der **alle Server** Seite im Server-Manager, wählen einen Server, auf dem Sie Rollen und Features installiert, und zeigen die **Rollen und Features** die Kachel auf der Seite für den ausgewählten Server. Sie können auch ausführen, die `Get-WindowsFeature` Cmdlet für den ausgewählten Server (Get-WindowsFeature-Computername <*Computer_name*>) zum Anzeigen einer Liste von Rollen und Features, die auf dem Server installiert sind.  
  
## <a name="remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard"></a>Entfernen von Rollen, Rollendienste und Features mithilfe von Entfernen von Rollen und Features-Assistenten  
Sie müssen auf einen Server als Administrator, um das Deinstallieren von Rollen, Rollendienste und Features angemeldet werden. Wenn Sie am lokalen Computer mit einem Konto angemeldet sind, das nicht über Administratorrechte auf dem Deinstallationszielserver verfügt, klicken Sie auf der Kachel **Server** mit der rechten Maustaste auf den Zielserver, und klicken Sie dann auf **Verwalten als** , um ein Konto mit Administratorrechten anzugeben. Der Server, auf dem eine Offline-VHD eingebunden werden soll, muss Server-Manager hinzugefügt werden. Zudem müssen Sie über Administratorrechte für diesen Server verfügen.  
  
#### <a name="to-remove-roles-and-features-by-using-the-remove-roles-and-features-wizard"></a>Zum Entfernen von Rollen und Features mit Entfernen von Rollen und Features-Assistenten  
  
1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.  
  
    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.  
  
    -   Klicken Sie auf dem Windows- **Startbildschirm** auf die Kachel **Server-Manager** .  
  
2.  Klicken Sie im Menü **Verwalten** auf **Rollen und Funktionen entfernen**.  
  
3.  Vergewissern Sie sich auf der Seite **Vorbemerkungen**, dass die Umgebung zum Entfernen von Rollen oder Features von einem Server vorbereitet ist. Klicken Sie auf **Weiter**.  
  
4.  Auf der **Zielserver auswählen** Seite, wählen Sie einen Server aus dem Serverpool oder eine offline-VHD auswählen. Um eine Offline-VHD auszuwählen, müssen Sie zuerst den Server auswählen, auf dem die VHD eingebunden werden soll. Wählen Sie anschließend die VHD-Datei aus.  
  
    > [!NOTE]  
    > Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.  
    >   
    > -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**  
    > -   Zugriffsrecht **Vollzugriff** auf der Registerkarte **Sicherheit** im Datei- oder Ordnerdialogfeld **Eigenschaften**  
  
    Weitere Informationen zum Hinzufügen von Servern zum Serverpool finden Sie unter [Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md). Klicken Sie nach dem Auswählen des Zielservers auf **Weiter**.  
  
    > [!NOTE]  
    > Können Sie das Entfernen von Rollen und Features-Assistenten zum Entfernen von Rollen und Features von Servern, auf denen die gleiche Version von Windows Server unterstützt die Version von Server-Manager, die Sie verwenden. Sie können keine Rollen, Rollendienste oder Features von Servern mit Windows Server 2016 entfernen, wenn Sie Server-Manager unter Windows Server 2012 R2, Windows Server 2012 oder Windows 8 ausgeführt werden. Können keine Entfernen von Rollen und Features-Assistenten zum Entfernen von Rollen und Features von Servern unter Windows Server 2008 oder Windows Server 2008 R2.  
  
5.  Wählen Sie Rollen und ggf. Rollendienste für die Rolle aus, und klicken Sie dann auf **Weiter** , um Features auszuwählen.  
  
    Wie Sie den Vorgang fortsetzen, Entfernen von Rollen und Features vom Assistenten automatisch aufgefordert, entfernen Sie alle Rollen, entfernen Rollendiensten oder Features, die nicht ohne die Rollen oder features ausgeführt, die Sie.  
  
    Darüber hinaus können Sie ggf. Verwaltungstools und Snap-Ins für Rollen auf dem Zielserver entfernen. Standardmäßig entfernen Rollen und Features-Assistenten werden Verwaltungstools zum Entfernen ausgewählt. Sie können die Verwaltungstools und Snap-Ins behalten, wenn Sie vorhaben, den ausgewählten Server zur Verwaltung der Rolle auf anderen Remoteservern zu verwenden.  
  
6.  Überprüfen Sie auf der Seite **Entfernungsauswahl bestätigen** Ihre Rollen-, Feature- und Serverauswahl. Wenn Sie die Rollen oder Features entfernen möchten, klicken Sie auf **entfernen**.  
  
7.  Nachdem Sie auf **entfernen**, **Entfernungsstatus** Seite zeigt Entfernungsstatus, Ergebnisse und Meldungen zu Warnungen, Fehlern oder nach dem Entfernen auszuführenden Schritten erforderlich, z. B. Neustarten des Zielservers an. In Windows Server 2012 und höhere Versionen von Windows Server können Sie das Entfernen von Rollen und Features-Assistenten während des Entfernens noch im Status und anzeigen schließen die Entfernungsergebnisse oder andere Meldungen im der **Benachrichtigungen** Bereich am oberen Rand der Server-Manager-Konsole. Klicken Sie auf die **Benachrichtigungen** Flag finden weitere Details zu entfernungen oder anderen Aufgaben, die Sie im Server-Manager ausführen.  
  
## <a name="remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Entfernen von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets  
Der Server-Manager-bereitstellungs-Cmdlets für Windows PowerShell funktionieren ähnlich wie der GUI-basierte Entfernen von Rollen und Features-Assistenten, jedoch einen wichtigen Unterschied. In Windows PowerShell werden im Gegensatz zu entfernen Rollen und Features-Assistent, Verwaltungstools und Snap-Ins für eine Rolle nicht standardmäßig entfernt. Um Verwaltungstools im Rahmen einer Rollenentfernung zu entfernen, fügen Sie dem Cmdlet den `IncludeManagementTools`-Parameter hinzu. Wenn Sie Rollen und Features von einem Server deinstallieren wird, die die Server Core-Installationsoption von Windows Server 2012 oder einer späteren Version von Windows Server, diese Parameter entfernt, die Befehlszeile und die Windows PowerShell-Verwaltungstools für die angegebene ausgeführt Rollen und Features.  
  
#### <a name="to-remove-roles-and-features-by-using-the-uninstall-windowsfeature-cmdlet"></a>So entfernen Sie Rollen und Features mit dem Cmdlet %%amp;quot;UnInstall-WindowsFeature%%amp;quot;  
  
1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.  
  
    > [!NOTE]  
    > Wenn Sie Rollen und Features von einem Remoteserver aus deinstallieren möchten, müssen Sie nicht zum Ausführen von Windows PowerShell mit erhöhten Benutzerrechten.  
  
    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.  
  
2.  Geben Sie **Get-WindowsFeature** ein, und drücken Sie anschließend die **EINGABETASTE** , um eine Liste der auf dem lokalen Server verfügbaren und installierten Rollen und Features anzuzeigen. Wenn der lokale Computer kein Server ist oder wenn Sie Informationen zu einem Remoteserver soll, führen **Get-WindowsFeature-Computername <***Computer_name***>** , in dem  *Computer_name* stellt den Namen eines Remotecomputers, auf denen Windows Server 2016 ausgeführt wird. Die Ergebnisse des Cmdlets enthalten die Befehlsnamen von Rollen und Features, die Sie dem Cmdlet in Schritt 4 hinzufügen.  
  
    > [!NOTE]  
    > In Windows PowerShell 3.0 und späteren Versionen von Windows PowerShell ist es nicht erforderlich, importieren das Server-Manager-Cmdlet-Modul in der Windows PowerShell-Sitzung, bevor die Ausführung von Cmdlets, die Teil des Moduls sind. Module werden automatisch importiert, wenn Sie ein zum Modul gehörendes Cmdlet zum ersten Mal ausführen. Darüber hinaus sind weder Windows PowerShell-Cmdlets noch den mit den Cmdlets verwendeten Featurenamen Groß-/Kleinschreibung beachtet.  
  
3.  Typ **Get-Help Uninstall-WindowsFeature**, und drücken Sie dann die **EINGABETASTE** an die Syntax und zugelassene Parameter für die `Uninstall-WindowsFeature` Cmdlet.  
  
4.  Geben Sie Folgendes ein, und drücken Sie dann die **EINGABETASTE**. Dabei steht *Featurename* für den Befehlsnamen einer Rolle oder eines Features, die bzw. das entfernt werden soll (abgerufen in Schritt 2), und *computer_name* für einen Remotecomputer, von dem Rollen und Features entfernt werden sollen. Trennen Sie mehrere Werte für *feature_name* durch Kommas. Der `Restart`-Parameter startet Zielserver automatisch neu, wenn die Entfernung der Rolle bzw. des Features dies erfordert.  
  
    ```  
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart  
    ```  
  
    Fügen Sie zum Deinstallieren von Rollen oder Features auf einer Offline-VHD die Parameter `computerName` und `VHD` hinzu. Wird der `computerName`-Parameter nicht hinzugefügt, geht das Cmdlet davon aus, dass der lokale Computer zum Zugreifen auf die VHD eingebunden wird. Der Parameter `computerName` enthält den Namen des Servers, auf dem die VHD eingebunden werden soll, und der Parameter `VHD` enthält den Pfad zur VHD-Datei auf dem angegebenen Server.  
  
    > [!NOTE]  
    > Sie müssen hinzufügen, die `computerName` -Parameters, wenn Sie dem Cmdlet auf einem Computer, die ausgeführt werden, ein Windows-Clientbetriebssystem ausgeführt wird.  
    >   
    > Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.  
    >   
    > -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**  
    > -   **Vollzugriff** Zugriff auf die **Sicherheit** Registerkarte Datei- oder Ordnerdialogfeld **Eigenschaften** Dialogfeld.  
  
    ```  
    Uninstall-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart  
    ```  
  
    **Beispiel:** Das folgende Cmdlet entfernt die active Directory-Domänendienste-Rolle und das Feature "Gruppenrichtlinienverwaltung" von einem Remoteserver ContosoDC1. Die Verwaltungstools und Snap-Ins werden ebenfalls entfernt, und der Zielserver wird automatisch neu gestartet, falls dies für das Entfernen erforderlich ist.  
  
    ```  
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart  
    ```  
  
5.  Nach Abschluss der Entfernung, stellen Sie sicher, dass die Rollen und Features, durch Öffnen entfernt werden der **alle Server** Seite im Server-Manager, wählen den Server, von dem Sie Rollen und Features entfernt, und zeigen die **Rollen und Features** Kachel auf der Seite für den ausgewählten Server. Sie können auch ausführen, die `Get-WindowsFeature` Cmdlet für den ausgewählten Server (Get-WindowsFeature-Computername <*Computer_name*>) zum Anzeigen einer Liste von Rollen und Features, die auf dem Server installiert sind.  
  
## <a name="install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script"></a>Installieren von Rollen und Features auf mehreren Servern per Ausführung eines Windows PowerShell-Skripts  
Obwohl Sie das Hinzufügen von Rollen und Features-Assistenten verwenden können, um Rollen, Rollendienste und Features auf mehr als einem Zielserver in einer einzelnen Assistenten-Sitzung zu installieren, können Sie ein Windows PowerShell-Skript verwenden, zum Installieren von Rollen, Rollendienste und Features auf mehreren Server, die Sie mithilfe des Server-Manager verwalten. Das Skript, das Sie zum Ausführen von batchbereitstellung verwenden, wie dieser Prozess aufgerufen wird, verweist auf eine XML-Konfigurationsdatei, die Sie ganz einfach erstellen können, indem Sie mithilfe des Hinzufügen von Rollen und Features-Assistenten und auf **Konfigurationseinstellungen exportieren** nach die batchbereitstellung auf die **Installationsauswahl bestätigen** auf der Seite des Hinzufügen von Rollen und Features-Assistenten.  
  
> [!IMPORTANT]  
> Alle Zielserver, die in Ihrem Skript angegeben werden müssen die Version von Windows Server ausgeführt werden, die Version von Server-Manager entspricht, die Sie auf dem lokalen Computer ausgeführt werden. Z. B. Wenn Sie Server-Manager unter Windows 10 ausführen, können Sie Rollen, Rollendienste und Features auf Servern installieren, auf denen Windows Server 2016 ausgeführt werden. Wenn es sich bei der Installation GUI-basierte Verwaltungstools hinzugefügt werden, Zielserver während des Installationsvorgangs automatisch konvertiert, die die Server Core-Installationsoption von Windows Server, auf die vollständige Installation (Server mit der eine vollständige GUI ausgeführt werden, auch bekannt als ausgeführten Grafische Shell für Server).  
>   
> Das Skript in diesem Abschnitt wird verdeutlicht, wie die batchbereitstellung mithilfe ausgeführt werden kann die `Install-WindowsFeature` Cmdlet und eine Windows PowerShell-Skript. Es gibt noch weitere mögliche Skripts und Methoden zur Durchführung der Batchbereitstellung auf mehreren Servern. Sie können das [Script Center-Repository](https://gallery.technet.microsoft.com/ScriptCenter)nutzen, um nach anderen Skripts zum Bereitstellen von Rollen und Features zu suchen oder diese bereitzustellen.  
  
#### <a name="to-install-roles-and-features-on-multiple-servers"></a>So installieren Sie Rollen und Features auf mehreren Servern  
  
1.  Wenn Sie nicht bereits geschehen, erstellen Sie eine XML-Konfigurationsdatei, die enthält die Rollen, Rollendienste und Features, die auf mehreren Servern installiert werden sollen. Sie können diese Konfigurationsdatei erstellen, indem Sie den Rollen hinzufügen und die Features-Assistenten ausführen, auswählen, Rollen, Rollendienste und Features, die Sie möchten und auf **Konfigurationseinstellungen exportieren** nach batchbereitstellung auf der **Installationsauswahl bestätigen** Seite. Speichern Sie die Konfigurationsdatei an einem geeigneten Speicherort. Sie müssen nicht auf **Installieren** klicken bzw. den Assistenten nicht bis zum Ende ausführen, wenn Sie lediglich eine Konfigurationsdatei erstellen möchten.  
  
2.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.  
  
    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.  
  
3.  Kopieren Sie das folgende Skript in der Windows PowerShell-Sitzung.  
  
    ```  
    function Invoke-WindowsFeatureBatchDeployment {  
        param (  
            [parameter(mandatory)]  
            [string[]] $computerNames,  
            [parameter(mandatory)]  
            [string] $ConfigurationFilepath  
        )  
  
        # Deploy the features on multiple computers simultaneously.  
        $jobs = @()  
        foreach($computerName in $computerNames) {  
            $jobs += start-Job -Command {  
                Install-WindowsFeature -ConfigurationFilepath $using:ConfigurationFilepath -computerName $using:computerName -Restart  
            }   
        }  
  
        Receive-Job -Job $jobs -Wait | select-Object Success, RestartNeeded, exitCode, FeatureResult  
    }  
    ```  
  
    Die Zielserver werden automatisch neu gestartet, falls dies für die von Ihnen gewählten Rollen und Features erforderlich ist.  
  
4.  Führen Sie die Funktion wie folgt aus.  
  
    1.  Erstellen Sie eine Variable, in der die Namen der Zielcomputer getrennt durch Kommas gespeichert werden. Im folgenden Beispiel sind in der Variablen `$ServerNames` die Namen der Zielserver *Contoso_01* und *Contoso_02*gespeichert. Drücken Sie die **EINGABETASTE**.  
  
        ```  
        # Sample Invocation  
        $ServerNames = 'Contoso_01','Contoso_02'  
        Invoke-WindowsFeatureBatchDeployment -computerNames $ServerNames -ConfigurationFilepath C:\Users\sampleuser\Desktop\DeploymentConfigTemplate.xml  
        ```  
  
    2.  Geben Sie zum Ausführen der Funktion Folgendes ein, und drücken Sie die **EINGABETASTE**. Hierbei ist `$ServerNames` ein Beispiel für die Variable, die Sie im vorherigen Schritt erstellt haben, und *C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml* ist ein Beispiel für einen Pfad zur Konfigurationsdatei, den Sie in Schritt 1 erstellt haben.  
  
        **Invoke-WindowsFeatureBatchDeployment -computerNames $ServerNames -ConfigurationFilepath C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml**  
  
5.  Wenn die Installation abgeschlossen ist, Überprüfen der Installation durch Öffnen der **alle Server** Seite im Server-Manager, wählen einen Server, auf dem Sie Rollen und Features installiert, und zeigen die **Rollen und Features** die Kachel auf der Seite für den ausgewählten Server. Sie können auch ausführen, die `Get-WindowsFeature` Cmdlet für einen bestimmten Server (`Get-WindowsFeature -computerName` <*Computer_name*>) zum Anzeigen einer Liste von Rollen und Features, die auf dem Server installiert sind.  
  
## <a name="install-net-framework-35-and-other-features-on-demand"></a>Installieren von .NET Framework 3.5 und anderen Features bei Bedarf  
ab Windows Server 2012 und Windows 8, sind die featuredateien für .NET Framework 3.5 (enthält .NET Framework 2.0 und .NET Framework 3.0) nicht auf dem lokalen Computer standardmäßig verfügbar. Die Dateien wurden entfernt. Dateien für Features, die bei der Konfiguration von %%amp;quot;Features bei Bedarf%%amp;quot; entfernt wurden, und Featuredateien für .NET Framework 3.5 stehen über Windows Update zur Verfügung. Wenn featuredateien nicht auf dem Zielserver verfügbar sind, auf denen Windows Server 2012 oder höheren Versionen ausgeführt wird sucht standardmäßig während des Installationsvorgangs für den fehlenden Dateien durch das Verbinden mit Windows Update. Sie können das Standardverhalten überschreiben, indem Sie eine gruppenrichtlinieneinstellung konfigurieren oder einen alternativen Quellpfad angeben, während der Installation können, ob Sie mit der hinzufügen-Rollen und Features GUI-Assistenten oder eine Befehlszeile installieren.  
  
Sie installieren .NET Framework 3.5 mit einer der folgenden Aktionen:  
  
-   Fügen Sie anhand von [So installieren Sie .NET Framework 3.5 durch Ausführen des Install-WindowsFeature-Cmdlets](#to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet) den `Source` -Parameter hinzu, und geben Sie eine Quelle an, aus der .NET Framework 3.5-Featuredateien abgerufen werden sollen. Wenn Sie den `Source`-Parameter nicht hinzufügen, wird vom Installationsprozess zunächst ermittelt, ob von den Gruppenrichtlinieneinstellungen ein Pfad zu Featuredateien angegeben wurde. Wird kein solcher Pfad gefunden, wird mithilfe von Windows Update nach fehlenden Featuredateien gesucht.  
  
-   Verwendung [So installieren Sie .NET Framework 3.5 mithilfe des Hinzufügen von Rollen und Features-Assistenten](#to-install-net-framework-35-by-using-the-add-roles-and-features-wizard) auf einen alternativen quelldateispeicherort an die **Installationsoptionen bestätigen** auf der Seite des Hinzufügen von Rollen und Features-Assistenten.  
  
-   Rufen Sie anhand von [So installieren Sie .NET Framework 3.5 mithilfe von DISM](#to-install-net-framework-35-by-using-dism) standardmäßig Dateien aus Windows Update oder durch Angabe eines Quellpfads zum Installationsmedium ab.  
  
[Konfigurieren alternativer Quellen für Featuredateien in der Gruppenrichtlinie](#configure-alternate-sources-for-feature-files-in-group-policy) für .NET Framework 3.5 oder andere Features, falls auf dem lokalen Computer keine Featuredateien gefunden werden.  
  
> [!IMPORTANT]  
> Bei der Installation von Featuredateien aus einer Remotequelle muss der Quellpfad oder die Dateifreigabe entweder der Gruppe **Jeder** (nicht empfohlen aus Sicherheitsgründen) oder dem Computerkonto (lokales System) des Zielservers Berechtigungen zum **Lesen** gewähren. Das Gewähren des Benutzerkontozugriffs ist nicht ausreichend.  
>   
> Server in Arbeitsgruppen können nicht auf externe Dateifreigaben zugreifen, auch wenn das Computerkonto des Arbeitsgruppenservers für die externe Freigabe über die Berechtigung **Lesen** verfügt. Alternative Quellspeicherorte, die für Arbeitsgruppenserver funktionieren, sind u. a. Installationsmedien, Windows Update sowie VHD- oder WIM-Dateien, die auf dem lokalen Arbeitsgruppenserver gespeichert sind.  
>   
> Sie können eine WIM-Datei als Quelle einer alternativen Funktion angeben, wenn Sie Rollen, Rollendienste und Features auf einem aktiven physischen Server installieren. Der Quellpfad für eine WIM-Datei muss in folgendem Format ein, wobei **WIM** als Präfix und der Index in der die featuredateien befinden als Suffix: **WIM:e:\Sources\Install.wim:4**. Jedoch kann keine WIM-Datei auch direkt als Quelle verwenden, für die Installation von Rollen, Rollendienste und Features auf einer offline-VHD. Sie müssen entweder die offline-VHD einbinden und zeigen Sie auf ihren Bereitstellungspfad für Quelldateien, oder Sie müssen auf einen Ordner mit einer Kopie des Inhalts der WIM-Datei verweisen.  
  
### <a name="to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet"></a>So installieren Sie .NET Framework 3.5 durch Ausführen des Install-WindowsFeature-Cmdlets  
  
1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.  
  
    > [!NOTE]  
    > Wenn Sie Rollen und Features von einem Remoteserver installieren, müssen Sie nicht zum Ausführen von Windows PowerShell mit erhöhten Benutzerrechten.  
  
    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.  
  
    -   Geben Sie auf einem Server, auf denen die Server Core-Installationsoption von Windows Server 2012 R2 ausgeführt wird oder Windows Server 2012 **PowerShell** an einer Eingabeaufforderung, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Geben Sie den folgenden Befehl aus, und drücken Sie dann **EINGABETASTE**. Im folgenden Beispiel befinden sich die Quelldateien in einem Seite-an-Seite-Speicher (als **SxS**bezeichnet) auf dem Installationsmedium in Laufwerk D.  
  
    ```  
    Install-WindowsFeature NET-Framework-Core -Source D:\Sources\SxS  
    ```  
  
    Falls der Befehl Windows Update als Quelle für fehlende Featuredateien verwenden soll oder bereits eine Standardquelle mithilfe der Gruppenrichtlinie konfiguriert wurde, muss der Parameter `Source` nur hinzugefügt werden, wenn Sie eine andere Quelle angeben möchten.  
  
### <a name="to-install-net-framework-35-by-using-the-add-roles-and-features-wizard"></a>So installieren Sie .NET Framework 3.5 mithilfe des Hinzufügen von Rollen und Features-Assistenten  
  
1.  Auf der **verwalten** im Server-Manager, klicken Sie anschließend auf **Rollen und Features hinzufügen**.  
  
2.  Wählen Sie einen Zielserver, auf der Windows Server 2016 ausgeführt wird.  
  
3.  Auf der **Funktionen auswählen** Seite des Hinzufügen von Rollen und Features-Assistenten die Option **.NET Framework 3.5**.  
  
4.  Ist dies durch die Gruppenrichtlinieneinstellungen für den lokalen Computer zugelassen, wird beim Installationsprozess versucht, die fehlenden Featuredateien mithilfe von Windows Update abzurufen. Klicken Sie auf **Installieren**. Sie müssen nicht mit dem nächsten Schritt fortfahren.  
  
    Wenn die gruppenrichtlinieneinstellungen diese Vorgehensweise nicht zulassen, oder Sie eine andere Quelle für die .NET Framework 3.5-featuredateien auf verwenden möchten die **Installationsauswahl bestätigen** Seite des Assistenten klicken Sie auf **alternativen Quellpfad angeben** .  
  
5.  Geben Sie einen Pfad zu einem Seite-an-Seite-Speicher (als **SxS**bezeichnet) auf einem Installationsmedium oder zu einer WIM-Datei an. Im folgenden Beispiel befindet sich das Installationsmedium in Laufwerk D.  
  
    **D:\Sources\SxS\\**  
  
    Fügen Sie zum Angeben einer WIM-Datei ein **WIM:** -Präfix und den Index des in der WIM-Datei zu verwendenden Images als Suffix hinzu. Dies wird im folgenden Beispiel dargestellt:  
  
    **WIM:\\\\***Server_name***\share\install.wim:3**  
  
6.  Klicken Sie auf **OK**und dann auf **Installieren**.  
  
### <a name="to-install-net-framework-35-by-using-dism"></a>So installieren Sie .NET Framework 3.5 mithilfe von DISM  
  
1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.  
  
    > [!NOTE]  
    > Wenn Sie Rollen und Features von einem Remoteserver installieren, müssen Sie nicht zum Ausführen von Windows PowerShell mit erhöhten Benutzerrechten.  
  
    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.  
  
    -   Geben Sie auf einem Server, auf denen die Server Core-Installationsoption ausgeführt wird, **PowerShell** an einer Eingabeaufforderung, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Führen Sie einen der folgenden DISM-Befehle aus.  
  
    -   Wenn der Computer Zugriff auf Windows Update hat oder einen Standardspeicherort für Quelldateien bereits in der Gruppenrichtlinie konfiguriert wurde, führen Sie den folgenden Befehl aus.  
  
        ```  
        DISM /online /Enable-Feature /Featurename:NetFx3 /All  
        ```  
  
    -   Wenn der Computer Zugriff auf den Installationsmedien, und führen Sie einen Befehl ähnlich dem folgenden verfügt. Im folgenden Beispiel befindet sich das Installationsmedium in Laufwerk D. Der `LimitAccess`-Parameter verhindert, dass der Befehl versucht, Windows Update oder einen Server mit WSUS zu kontaktieren.  
  
        ```  
        DISM /online /Enable-Feature /Featurename:NetFx3 /All /LimitAccess /Source:d:\sources\sxs  
        ```  
  
    > [!NOTE]  
    > Beim DISM-Befehl muss die Groß-/Kleinschreibung beachtet werden.  
  
### <a name="configure-alternate-sources-for-feature-files-in-group-policy"></a>Konfigurieren alternativer Quellen für Featuredateien in der Gruppenrichtlinie  
Die in diesem Abschnitt beschriebene Gruppenrichtlinieneinstellung gibt autorisierte Quellspeicherorte für .NET Framework 3.5-Dateien und andere Featuredateien an, die im Rahmen der Konfiguration von %%amp;quot;Features bei Bedarf%%amp;quot; entfernt wurden. Die richtlinieneinstellung **Geben Sie Einstellungen für die Installation optionaler Komponenten und Reparatur von Komponenten** befindet sich in der **Computer Computerkonfiguration\Administrative Vorlagen\System** Ordner in der Gruppenrichtlinie -Verwaltungskonsole oder der lokalen Gruppenrichtlinien-Editor.  
  
> [!NOTE]  
> Sie müssen Mitglied der Administratorgruppe sein, um Gruppenrichtlinieneinstellungen auf dem lokalen Computer ändern zu können. Falls die Gruppenrichtlinieneinstellungen für den zu verwaltenden Computer auf der Domänenebene gesteuert werden, müssen Sie Mitglied der Gruppe %%amp;quot;Domänenadministratoren%%amp;quot; sein, um Gruppenrichtlinieneinstellungen ändern zu können.  
  
##### <a name="to-configure-a-default-alternate-source-path-in-group-policy"></a>So konfigurieren Sie einen alternativen Standardquellpfad in der Gruppenrichtlinie  
  
1.  Öffnen Sie in lokalen Gruppenrichtlinien-Editor oder Gruppenrichtlinien-Verwaltungskonsole die folgende richtlinieneinstellung.  
  
    **Computerkonfiguration\Administrative vorlagen\system\einstellungen für die Installation optionaler Komponenten und Reparatur von Komponenten**  
  
2. Swählen **aktiviert** die richtlinieneinstellung ggf. zu aktivieren, wenn sie nicht bereits aktiviert ist.  
  
3.  Geben Sie im Textfeld **Alternativer Dateiquellpfad** im Bereich **Optionen** einen vollqualifizierten Pfad zu einem freigegebenen Ordner oder einer WIM-Datei an. Fügen Sie zum Angeben einer WIM-Datei als alternativer Quelldateispeicherort dem Pfad das Präfix **WIM:** und den Index des in der WIM-Datei zu verwendenden Images als Suffix hinzu. Die folgenden Beispiele enthalten Werte, die Sie angeben können.  
  
    -   Pfad zu einem freigegebenen Ordner: * *\\\\***Server_name***\share\\*** Ordnername*  
  
    -   Pfad zu einer WIM-Datei, in dem **3** stellt den Index des Bilds in dem sich die featuredateien befinden:  **WIM:\\\\***Server_name***\share\install.wim:3**  
  
4.  Wenn Sie Computer nicht möchten, die von dieser richtlinieneinstellung zum Suchen nach fehlenden featuredateien in Windows Update auswählen gesteuert werden **nie versuchen, nutzlastdateien über Windows Update herunterzuladen**.  
  
5.  Falls die von dieser Richtlinieneinstellung gesteuerten Richtlinieneinstellung in der Regel Updates über WSUS erhalten, Sie jedoch fehlende Featuredateien lieber über Windows Update und nicht über WSUS suchen möchten, aktivieren Sie **Stellen Sie direkt eine Verbindung mit Windows Update her, um Inhalte für das Reparieren herunterzuladen, anstatt WSUS (Windows Server Update Services) zu verwenden.**  
  
6.  Klicken Sie auf **OK**, wenn Sie diese Richtlinieneinstellung geändert haben. Schließend Sie dann den Gruppenrichtlinien-Editor.  
  
## <a name="see-also"></a>Siehe auch  
[Windows Server-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkId=241573)  
[Überlegungen zur Bereitstellung von Microsoft .NET Framework 3.5](https://go.microsoft.com/fwlink/p/?LinkId=248869)  
[Aktivieren oder Deaktivieren von Windows-Features](https://go.microsoft.com/fwlink/p/?LinkId=246552)  
  


