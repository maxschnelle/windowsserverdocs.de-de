---
title: App-Kompatibilität von Server Core-Feature on Demand (FOD)
description: Installieren von Windows Server-Features bei Bedarf
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 9ba0303d1eebc2138db7c5f1428ce920b0cb8af0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360821"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>App-Kompatibilität von Server Core-Feature on Demand (FOD)

> Gilt für: Windows Server 2019, Windows Server halbjährlicher Kanal

Das **App-Kompatibilität von Server Core-Feature on Demand** ist ein optionales Featurepaket, das jederzeit zu Windows Server 2019 Server Core-Installationen oder zum halbjährlichen Kanal von Windows Server hinzugefügt werden kann.

Weitere Informationen zu Features bei Bedarf (Features on Demand, FOD) finden Sie unter [Features On Demand](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) (Features bei Bedarf).

## <a name="why-install-the-app-compatibility-fod"></a>Warum sollte das App-Kompatibilitäts-FOD installiert werden?

App-Kompatibilität, ein optionales Feature (FOD) für Server Core, verbessert die App-Kompatibilität für die Windows Server Core-Installationsoption erheblich durch Hinzufügen einer Teilmenge von Binärdateien und Paketen von Windows Server mit Desktopdarstellung, ohne dass die Windows Server Desktop Experience-Grafikumgebung hinzugefügt wird. Dieses optionale Paket ist in einer separaten ISO oder über Windows Update verfügbar, kann aber nur Windows Server Core-Installationen und Images hinzugefügt werden.

Dies sind die zwei wichtigsten Vorteile, die das optionale Feature App-Kompatibilität bietet:

- Es steigert die Kompatibilität von Server Core für Serveranwendungen, die bereits auf dem Markt sind oder bereits von Organisationen entwickelt und bereitgestellt wurden.
- Es unterstützt die Bereitstellung von Betriebssystemkomponenten und gesteigerter App-Kompatibilität von Softwaretools, die in der akuten Problembehandlung und in Debugszenarien verwendet werden.

Zu den Betriebssystemkomponenten, die im Rahmen des Server Core-App-Kompatibilitäts-FODs verfügbar sind, zählen:

-   Microsoft Management Console (mmc.exe)

-   Ereignisanzeige (Eventvwr.msc)

-   Systemmonitor (PerfMon.exe)

-   Ressourcenmonitor (Resmon.exe)

-   Geräte-Manager (Devmgmt.msc)

-   Datei-Explorer (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   Datenträgerverwaltung (Diskmgmt.msc)

-   Failovercluster-Manager (CluAdmin.msc)

    -   Erfordert zunächst das Hinzufügen des Windows Server-Features Failoverclusterunterstützung.

        -   In einer PowerShell-Sitzung mit erhöhten Rechten: 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   Geben Sie **cluadmin** an der Eingabeaufforderung an, um den Failovercluster-Manager zu öffnen.

Server, die Windows Server, Version 1903 und höher, ausführen, unterstützen außerdem die folgenden Komponenten (wenn die gleiche Version des App-Kompatibilitäts-FODs verwendet wird):

- Hyper-V Manager (virtmgmt.msc)
- Aufgabenplanung (taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>Installieren des App-Kompatibilitäts-FODs

Das App-Kompatibilitäts-FOD kann nur unter Server Core installiert werden. Versuchen Sie nicht, das Server Core-FOD App-Kompatibilität zu einer Windows Server-Installation von Windows Server mit Desktopdarstellung hinzuzufügen. Die gleiche ISO mit optionalen FOD-Paketen kann für Windows Server 2019 Server Core-Installationen oder Windows Server-Installationen im halbjährlichen Kanal verwendet werden.

1. Wenn der Server eine Verbindung mit Windows Update herstellen kann, brauchen Sie lediglich in einer PowerShell-Sitzung mit erhöhten Rechten den folgenden Befehl auszuführen und dann Windows Server neu zu starten, nachdem die Ausführung des Befehls abgeschlossen wurde:

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. Wenn der Server keine Verbindung mit Windows Update herstellen kann, laden Sie stattdessen die ISO mit den optionalen Server-FOD-Paketen herunter, und kopieren Sie die ISO in einen freigegebenen Ordner in Ihrem lokalen Netzwerk:

   - Wenn Sie eine Volumenlizenz besitzen, können Sie die Server-FOD-ISO-Imagedatei aus dem gleichen Portal herunterladen, aus dem auch das ISO-Image des Betriebssystems bezogen werden kann: [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
   - Die Server-FOD-ISO-Imagedatei steht außerdem für Abonnenten im [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) oder im [Visual Studio-Portal](https://visualstudio.microsoft.com) zur Verfügung.

3. Melden Sie sich mit einem Administratorkonto auf dem Server Core-Computer an, der mit Ihrem lokalen Netzwerk verbunden ist und dem Sie das FOD hinzufügen möchten.

4. Verwenden Sie **net use** oder ein anderes Verfahren, um eine Verbindung zum Speicherort der FOD-ISO herzustellen.

5. Kopieren Sie die FOD-ISO in einen lokalen Ordner Ihrer Wahl.

6. Binden Sie die FOD-ISO in einer PowerShell-Sitzung mit erhöhten Rechten mithilfe des folgenden Befehls ein:

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. Führen Sie den folgenden Befehl aus:

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. Nachdem die Statusanzeige den Abschluss anzeigt, führen Sie einen Neustart des Betriebssystems aus.

   Weitere Informationen zu DISM-Befehlen finden Sie unter [Verwenden von DISM in Windows PowerShell](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>Optionales Hinzufügen von Internet Explorer 11 zu Server Core (nach dem Hinzufügen des Server Core-App-Kompatibilitäts-FODs)

 >[!NOTE]  
   > Das Server Core-App-Kompatibilitäts-FOD ist erforderlich, um Internet Explorer 11 hinzuzufügen, nicht aber umgekehrt.

1. Melden Sie sich als Administrator auf dem Server Core-Computer an, dem das App-Kompatibilitäts-FOD bereits hinzugefügt und auf den die ISO-Datei mit dem optionalen Server-FOD-Paket lokal kopiert wurde.

2. Starten Sie PowerShell durch Eingeben von **powershell.exe** an einer Eingabeaufforderung.

3. Binden Sie die FOD-ISO mithilfe des folgenden Befehls ein:

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. Führen Sie den folgenden Befehl aus, und verwenden Sie die `$package_path`-Variable, um den Pfad zur CAB-Datei von Internet Explorer anzugeben:

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. Nachdem die Statusanzeige den Abschluss anzeigt, führen Sie einen Neustart des Betriebssystems aus.

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>Versionsanmerkungen und Vorschläge zum Server Core-App-Kompatibilitäts-FOD und dem optionalen Internet Explorer 11-Paket

> [!IMPORTANT]
> Unter Windows Server, Version 1809, installierte FODs bleiben nach einem lokalen Upgrade auf Windows Server, Version 1903, nicht erhalten, sodass Sie sie nach dem Upgrade erneut installieren müssen. Alternativ können Sie vor dem Upgrade FODs zur neuen Installationsquelle von Windows Server hinzufügen. Dadurch wird sichergestellt, dass nach dem Abschluss des Upgrades die neuen Versionen aller FODs vorhanden sind. Weitere Informationen finden Sie unter [Hinzufügen von Funktionen und optionalen Paketen zu einem WIM Server Core-Offlineimage](install-fod-19.md#add-capabilities).

- **Wichtig:** Lesen Sie zu eventuellen Problemen, Überlegungen und Anleitungen die Versionsanmerkungen für Windows Server-2019 , bevor Sie mit der Installation und Verwendung des Server Core-App-Kompatibilitäts-FODs und des optionalen Internet Explorer 11-Pakets fortfahren.

- In der Server Core-Konsolendarstellung kann es zu Flackern kommen, wenn das App-Kompatibilitäts-FOD nach dem Verwenden von Windows Update zum Installieren kumulativer Updates hinzugefügt wird.  Dieses Problem wurde mit den Updates aus Dezember 2018 behoben.  Weitere Informationen und Schritte zur Problemlösung finden Sie im [Knowledge Base-Artikel 4481610: Screen flickers after you install Server Core App Compatibility FOD in Windows Server 2019 Server Core](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core) (Bildschirmflackern nach der Installation des Server Core-App-Kompatibilitäts-FODs unter Windows Server 2019 Server Core).

- Nach der Installation des App-Kompatibilitäts-FODs und dem Neustart des Servers ändert sich die Rahmenfarbe des Befehlskonsolenfensters in einen anderen Blauton.

- Wenn Sie sich außerdem für die Installation des optionalen Internet Explorer 11-Pakets entscheiden, beachten Sie, dass Doppelklicken zum Öffnen lokal gespeicherter HTM-Dateien nicht unterstützt wird. Jedoch können Sie **mit der rechten Maustaste klicken** und **Mit IE öffnen** auswählen oder eine gewünschte Datei über **Datei** -> **Öffnen** direkt in Internet Explorer öffnen.

- Um die App-Kompatibilität von Server Core mit dem App-Kompatibilitäts-FOD weiter zu steigern, wurde Server Core die IIS-Verwaltungskonsole als optionale Komponente hinzugefügt.  Allerdings ist es unbedingt erforderlich, zuerst das App-Kompatibilitäts-FOD hinzuzufügen, um die IIS-Verwaltungskonsole zu verwenden. Die IIS-Verwaltungskonsole baut auf der Microsoft Management Console (mmc.exe) auf, die unter Server Core nur durch den Zusatz des App-Kompatibilitäts-FODs verfügbar ist.  Verwenden Sie den Powershell-Befehl [**Install-WindowsFeature**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps), um die IIS-Verwaltungskonsole hinzuzufügen.

- Als allgemeiner Anhaltspunkt ist es beim Installieren von Apps unter Server Core (mit oder ohne diese optionalen Pakete) manchmal erforderlich, die Optionen und Anweisungen für die Installation im Hintergrund zu verwenden. 
    
  - Beispielsweise kann SQL Server Management Studio für SQL Server 2016 und SQL Server 2017 unter Server Core installiert werden und weist den vollen Funktionsumfang auf, wenn das App-Kompatibilitäts-FOD vorhanden ist.  Weitere Informationen finden Sie unter [Installieren von SQL Server von der Eingabeaufforderung](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017).
  - Wenn SQL Server Management Studio nicht gewünscht ist, ist es nicht erforderlich, das Server Core-App-Kompatibilitäts-FOD zu installieren.  Mehr dazu erfahren Sie unter [Installieren von SQL Server unter Server Core](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017).

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> Hinzufügen von Funktionen und optionalen Paketen zu einem WIM Server Core-Offlineimage

1. Laden Sie die ISO-Imagedateien für Windows Server und das Server-FOD ISO in einen lokalen Ordner auf einem Windows-Computer herunter.

   - Wenn Sie über eine Volumenlizenz verfügen, können Sie die ISO-Imagedateien für Windows Server und das Server-FOD aus dem [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) herunterladen.
   - Die Server-FOD-ISO-Imagedatei steht für Releases im Long-Term Servicing Channel für Abonnenten außerdem im [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) oder im [Visual Studio-Portal](https://visualstudio.microsoft.com) zur Verfügung.

2. Öffnen Sie eine PowerShell-Sitzung als Administrator, und verwenden Sie anschließend die folgenden Befehle, um die Imagedateien als Laufwerke einzubinden:

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. Kopieren Sie den Inhalt der Windows Server-ISO-Datei in einen lokalen Ordner (beispielsweise *C:\SetupFiles\WindowsServer*).

4. Rufen Sie den Namen des Images, den Sie innerhalb der Install.wim-Datei ändern möchten, mithilfe des folgenden Befehls ab.<br>
Verwenden Sie die `$install_wim_path`-Variable, um den Pfad zur Install.wim-Datei einzugeben, die sich innerhalb des Ordners „\Sources“ der ISO-Datei befindet.

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. Binden Sie die Install.wim-Datei in einem neuen Ordner ein, indem Sie den folgenden Befehl verwenden, dabei die Beispielwerte der Variablen durch Ihre eigenen ersetzen und die Variable `$install_wim_path` aus dem vorhergehenden Befehl wiederverwenden.<br>

   - `$image_name`: Geben Sie den Namen des Images ein, das Sie einbinden möchten.
   - `$mount_folder variable`: Geben Sie den Ordner an, der für den Zugriff auf den Inhalt der Install.wim-Datei verwendet werden soll.

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. Fügen Sie dem eingebundenen Install.wim-Image die gewünschten Funktionen und Pakete hinzu, indem Sie die folgenden Befehle verwenden und die Beispielwerte der Variablen durch eigene ersetzen.<br>

   - `$capability_name`: Geben Sie den Namen der zu installierenden Funktion an (in diesem Fall die Funktion AppCompatibility).
   - `$package_path`: Geben Sie den Pfad zum zu installierenden Paket an (in diesem Fall Internet Explorer).
   - `$fod_drive`: Geben Sie den Laufwerksbuchstaben des eingebundenen Server-FOD-Images an.

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. Heben Sie die Einbindung auf, und committen Sie Änderungen an der Install.wim-Datei mit dem folgenden Befehl, der die `$mount_folder`-Variable aus den vorhergehenden Befehlen verwendet:

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

Jetzt können Sie ein Upgrade Ihres Servers ausführen, indem Sie aus dem Ordner, den Sie für die Windows Server-Installationsdateien erstellt haben, „setup.exe“ ausführen (in diesem Beispiel: *C:\SetupFiles\WindowsServer*). Dieser Ordner enthält nun die Windows Server-Installationsdateien mit eingeschlossenen zusätzlichen Funktionen und optionalen Paketen.