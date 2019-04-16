---
title: App-Kompatibilität von Server Core-Feature on Demand (FOD)
description: So installieren Sie Windows Server-Features bei Bedarf
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
ms.sourcegitcommit: dbb4738fdac3b7911952ff11f1eaed9649d6567a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2019
ms.locfileid: "9149900"
---
# App-Kompatibilität von Server Core-Feature on Demand (FOD)

> Gilt für Windows Server 2019 und Windows Server, Version 1809

Das **Server Core App-Kompatibilität Features bei Bedarf** ist ein optionales Feature-Paket, die Windows Server 2019 Server Core-Installationen oder Windows Server, Version 1809, zu einem beliebigen Zeitpunkt hinzugefügt werden können.

Weitere Informationen zu Features on Demand (FOD) finden Sie unter [Features bei Bedarf](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities).


## Warum installieren die App Compatibility FOD? 

App-Kompatibilität, ein Feature bei Bedarf für Server Core, verbessert die app-Kompatibilität für die Windows Server Core-Installationsoption erheblich durch Hinzufügen einer Teilmenge von Binärdateien und Pakete aus Windows Server mit Desktop Experience, ohne die Windows Server Desktop Experience-grafikumgebung. Dieses optionale Paket ist in einer separaten ISO oder von Windows Update verfügbar, aber Sie können nur Windows Server Core-Installationen und-Bildern hinzugefügt werden.

Die zwei primäre bereitgestellten Werte aus der App Compatibility FOD sind:

1.  Erhöht die Kompatibilität von Server Core für serveranwendungen, die bereits im Markt sind oder bereits von Organisationen entwickelt und wurden bereitgestellt.

2.  Hilfe bei der Bereitstellung von Komponenten des Betriebssystems und eine höhere app-Kompatibilität für Software-Tools, die in Spitzen zur Problembehandlung und Debuggen von Szenarien verwendet.

Komponenten des Betriebssystems, die verfügbar sind, als Teil der Server Core App Compatibility FOD enthalten:

-   Microsoft Management Console (mmc.exe)

-   Ereignisanzeige (Eventvwr.msc)

-   Systemmonitor (PerfMon.exe)

-   Ressourcenmonitor (Resmon.exe)

-   Geräte-Manager (Devmgmt.msc)

-   Datei-Explorer (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   Datenträgerverwaltung (Diskmgmt.msc)

-   Failovercluster-Manager (CluAdmin.msc)

    -   Hinzufügen der Failover-Clusterunterstützung Windows Server-Features erfordert zuerst.

        -   Verwenden Sie Powershell-Cmdlet, um hinzuzufügen, `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   Um Failovercluster-Manager, geben Sie ein **Cluadmin** in der Befehlszeile.

## Installieren die App-Kompatibilität FOD

 >[!IMPORTANT] 
   >Die App Compatibility FOD kann nur auf Server Core installiert werden. Versuchen Sie nicht die Server Core App Compatibility FOD zu einer Windows Server-Installation von Windows Server mit Desktop Experience hinzufügen.

### Hinzufügen das Server Core-Anwendungskompatibilität-Feature on Demand (FOD) zu einer ausgeführten Instanz von Server Core

 >[!NOTE] 
   > Bei diesem Verfahren wird Deployment Image Servicing and Management (DISM.exe), ein Befehlszeilentool verwendet. Weitere Informationen zu DISM-Befehle finden Sie unter [DISM Funktionen Paket Befehlszeilenoptionen zum Warten](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options).

>[!NOTE] 
   > Die gleichen optionale FOD-Pakete ISO können für Windows Server 2019 Server Core-Installationen oder Windows Server, Version 1809, Installationen verwendet werden.

>[!NOTE] 
   > Wenn Ihr Computer oder einem virtuellen Computer, auf dem Server Core ausgeführt wird zu Windows Update herstellen kann, können die Schritte 1 bis 7 unten übersprungen werden. Jedoch unbedingt/Source und /LimitAccess aus den DISM-Befehl in Schritt 8 weglassen.

1. Herunterladen Sie der optionale Server FOD-Pakete ISO-Datei, und kopieren Sie die ISO-Datei in einen freigegebenen Ordner auf Ihrem lokalen Netzwerk:

 - Besitzen Sie keine Volumenlizenz können Sie die Server FOD-ISO-Image-Datei herunterladen, aus dem gleichen Portal, in denen die Betriebssystem-ISO-Image-Datei abgerufen wird: [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
 - Die Server FOD-ISO-Image-Datei ist auch im [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) oder im [Visual Studio-Portal](https://visualstudio.microsoft.com) für Abonnenten verfügbar.


2. Melden Sie sich als Administrator auf dem Server Core-Computer, die mit Ihrem lokalen Netzwerk verbunden ist und, die Sie der FOD, hinzufügen möchten.

3. Verwenden Sie **net Use**oder eine andere Methode, um zum Speicherort des FOD ISO verbinden.

4. Kopieren Sie die FOD ISO in einen lokalen Ordner Ihrer Wahl.

5. Starten Sie PowerShell, indem Sie **powershell.exe** in einer Befehlszeile eingeben.

6. Binden Sie die FoD ISO mithilfe des folgenden Befehls:

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. Geben Sie zum Beenden der PowerShell **zu beenden** .

8.  Führen Sie den folgenden Befehl aus:

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  Nachdem die Statusanzeige abgeschlossen ist, starten Sie das Betriebssystem neu.

### Optional Internet Explorer 11 Server Core hinzu (nach dem Hinzufügen der Server Core App Compatibility FOD)

 >[!NOTE]  
   > Die Server Core App Compatibility FOD ist erforderlich für das Hinzufügen von Internet Explorer 11, Internet Explorer 11 ist jedoch nicht erforderlich, um die Server Core App Compatibility FOD hinzufügen.

1.  Melden Sie sich als Administrator auf dem Server Core-Computer, der die App Compatibility FOD bereits hinzugefügt wurde und das optionale FOD Server-Paket, die, das ISO-Datei lokal kopiert.

2.  Starten Sie PowerShell, indem Sie **powershell.exe** in einer Befehlszeile eingeben.

3.  Binden Sie die FoD ISO mithilfe des folgenden Befehls:

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  Geben Sie zum Beenden der PowerShell **zu beenden** .


5.  Führen Sie den folgenden Befehl aus:

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  Nachdem die Statusanzeige abgeschlossen ist, starten Sie das Betriebssystem neu.

 
#### Versionshinweise und Vorschläge für das optionale Paket Server Core App Compatibility FOD und Internet Explorer 11

- **Wichtig:** Bitte lesen Sie die Windows Server 2019-Versionshinweise für alle Probleme, Aspekte oder Richtlinien, bevor Sie mit der Installation und Verwendung von das optionale Paket Server Core App Compatibility FOD und Internet Explorer 11.
 
 >[!NOTE] 
   > Es ist möglich, mit der Server Core-Konsole Erfahrung Flimmern, wenn die App Compatibility FOD hinzufügen, nachdem Sie mit Windows Update installieren des kumulativen Updates auftreten.  Dieses Problem mit Dezember 2018 aktualisiert.  Weitere Informationen und Auflösung finden Sie unter [Knowledge Base-Artikel 4481610: Bildschirm flimmert, nach der Installation von Server Core App Compatibility FOD in Windows Server 2019 servercore](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core).

- Nach der Installation der App Compatibility FOD und Neustart des Servers ändert sich der Befehl Konsole Fenster Frame Farbe auf eine andere blau dargestellt.

- Wenn Sie auch das optionale Paket für Internet Explorer 11 installieren, beachten Sie, dass Doppelklicken auf offenen lokal gespeicherte HTML-Dateien nicht unterstützt wird. Sie können jedoch **mit der rechten Maustaste** öffnen **mit Internet Explorer**, und Sie können es direkt von Internet Explorer- **Datei**öffnen -> **Öffnen**. 

- Um die app-Kompatibilität von Server Core mit der App Compatibility FOD weiter zu verbessern, wurde die IIS-Verwaltungskonsole zu Server Core als eine optionale Komponente hinzugefügt.  Allerdings ist es unbedingt erforderlich, fügen Sie zunächst die App Compatibility FOD, um die IIS-Verwaltungskonsole zu verwenden. IIS-Verwaltungskonsole abhängig von der Microsoft Management Console (mmc.exe), die nur auf Server Core durch das Hinzufügen von der App Compatibility FOD verfügbar ist.  Verwenden Sie Powershell- [**Installation-WindowsFeature**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) , um IIS-Verwaltungskonsole hinzuzufügen.

- Als Ausgangspunkt allgemeine Richtlinien, wenn die Installation von apps auf Server (mit oder ohne diese optionale Pakete) es Core manchmal erforderlich, Optionen für die automatische Installation und Anweisungen zu verwenden ist. 
    
 - Als Beispiel SQL Server Management Studio für SQL Server 2016 und SQL Server 2017 auf Server Core installiert werden kann und voll funktionsfähig ist, wenn die App Compatibility FOD vorhanden ist.  Finden Sie unter [Installieren von SQLServer über die Befehlszeile](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017).
 - Wenn SQL Server Management Studio nicht erwünscht ist, ist es nicht erforderlich, die Server Core App Compatibility FOD installieren.  Finden Sie unter [Installieren von SQLServer auf servercore](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017).

