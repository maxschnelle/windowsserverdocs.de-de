---
title: Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features
description: Server-Manager
ms.topic: article
ms.assetid: 04f16d84-45c2-4771-84c1-1cc973d0ee02
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d77ad8e55c8e61f2419cfd1c7ad8c8ce8195022
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895779"
---
# <a name="install-or-uninstall-roles-role-services-or-features"></a>Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server ermöglichen die Server-Manager-Konsole und Windows PowerShell-Cmdlets für Server-Manager die Installation von Rollen und Features auf lokalen oder Remote Servern oder virtuellen Festplatten (VHDs) im Offline Modus. Sie können mehrere Rollen und Features auf einem einzelnen Remote Server oder einer Offline-VHD in einem einzelnen Assistenten zum Hinzufügen von Rollen und Features oder in einer Windows PowerShell-Sitzung installieren.

> [!IMPORTANT]
> Server-Manager können nicht verwendet werden, um eine neuere Version des Windows Server-Betriebssystems zu verwalten. Server-Manager, die unter Windows Server 2012 R2 oder Windows 8.1 ausgeführt werden, können nicht zum Installieren von Rollen, Rollen Diensten und Features auf Servern verwendet werden, auf denen Windows Server 2016 ausgeführt wird.

Sie müssen bei einem Server als Administrator angemeldet sein, um Rollen, Rollen Dienste und Features zu installieren oder zu deinstallieren. Wenn Sie am lokalen Computer mit einem Konto angemeldet sind, das nicht über Administratorrechte auf dem Zielserver verfügt, klicken Sie auf der Kachel **Server** mit der rechten Maustaste auf den Zielserver, und klicken Sie dann auf **Verwalten als**, um ein Konto mit Administratorrechten anzugeben. Der Server, auf dem eine Offline-VHD eingebunden werden soll, muss Server-Manager hinzugefügt werden. Zudem müssen Sie über Administratorrechte für diesen Server verfügen.

Weitere Informationen zu Rollen, Rollen Diensten und Features finden Sie unter [Rollen, Rollen Dienste und Features](https://go.microsoft.com/fwlink/p/?LinkId=239558).

Dieses Thema enthält folgende Abschnitte:

-   [Installieren von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)

-   [Installieren von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets](#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)

-   [Entfernen von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Entfernen von Rollen und Features](#remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard)

-   [Entfernen von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets](#remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets)

-   [Installieren von Rollen und Features auf mehreren Servern per Ausführung eines Windows PowerShell-Skripts](#install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script)

-   [Installieren von .NET Framework 3.5 und anderen Features bei Bedarf](#install-net-framework-35-and-other-features-on-demand)

## <a name="install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard"></a>Installieren von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features
In einer einzelnen Sitzung des Assistenten zum Hinzufügen von Rollen und Features können Sie Rollen, Rollen Dienste und Features auf dem lokalen Server, einem Remote Server, der Server-Manager hinzugefügt wurde, oder einer Offline-VHD installieren. Weitere Informationen zum Hinzufügen eines Servers zu Server-Manager zur Verwaltung von finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md).

> [!NOTE]
> Wenn Sie Server-Manager unter Windows Server 2016 oder Windows 10 ausführen, können Sie den Assistenten zum Hinzufügen von Rollen und Features verwenden, um Rollen und Features nur auf Servern und Offline-VHDs zu installieren, auf denen Windows Server 2016 ausgeführt wird.

#### <a name="to-install-roles-and-features-by-using-the-add-roles-and-features-wizard"></a>So installieren Sie Rollen und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features

1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

    -   Klicken Sie auf dem Windows- **Start** Bildschirm auf die Kachel **Server-Manager** .

2.  Klicken Sie im Menü **Verwalten** auf **Rollen und Features hinzufügen**.

3.  Überprüfen Sie auf der Seite **Vorbemerkungen**, ob der Zielserver und die Netzwerkumgebung für die Installation der Rolle und des Features vorbereitet sind. Klicken Sie auf **Weiter**.

4.  Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, um alle Teile von Rollen oder Features auf einem Server zu installieren. Wählen Sie alternativ **Installation von Remotedesktopdiensten** aus, um entweder eine Desktopinfrastruktur mit virtuellen Computern oder eine sitzungsbasierte Desktopinfrastruktur für die Remotedesktopdienste zu installieren. Bei Verwendung der Option **Szenariobasierte Installation von Remotedesktopdiensten** werden logische Teile der Remotedesktopdienste-Rolle von Administratoren je nach Bedarf auf verschiedene Server verteilt. Klicken Sie auf **Weiter**.

5.  Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, oder wählen Sie eine Offline-VHD aus. Um eine Offline-VHD als Zielserver auszuwählen, müssen Sie zuerst den Server auswählen, auf dem die VHD eingebunden werden soll. Wählen Sie anschließend die VHD-Datei aus. Weitere Informationen zum Hinzufügen von Servern zum-Server Pool finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md). Klicken Sie nach dem Auswählen des Zielservers auf **Weiter**.

    > [!NOTE]
    > Zum Installieren von Rollen und Features auf Offline-VHDs müssen Ziel-VHDs die folgenden Anforderungen erfüllen.
    >
    > -   Auf VHDs muss die Version von Windows Server ausgeführt werden, die mit der Version von Server-Manager übereinstimmt, die Sie ausführen. Weitere Informationen finden Sie im Hinweis zu Beginn der [Installation von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard).
    > -   VHDs dürfen nicht mehr als ein Systemvolume oder eine Partition aufweisen.
    > -   Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.
    >
    >     -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**
    >     -   **Voll** Zugriff auf die Registerkarte " **Sicherheit** ", Dialogfeld "Datei-oder Ordner **Eigenschaften** ".

6.  Wählen Sie Rollen und ggf. Rollendienste für die Rolle aus, und klicken Sie dann zum Auswählen von Features auf **Weiter**.

    Wenn Sie fortfahren, werden Sie vom Assistenten zum Hinzufügen von Rollen und Features automatisch informiert, wenn Konflikte auf dem Zielserver gefunden wurden, die die Installation oder den normalen Betrieb von ausgewählten Rollen oder Features verhindern können. Sie werden außerdem aufgefordert, Rollen, Rollendienste oder Features hinzuzufügen, die für die ausgewählten Rollen oder Features erforderlich sind.

    Wenn die Rolle von einem anderen Server oder einem Windows Client-basierten Computer mit Remoteserver-Verwaltungstools aus verwaltet werden soll, brauchen Sie die Verwaltungstools und Snap-Ins für Rollen auf dem Zielserver nicht zu installieren. Standardmäßig werden im Assistenten zum Hinzufügen von Rollen und Features Verwaltungs Tools für die Installation ausgewählt.

7.  Überprüfen Sie auf der Seite **Installationsauswahl bestätigen** Ihre Rollen-, Feature- und Serverauswahl. Klicken Sie anschließend auf **Installieren**.

    Sie können Ihre Auswahl auch in eine XML-basierte Konfigurationsdatei exportieren, die Sie für unbeaufsichtigte Installationen mit Windows PowerShell verwenden können. Um die in dieser Sitzung zum Hinzufügen von Rollen und Features angegebene Konfiguration zu exportieren, klicken Sie auf **Konfigurationseinstellungen exportieren**, und speichern Sie die XML-Datei dann an einem geeigneten Speicherort.

    Mit dem Befehl **Alternativen Quellpfad angeben** auf der Seite **Installationsauswahl bestätigen** geben Sie einen alternativen Quellpfad für die Dateien an, die für die Installation von Rollen und Features auf dem ausgewählten Server erforderlich sind. In Windows Server 2012 und neueren Versionen von Windows Server können Sie mithilfe von [Features bei Bedarf](https://go.microsoft.com/fwlink/p/?LinkID=241573) die Menge des vom Betriebssystem genutzten Speicherplatzes verringern, indem Sie Rollen-und Featuredateien von Servern entfernen, die ausschließlich Remote verwaltet werden. Wenn Sie Rollen- und Featuredateien mit dem Cmdlet `Uninstall-WindowsFeature -remove` von einem Server entfernt haben, können Sie später Rollen und Features auf dem Server installieren, indem Sie einen alternativen Quellpfad oder eine Freigabe angeben, an dem bzw. auf der die erforderlichen Rollen- und Featuredateien gespeichert sind. Der Quellpfad oder die Dateifreigabe muss entweder der Gruppe **jeder** (nicht empfohlen aus Sicherheitsgründen) oder dem Computer Konto (*Domäne* **Read** \\ *Servername*$) des Zielservers Leseberechtigungen erteilen. das Gewähren des Benutzerkonto Zugriffs ist nicht ausreichend. Weitere Informationen zu Features bei Bedarf finden Sie unter [Windows Server-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkId=241573).

    Sie können eine WIM-Datei als Alternative Funktions Datei Quelle angeben, wenn Sie Rollen, Rollen Dienste und Features auf einem laufenden physischen Server installieren. Der Quellpfad für eine WIM-Datei sollte das folgende Format haben, wobei **WIM** als Präfix und der Index, unter dem sich die Featuredateien befinden, als Suffix angegeben wird: **WIM:e:\sources\install.wim:4**. Sie können eine WIM-Datei jedoch nicht direkt als Quelle zum Installieren von Rollen, Rollen Diensten und Features auf einer Offline-VHD verwenden. Sie müssen entweder die Offline-VHD einbinden und auf den zugehörigen einstellungspfad für Quelldateien verweisen, oder Sie müssen auf einen Ordner verweisen, der eine Kopie des Inhalts der WIM-Datei enthält.

8.  Nachdem Sie auf **Installieren**klicken, werden auf der Seite **Installations** Status der Installationsfortschritt, Ergebnisse und Meldungen wie Warnungen, Fehler oder nach der Installation erforderliche Konfigurationsschritte angezeigt, die für die installierten Rollen oder Features erforderlich sind. In Windows Server 2012 und neueren Versionen von Windows Server können Sie den Assistenten zum Hinzufügen von Rollen und Features schließen, während die Installation noch läuft, und Installations Ergebnisse oder andere Meldungen im **Benachrichtigungs** Bereich oben in der Server-Manager-Konsole anzeigen. Klicken Sie auf das Symbol **Benachrichtigungen** , um weitere Details zu Installationen oder anderen Aufgaben anzuzeigen, die Sie in Server-Manager ausführen.

## <a name="install-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Installieren von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets
Die Server-Manager Bereitstellungs-Cmdlets für Windows PowerShell funktionieren ähnlich wie der GUI-basierte Assistent zum Hinzufügen von Rollen und Features und der Assistent zum Entfernen von Rollen und Features mit einem wichtigen Unterschied. Im Gegensatz zum Assistenten zum Hinzufügen von Rollen und Features sind in Windows PowerShell die Verwaltungs Tools und Snap-Ins für eine Rolle nicht standardmäßig enthalten. Um Verwaltungstools in eine Rolleninstallation einzuschließen, fügen Sie dem Cmdlet den `IncludeManagementTools` -Parameter hinzu. Wenn Sie Rollen und Features auf einem Server installieren, auf dem die Server Core-Installationsoption von Windows Server 2012 oder höher ausgeführt wird, können Sie einer Installation die Verwaltungs Tools einer Rolle hinzufügen. GUI-basierte Verwaltungs Tools und Snap-Ins können jedoch nicht auf Servern installiert werden, auf denen die Server Core-Installationsoption von Windows Server ausgeführt wird. Nur die Befehlszeilen-und Windows PowerShell-Verwaltungs Tools können auf der Server Core-Installationsoption installiert werden.

#### <a name="to-install-roles-and-features-by-using-the-install-windowsfeature-cmdlet"></a>So installieren Sie Rollen und Features mit dem Cmdlet %%amp;quot;Install-WindowsFeature%%amp;quot;

1. Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, indem Sie einen der folgenden Schritte durchführen.

   > [!NOTE]
   > Wenn Sie Rollen und Features auf einem Remote Server installieren, müssen Sie Windows PowerShell nicht mit erhöhten Benutzerrechten ausführen.

   -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

   -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel für Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

2. Geben Sie **Get-WindowsFeature** ein, und drücken Sie anschließend die **EINGABETASTE**, um eine Liste der auf dem lokalen Server verfügbaren und installierten Rollen und Features anzuzeigen. Wenn der lokale Computer kein Server ist oder Sie Informationen zu einem Remote Server benötigen, führen Sie **Get-Windows Feature-Computername <** <em>computer_name</em> **>** aus, wobei *computer_name* den Namen eines Remote Computers darstellt, auf dem Windows Server 2016 ausgeführt wird. Die Ergebnisse des Cmdlets enthalten die Befehlsnamen der Rollen und Features, die Sie Ihrem Cmdlet in Schritt 4 hinzufügen.

   > [!NOTE]
   > In Windows PowerShell 3,0 und neueren Versionen von Windows PowerShell müssen Sie das Server-Manager Cmdlet-Modul nicht in die Windows PowerShell-Sitzung importieren, bevor Sie die Cmdlets ausführen, die Teil des Moduls sind. Module werden automatisch importiert, wenn Sie ein zum Modul gehörendes Cmdlet zum ersten Mal ausführen. Außerdem wird bei beiden Windows PowerShell-Cmdlets und den Funktionsnamen, die mit den Cmdlets verwendet werden, die Groß-/Kleinschreibung beachtet.

3. geben **Sie Get-Help install-Windows Feature**ein, und drücken **Sie** dann die EINGABETASTE, um die Syntax und die zulässigen Parameter für das `Install-WindowsFeature` Cmdlet anzuzeigen.

4. Geben Sie Folgendes ein, und drücken **Sie**dann die EINGABETASTE, wobei *feature_name* den Befehlsnamen einer Rolle oder eines Features darstellt, die Sie installieren möchten (abgerufen in Schritt 2), und *computer_name* einen Remote Computer darstellt, auf dem Sie Rollen und Features installieren möchten. Trennen Sie mehrere Werte für *feature_name* durch Kommas. Der `Restart` -Parameter startet den Zielserver automatisch neu, wenn die Installation der Rolle bzw. des Features dies erfordert.

   ```
   Install-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart
   ```

   Fügen Sie zum Installieren von Rollen oder Features auf einer Offline-VHD die Parameter `computerName` und `VHD` hinzu. Wird der `computerName` -Parameter nicht hinzugefügt, geht das Cmdlet davon aus, dass der lokale Computer zum Zugreifen auf die VHD eingebunden wird. Der Parameter `computerName` enthält den Namen des Servers, auf dem die VHD eingebunden werden soll, und der Parameter `VHD` enthält den Pfad zur VHD-Datei auf dem angegebenen Server.

   > [!NOTE]
   > Sie müssen den- `computerName` Parameter hinzufügen, wenn Sie das Cmdlet auf einem Computer ausführen, auf dem ein Windows-Client Betriebssystem ausgeführt wird.
   >
   > Zum Installieren von Rollen und Features auf Offline-VHDs müssen Ziel-VHDs die folgenden Anforderungen erfüllen.
   >
   > -   Auf VHDs muss die Version von Windows Server ausgeführt werden, die mit der Version von Server-Manager übereinstimmt, die Sie ausführen. Weitere Informationen finden Sie im Hinweis zu Beginn der [Installation von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard).
   > -   VHDs dürfen nicht mehr als ein Systemvolume oder eine Partition aufweisen.
   > -   Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.
   >
   >     -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**
   >     -   **Voll** Zugriff auf die Registerkarte " **Sicherheit** ", Dialogfeld "Datei-oder Ordner **Eigenschaften** ".

   ```
   Install-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart
   ```

   **Beispiel:** Mit dem folgenden Cmdlet werden die Active Directory-Domänen Dienste-Rolle und das Gruppenrichtlinie Verwaltungs Feature auf einem Remote Server, ContosoDC1, installiert. Die Verwaltungstools und Snap-Ins werden mit dem Parameter `IncludeManagementTools` hinzugefügt, und der Zielserver wird automatisch neu gestartet, falls dies für die Installation erforderlich ist.

   ```
   Install-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart
   ```

5. Wenn die Installation abgeschlossen ist, überprüfen Sie die Installation, indem Sie in Server-Manager die Seite **alle Server** öffnen, einen Server auswählen, auf dem Sie Rollen und Features installiert haben, und die Kachel **Rollen und Features** auf der Seite für den ausgewählten Server anzeigen. Sie können auch das- `Get-WindowsFeature` Cmdlet für den ausgewählten Server (Get-Windows Feature-Computername <*computer_name*>) ausführen, um eine Liste der Rollen und Features anzuzeigen, die auf dem Server installiert sind.

## <a name="remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard"></a>Entfernen von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Entfernen von Rollen und Features
Sie müssen bei einem Server als Administrator angemeldet sein, um Rollen, Rollen Dienste und Features zu deinstallieren. Wenn Sie am lokalen Computer mit einem Konto angemeldet sind, das nicht über Administratorrechte auf dem Deinstallationszielserver verfügt, klicken Sie auf der Kachel **Server** mit der rechten Maustaste auf den Zielserver, und klicken Sie dann auf **Verwalten als**, um ein Konto mit Administratorrechten anzugeben. Der Server, auf dem eine Offline-VHD eingebunden werden soll, muss Server-Manager hinzugefügt werden. Zudem müssen Sie über Administratorrechte für diesen Server verfügen.

#### <a name="to-remove-roles-and-features-by-using-the-remove-roles-and-features-wizard"></a>So entfernen Sie Rollen und Features mithilfe des Assistenten zum Entfernen von Rollen und Features

1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

    -   Klicken Sie auf der **** Windows-Startseite auf die Kachel **Server-Manager**.

2.  Klicken Sie im Menü **Verwalten** auf **Rollen und Funktionen entfernen**.

3.  Überprüfen Sie auf der Seite **Vorbemerkungen**, ob alle Vorbereitungen zum Entfernen von Rollen oder Features von einem Server getroffen wurden. Klicken Sie auf **Weiter**.

4.  Wählen Sie auf der Seite **Ziel Server auswählen** einen Server aus dem Server Pool aus, oder wählen Sie eine Offline-VHD aus. Um eine Offline-VHD auszuwählen, müssen Sie zuerst den Server auswählen, auf dem die VHD eingebunden werden soll. Wählen Sie anschließend die VHD-Datei aus.

    > [!NOTE]
    > Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.
    >
    > -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**
    > -   Zugriffsrecht **Vollzugriff** auf der Registerkarte **Sicherheit** im Datei- oder Ordnerdialogfeld **Eigenschaften**

    Weitere Informationen zum Hinzufügen von Servern zum-Server Pool finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md). Klicken Sie nach dem Auswählen des Zielservers auf **Weiter**.

    > [!NOTE]
    > Mit dem Assistenten zum Entfernen von Rollen und Features können Sie Rollen und Features von Servern entfernen, auf denen dieselbe Version von Windows Server ausgeführt wird, die die von Ihnen verwendete Version von Server-Manager unterstützt. Es ist nicht möglich, Rollen, Rollen Dienste oder Features von Servern zu entfernen, auf denen Windows Server 2016 ausgeführt wird, wenn Sie Server-Manager unter Windows Server 2012 R2, Windows Server 2012 oder Windows 8 ausführen. Sie können den Assistenten zum Entfernen von Rollen und Features nicht zum Entfernen von Rollen und Features von Servern verwenden, auf denen Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird.

5.  Wählen Sie Rollen und ggf. Rollendienste für die Rolle aus, und klicken Sie dann zum Auswählen von Features auf **Weiter**.

    Wenn Sie fortfahren, werden Sie vom Assistenten zum Entfernen von Rollen und Features automatisch aufgefordert, Rollen, Rollen Dienste oder Features zu entfernen, die nicht ohne die zu entfernenden Rollen oder Features ausgeführt werden können.

    Außerdem können Sie die Verwaltungs Tools und Snap-Ins für Rollen auf dem Zielserver entfernen. Standardmäßig sind die Verwaltungs Tools im Assistenten zum Entfernen von Rollen und Features zum Entfernen ausgewählt. Sie können die Verwaltungstools und Snap-Ins behalten, wenn Sie vorhaben, den ausgewählten Server zur Verwaltung der Rolle auf anderen Remoteservern zu verwenden.

6.  Überprüfen Sie auf der Seite **Entfernungsauswahl bestätigen** Ihre Rollen-, Feature- und Serverauswahl. Wenn Sie bereit sind, die Rollen oder Features zu entfernen, klicken Sie auf **Entfernen**.

7.  Nachdem Sie auf **Entfernen**klicken, werden auf der Seite **Entfernungs** Status der Entfernungs Status, Ergebnisse und Meldungen, wie z. b. Warnungen, Fehler oder nach der Entfernung erforderliche Konfigurationsschritte, wie z. b. der Neustart des Zielservers, angezeigt. In Windows Server 2012 und neueren Versionen von Windows Server können Sie den Assistenten zum Entfernen von Rollen und Features schließen, während der Deinstallations Vorgang noch ausgeführt wird, und die Entfernungs Ergebnisse oder andere Meldungen im **Benachrichtigungs** Bereich oben in der Server-Manager-Konsole anzeigen. Klicken Sie auf das **Benachrichtigungs** Kennzeichen, um weitere Details zu Entfernungen oder anderen Aufgaben anzuzeigen, die Sie in Server-Manager ausführen.

## <a name="remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Entfernen von Rollen, Rollendiensten und Features mit Windows PowerShell-Cmdlets
Die Server-Manager Bereitstellungs-Cmdlets für Windows PowerShell funktionieren ähnlich wie der GUI-basierte Assistent zum Entfernen von Rollen und Features mit einem wichtigen Unterschied. Im Gegensatz zum Assistenten zum Entfernen von Rollen und Features werden in Windows PowerShell die Verwaltungs Tools und Snap-Ins für eine Rolle nicht standardmäßig entfernt. Um Verwaltungstools im Rahmen einer Rollenentfernung zu entfernen, fügen Sie dem Cmdlet den `IncludeManagementTools` -Parameter hinzu. Wenn Sie Rollen und Features von einem Server deinstallieren, auf dem die Server Core-Installationsoption von Windows Server 2012 oder einer neueren Version von Windows Server ausgeführt wird, entfernt dieser Parameter die Befehlszeilen-und Windows PowerShell-Verwaltungs Tools für die angegebenen Rollen und Features.

#### <a name="to-remove-roles-and-features-by-using-the-uninstall-windowsfeature-cmdlet"></a>So entfernen Sie Rollen und Features mit dem Cmdlet %%amp;quot;UnInstall-WindowsFeature%%amp;quot;

1. Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, indem Sie einen der folgenden Schritte durchführen.

   > [!NOTE]
   > Wenn Sie Rollen und Features von einem Remote Server deinstallieren, müssen Sie Windows PowerShell nicht mit erhöhten Benutzerrechten ausführen.

   -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

   -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

2. Geben Sie **Get-WindowsFeature** ein, und drücken Sie anschließend die **EINGABETASTE**, um eine Liste der auf dem lokalen Server verfügbaren und installierten Rollen und Features anzuzeigen. Wenn der lokale Computer kein Server ist oder Sie Informationen zu einem Remote Server benötigen, führen Sie **Get-Windows Feature-Computername <** <em>computer_name</em> **>** aus, wobei *computer_name* den Namen eines Remote Computers darstellt, auf dem Windows Server 2016 ausgeführt wird. Die Ergebnisse des Cmdlets enthalten die Befehlsnamen der Rollen und Features, die Sie Ihrem Cmdlet in Schritt 4 hinzufügen.

   > [!NOTE]
   > In Windows PowerShell 3,0 und neueren Versionen von Windows PowerShell müssen Sie das Server-Manager Cmdlet-Modul nicht in die Windows PowerShell-Sitzung importieren, bevor Sie die Cmdlets ausführen, die Teil des Moduls sind. Module werden automatisch importiert, wenn Sie ein zum Modul gehörendes Cmdlet zum ersten Mal ausführen. Außerdem wird bei beiden Windows PowerShell-Cmdlets und den Funktionsnamen, die mit den Cmdlets verwendet werden, die Groß-/Kleinschreibung beachtet.

3. geben **Sie Get-Help Uninstall-Windows Feature**ein, und drücken **Sie** dann die EINGABETASTE, um die Syntax und die zulässigen Parameter für das `Uninstall-WindowsFeature` Cmdlet anzuzeigen.

4. Geben Sie Folgendes ein, und drücken Sie dann die **EINGABETASTE**. Dabei steht *Featurename* für den Befehlsnamen einer Rolle oder eines Features, die bzw. das entfernt werden soll (abgerufen in Schritt 2), und *computer_name* für einen Remotecomputer, von dem Rollen und Features entfernt werden sollen. Trennen Sie mehrere Werte für *feature_name* durch Kommas. Der `Restart` -Parameter startet Zielserver automatisch neu, wenn die Entfernung der Rolle bzw. des Features dies erfordert.

   ```
   Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart
   ```

   Fügen Sie zum Deinstallieren von Rollen oder Features auf einer Offline-VHD die Parameter `computerName` und `VHD` hinzu. Wird der `computerName` -Parameter nicht hinzugefügt, geht das Cmdlet davon aus, dass der lokale Computer zum Zugreifen auf die VHD eingebunden wird. Der Parameter `computerName` enthält den Namen des Servers, auf dem die VHD eingebunden werden soll, und der Parameter `VHD` enthält den Pfad zur VHD-Datei auf dem angegebenen Server.

   > [!NOTE]
   > Sie müssen den- `computerName` Parameter hinzufügen, wenn Sie das Cmdlet auf einem Computer ausführen, auf dem ein Windows-Client Betriebssystem ausgeführt wird.
   >
   > Der freigegebene Netzwerkordner, in dem die VHD-Datei gespeichert ist, muss dem Computerkonto (bzw. lokalen System) des Servers, den Sie zum Einbinden der VHD ausgewählt haben, die folgenden Zugriffsrechte gewähren. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.
   >
   > -   Zugriffsrecht **Lesen/Schreiben** im Dialogfeld **Dateifreigabe**
   > -   **Voll** Zugriff auf die Registerkarte " **Sicherheit** ", Dialogfeld "Datei-oder Ordner **Eigenschaften** ".

   ```
   Uninstall-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart
   ```

   **Beispiel:** Mit dem folgenden Cmdlet werden die Active Directory-Domänen Dienste-Rolle und die Gruppenrichtlinie Verwaltungsfunktion von einem Remote Server (ContosoDC1) entfernt. Die Verwaltungstools und Snap-Ins werden ebenfalls entfernt, und der Zielserver wird automatisch neu gestartet, falls dies für das Entfernen erforderlich ist.

   ```
   Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart
   ```

5. Wenn die Deinstallation abgeschlossen ist, überprüfen Sie, ob die Rollen und Features entfernt wurden, indem Sie in Server-Manager die Seite **alle Server** öffnen, den Server auswählen, von dem Sie Rollen und Features entfernt haben, und die Kachel **Rollen und Features** auf der Seite für den ausgewählten Server anzeigen. Sie können auch das- `Get-WindowsFeature` Cmdlet für den ausgewählten Server (Get-Windows Feature-Computername <*computer_name*>) ausführen, um eine Liste der Rollen und Features anzuzeigen, die auf dem Server installiert sind.

## <a name="install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script"></a>Installieren von Rollen und Features auf mehreren Servern per Ausführung eines Windows PowerShell-Skripts
Obwohl Sie den Assistenten zum Hinzufügen von Rollen und Features nicht zum Installieren von Rollen, Rollen Diensten und Features auf mehr als einem Zielserver in einer einzelnen Assistenten Sitzung verwenden können, können Sie mithilfe eines Windows PowerShell-Skripts Rollen, Rollen Dienste und Features auf mehreren Ziel Servern installieren, die Sie mit Server-Manager verwalten. Das Skript, das Sie zum Ausführen der Batch Bereitstellung verwenden, wenn dieser Vorgang aufgerufen wird, verweist auf eine XML-Konfigurationsdatei, die Sie mithilfe des Assistenten zum Hinzufügen von Rollen und Features auf einfache Weise erstellen können, und auf **Konfigurationseinstellungen exportieren** , nachdem Sie den Assistenten im Assistenten zum Hinzufügen von Rollen und Features auf die Seite " **Installations Auswahl bestätigen** " geklickt haben.

> [!IMPORTANT]
> Auf allen in Ihrem Skript angegebenen Ziel Servern muss die Version von Windows Server ausgeführt werden, die mit der Version von übereinstimmt, die Server-Manager auf dem lokalen Computer ausgeführt wird. Wenn Sie z. b. Server-Manager unter Windows 10 ausführen, können Sie Rollen, Rollen Dienste und Features auf Servern installieren, auf denen Windows Server 2016 ausgeführt wird. Wenn der Installation GUI-basierte Verwaltungs Tools hinzugefügt werden, werden Zielserver, auf denen die Server Core-Installationsoption von Windows Server ausgeführt wird, beim Installationsvorgang automatisch in die vollständige Installationsoption (Server mit einer vollständigen GUI, auch als "Running Server Graphical Shell" bezeichnet) konvertiert.
>
> Das in diesem Abschnitt angegebene Skript ist ein Beispiel dafür, wie die Batch Bereitstellung mithilfe des `Install-WindowsFeature` -Cmdlets und eines Windows PowerShell-Skripts ausgeführt werden kann. Es gibt noch weitere mögliche Skripts und Methoden zur Durchführung der Batchbereitstellung auf mehreren Servern. Sie können das [Script Center-Repository](https://gallery.technet.microsoft.com/ScriptCenter)nutzen, um nach anderen Skripts zum Bereitstellen von Rollen und Features zu suchen oder diese bereitzustellen.

#### <a name="to-install-roles-and-features-on-multiple-servers"></a>So installieren Sie Rollen und Features auf mehreren Servern

1.  Wenn Sie dies nicht bereits getan haben, erstellen Sie eine XML-Konfigurationsdatei, die die Rollen, Rollen Dienste und Features enthält, die auf mehreren Servern installiert werden sollen. Sie können diese Konfigurationsdatei erstellen, indem Sie den Assistenten zum Hinzufügen von Rollen und Features ausführen, Rollen, Rollen Dienste und Features auswählen und auf **Konfigurationseinstellungen exportieren** klicken, nachdem Sie den Assistenten auf der Seite **Installations Auswahl bestätigen** fortfahren. Speichern Sie die Konfigurationsdatei an einem geeigneten Speicherort. Sie müssen nicht auf **Installieren** klicken bzw. den Assistenten nicht bis zum Ende ausführen, wenn Sie lediglich eine Konfigurationsdatei erstellen möchten.

2.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, indem Sie einen der folgenden Schritte durchführen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

3.  Kopieren Sie das folgende Skript, und fügen Sie es in Ihre Windows PowerShell-Sitzung ein.

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

    1.  Erstellen Sie eine Variable, in der die Namen der Zielcomputer getrennt durch Kommas gespeichert werden. Im folgenden Beispiel sind in der Variablen `$ServerNames` die Namen der Zielserver *Contoso_01* und *Contoso_02* gespeichert. Drücken Sie die **EINGABETASTE**.

        ```
        # Sample Invocation
        $ServerNames = 'Contoso_01','Contoso_02'
        Invoke-WindowsFeatureBatchDeployment -computerNames $ServerNames -ConfigurationFilepath C:\Users\sampleuser\Desktop\DeploymentConfigTemplate.xml
        ```

    2.  Geben Sie zum Ausführen der Funktion Folgendes ein, und drücken Sie die **EINGABETASTE**. Hierbei ist `$ServerNames` ein Beispiel für die Variable, die Sie im vorherigen Schritt erstellt haben, und *C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml* ist ein Beispiel für einen Pfad zur Konfigurationsdatei, den Sie in Schritt 1 erstellt haben.

        **Aufrufen-windowsfeaturebatchdeployment-Computer Names $ServerNames-configurationfilepath C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml**

5.  Wenn die Installation abgeschlossen ist, überprüfen Sie die Installation, indem Sie in Server-Manager die Seite **alle Server** öffnen, einen Server auswählen, auf dem Sie Rollen und Features installiert haben, und die Kachel **Rollen und Features** auf der Seite für den ausgewählten Server anzeigen. Sie können auch das- `Get-WindowsFeature` Cmdlet für einen bestimmten Server ( `Get-WindowsFeature -computerName`  < *computer_name*>) ausführen, um eine Liste der Rollen und Features anzuzeigen, die auf dem Server installiert sind.

## <a name="install-net-framework-35-and-other-features-on-demand"></a>Installieren von .NET Framework 3.5 und anderen Features bei Bedarf
ab Windows Server 2012 und Windows 8 sind die Featuredateien für .NET Framework 3,5 (einschließlich .NET Framework 2,0 und .NET Framework 3,0) nicht standardmäßig auf dem lokalen Computer verfügbar. Die Dateien wurden entfernt. Dateien für Features, die bei der Konfiguration von %%amp;quot;Features bei Bedarf%%amp;quot; entfernt wurden, und Featuredateien für .NET Framework 3.5 stehen über Windows Update zur Verfügung. Wenn Featuredateien auf dem Zielserver, auf dem Windows Server 2012 oder höhere Versionen ausgeführt werden, nicht verfügbar sind, wird beim Installationsvorgang standardmäßig nach den fehlenden Dateien gesucht, indem eine Verbindung mit Windows Update hergestellt wird. Sie können das Standardverhalten überschreiben, indem Sie eine Gruppenrichtlinie Einstellung konfigurieren oder während der Installation einen alternativen Quellpfad angeben. Dies ist unabhängig davon, ob Sie die Installation mit dem Assistenten zum Hinzufügen von Rollen und Features oder einer Befehlszeile durchlaufen.

Sie installieren .NET Framework 3.5 mit einer der folgenden Aktionen:

-   Fügen Sie anhand von [So installieren Sie .NET Framework 3.5 durch Ausführen des Install-WindowsFeature-Cmdlets](#to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet) den `Source`-Parameter hinzu, und geben Sie eine Quelle an, aus der .NET Framework 3.5-Featuredateien abgerufen werden sollen. Wenn Sie den `Source` -Parameter nicht hinzufügen, wird vom Installationsprozess zunächst ermittelt, ob von den Gruppenrichtlinieneinstellungen ein Pfad zu Featuredateien angegeben wurde. Wird kein solcher Pfad gefunden, wird mithilfe von Windows Update nach fehlenden Featuredateien gesucht.

-   Verwenden [Sie zum Installieren von .NET Framework 3,5 mithilfe des Assistenten zum Hinzufügen von Rollen und Features](#to-install-net-framework-35-by-using-the-add-roles-and-features-wizard) auf der Seite **Installationsoptionen bestätigen** des Assistenten zum Hinzufügen von Rollen und Features.

-   Rufen Sie anhand von [So installieren Sie .NET Framework 3.5 mithilfe von DISM](#to-install-net-framework-35-by-using-dism) standardmäßig Dateien aus Windows Update oder durch Angabe eines Quellpfads zum Installationsmedium ab.

[Konfigurieren Sie alternative Quellen für Featuredateien in der Gruppenrichtlinie](#configure-alternate-sources-for-feature-files-in-group-policy) für .NET Framework 3.5 oder andere Features, falls keine Featuredateien auf dem lokalen Computer gefunden werden.

> [!IMPORTANT]
> Bei der Installation von Featuredateien aus einer Remotequelle muss der Quellpfad oder die Dateifreigabe entweder der Gruppe **Jeder** (nicht empfohlen aus Sicherheitsgründen) oder dem Computerkonto (lokales System) des Zielservers Berechtigungen zum **Lesen** gewähren. Das Gewähren des Benutzerkontozugriffs ist nicht ausreichend.
>
> Server in Arbeitsgruppen können nicht auf externe Dateifreigaben zugreifen, auch wenn das Computerkonto des Arbeitsgruppenservers für die externe Freigabe über die Berechtigung **Lesen** verfügt. Alternative Quellspeicherorte, die für Arbeitsgruppenserver funktionieren, sind u. a. Installationsmedien, Windows Update sowie VHD- oder WIM-Dateien, die auf dem lokalen Arbeitsgruppenserver gespeichert sind.
>
> Sie können eine WIM-Datei als Alternative Funktions Datei Quelle angeben, wenn Sie Rollen, Rollen Dienste und Features auf einem laufenden physischen Server installieren. Der Quellpfad für eine WIM-Datei sollte das folgende Format haben, wobei **WIM** als Präfix und der Index, unter dem sich die Featuredateien befinden, als Suffix angegeben wird: **WIM:e:\sources\install.wim:4**. Sie können eine WIM-Datei jedoch nicht direkt als Quelle zum Installieren von Rollen, Rollen Diensten und Features auf einer Offline-VHD verwenden. Sie müssen entweder die Offline-VHD einbinden und auf den zugehörigen einstellungspfad für Quelldateien verweisen, oder Sie müssen auf einen Ordner verweisen, der eine Kopie des Inhalts der WIM-Datei enthält.

### <a name="to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet"></a>So installieren Sie .NET Framework 3.5 durch Ausführen des Install-WindowsFeature-Cmdlets

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, indem Sie einen der folgenden Schritte durchführen.

    > [!NOTE]
    > Wenn Sie Rollen und Features von einem Remote Server installieren, müssen Sie Windows PowerShell nicht mit erhöhten Benutzerrechten ausführen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

    -   Geben Sie auf einem Server, auf dem die Server Core-Installationsoption von Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, **PowerShell** in die Eingabeaufforderung ein, und drücken Sie dann die **Eingabe**Taste.

2.  Geben Sie den folgenden Befehl ein, und drücken Sie dann die **Eingabe**Taste. Im folgenden Beispiel befinden sich die Quelldateien in einem Seite-an-Seite-Speicher (als **SxS** bezeichnet) auf dem Installationsmedium in Laufwerk D.

    ```
    Install-WindowsFeature NET-Framework-Core -Source D:\Sources\SxS
    ```

    Falls der Befehl Windows Update als Quelle für fehlende Featuredateien verwenden soll oder bereits eine Standardquelle mithilfe der Gruppenrichtlinie konfiguriert wurde, muss der Parameter `Source` nur hinzugefügt werden, wenn Sie eine andere Quelle angeben möchten.

### <a name="to-install-net-framework-35-by-using-the-add-roles-and-features-wizard"></a>So installieren Sie .NET Framework 3,5 mithilfe des Assistenten zum Hinzufügen von Rollen und Features

1. Klicken Sie in Server-Manager im Menü **Verwalten** auf **Rollen und Features hinzufügen**.

2. Wählen Sie einen Zielserver aus, auf dem Windows Server 2016 ausgeführt wird.

3. Wählen Sie im Assistenten zum Hinzufügen von Rollen und Features auf der Seite **Features auswählen** die Option **.NET Framework 3,5**aus.

4. Ist dies durch die Gruppenrichtlinieneinstellungen für den lokalen Computer zugelassen, wird beim Installationsprozess versucht, die fehlenden Featuredateien mithilfe von Windows Update abzurufen. Klicken Sie auf **Installieren**. Sie müssen nicht mit dem nächsten Schritt fortfahren.

   Wenn Gruppenrichtlinie Einstellungen dies nicht zulassen oder Sie eine andere Quelle für die .NET Framework 3,5-Featuredateien verwenden möchten, klicken Sie auf der Seite **Installations Auswahl bestätigen** des Assistenten auf **Alternativen Quellpfad angeben**.

5. Geben Sie einen Pfad zu einem Seite-an-Seite-Speicher (als **SxS** bezeichnet) auf einem Installationsmedium oder zu einer WIM-Datei an. Im folgenden Beispiel befindet sich das Installationsmedium in Laufwerk D.

   **D:\Sources\SxS\\**

   Fügen Sie zum Angeben einer WIM-Datei das Präfix **WIM:** und den Index des in der WIM-Datei zu verwendenden Images als Suffix hinzu. Dies wird im folgenden Beispiel dargestellt:

   **Wim: \\ \\ ** <em>server_name</em>**\share\install.Wim: 3**

6. Klicken Sie auf **OK** und dann auf **Installieren**.

### <a name="to-install-net-framework-35-by-using-dism"></a>So installieren Sie .NET Framework 3.5 mithilfe von DISM

1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, indem Sie einen der folgenden Schritte durchführen.

    > [!NOTE]
    > Wenn Sie Rollen und Features von einem Remote Server installieren, müssen Sie Windows PowerShell nicht mit erhöhten Benutzerrechten ausführen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

    -   Geben Sie auf einem Server, auf dem die Server Core-Installationsoption ausgeführt wird, **PowerShell** in die Eingabeaufforderung ein, und drücken Sie dann die **Eingabe**Taste.

2.  Führen Sie einen der folgenden DISM-Befehle aus.

    -   Wenn der Computer Zugriff auf Windows Update hat oder in Gruppenrichtlinie bereits ein Standard Speicherort für Quelldateien konfiguriert wurde, führen Sie den folgenden Befehl aus.

        ```
        DISM /online /Enable-Feature /Featurename:NetFx3 /All
        ```

    -   Wenn der Computer Zugriff auf die Installationsmedien hat, führen Sie einen Befehl aus, der dem folgenden ähnelt. Im folgenden Beispiel befindet sich das Installationsmedium in Laufwerk D. Der `LimitAccess` -Parameter verhindert, dass der Befehl versucht, Windows Update oder einen Server mit WSUS zu kontaktieren.

        ```
        DISM /online /Enable-Feature /Featurename:NetFx3 /All /LimitAccess /Source:d:\sources\sxs
        ```

    > [!NOTE]
    > Beim DISM-Befehl muss die Groß-/Kleinschreibung beachtet werden.

### <a name="configure-alternate-sources-for-feature-files-in-group-policy"></a>Konfigurieren alternativer Quellen für Featuredateien in der Gruppenrichtlinie
Die in diesem Abschnitt beschriebene Gruppenrichtlinieneinstellung gibt autorisierte Quellspeicherorte für .NET Framework 3.5-Dateien und andere Featuredateien an, die im Rahmen der Konfiguration von %%amp;quot;Features bei Bedarf%%amp;quot; entfernt wurden. Die Richtlinien Einstellung **Einstellungen für die Installation optionaler Komponenten und die Reparatur von Komponenten angeben** befindet sich im Ordner **Computerkonfiguration\Administrative Vorlagen\System** im Gruppenrichtlinien-Verwaltungskonsole-oder lokalen Gruppenrichtlinie-Editor.

> [!NOTE]
> Sie müssen Mitglied der Administratorgruppe sein, um Gruppenrichtlinieneinstellungen auf dem lokalen Computer ändern zu können. Falls die Gruppenrichtlinieneinstellungen für den zu verwaltenden Computer auf der Domänenebene gesteuert werden, müssen Sie Mitglied der Gruppe %%amp;quot;Domänenadministratoren%%amp;quot; sein, um Gruppenrichtlinieneinstellungen ändern zu können.

##### <a name="to-configure-a-default-alternate-source-path-in-group-policy"></a>So konfigurieren Sie einen alternativen Standardquellpfad in der Gruppenrichtlinie

1. Öffnen Sie im Editor für lokale Gruppenrichtlinie oder Gruppenrichtlinien-Verwaltungskonsole die folgende Richtlinien Einstellung.

   **Computerkonfiguration\Administrative vorlagen\system\einstellungen für die Installation optionaler Komponenten und die Reparatur von Komponenten angeben**

2. Das Aktivieren der Richtlinien Einstellung wurde von sselect **aktiviert** , wenn Sie nicht bereits aktiviert ist.

3. Geben Sie im Textfeld **Alternativer Dateiquellpfad** im Bereich **Optionen** einen vollqualifizierten Pfad zu einem freigegebenen Ordner oder einer WIM-Datei an. Fügen Sie zum Angeben einer WIM-Datei als alternativer Quelldateispeicherort dem Pfad das Präfix **WIM:** und den Index des in der WIM-Datei zu verwendenden Images als Suffix hinzu. Die folgenden Beispiele enthalten Werte, die Sie angeben können.

   - Pfad zu einem freigegebenen Ordner: **\\\\** <em>server_name</em>**\share \\ **<em>FOLDER_NAME</em>

   - Pfad zu einer WIM-Datei, in der **3** den Index des Images darstellt, in dem sich die Featuredateien befinden: **Wim: \\ \\ **<em>server_name</em>**\share\install.Wim: 3**

4. Wenn Sie nicht möchten, dass Computer, die von dieser Richtlinien Einstellung gesteuert werden, in Windows Update nach fehlenden Featuredateien suchen, wählen Sie **nie versuchen, Nutzlast von Windows Update herunterzuladen**.

5. Falls die von dieser Richtlinieneinstellung gesteuerten Richtlinieneinstellung in der Regel Updates über WSUS erhalten, Sie jedoch fehlende Featuredateien lieber über Windows Update und nicht über WSUS suchen möchten, aktivieren Sie **Stellen Sie direkt eine Verbindung mit Windows Update her, um Inhalte für das Reparieren herunterzuladen, anstatt WSUS (Windows Server Update Services) zu verwenden.**

6. Klicken Sie auf **OK**, wenn Sie diese Richtlinieneinstellung geändert haben. Schließend Sie dann den Gruppenrichtlinien-Editor.

## <a name="see-also"></a>Weitere Informationen
[Windows Server-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkId=241573) 
 [Microsoft .NET Framework 3,5 Bereitstellungs Überlegungen](https://go.microsoft.com/fwlink/p/?LinkId=248869) 
 [Aktivieren oder Deaktivieren von Windows-Features](https://go.microsoft.com/fwlink/p/?LinkId=246552)



