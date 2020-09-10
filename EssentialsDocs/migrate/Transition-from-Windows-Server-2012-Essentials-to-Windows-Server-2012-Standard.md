---
title: Umstellung von Windows Server Essentials auf Windows Server 2012 Standard
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 3a73b744ca0b28802617881cbb64420f9f033dab
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625309"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Umstellung von Windows Server Essentials auf Windows Server 2012 Standard

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows Server &reg; 2012 Essentials unterstützt bis zu 25 Benutzer und 50 Geräte. Wenn Ihr Geschäftsbedarf den Grenzwert überschreitet, können Sie eine direkte Lizenz Umstellung von Windows Server Essentials auf Windows Server 2012 Standard durchführen, um die Lizenz Konformität zu gewährleisten.

## <a name="how-the-transition-affects-user-and-device-limits"></a>So wirkt sich die Umstellung auf Benutzer- und Gerätebegrenzungen aus
 Nach dem Wechsel zu Windows Server 2012 Standard werden die Benutzerkonten-und Geräte Limits entfernt, aber die Features, die für Windows Server Essentials eindeutig sind (z. b. das Dashboard, die Remote Webzugriff und die Client Computer Sicherung), bleiben weiterhin verfügbar. Aufgrund technischer Einschränkungen für diese Funktionen werden jedoch höchstens 75 Benutzerkonten und 75 Geräte unterstützt. Wenn es erforderlich ist, mehr als 75 Benutzerkonten oder Geräte hinzuzufügen, sollten Sie die Windows Server Essentials-Features deaktivieren und die systemeigenen Windows Server 2012-Tools zum Verwalten von Benutzerkonten und Geräten verwenden.

> [!IMPORTANT]
>   Windows Server 2012 Standard erfordert eine Client Zugriffslizenz (Client Access License, CAL) für jeden Benutzer bzw. jedes Gerät in Ihrer Umgebung. Dies unterscheidet sich von Windows Server Essentials, bei dem das CAL-Modell nicht verwendet wird und keine CALs vorhanden sind.  Wenn Sie von Windows Server Essentials zu Windows Server 2012 Standard wechseln, müssen Sie die entsprechende Anzahl und Art von CALs für Ihre Umgebung erwerben (die meisten Kunden erwerben Benutzer-CALs).

## <a name="before-the-transition"></a>Vor der Umstellung

-   Vor der Umstellung von Windows Server Essentials auf Windows Server 2012 Standard sollten Sie die Server Daten vollständig sichern.

    > [!IMPORTANT]
    >  Ohne eine vollständige Sicherung des Servers kann der Zustand des Servers vor der Umstellung nicht wiederhergestellt werden.

-   Stellen Sie außerdem sicher, dass Sie den Endbenutzer-Lizenzvertrag (EULA) für Windows Server 2012 Standard gelesen und verstanden haben. So zeigen Sie die EULA an:

    1.  Öffnen Sie ein Befehlsfenster als Administrator.

    2.  Führen Sie den folgenden Befehl aus:

         **dismus/Online/Set-Edition: Server Standard/geteula: EULA-Pfad**

         Dabei steht **eula path** für den Speicherort, an dem die EULA-Datei gespeichert werden soll. Beispiel: C:\ws8std_eula.rtf.  Achten Sie darauf, RTF als Dateierweiterung zu verwenden.

    3.  Navigieren Sie zum Speicherort der Datei, und doppelklicken Sie darauf, um sie zu öffnen.

## <a name="transition-to--windows-server-2012-standard"></a>Umstellung auf Windows Server 2012 Standard
 Nachdem Sie beschlossen haben, von Windows Server Essentials zu Windows Server 2012 Standard zu wechseln, führen Sie die folgenden beiden Schritte aus:

1. Erwerben Sie eine Lizenz für Windows Server 2012 Standard und die entsprechende Anzahl von Benutzer-und/oder Geräte-Client Zugriffs Lizenzen für Ihre Umgebung.

    Sie können eine Lizenz für Windows Server 2012 Standard von einem Einzelhandelsunternehmen, einem Verteiler oder mit der Hilfe eines [Microsoft-Partners](https://pinpoint.microsoft.com/SelectCulture.aspx)erwerben.

   > [!NOTE]
   >  Wenn Sie zunächst Windows Server 2012 Standard erworben haben und Ihre Downgrade-Rechte zum Installieren einer ihrer beiden virtuellen Instanzen als Windows Server Essentials übernommen haben, müssen Sie keine zusätzlichen Schritte erwerben.
   >
   >  Wenn Sie Windows Server 2012 Standard über den Volumenlizenz Kanal erwerben, können Sie ein ISO-Abbild und ein Product Key für Windows Server 2012 Standard aus dem Volume Licensing Service Center (VLSC) herunterladen.
   >
   >  Wenn Sie Windows Server 2012 Standard von allen anderen Kanälen erwerben, können Sie ein ISO-Abbild und einen Evaluierungs Product Key für Windows Server Essentials aus dem [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)herunterladen. Durch das Ausführen der Umstellung gemäß der Beschreibung im folgenden Schritt wird das Evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.

2. Öffnen Sie Windows PowerShell als Administrator, und führen Sie dann den folgenden Befehl aus.

    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *Product Key*

    Dabei ist *Product Key* die Product Key für Ihre Kopie von Windows Server 2012 Standard.

    Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.

   Nach dem Übergang verbleiben die Windows Server Essentials-Features auf dem Server und werden von bis zu 75 Benutzern und 75 Geräten unterstützt. Wenn Sie eine dieser Grenzwerte überschreiten, sollten Sie die systemeigenen Windows Server 2012-Standard Tools zum Verwalten von Benutzerkonten und Geräten verwenden.

   Außerdem sind die Medien Features von Windows Server Essentials nach der Umstellung auf Windows Server 2012 Standard nicht mehr verfügbar. Dazu zählen die Medienfunktionen des Remotewebzugriffs sowie die Medieneinstellungen auf dem Dashboard.

## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials-Features deaktivieren
 Wenn Sie das Windows Server Essentials-Dashboard oder andere Features zum Verwalten des Servers nicht mehr benötigen, können Sie die Funktionen deaktivieren und Sie vom Server entfernen.

 Der **Assistent zum Deaktivieren von Windows Server Essentials-Features:**

- hilft Ihnen bei der Deinstallation der Features. Außerdem wird der Server von Dateien bereinigt, die von der Windows Server Essentials-Server Software erstellt wurden.  Einige Bereinigungsoptionen werden sofort ausgeführt, während andere nach einem Neustart des Servers initiiert werden.

- erfordert, dass Sie alle Add-ins manuell deinstallieren, bevor Sie den Assistenten beenden können. Zum Anzeigen einer Liste der installierten Add-Ins öffnen Sie im Dashboard die Anwendungsseite. Wenn der Assistent installierte Add-Ins ermittelt werden Sie benachrichtigt und aufgefordert, diese zu deinstallieren.

- Hiermit können Sie auswählen, ob Sicherungsdateien für Client Computer aufbewahrt werden sollen, nachdem die Windows Server Essentials-Features ausgeschaltet wurden.

 Es gibt zwei Möglichkeiten, den **Assistenten zum Deaktivieren von Windows Server Essentials-Features über** das Dashboard auszuführen:

#### <a name="from-the-alert"></a>In der Warnmeldung

1.  Öffnen Sie im Dashboard die Meldungsanzeige.

2.  Wählen Sie in der Liste organisieren die Warnung aus, die Informationen über das Ausschalten von Windows Server Essentials-Features nach dem Übergang meldet.

3.  Klicken Sie in der Warnung auf **Windows Server Essentials-Features deaktivieren**.

#### <a name="from-the-get-help-and-support-pane"></a>Im Bereich %%amp;quot;Hilfe und Support%%amp;quot;

1. Klicken Sie auf der Startseite auf %%amp;quot;Hilfe und Support%%amp;quot;.

2. Klicken Sie auf **Assistent zum Deaktivieren von Windows Server Essentials-Funktionen**.

   Es ist möglich, dass einige vom Assistenten zum **Deaktivieren von Windows Server Essentials-Funktionen** ausgeführte Aufgaben nicht erfolgreich abgeschlossen werden. In einigen Fällen wird dadurch die Ausführung des Dashboards verhindert. In diesem Fall können Sie den Assistenten manuell starten, indem Sie folgende Datei ausführen:

   **%SYSTEMDRIVE%\Programme\Windows Server\Bin\TurnOffFeaturesWizard.exe**

## <a name="additional-references"></a>Weitere Verweise


-   [Umstellung auf Windows Server 2012 R2 Standard](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

