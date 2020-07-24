---
title: Übersicht über Datei Server Ressourcen-Manager (Übersicht)
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 5/14/2018
description: File Server Ressourcen-Manager (FSRM) ist ein Tool, mit dem Sie Daten auf einem Windows Server-Dateiserver verwalten und klassifizieren können.
ms.openlocfilehash: 58b410e51dae3ea102bb1a15f5bb60f00ab702fa
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964562"
---
# <a name="file-server-resource-manager-fsrm-overview"></a>Übersicht über Datei Server Ressourcen-Manager (Übersicht)

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal),

Beim Dateiserver Ressourcen-Manager (FSRM) handelt es sich um einen Rollen Dienst in Windows Server, mit dem Sie auf Dateiservern gespeicherte Daten verwalten und klassifizieren können. Sie können Datei Server Ressourcen-Manager verwenden, um Dateien automatisch zu klassifizieren, Aufgaben auf der Grundlage dieser Klassifizierungen auszuführen, Kontingente für Ordner festzulegen und Berichte zu erstellen, die die Speicherauslastung überwachen.

Es ist ein kleiner Punkt, aber wir haben auch [die Möglichkeit zum Deaktivieren von Änderungs Journalen](#whats-new) in Windows Server, Version 1803, hinzugefügt.

## <a name="features"></a>Features

Der Ressourcen-Manager für Dateiserver umfasst die folgenden Features:

-   Die [Kontingent Verwaltung](quota-management.md) ermöglicht es Ihnen, den für ein Volume oder einen Ordner zulässigen Speicherplatz einzuschränken, und Sie können automatisch auf neue Ordner angewendet werden, die auf einem Volume erstellt werden. Sie können außerdem Kontingentvorlagen definieren, die auf neue Volumes oder Ordner angewendet werden können.
-   Die [Datei Klassifizierungs Infrastruktur](classification-management.md) bietet Einblicke in Ihre Daten, indem Klassifizierungs Prozesse automatisiert werden, sodass Sie Ihre Daten effektiver verwalten können. Sie können Dateien klassifizieren und Richtlinien auf der Basis dieser Klassifizierung anwenden. Beispielrichtlinien umfassen die dynamische Zugriffsteuerung zum Einschränken des Dateizugriffs, Dateiverschlüsselung und Dateiablauf. Dateien können anhand von Dateiklassifizierungsregeln oder manuell durch Ändern der Eigenschaften einer ausgewählten Datei oder eines Ordners automatisch klassifiziert werden.
-   Mithilfe von [Datei Verwaltungsaufgaben](file-management-tasks.md) können Sie auf Grundlage ihrer Klassifizierung eine bedingte Richtlinie oder eine Aktion auf Dateien anwenden. Zu den Bedingungen einer Dateiverwaltungsaufgabe zählen der Dateispeicherort, die Klassifizierungseigenschaften, das Erstellungsdatum der Datei, das Datum der letzten Dateiänderung oder das Datum des letzten Dateizugriffs. Zu den möglichen Aktionen für eine Dateiverwaltungsaufgabe gehören die Fähigkeit zum Ablaufen von Dateien, zum Verschlüsseln von Dateien oder zum Ausführen eines benutzerdefinierten Befehls.
-   Mithilfe der [Datei Prüfungsverwaltung](file-screening-management.md) können Sie die Dateitypen steuern, die Benutzer auf einem Dateiserver speichern können. Sie können die Erweiterungen einschränken, die für freigegebene Dateien gespeichert werden können. Sie können beispielsweise eine Dateiprüfung erstellen, die verhindert, dass Dateien mit der Erweiterung %%amp;quot;MP3%%amp;quot; in persönlichen freigegebenen Ordnern auf einem Dateiserver gespeichert werden.
-   Mithilfe von [Speicher Berichten](storage-reports-management.md) erkennen Sie Trends bei der Datenträger Verwendung und wie Ihre Daten klassifiziert werden. Zudem können Sie eine ausgewählte Benutzergruppe bezüglich Versuchen überwachen, nicht autorisierte Dateien zu speichern.

Die in Dateiserver Ressourcen-Manager enthaltenen Features können mithilfe der Dateiserver Ressourcen-Manager-App oder mithilfe von Windows PowerShell konfiguriert und verwaltet werden.

> [!IMPORTANT]
>  Der Ressourcen-Manager für Dateiserver unterstützt nur Volumes, die mit dem NTFS-Dateisystem formatiert sind. Das robuste Datei System wird nicht unterstützt.

## <a name="practical-applications"></a>Praktische Anwendung
 Im Folgenden finden Sie einige praktische Anwendungsfallbeispiele für den Ressourcen-Manager für Dateiserver:

-   Erstellen Sie mit der Dateiklassifizierungsinfrastruktur und dem Szenario für die dynamische Zugriffssteuerung eine Richtlinie, mit der Sie auf Basis der Dateiklassifizierung auf dem Dateiserver Zugriff auf Dateien und Ordner erteilen.

-   Erstellen Sie eine Dateiklassifizierungsregel, mit der beliebige Dateien, die mindestens 10 Sozialversicherungsnummern enthalten, als Dateien mit personenbezogenen Daten gekennzeichnet werden können.

-   Kennzeichnen Sie Dateien, die in den letzten 10 Jahren nicht geändert wurden, als abgelaufen.

-   Erstellen Sie ein Kontingent von 200 Megabyte für das Basisverzeichnis jedes Benutzers, und Benachrichtigen Sie Sie, wenn Sie 180 Megabyte verwenden.

-   Verhindern Sie das Speichern von Musikdateien in persönlichen freigegebenen Ordnern.

-   Planen Sie einen Bericht, der jeden Sonntag um Mitternacht ausgeführt wird und eine Liste mit den Dateien generiert, auf die in den beiden vorherigen Tagen am häufigsten zugegriffen wurde. Damit können Sie die Speicheraktivität am Wochenende ermitteln und Serverausfallzeiten entsprechend einplanen.

## <a name="whats-new---prevent-fsrm-from-creating-change-journals"></a><a name="whats-new"></a>Neuerungen: verhindern der Erstellung von Änderungs Journalen in f

Ab Windows Server, Version 1803, können Sie verhindern, dass der Datei Server Ressourcen-Manager-Dienstanbieter ein Änderungs Journal (auch als "US-Journal" bezeichnet) auf Volumes erstellt, wenn der Dienst gestartet wird. Dadurch kann ein wenig Speicherplatz auf jedem Volume eingespart werden, die Echt Zeit Datei Klassifizierung wird jedoch deaktiviert.

Informationen zu älteren neuen Features finden Sie unter [What es New in File Server Ressourcen-Manager](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383587(v=ws.11)).

Führen Sie die folgenden Schritte aus, um zu verhindern, dass Datei Server Ressourcen-Manager ein Änderungs Journal auf einigen oder allen Volumes erstellt, wenn der Dienst gestartet wird:

1. Beendet den SRMSVC-Dienst. Öffnen Sie beispielsweise eine PowerShell-Sitzung als Administrator, und geben Sie ein `Stop-Service SrmSvc` .
2. Löschen Sie mit dem Befehl "fsutil" das "US-Journal" für die Volumes, auf denen Sie Speicherplatz einsparen möchten:

      ```
      fsutil usn deletejournal /d <VolumeName>
      ```
    Beispiel: `fsutil usn deletejournal /d c:`

3. Öffnen Sie den Registrierungs-Editor, indem Sie z `regedit` . b. in derselben PowerShell-Sitzung eingeben.
4. Navigieren Sie zum folgenden Schlüssel: **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\srmsvc\settings** .
5. So können Sie optional die Änderungs Journal Erstellung für den gesamten Server überspringen (überspringen Sie diesen Schritt, wenn Sie ihn nur auf bestimmten Volumes deaktivieren möchten):
    1. Klicken Sie mit der rechten Maustaste auf den **Einstellungs** Schlüssel, und wählen Sie dann **neuer**  >  **DWORD-Wert (32-Bit)** aus.
    1. Benennen Sie den Wert `SkipUSNCreationForSystem` .
    1. Legen Sie den Wert auf **1** (in Hexadezimal) fest.
6. So können Sie optional die Änderungs Journal Erstellung für bestimmte Volumes überspringen:
    1. Verwenden Sie den `fsutil volume list` Befehl oder den folgenden PowerShell-Befehl, um die volumepfade zu überspringen:
        ```PowerShell
        Get-Volume | Format-Table DriveLetter,FileSystemLabel,Path
        ```
       Im folgenden finden Sie eine Beispielausgabe:

       ```
        DriveLetter FileSystemLabel Path
        ----------- --------------- ----
                    System Reserved \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        C                           \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
       ```
    2. Klicken Sie im Registrierungs-Editor mit der rechten Maustaste auf den Schlüssel **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\srmsvc\settings** , und wählen Sie dann **neuer**  >  **Wert für mehrere Zeichen**Folgen aus.
    3. Benennen Sie den Wert `SkipUSNCreationForVolumes` .
    4. Geben Sie den Pfad für jedes Volume ein, auf dem Sie das Erstellen eines Änderungs Journals überspringen, und platzieren Sie die einzelnen Pfade in einer separaten Zeile. Beispiel:

        ```
        \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
        ```

        > [!NOTE]
        > Der Registrierungs-Editor weist möglicherweise darauf hin, dass leere Zeichen folgen entfernt wurden. diese Warnung wird angezeigt, die Sie sicher ignorieren können: *Daten vom Typ REG_MULTI_SZ dürfen keine leeren Zeichen folgen enthalten. Der Registrierungs-Editor entfernt alle gefundenen leeren* Zeichen folgen.

7. Starten Sie den Dienst SRMSVC. Geben Sie z. b. in einer PowerShell-Sitzung ein `Start-Service SrmSvc` .



## <a name="additional-references"></a>Zusätzliche Referenzen

- [Dynamische Access Control](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408191(v=ws.11))
