---
title: Übersicht über Ressourcen-Manager für Dateiserver (File Server Resource Manager, FSRM)
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 5/14/2018
description: Resource Manager für Dateiserver (FSRM) ist ein Tool, Ihnen ermöglicht das Verwalten und Klassifizieren von Daten auf einem Windows Server-Dateiserver.
ms.openlocfilehash: 8488c7418ac03be53db7164678fad353bc7c637d
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476127"
---
# <a name="file-server-resource-manager-fsrm-overview"></a>Übersicht über Ressourcen-Manager für Dateiserver (File Server Resource Manager, FSRM)

> Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer (Halbjährlicher Kanal) 

Der Ressourcen-Manager für Dateiserver (FSRM) ist ein Rollendienst unter Windows Server, der Ihnen das Verwalten und Klassifizieren von auf Dateiservern gespeicherten Daten ermöglicht. Sie können File Server Resource Manager verwenden, um automatisch Klassifizieren von Dateien, Aufgaben, die basierend auf folgenden Klassifizierungen, Festlegen von Kontingenten für Ordner und Erstellen von Berichten, die Überwachung der speicherauslastung.

Es ist auch ein sehr wichtig, aber wir [die Möglichkeit zum Deaktivieren von Change Journale hinzugefügt](#whats-new) in Windows Server, Version 1803.

## <a name="features"></a>Features

Der Ressourcen-Manager für Dateiserver umfasst die folgenden Features:

-   [Kontingentverwaltung](quota-management.md) können Sie den Speicherplatz einschränken, die für ein Volume oder einen Ordner zulässig ist, und sie können automatisch auf neue Ordner, die auf einem Volume erstellt werden angewendet werden. Sie können außerdem Kontingentvorlagen definieren, die auf neue Volumes oder Ordner angewendet werden können.  
-   [Dateiklassifizierungsinfrastruktur](classification-management.md) bietet Einsicht in Ihre Daten indem klassifizierungsvorgänge automatisiert werden, damit Sie Ihre Daten effektiver verwalten können. Sie können Dateien klassifizieren und Richtlinien auf der Basis dieser Klassifizierung anwenden. Beispielrichtlinien umfassen die dynamische Zugriffsteuerung zum Einschränken des Dateizugriffs, Dateiverschlüsselung und Dateiablauf. Dateien können anhand von Dateiklassifizierungsregeln oder manuell durch Ändern der Eigenschaften einer ausgewählten Datei oder eines Ordners automatisch klassifiziert werden.
-   [Dateiverwaltungsaufgaben](file-management-tasks.md) ermöglicht es Ihnen, Dateien, die basierend auf deren Klassifizierung eine bedingte Richtlinie oder Aktion zuweisen. Zu den Bedingungen einer Dateiverwaltungsaufgabe zählen der Dateispeicherort, die Klassifizierungseigenschaften, das Erstellungsdatum der Datei, das Datum der letzten Dateiänderung oder das Datum des letzten Dateizugriffs. Zu den möglichen Aktionen für eine Dateiverwaltungsaufgabe gehören die Fähigkeit zum Ablaufen von Dateien, zum Verschlüsseln von Dateien oder zum Ausführen eines benutzerdefinierten Befehls.
-   [Dateiprüfungsverwaltung](file-screening-management.md) können Sie die Dateitypen steuern, die Benutzer kann auf einem Dateiserver speichern. Sie können die Erweiterungen einschränken, die für freigegebene Dateien gespeichert werden können. Sie können beispielsweise eine Dateiprüfung erstellen, die verhindert, dass Dateien mit der Erweiterung %%amp;quot;MP3%%amp;quot; in persönlichen freigegebenen Ordnern auf einem Dateiserver gespeichert werden.
-   [Speicherberichte](storage-reports-management.md) Ihnen beim Identifizieren von Trends bei der Datenträgerverwendung und die Art der datenklassifizierung ist. Zudem können Sie eine ausgewählte Benutzergruppe bezüglich Versuchen überwachen, nicht autorisierte Dateien zu speichern.  
  
Die Ressourcen-Managers für Dateiserver-Funktionen können konfiguriert und mithilfe der app File Server Resource Manager oder mithilfe von Windows PowerShell verwaltet werden.
  
> [!IMPORTANT]
>  Der Ressourcen-Manager für Dateiserver unterstützt nur Volumes, die mit dem NTFS-Dateisystem formatiert sind. Das ReFS (Resilient File System, Robustes Dateisystem) wird nicht unterstützt.  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
 Im Folgenden finden Sie einige praktische Anwendungsfallbeispiele für den Ressourcen-Manager für Dateiserver:  
  
-   Erstellen Sie mit der Dateiklassifizierungsinfrastruktur und dem Szenario für die dynamische Zugriffssteuerung eine Richtlinie, mit der Sie auf Basis der Dateiklassifizierung auf dem Dateiserver Zugriff auf Dateien und Ordner erteilen.  
  
-   Erstellen Sie eine Dateiklassifizierungsregel, mit der beliebige Dateien, die mindestens 10 Sozialversicherungsnummern enthalten, als Dateien mit personenbezogenen Daten gekennzeichnet werden können.  
  
-   Kennzeichnen Sie Dateien, die in den letzten 10 Jahren nicht geändert wurden, als abgelaufen.  
  
-   Erstellen Sie ein Kontingent mit 200 MB für das jeweilige Stammverzeichnis der Benutzer, und benachrichtigen Sie sie, wenn sie 180 MB verwenden.  
  
-   Verhindern Sie das Speichern von Musikdateien in persönlichen freigegebenen Ordnern.  
  
-   Planen Sie einen Bericht, der jeden Sonntag um Mitternacht ausgeführt wird und eine Liste mit den Dateien generiert, auf die in den beiden vorherigen Tagen am häufigsten zugegriffen wurde. Damit können Sie die Speicheraktivität am Wochenende ermitteln und Serverausfallzeiten entsprechend einplanen.  

## <a name="whats-new"></a>Was ist neu – verhindern, dass FSRM Änderung Journale erstellen

Beginnend mit Windows Server, Version 1803, können Sie jetzt verhindern den File Server Resource Manager-Dienst erstellen ein Änderungsjournal (auch bekannt als eine USN-Journal) auf Volumes, wenn der Dienst gestartet wird. Dies kann ein wenig auf jedem Volume Speicherplatz sparen, aber Sie wird in Echtzeit dateiklassifizierung deaktiviert.

Informationen zu älteren neuen Funktionen finden Sie unter [neues im Ressourcen-Manager](https://technet.microsoft.com/library/dn383587.aspx).

Um zu verhindern, dass File Server Resource Manager erstellen ein Änderungsjournal auf einige oder alle Volumes, wenn der Dienst gestartet wird, verwenden Sie die folgenden Schritte aus: 

1. Beenden Sie den SRMSVC-Dienst. Z. B. Öffnen Sie eine PowerShell-Sitzung als Administrator, und geben Sie `Stop-Service SrmSvc`.
2. Löschen Sie das USN-Journal für die Volumes auf Speicherplatz zu sparen, mit dem Befehl "Fsutil" werden sollen: 

      ```
      fsutil usn deletejournal /d <VolumeName>
      ```
    Beispiel: `fsutil usn deletejournal /d c:`

3. Öffnen Sie die Registrierungs-Editor, z. B. durch Eingabe `regedit` in der gleichen PowerShell-Sitzung.
4. Navigieren Sie zum folgenden Schlüssel: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SrmSvc\Settings**
5. Um optional überspringen ändern Journal-Erstellung für den gesamten Server (überspringen Sie diesen Schritt, wenn es sich nur auf bestimmten Volumes deaktivieren möchten):
    1. Mit der rechten Maustaste die **Einstellungen** gedrückt, und wählen Sie dann **neu** > **DWORD-Wert (32-Bit)** . 
    1. Nennen Sie den Wert `SkipUSNCreationForSystem`.
    1. Legen Sie den Wert **1** (in hexadezimal).
6. Journal erstellen und Ändern eines bestimmten Volumes optional zu überspringen:
    1. Abrufen der volumepfade, die Sie mithilfe von überspringen möchten die `fsutil volume list` Befehl oder den folgenden PowerShell-Befehl:
        ```PowerShell
        Get-Volume | Format-Table DriveLetter,FileSystemLabel,Path
        ```
       Hier ist eine Beispielausgabe:

       ```
        DriveLetter FileSystemLabel Path
        ----------- --------------- ----
                    System Reserved \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        C                           \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
       ```
    2. Zurück im Registrierungs-Editor, Maustaste den **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SrmSvc\Settings** gedrückt, und wählen Sie dann **neu** > **mehrteilige Zeichenfolge Wert**.
    3. Nennen Sie den Wert `SkipUSNCreationForVolumes`.
    4. Geben Sie den Pfad der einzelnen, den Volumes auf dem Sie lassen das Erstellen ein Änderungsjournal jeder Pfad in einer eigenen Zeile platzieren. Zum Beispiel:

        ```
        \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
        ```

        > [!NOTE] 
        > Registrierungs-Editor könnte sich herausstellen, dass sie leere Zeichenfolgen, entfernt dieser Warnung, die Sie ignorieren können anzuzeigen: *Daten vom Typ REG_MULTI_SZ darf keine leere Zeichenfolgen enthalten. Registrierungs-Editor wird entfernt, alle leere Zeichenfolgen gefunden.*

7. Starten Sie den SRMSVC-Dienst. Geben Sie beispielsweise in einer PowerShell-Sitzung `Start-Service SrmSvc`.



## <a name="see-also"></a>Siehe auch

- [Dynamische Zugriffssteuerung](https://technet.microsoft.com/library/dn408191(v=ws.11).aspx) 