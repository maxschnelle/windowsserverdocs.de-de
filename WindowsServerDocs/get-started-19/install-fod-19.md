---
title: App-Kompatibilität von Server Core-Feature on Demand (FOD)
description: 'Vorgehensweise: Installieren von Windows Server-Features bei Bedarf'
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 05/29/2019
ms.openlocfilehash: e76b7862549814d5453717c40cec45e341141d7a
ms.sourcegitcommit: 8eea7aadbe94f5d4635c4ffedc6a831558733cc0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308594"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>App-Kompatibilität von Server Core-Feature on Demand (FOD)

> Gilt für: WindowsServer 2019, Windows Server Halbjährlicher Kanal

Die **Kompatibilitätsfeature der Server Core-App bei Bedarf** ist ein optionales Feature-Paket, das Windows Server 2019 Server Core-Installationen oder Windows Server Halbjährlicher Kanal zu einem beliebigen Zeitpunkt hinzugefügt werden kann.

Weitere Informationen zu Funktionen für die Anforderung (Feature-On) finden Sie unter [Features bei Bedarf](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities).

## <a name="why-install-the-app-compatibility-fod"></a>Warum installieren Sie die App-Kompatibilität Feature-On?

App-Kompatibilität, eine Funktion bei Bedarf für Server Core, wesentlich verbessert die Anwendungskompatibilität für die Windows Server Core-Installationsoption dazu eine Teilmenge der Binärdateien und Pakete von Windows Server mit Desktopdarstellung, ohne die Windows Server-Desktopdarstellung grafischen Umgebung. Diese optionalen Pakets auf eine separate ISO-Datei oder über Windows Update verfügbar ist, jedoch kann nur auf Windows Server Core-Installationen und Bilder hinzugefügt werden.

Die zwei primären bereitgestellten Werte aus der App-Kompatibilität Feature-On sind:

- Erhöht die Kompatibilität der Server Core für serveranwendungen, die bereits im Markt sind oder haben bereits von Organisationen entwickelt und bereitgestellt.
- Hilfe bei der Bereitstellung von Betriebssystemkomponenten und höhere app-Kompatibilität von Softwaretools, die in akute Problembehandlung und Debuggen von Szenarios verwendet.

Komponenten des Betriebssystems, die verfügbar sind, als Teil der Server Core-App-Kompatibilität Feature-On zählen:

-   Microsoft Management Console (mmc.exe)

-   Ereignisanzeige (Eventvwr.msc)

-   Systemmonitor (PerfMon.exe)

-   Ressourcenmonitor (Resmon.exe)

-   Device Manager (Devmgmt.msc)

-   Datei-Explorer (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   Die Datenträgerverwaltung (Diskmgmt.msc)

-   Failovercluster-Manager (' CluAdmin.msc)

    -   Hinzufügen der Failover-Clusterunterstützung von Windows Server-Funktion erfordert zuerst.

        -   Aus einer PowerShell-Sitzung mit erhöhten Rechten aus: 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   Geben Sie zum Failovercluster-Manager ausführen **Cluadmin** an der Eingabeaufforderung.

Server unter Windows Server, Version 1903 und höher auch unterstützen die folgenden Komponenten:

- Hyper-V-Manager (virtmgmt.msc)
- Aufgabenplanung (taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>Installieren die App-Kompatibilität Feature-On

Die App-Kompatibilität Feature-On kann nur auf Server Core installiert werden. Versuchen Sie nicht die Server Core-App-Kompatibilität Feature-On einer Windows Server-Installation von Windows Server mit Desktopdarstellung hinzu. Die gleichen optionalen Feature-On-Pakete ISO können für Windows Server 2019 Server Core-Installationen oder Windows Server Halbjährlicher Kanal-Installationen verwendet werden.

1. Wenn der Server mit Windows Update verbinden kann, müssen Sie, lediglich führen Sie den folgenden Befehl aus einer PowerShell-Sitzung mit erhöhten Rechten aus, und starten Sie Windows Server nach Ausführung des Befehls neu:

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. Wenn der Server kann nicht auf Windows Update verbunden sind, stattdessen herunterladen Sie die optionalen Server Feature-On-Pakete ISO, und kopieren Sie die ISO-Datei an einen freigegebenen Ordner auf Ihrem lokalen Netzwerk:

   - Wenn Sie über eine Volumenlizenz verfügen können Sie die Server Feature-On-ISO-Image-Datei im gleichen Portal herunterladen, in denen die Betriebssystem-ISO-Image-Datei abgerufen wird: [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
   - Der Server Feature-On-ISO-Abbilddatei steht auch auf die [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) oder auf die [Visual Studio-Portal](https://visualstudio.microsoft.com) für Abonnenten.

3. Melden Sie sich mit einem Administratorkonto auf dem Server Core-Computer, die mit Ihrem lokalen Netzwerk verbunden ist und, die die Feature-On zu hinzugefügt werden soll.

4. Verwenden Sie **net verwenden**, oder eine andere Methode, für die Verbindung auf den Speicherort der FOD ISO.

5. Kopieren Sie die FOD ISO in einen lokalen Ordner Ihrer Wahl ein.

6. Binden Sie die FOD ISO mit den folgenden Befehl in einer PowerShell-Sitzung mit erhöhten Rechten aus:

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. Führen Sie den folgenden Befehl aus:

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. Sobald der Statusbalken vollständig ist, starten Sie das Betriebssystem neu.

 Weitere Informationen zu DISM-Befehlen finden Sie unter [Verwenden von DISM in Windows PowerShell](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>Internet Explorer 11 zu Server Core optional hinzugefügt werden soll, (nach dem Hinzufügen der Server Core-App-Kompatibilität Feature-On.)

 >[!NOTE]  
   > Der Server Core-App-Kompatibilität Feature-On ist für das Hinzufügen von Internet Explorer 11 erforderlich, aber Internet Explorer 11 ist nicht erforderlich, um die Server Core-App-Kompatibilität Feature-On hinzuzufügen.

1. Melden Sie sich als Administrator auf dem Server Core-Computer, der die App-Kompatibilität Feature-On bereits hinzugefügt wurde und das optionale Server Feature-On-Paket, das ISO lokal kopiert.

2. Starten Sie PowerShell, indem Sie eingeben **powershell.exe** an einer Eingabeaufforderung.

3. Einbinden der FOD ISO mithilfe des folgenden Befehls:

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. Führen Sie den folgenden Befehl, mit der `$package_path` Variable, die den Pfad zur Cab-Datei von Internet Explorer eingeben:

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. Sobald der Statusbalken vollständig ist, starten Sie das Betriebssystem neu.

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>Anmerkungen zu Releases und Vorschläge für das optionale Feature-On von Server Core-App-Kompatibilität und Internet Explorer 11-Paket

> [!IMPORTANT]
> FODs unter Windows Server installiert, wird nicht Version 1809 bleiben unverändert nach einem für ein direktes Upgrade auf Windows Server, Version 1903 sein, sodass Sie ihn nach dem Upgrade erneut installieren. Alternativ können Sie vor dem Upgrade der neuen Windows Server-Installationsquelle FODs hinzufügen. Dadurch wird sichergestellt, dass die neue Version von jedem FODs sind vorhanden, nachdem das Upgrade abgeschlossen ist. Weitere Informationen finden Sie in der [Hinzufügen von Funktionen und optionale Pakete zu einem Server Core von WIM-Offlineabbild](install-fod-19.md#add-capabilities).

- **Wichtig:** Lesen Sie den Anmerkungen zur Version von Windows Server-2019 für alle Probleme, Überlegungen und Anleitungen, bevor Sie mit der Installation und Verwendung des optionalen Pakets Feature-On von Server Core-App-Kompatibilität und Internet Explorer 11.

- Es ist möglich, die auftreten, mit der Server Core-konsolenumgebung Flimmern, wenn Sie die App-Kompatibilität Feature-On hinzufügen, nach der Verwendung von Windows Update zum Installieren von kumulativen Updates.  Dieses Problem wird mit Dezember 2018 aufgelöst wird aktualisiert.  Weitere Informationen und Lösungen finden Sie unter [4481610 Knowledge Base-Artikel: Bildschirm flackert, nach der Installation von Server Core-App-Kompatibilität Feature-On in Windows Server 2019 Server Core](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core).

- Der Befehl im Fenster-Frames Konsolenfarbe ändert sich nach der Installation der App-Kompatibilität Feature-on und Neustart des Servers in einen anderen Blauton.

- Möchten Sie die optionale Internet Explorer 11-Paket auch installieren, beachten Sie, dass die HTM-Dateien doppelklicken, um öffnen lokal gespeichert werden, wird nicht unterstützt. Sie können jedoch **mit der rechten Maustaste** , und wählen Sie **Öffnen mit IE**, oder Sie können sie direkt über Internet Explorer öffnen **Datei** -> **Öffnen**.

- Um die app-Kompatibilität von Server Core mit der App-Kompatibilität Feature-On weiter zu verbessern, wurde die IIS-Verwaltungskonsole auf Server Core als optionale Komponente hinzugefügt.  Allerdings ist es absolut notwendig ist, zuerst die App-Kompatibilität Feature-On Verwendung der IIS-Verwaltungskonsole hinzufügen. IIS-Verwaltungskonsole hängt von der Microsoft Management Console (mmc.exe), steht nur auf Server Core durch das Hinzufügen von der App-Kompatibilität Feature-On.  Verwenden von Powershell [ **Install-WindowsFeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS-Verwaltungskonsole hinzufügen.

- Wie Sie ein allgemeinen Punkt Anleitungen, die beim Installieren von apps auf Server (mit oder ohne diese optionale Pakete) es Core manchmal erforderlich, Installation im Hintergrund und Anweisungen zu verwenden ist. 
    
 - Beispielsweise SQL Server Management Studio für SQL Server 2016 und SQL Server 2017 kann auf Server Core installiert werden und ist voll funktionsfähig, wenn die App-Kompatibilität Feature-On vorhanden ist.  Angezeigt wird, [Installieren von SQLServer über die Eingabeaufforderung](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017).
 - Wenn SQL Server Management Studio nicht gewünscht ist, ist es nicht erforderlich ist, installieren Sie die Server Core-App-Kompatibilität Feature-On.  Angezeigt wird, [Installieren von SQLServer unter Server Core](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017).

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> Hinzufügen von Funktionen und optionale Pakete zu einem Server Core von WIM-Offlineabbild

1. Laden Sie die Windows Server und Server Feature-On-ISO-Dateien in einen lokalen Ordner auf einem Windows-Computer herunter.

   - Wenn Sie über eine Volumenlizenz verfügen können Sie die Windows Server und Server Feature-On-ISO-Image-Dateien aus dem [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
   - Der Server Feature-On-ISO-Abbilddatei finden Sie auch für langfristigen Wartungskanal auf Versionen der [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) oder auf die [Visual Studio-Portal](https://visualstudio.microsoft.com) für Abonnenten.

2. Öffnen Sie eine PowerShell-Sitzung als Administrator aus, und klicken Sie dann verwenden Sie die folgenden Befehle, um die Bilddateien als Laufwerke einbinden:

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. Kopieren der den Inhalt der Windows Server-ISO-Datei in einen lokalen Ordner (z. B. *C:\SetupFiles\WindowsServer*).

4. Rufen Sie den imagenamen, die, den Sie in der Datei "Install.wim" mithilfe des folgenden Befehls ändern möchten.<br>
Verwenden der `$install_wim_path` Variable, die den Pfad zu der Datei "Install.wim" im Ordner "\Sources" der ISO-Datei eingeben.

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. Bereitstellen die Datei "Install.wim" in einem neuen Ordner mit den folgenden Befehl wird die Variable Beispielwerte durch Ihre eigenen ersetzen und Wiederverwenden von der `$install_wim_path` Variable aus dem vorherigen Befehl.<br>

   - `$image_name` -Geben Sie den Namen des Images, die Sie bereitstellen möchten.
   - `$mount_folder variable` -Geben Sie den Ordner für den Inhalt der Datei "Install.wim" den Zugriff auf ein.

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. Hinzufügen von Funktionen und Pakete auf das bereitgestellte Install.wim-Abbild mithilfe der folgenden Befehle aus, und Ersetzen Sie dabei die Variable Beispielwerte durch Ihre eigenen.<br>

   - `$capability_name` -Geben Sie den Namen der Funktion, die (in diesem Fall die AppCompatibility-Funktion) zu installieren.
   - `$package_path` -Geben Sie den Pfad des Pakets an (in diesem Fall Internet Explorer) zu installieren.
   - `$fod_drive` -Geben Sie den Laufwerkbuchstaben des bereitgestellten Server Feature-On-Abbilds.

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. Aufheben der Bereitstellung und Änderungen in die Datei "Install.wim" mit den folgenden Befehl, der verwendet die `$mount_folder` -Variable wurde in den vorherigen Befehlen:

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

Sie können jetzt Ihren Server aktualisieren, dazu führen Sie setup.exe aus dem Ordner, die Sie erstellt, für die Windows Server-Installationsdateien haben (in diesem Beispiel: *C:\SetupFiles\WindowsServer*). Dieser Ordner enthält nun die Windows Server-Installationsdateien mit den zusätzlichen Funktionen und optionale Pakete enthalten.