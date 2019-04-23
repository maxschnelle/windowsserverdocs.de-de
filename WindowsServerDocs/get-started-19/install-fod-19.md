---
title: App-Kompatibilität von Server Core-Feature on Demand (FOD)
description: 'Vorgehensweise: Installieren von Windows Server-Features bei Bedarf'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: b8211ace56aa6565295a15adce26a8dfbc98e1e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866111"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>App-Kompatibilität von Server Core-Feature on Demand (FOD)

> Gilt für Windows Server-2019 und Windows Server, Version 1809

Die **Kompatibilitätsfeature der Server Core-App bei Bedarf** ist ein optionales Feature-Paket, das Windows Server 2019 Server Core-Installationen oder Windows Server, Version 1809, zu einem beliebigen Zeitpunkt hinzugefügt werden kann.

Weitere Informationen zu Funktionen für die Anforderung (Feature-On) finden Sie unter [Features bei Bedarf](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities).


## <a name="why-install-the-app-compatibility-fod"></a>Warum installieren Sie die App-Kompatibilität Feature-On? 

App-Kompatibilität, eine Funktion bei Bedarf für Server Core, wesentlich verbessert die Anwendungskompatibilität für die Windows Server Core-Installationsoption dazu eine Teilmenge der Binärdateien und Pakete von Windows Server mit Desktopdarstellung, ohne die Windows Server-Desktopdarstellung grafischen Umgebung. Diese optionalen Pakets auf eine separate ISO-Datei oder über Windows Update verfügbar ist, jedoch kann nur auf Windows Server Core-Installationen und Bilder hinzugefügt werden.

Die zwei primären bereitgestellten Werte aus der App-Kompatibilität Feature-On sind:

1.  Erhöht die Kompatibilität der Server Core für serveranwendungen, die bereits im Markt sind oder haben bereits von Organisationen entwickelt und bereitgestellt.

2.  Hilfe bei der Bereitstellung von Betriebssystemkomponenten und höhere app-Kompatibilität von Softwaretools, die in akute Problembehandlung und Debuggen von Szenarios verwendet.

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

        -   Mithilfe von Powershell-Cmdlet hinzu, `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   Geben Sie zum Failovercluster-Manager ausführen **Cluadmin** an der Eingabeaufforderung.

## <a name="installing-the-app-compatibility-fod"></a>Installieren die App-Kompatibilität Feature-On

 >[!IMPORTANT] 
   >Die App-Kompatibilität Feature-On kann nur auf Server Core installiert werden. Versuchen Sie nicht die Server Core-App-Kompatibilität Feature-On einer Windows Server-Installation von Windows Server mit Desktopdarstellung hinzu.

### <a name="to-add-the-server-core-app-compatibility-feature-on-demand-fod-to-a-running-instance-of-server-core"></a>Um die Kompatibilität der Server Core-App-Funktion bei Bedarf (Feature-On) an eine ausgeführte Instanz von Server Core hinzuzufügen

 >[!NOTE] 
   > Diese Prozedur verwendet das Deployment Image Servicing and Management (DISM.exe), ein Befehlszeilentool. Weitere Informationen zu DISM-Befehlen finden Sie unter [DISM Funktionen Paket Befehlszeilenoptionen zum Warten von](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options).

>[!NOTE] 
   > Die gleichen optionalen Feature-On-Pakete ISO können für Windows Server 2019 Server Core-Installationen oder Windows Server, Version 1809, Installationen verwendet werden.

>[!NOTE] 
   > Wenn Ihren Computer oder virtuellen Computer, auf dem Server Core ausgeführt wird, Herstellen einer Verbindung mit Windows Update ist, können die Schritte 1 bis 7 unten übersprungen werden. Aber stellen Sie sicher, / Source "und" /LimitAccess vom das DISM-Befehl in Schritt 8.

1. Herunterladen Sie die optionalen Server Feature-On-Pakete ISO und kopieren Sie die ISO-Datei in einem freigegebenen Ordner auf Ihrem lokalen Netzwerk:

 - Wenn Sie über eine Volumenlizenz verfügen können Sie die Server Feature-On-ISO-Image-Datei im gleichen Portal herunterladen, in denen die Betriebssystem-ISO-Image-Datei abgerufen wird: [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
 - Der Server Feature-On-ISO-Abbilddatei steht auch auf die [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) oder auf die [Visual Studio-Portal](https://visualstudio.microsoft.com) für Abonnenten.


2. Melden Sie sich als Administrator auf dem Server Core-Computer, die mit Ihrem lokalen Netzwerk verbunden ist und, die die Feature-On zu hinzugefügt werden soll.

3. Verwenden Sie **net verwenden**, oder eine andere Methode, für die Verbindung auf den Speicherort der FOD ISO.

4. Kopieren Sie die FOD ISO in einen lokalen Ordner Ihrer Wahl ein.

5. Starten Sie PowerShell, indem Sie eingeben **powershell.exe** an einer Eingabeaufforderung.

6. Einbinden der FoD ISO mithilfe des folgenden Befehls:

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. Typ **beenden** um PowerShell zu beenden.

8.  Führen Sie den folgenden Befehl aus:

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  Sobald der Statusbalken vollständig ist, starten Sie das Betriebssystem neu.

### <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>Internet Explorer 11 zu Server Core optional hinzugefügt werden soll, (nach dem Hinzufügen der Server Core-App-Kompatibilität Feature-On.)

 >[!NOTE]  
   > Der Server Core-App-Kompatibilität Feature-On ist für das Hinzufügen von Internet Explorer 11 erforderlich, aber Internet Explorer 11 ist nicht erforderlich, um die Server Core-App-Kompatibilität Feature-On hinzuzufügen.

1.  Melden Sie sich als Administrator auf dem Server Core-Computer, der die App-Kompatibilität Feature-On bereits hinzugefügt wurde und das optionale Server Feature-On-Paket, das ISO lokal kopiert.

2.  Starten Sie PowerShell, indem Sie eingeben **powershell.exe** an einer Eingabeaufforderung.

3.  Einbinden der FoD ISO mithilfe des folgenden Befehls:

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  Typ **beenden** um PowerShell zu beenden.


5.  Führen Sie den folgenden Befehl aus:

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  Sobald der Statusbalken vollständig ist, starten Sie das Betriebssystem neu.

 
#### <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>Anmerkungen zu Releases und Vorschläge für das optionale Feature-On von Server Core-App-Kompatibilität und Internet Explorer 11-Paket

- **Wichtig:** lesen Sie den Anmerkungen zur Version von Windows Server-2019 für alle Probleme, Überlegungen und Anleitungen, bevor Sie mit der Installation und Verwendung des optionalen Pakets Feature-On von Server Core-App-Kompatibilität und Internet Explorer 11.
 
 >[!NOTE] 
   > Es ist möglich, die auftreten, mit der Server Core-konsolenumgebung Flimmern, wenn Sie die App-Kompatibilität Feature-On hinzufügen, nach der Verwendung von Windows Update zum Installieren von kumulativen Updates.  Dieses Problem wird mit Dezember 2018 aufgelöst wird aktualisiert.  Weitere Informationen und Lösungen finden Sie unter [4481610 Knowledge Base-Artikel: Bildschirm flackert, nach der Installation von Server Core-App-Kompatibilität Feature-On in Windows Server 2019 Server Core](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core).

- Der Befehl im Fenster-Frames Konsolenfarbe ändert sich nach der Installation der App-Kompatibilität Feature-on und Neustart des Servers in einen anderen Blauton.

- Möchten Sie die optionale Internet Explorer 11-Paket auch installieren, beachten Sie, dass die HTM-Dateien doppelklicken, um öffnen lokal gespeichert werden, wird nicht unterstützt. Sie können jedoch **mit der rechten Maustaste** , und wählen Sie **Öffnen mit IE**, oder Sie können sie direkt über Internet Explorer öffnen **Datei** -> **Öffnen**. 

- Um die app-Kompatibilität von Server Core mit der App-Kompatibilität Feature-On weiter zu verbessern, wurde die IIS-Verwaltungskonsole auf Server Core als optionale Komponente hinzugefügt.  Allerdings ist es absolut notwendig ist, zuerst die App-Kompatibilität Feature-On Verwendung der IIS-Verwaltungskonsole hinzufügen. IIS-Verwaltungskonsole hängt von der Microsoft Management Console (mmc.exe), steht nur auf Server Core durch das Hinzufügen von der App-Kompatibilität Feature-On.  Verwenden von Powershell [ **Install-WindowsFeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS-Verwaltungskonsole hinzufügen.

- Wie Sie ein allgemeinen Punkt Anleitungen, die beim Installieren von apps auf Server (mit oder ohne diese optionale Pakete) es Core manchmal erforderlich, Installation im Hintergrund und Anweisungen zu verwenden ist. 
    
 - Beispielsweise SQL Server Management Studio für SQL Server 2016 und SQL Server 2017 kann auf Server Core installiert werden und ist voll funktionsfähig, wenn die App-Kompatibilität Feature-On vorhanden ist.  Angezeigt wird, [Installieren von SQLServer über die Eingabeaufforderung](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017).
 - Wenn SQL Server Management Studio nicht gewünscht ist, ist es nicht erforderlich ist, installieren Sie die Server Core-App-Kompatibilität Feature-On.  Angezeigt wird, [Installieren von SQLServer unter Server Core](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017).

